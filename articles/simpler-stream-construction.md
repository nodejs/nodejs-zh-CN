# io.js 中的流
===

## 什么是流？

「流」是一种处理 IO 的方式。其特点是：数据不是一次完整获取到，而是一点点地从管道（pipeline）中流出。就好比将一根水管的一头接到水龙头上，龙头一开，水便源源不断的从管子的另一头流出来。

#### 流处理 IO 的优势在于：

* 不必等到数据全部准备好了，才开始处理（就像我们在线看视频一样，不用等到视频下载完，就可以边下边看）
* 较低的内存占用（由于数据是一点点过来的，所以只需要分配一个较小 buffer 来缓存）
* 事件友好的 API
* 很好的解决了背压（数据消费的速度小于产生的速度）的问题

#### 当然流也有其劣势：

* 由于数据不完整，可能给处理带来麻烦
* 有一定的学习成本

## 流的基本用法

实际开发中，我们对流的使用一般分为两种：

#### 对内置的流对象的使用 

io.js 很多内置对象都有对流的支持。比如，我们要实现一个文件拷贝：

```javascript
var fs = require('fs');
var readStream = fs.createReadStream('/path/to/source');
var writeStream = fs.createWriteStream('/path/to/dest');

readStream.on('data', function(chunk) { // 当有数据流出时，写入数据
    writeStream.write(chunk);
});

readStream.on('end', function() { // 当没有数据时，关闭数据流
    writeStream.end();
});
```

上面的写法有一些问题，如果写入的速度跟不上读取的速度，有可能导致数据丢失。正常的情况应该是，写完一段，再读取下一段，如果没有写完的话，就让读取流先暂停，等写完再继续，于是代码可以修改为：

```javascript
var fs = require('fs');
var readStream = fs.createReadStream('/path/to/source');
var writeStream = fs.createWriteStream('/path/to/dest');

readStream.on('data', function(chunk) { // 当有数据流出时，写入数据
    if (writeStream.write(chunk) === false) { // 如果没有写完，暂停读取流
        readStream.pause();
    }
});

writeStream.on('drain', function() { // 写完后，继续读取
    readStream.resume();
});

readStream.on('end', function() { // 当没有数据时，关闭数据流
    writeStream.end();
});
```

或者使用更直接的`pipe`

```javascript
// pipe自动调用了data,end等事件
fs.createReadStream('/path/to/source').pipe(fs.createWriteStream('/path/to/dest'));
```

#### 自定流对象

有些时候，我们可能需要自己实现流对象。下面是一个实际的示例：实现逐行地的读一个文件的流

```javascript
var util = require('util');
var stream = require('stream')
var Transform = require('stream').Transform;

// 继承自 Transform
util.inherits(Liner, Transform);

function Liner(options) {
  options = options || {};
  options.objectMode = true;

  Transform.call(this, options);
}

Liner.prototype._transform = function (chunk, encoding, done) {
  var data = chunk.toString()
  if (this._lastLineData) data = this._lastLineData + data

  var lines = data.split('\n')
  this._lastLineData = lines.splice(lines.length - 1, 1)[0]

  lines.forEach(this.push.bind(this))
  done()
};

Liner.prototype._flush = function (done) {
  if (this._lastLineData) this.push(this._lastLineData)
  this._lastLineData = null
  done()
};

// 调用方法：
var fs = require('fs')
var liner = new Liner();
var source = fs.createReadStream('./access_log')
source.pipe(liner)
liner.on('readable', function () {
  var line
  while (line = liner.read()) {
    // do something with line
  }
})
```

## io.js 里面流的简单构建方式

io.js@1.2.0 版本里提供了一种更为简单的流的构造方式：不用先继承出一个新的流的类，直接从 4 种内置流中选择一个 new 一个流对象，将需要自己实现的方法通过构造函数的参数传入即可，具体参考下面的代码示例：

### Readable
```javascript
var readable = new stream.Readable({
  read: function(n) {
    // sets this._read under the hood
  }
});
```

### Writable
```javascript
var writable = new stream.Writable({
  write: function(chunk, encoding, next) {
    // sets this._write under the hood
  }
});

// or

var writable = new stream.Writable({
  writev: function(chunks, next) {
    // sets this._writev under the hood
  }
});
```

### Duplex
```javascript
var duplex = new stream.Duplex({
  read: function(n) {
    // sets this._read under the hood
  },
  write: function(chunk, encoding, next) {
    // sets this._write under the hood
  }
});

// or

var duplex = new stream.Duplex({
  read: function(n) {
    // sets this._read under the hood
  },
  writev: function(chunks, next) {
    // sets this._writev under the hood
  }
});
```

### Transform
```javascript
var transform = new stream.Transform({
  transform: function(chunk, encoding, next) {
    // sets this._transform under the hood
  },
  flush: function(done) {
    // sets this._flush under the hood
  }
});
```

那么上面那个逐行读取文件的流，我们可以这么实现

```javascript
var fs = require('fs')
var liner = new stream.Transform({
  transform: function (chunk, encoding, next) {
    var data = chunk.toString()
    if (this._lastLineData) data = this._lastLineData + data

    var lines = data.split('\n')
    this._lastLineData = lines.splice(lines.length - 1, 1)[0]

    lines.forEach(this.push.bind(this))
    next()
  },
  flush: function (done) {
    if (this._lastLineData) this.push(this._lastLineData)
    this._lastLineData = null
    done()
  }
});
var source = fs.createReadStream('./access_log')
source.pipe(liner)
liner.on('readable', function () {
  var line
  while (line = liner.read()) {
    // do something with line
  }
});
```
