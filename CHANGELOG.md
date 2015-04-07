# io.js 更新记录

## [2015-03-31, Version 1.6.3, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-03-31-version-163-rvagg)

### 主要更新

* **fs**: `fs.writeFileSync()` 以及特定情况下处于追加模式的 `fs.writeFile()` 和 `fs.writeFileSync()` 会造成文件损坏，查看 [#1058](https://github.com/iojs/io.js/issues/1058)，已在 [#1063](https://github.com/iojs/io.js/pull/1063) 中修复。(Olov Lassus)
* **iojs**: 引入了一个 "internal modules" API，允许核心代码共享 JavaScript 模块而不需要将它们暴露成公共的 API，这个特性是 core-only 的，查看 [#848](https://github.com/iojs/io.js/pull/848)。(Vladimir Kurchatkin)
* **timers**: 修复了两个关于定时器的小问题：
  - `Timer#close()` 现在是正确幂等的，查看 [#1288](https://github.com/iojs/io.js/issues/1288)。(Petka Antonov)
  - `setTimeout()` 在调用 `unref()` 后只会执行一次回调函数，查看 [#1231](https://github.com/iojs/io.js/pull/1231)。(Roman Reiss)
  - 注意：依然有其他定时器相关的问题没有被解决，例如 [#1152](https://github.com/iojs/io.js/pull/1152)。
* **Windows**: 为 Windows 平台上编译过的附加组件增加了一个 "delay-load hook"，这应该能减少一些 Windows 用户使用 io.js 附加组件的问题，查看 [#1251](https://github.com/iojs/io.js/pull/1251)。(Bert Belder)
* **V8**: V8 升级至 4.1.0.27，修复了一些小 bug。
* **npm**: 升级 npm 到 2.7.4。查看详情 [npm CHANGELOG.md](https://github.com/npm/npm/blob/master/CHANGELOG.md#v274-2015-03-20)。主要变更：
  * [`1549106`](https://github.com/npm/npm/commit/1549106f518000633915686f5f1ccc6afcf77f8f) [#7641](https://github.com/npm/npm/issues/7641) 因为 448efd0，执行 `npm shrinkwrap --dev` 不会再将 production 依赖包含到 `npm-shrinkwrap.json` 中。Whoopsie! ([@othiym23](https://github.com/othiym23))
  * [`fb0ac26`](https://github.com/npm/npm/commit/fb0ac26eecdd76f6eaa4a96a865b7c6f52ce5aa5) [#7579](https://github.com/npm/npm/issues/7579) 只有在我们确信 npm 不对它们负责时才阻止删除文件和链接。这个改变很难总结，因为如果一切正常你应该永远不会看到它，如果你想了解更多的情况，可以[看一看 commit 信息](https://github.com/npm/npm/commit/fb0ac26eecdd76f6eaa4a96a865b7c6f52ce5aa5)，这里做了详细的说明。([@othiym23](https://github.com/othiym23))
  * [`051c473`](https://github.com/npm/npm/commit/051c4738486a826300f205b71590781ce7744f01) [#7552](https://github.com/npm/npm/issues/7552) `bundledDependencies` 现在被正确的包含在安装上下文中了。这是另一个非常难以总结的 bug，再次，如果你对细节好奇我鼓励你[看一看 commit 信息](https://github.com/npm/npm/commit/051c4738486a826300f205b71590781ce7744f01)。好的总结是它修补了很多 `ember-cli` 的用例。([@othiym23](https://github.com/othiym23))
  * [`fe1bc38`](https://github.com/npm/npm/commit/fe1bc387a14475e373557de669e03d9d006d3173)[#7672](https://github.com/npm/npm/issues/7672) `npm-registry-client@3.1.2`: 通过纠正属性名修复了客户端证书处理。([@atamon](https://github.com/atamon))
  * [`89ce829`](https://github.com/npm/npm/commit/89ce829a00b526d0518f5cd855c323bffe182af0)[#7630](https://github.com/npm/npm/issues/7630) `hosted-git-info@1.5.3`: 确保 GitHub 简写被一致的处理，第三部分。([@othiym23](https://github.com/othiym23))
  * [`63313eb`](https://github.com/npm/npm/commit/63313eb0c37891c355546fd1093010c8a0c3cd81)[#7630](https://github.com/npm/npm/issues/7630) `realize-package-specifier@2.2.0`: 确保 GitHub 简写被一致的处理，第二部分。([@othiym23](https://github.com/othiym23))
  * [`3ed41bf`](https://github.com/npm/npm/commit/3ed41bf64a1bb752bb3155c74dd6ffbbd28c89c9)[#7630](https://github.com/npm/npm/issues/7630) `npm-package-arg@3.1.1`: 确保 GitHub 简写被一致的处理，第一部分。([@othiym23](https://github.com/othiym23))

### 已知问题

* 依然存在一些定时器和 `unref()` 待被解决。查看 [#1152](https://github.com/iojs/io.js/pull/1152)
* 可能还存在一些小的内存泄露，但是依然没有确定，查看 [#1075](https://github.com/iojs/io.js/issues/1075)
* REPL 中的 Surrogate pair 会导致终端僵死，查看 [#690](https://github.com/iojs/io.js/issues/690)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-03-23, Version 1.6.2, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-03-23-version-162-rvagg)

### 主要更新

* **Windows**: 正在进行的改善 Windows 支持状况的工作让完整的测试用例再次通过。正如 v1.4.2 的发布说明指出的，CI 系统和它的配置问题导致无法正确报告 Windows 下的测试问题，现在 CI 和代码库的问题似乎被完全解决了。
* **FreeBSD**: [发现](https://github.com/joyent/node/issues/9326)了一个影响 io.js/Node.js 的[内核bug](](https://lists.freebsd.org/pipermail/freebsd-current/2015-March/055043.html)，io.js 已经引入了一个补丁来阻止它引发问题。(Fedor Indutny) [#1218](https://github.com/iojs/io.js/pull/1218)
* **module**: 你现在可以使用 `require('.')` 代替 `require('./')`，这被认定为一个 bug 修复。(Michaël Zasso) [#1185](https://github.com/iojs/io.js/pull/1185)
* **v8**: 升级到 4.1.0.25，包括了 `--max_old_space_size` 值超过 `4096` 和 Solaris 支持的补丁，两个已经被包含在 io.js 中。

### 已知问题

* 可能还存在一些小的内存泄露，但是依然没有确定，查看 [#1075](https://github.com/iojs/io.js/issues/1075)
* REPL 中的 Surrogate pair 会导致终端僵死，查看 [#690](https://github.com/iojs/io.js/issues/690)
* 无法将 io.js 编译成静态库 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-03-20, Version 1.6.1, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-03-20-version-161-rvagg)

### 主要更新

* **path**: path.resolve() 使用了新的类型检查, [#1153](https://github.com/iojs/io.js/pull/1153) 发现了一些边缘案例依赖它，最显著的是 path.dirname(undefined)。放宽了对 path.dirname()，path.basename()，path.extname() 的类型检查。(Colin Ihrig) [#1216](https://github.com/iojs/io.js/pull/1216)
* **querystring**: querystring.parse() 和 querystring.stringify() 方法进行了内部优化，查看 [#847](https://github.com/iojs/io.js/pull/847)，querystring.escape() 阻止了数字字面量被正确的转化，查看 [#1208](https://github.com/iojs/io.js/issues/1208)，暴露了一个测试盲点。这个 bug 和测试现在已被修复。(Jeremiah Senkpiel) [#1213](https://github.com/iojs/io.js/pull/1213)

### 已知问题

* 可能依然存在与 TLS 相关内存泄露问题，查看 [#1075](https://github.com/iojs/io.js/issues/1075)
* REPL 中的 Surrogate pair 会导致终端僵死，查看 [#690](https://github.com/iojs/io.js/issues/690)
* 无法将 io.js 编译成静态库 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-03-19, Version 1.6.0, @chrisdickinson](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-03-19-version-160-chrisdickinson)

### 主要更新

* **node**: 新增一个命令行参数 -r 或者 --require，可以用来在启动的时候预加载模块。(Ali Ijaz Sheikh) [#881](https://github.com/iojs/io.js/pull/881)
* **querystring**: parse() and stringify() 现在更快了。(Brian White) [#847](https://github.com/iojs/io.js/pull/847)
* **http**: http.ClientRequest#flush() 方法已经被弃用并且替换为 http.ClientRequest#flushHeaders()，为了匹配 [joyent/node#9048](https://github.com/joyent/node/pull/9048) 中相同的改变。(Yosuke Furukawa) [#1156](https://github.com/iojs/io.js/pull/1156)
* **net**: 允许 server.listen() 的 port 参数接受 String 类型的选项，例如：{ port: "1234" }，为了匹配 [joyent/node#9268](https://github.com/joyent/node/pull/9268) 中 net.connect() 可以接受相同的选项。(Ben Noordhuis) [#1116](https://github.com/iojs/io.js/pull/1116)
* **tls**: 已报告的内存泄露有了进一步工作，虽然在一些尚未明确的使用情况下还有轻微的泄露，在 [#1075](https://github.com/iojs/io.js/issues/1075) 跟踪进度。
* **v8**: Backport 了一个补丁，当 --max_old_space_size 超过 4096 时会发生整数溢出。(Ben Noordhuis) [#1166](https://github.com/iojs/io.js/pull/1166)
* **platforms**: io.js CI 系统在 FreeBSD 和 SmartOS (Solaris) 报告通过。
* **npm**: 升级 npm 到 2.7.1。查看详情 [npm CHANGELOG.md](https://github.com/npm/npm/blob/master/CHANGELOG.md#v270-2015-02-26)。主要变更：
  * [`6823807`](https://github.com/npm/npm/commit/6823807bba) [#7121](https://github.com/npm/npm/issues/7121) npm install --save 的 Git 依赖保存传递进来的 URL 而不是用来缓存远程仓库的目录。修复在 shrinkwwapping 中使用 Git 依赖。正在重写缓存 Git 依赖的代码。重申。不会再有 single-letter 变量名字，工作流程更清晰了。([@othiym23](https://github.com/othiym23))
  * [`abdd040`](https://github.com/npm/npm/commit/abdd040da9) read-package-json@1.3.2: 当解析 JSON 出错时，使用更宽容的 JSON 解析器替代 JSON.parse 提供更有用的出错信息。([@smikes](https://github.com/smikes))
  * [`c56cfcd`](https://github.com/npm/npm/commit/c56cfcd79c) [#7525](https://github.com/npm/npm/issues/7525) npm dedupe 能够处理 scoped packages。 ([@KidkArolis](https://github.com/KidkArolis))
  * [`4ef1412`](https://github.com/npm/npm/commit/4ef1412d00) [#7075](https://github.com/npm/npm/issues/7075) 当尝试使用一个无效的 semver 范围标记 release 时，npm publish 和 npm tag 将会在处理之前报错。([@smikes](https://github.com/smikes))

### 已知问题

* 可能依然存在与 TLS 相关内存泄露问题，查看 [#1075](https://github.com/iojs/io.js/issues/1075)
* REPL 中的 Surrogate pair 会导致终端僵死，查看 [#690](https://github.com/iojs/io.js/issues/690)
* 无法将 io.js 编译成静态库，查看 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-03-09, Version 1.5.1, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-03-09-version-151-rvagg)

### Notable changes

* **tls**: 被报的 TLS 内存泄漏问题至少已被部分解决，在这次发布中有不少提交。现在的测试表明_可能_依然存在泄漏问题。可在 [#1075](https://github.com/iojs/io.js/issues/1075) 跟进整个过程。
* **http**: 修复了 [joyent/node#9348](https://github.com/joyent/node/issues/9348) 和 [npm/npm#7349](https://github.com/npm/npm/issues/7349) 所报的错误。当触发 `error` 事件，pending 的数据并未被完全读取，导致 `socket.destroy()` 有一个断言错误。(Fedor Indutny) [#1103](https://github.com/iojs/io.js/pull/1103)

### Known issues

* 可能与 TLS 相关的内存溢出问题，查看详情 [#1075](https://github.com/iojs/io.js/issues/1075).
* Windows 支持有一些明显的错误并未被 io.js 持续集成系统识别，由人为、程序和 Jenkins 错误等一系列原因造成。查看 [#1005](https://github.com/iojs/io.js/issues/1005) 的详情和讨论，希望这些错误能被尽快解决。
* REPL 中的 Surrogate pair 会导致终端僵死 [#690](https://github.com/iojs/io.js/issues/690)
* 无法将 io.js 编译成静态库 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-03-06, 版本 1.5.0, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-03-06-version-150-rvagg)

### 主要更新

* **buffer**: 新增 `Buffer#indexOf()` 方法, 模仿 [`Array#indexOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)。接受一个字符串，Buffer 或数值。字符串会使用 UTF8 解析。(Trevor Norris) [#561](https://github.com/iojs/io.js/pull/561)
* **fs**: `’fs’` 的方法中的 `options` 对象属性将不会做 `hasOwnProperty()` 检测，因此 options 对象允许原型链上的属性。(Jonathan Ong) [#635](https://github.com/iojs/io.js/pull/635)
* **tls**: PayPal 上报了一个疑似 TLS 内存溢出的问题，可能问题在最近 **stream_wrap** 中的一些修改上。最初修复在 [#1078](https://github.com/iojs/io.js/pull/1078), 你可以关注整个关闭溢出的过程 [#1075](https://github.com/iojs/io.js/issues/1075) (Fedor Indutny).
* **npm**: 升级 npm 到 2.7.0，查看详情 [npm CHANGELOG.md](https://github.com/npm/npm/blob/master/CHANGELOG.md#v270-2015-02-26)，从中可以看出为什么这只升级了 minor 而不是 major。以下为摘要：
  * [`145af65`](https://github.com/npm/npm/commit/145af6587f45de135cc876be2027ed818ed4ca6a) [#4887](https://github.com/npm/npm/issues/4887) 通过传入 `—node-gyp=/path/to/node-gyp` 参数给 npm，可替换 npm 自带的 `node-gyp` 脚本。不用修改 npm 的代码就可使用 `pangyp` 或 一个修改过的 `node-gyp` 版本来支持 io.js！([@ackalker](https://github.com/ackalker))
  * [`2f6a1df`](https://github.com/npm/npm/commit/2f6a1df3e1e3e0a3bc4abb69e40f59a64204e7aa) [#1999](https://github.com/npm/npm/issues/1999) 当没有定义 restart 脚本，只运行 `stop` 和 `start`（包括 pre- 和 post- 脚本），这样可更简单的让 npm 所管理的服务支持优雅的重启。([@watilde](https://github.com/watilde) / [@scien](https://github.com/scien))
  * [`448efd0`](https://github.com/npm/npm/commit/448efd0eaa6f97af0889bf47efc543a1ea2f8d7e) [#2853](https://github.com/npm/npm/issues/2853) `npm ls` 新增支持 `--dev` 和 `--prod`，使得只显示生产或开发时的依赖。 ([@watilde](https://github.com/watilde))
  * [`a0a8777`](https://github.com/npm/npm/commit/a0a87777af8bee180e4e9321699f050c29ed5ac4) [#7463](https://github.com/npm/npm/issues/7463) 将 `npm run-script` 打印的日志拆分成生命周期的脚本和 `npm run-script` 直接调用的脚本。 ([@watilde](https://github.com/watilde))
  * [`a5edc17`](https://github.com/npm/npm/commit/a5edc17d5ef1435b468a445156a4a109df80f92b) [#6749](https://github.com/npm/npm/issues/6749) `init-package-json@1.3.1`:
支持传递作用域给 `npm init`，所以包可以被初始化成 scope / organization / team 的一部分。 ([@watilde](https://github.com/watilde))
* **TC**: Colin Ihrig (@cjihrig) 离开 TC，因为想更多的贡献代码，而少参加会议。

### 已知问题

* 可能与 TLS 相关的内存溢出问题，查看详情 [#1075](https://github.com/iojs/io.js/issues/1075).
* Windows 支持有一些明显的错误并未被 io.js 持续集成系统识别，由人为、程序和 Jenkins 错误等一系列原因造成。查看 [#1005](https://github.com/iojs/io.js/issues/1005) 的详情和讨论，希望这些错误能被尽快解决。
* REPL 中的 Surrogate pair 会导致终端僵死 [#690](https://github.com/iojs/io.js/issues/690)
* 无法将 io.js 编译成静态库 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-03-02, 版本 1.4.3, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-03-02-version-143-rvagg)

### 主要更新

* **stream**: 修复在不支持 `writev()` 的平台（尤其是 Windows）的一些问题。在 1.4.1 中有修改 [#926](https://github.com/iojs/io.js/pull/926)，造成这些平台的一些功能无法使用，现在已经被解决 [#1008](https://github.com/iojs/io.js/pull/1008) (Fedor Indutny)
* **arm**: 我们已经初步支持 ARMv8 / ARM64 / AARCH64。如果要完全支持需要将 OpenSSL 升级到 1.0.2。[#1028](https://github.com/iojs/io.js/pull/1028) (Ben Noordhuis)
* 新增合作开发者: Julian Duque ([@julianduque](https://github.com/julianduque))

### 已知问题

* Windows 支持有一些明显的错误并未被 io.js 持续集成系统识别，由人为、程序和 Jenkins 错误等一系列原因造成。查看 [#1005](https://github.com/iojs/io.js/issues/1005) 的详情和讨论，希望这些错误能被尽快解决。
* REPL 中的 Surrogate pair 会导致终端僵死 [#690](https://github.com/iojs/io.js/issues/690)
* 无法将 io.js 编译成静态库 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-02-28, 版本 1.4.2, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-02-28-version-142-rvagg)

### 主要更新

* **tls**: 在 [#840](https://github.com/iojs/io.js/pull/840) 中修改 TLSWrap 时引入了一个拼写错误导致报错，这个错误只会在 Windows 上出现。并没有在 io.js 的持续集成系统发现，因为 Windows 编译脚本和 slave 配置有问题，见「已知问题」。已在 [#994](https://github.com/iojs/io.js/pull/994) 和 [#1004](https://github.com/iojs/io.js/pull/1004) 修复. (Fedor Indutny)
* **npm**: 更新 npm 到 2.6.1。查看详情 [npm CHANGELOG.md](https://github.com/npm/npm/blob/master/CHANGELOG.md#v260-2015-02-12)，主要变更：
  * [`8b98f0e`](https://github.com/npm/npm/commit/8b98f0e709d77a8616c944aebd48ab726f726f76) [#4471](https://github.com/npm/npm/issues/4471) `npm outdated` (只是 `npm outdated`) 默认值改为 `--depth=0`。而且 `npm update -g` 能像人们预期的那样工作，这之前是没想到的。查看 [`--depth` 的文档](https://github.com/npm/npm/blob/82f484672adb1a3caf526a8a48832789495bb43d/doc/misc/npm-config.md#depth)，细节有点略有混淆。([@smikes](https://github.com/smikes))
  * [`aa79194`](https://github.com/npm/npm/commit/aa791942a9f3c8af6a650edec72a675deb7a7c6e) [#6565](https://github.com/npm/npm/issues/6565) 调整 `peerDependency` 废弃警告，提示哪个包依赖的哪个 peerDependency 需要修改。 ([@othiym23](https://github.com/othiym23))
  * [`5fa067f`](https://github.com/npm/npm/commit/5fa067fd47682ac3cdb12a2b009d8ca59b05f992) [#7171](https://github.com/npm/npm/issues/7171) 调整 `engineStrict` 废弃警告，提示哪个 `package.json` 正在使用。([@othiym23](https://github.com/othiym23))
* 新增合作开发者：
  - Robert Kowalski ([@robertkowalski](https://github.com/robertkowalski))
  - Christian Vaagland Tellnes ([@tellnes](https://github.com/tellnes))
  - Brian White ([@mscdex](https://github.com/mscdex))

### 已知问题

* Windows 支持有一些明显的错误并未被 io.js 持续集成系统识别，由人为、程序和 Jenkins 错误等一系列原因造成。查看 [#1005](https://github.com/iojs/io.js/issues/1005) 的详情和讨论，希望这些错误能被尽快解决。
* REPL 中的 Surrogate pair 会导致终端僵死 [#690](https://github.com/iojs/io.js/issues/690)
* 无法将 io.js 编译成静态库 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-02-26，版本 1.4.1，@rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-02-26-version-141-rvagg)

_注意：版本 **1.4.0** 原本进行了标记和构建，但在发布过程中发现一个 libuv bug 所以被中止了，没有发布。该 tag 在[`a558cd0a61`](https://github.com/iojs/io.js/commit/a558cd0a61) 之后，但是被删除了。为了避免困惑，直接把版本升到了 1.4.1 。_

### 主要更新

* **process** / **promises**：如果一个 `Promise` 被 reject 了，并且在一次事件循环之内没有添加错误处理 handler， `process` 会触发一个 `'unhandledRejection'` 事件。如果一个 `Promise` 被 reject 了，并且在一次事件循环之后添加了错误处理 handler，`process` 会触发一个 `'rejectionHandled'` 事件。详情参看文档 [process](https://iojs.org/api/process.html) [#758](https://github.com/iojs/io.js/pull/758) (Petka Antonov)
* **streams**：在 `tls.connect()` 时可以将普通 streams 当做 socket 使用 [#926](https://github.com/iojs/io.js/pull/926) (Fedor Indutny)
* **http**：在客户端中止一个 `http.ClientRequest` 时会触发一个新的 `'abort'` 事件。 [#945](https://github.com/iojs/io.js/pull/945) (Evan Lucas)
* **V8**：V8 更新到 4.1.0.21，包含一个修复（但被禁止访问），详情参看 https://code.google.com/p/chromium/issues/detail?id=430201。此次更新因一个非兼容的 ABI 更新受阻，可能会在合并 v8 4.2 时支持。参看讨论 [#952](https://github.com/iojs/io.js/pull/952)。
* **npm**：更新 npm 到 2.6.0. 包含用以支持新 registry 的一些特性，并为 `npm@3` 做准备。详情参看 [npm CHANGELOG.md](https://github.com/npm/npm/blob/master/CHANGELOG.md#v260-2015-02-12)：
  * [`38c4825`](https://github.com/npm/npm/commit/38c48254d3d217b4babf5027cb39492be4052fc2) [#5068](https://github.com/npm/npm/issues/5068) 添加 logout 命令，该命令对基于 bearer 和 basic 的客户端验证会有帮助。([@othiym23](https://github.com/othiym23))
  * [`c8e08e6`](https://github.com/npm/npm/commit/c8e08e6d91f4016c80f572aac5a2080df0f78098) [#6565](https://github.com/npm/npm/issues/6565) 添加警告：`peerDependency` 的行为正在改变，并在文档中添加声明。 ([@othiym23](https://github.com/othiym23))
  * [`7c81a5f`](https://github.com/npm/npm/commit/7c81a5f5f058941f635a92f22641ea68e79b60db) [#7171](https://github.com/npm/npm/issues/7171) 添加警告：`package.json` 中的 `engineStrict` 在下一个主要版本(很快发布!)中将被移除 ([@othiym23](https://github.com/othiym23))
* **libuv**: 更新到 1.4.2 。修复详情参看 [libuv ChangeLog](https://github.com/libuv/libuv/blob/v1.x/ChangeLog)。

### 已知问题

* REPL 中的 Surrogate pair 会导致终端僵死 [#690](https://github.com/iojs/io.js/issues/690)
* 无法将 io.js 编译成静态库 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-02-20，版本 1.3.0，@rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-02-20-version-130-rvagg)

### 主要更新

* **url**: `url.resolve('/path/to/file', '.')` 现在的返回值会以斜杠结尾（如 `/path/to/`），`url.resolve('/', '.')` 会返回 `/`。[#278](https://github.com/iojs/io.js/issues/278) (Amir Saboury)
* **tls**: `tls` 和 `https` 所使用的默认密码套件被修改成所有现代浏览器已经实现的 `Perfect Forward Secrecy`。除此以外，去除了不安全的 RC4 密码，如果你直接使用了 RC4，请指定你自己的密码套件。 [#826](https://github.com/iojs/io.js/issues/826) (Roman Reiss)

### 已知问题

* REPL 中的代理对会冻结终端 [#690](https://github.com/iojs/io.js/issues/690)
* 无法将 io.js 编译成静态库 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 并非如文档所述是同步的，1.0.2 引入的问题，查看 [#760](https://github.com/iojs/io.js/issues/760)，解决 [#774](https://github.com/iojs/io.js/issues/774)
* 当 DNS 查询正在进行中时调用 `dns.setServers()` 会造成 process 崩溃，原因是断言错误 [#894](https://github.com/iojs/io.js/issues/894)

## [2015-02-10，版本 1.2.0，@rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-02-10-version-120-rvagg)

### 主要更新

* **stream**：
  - 简化 stream 构造方法，详情参看 [readable-stream/issues#102](https://github.com/iojs/readable-stream/issues/102)。并且扩展了streams 的基础对象，来让他们的构造方法接受默认的实现方法，减少创建自定义stream 所需的模板(通用)代码。一个更新版的 readable-stream 最终也会发布来匹配 core 的该变化。(@sonewman)
* **dns**：
  - `lookup()` 增加支持 `'all'` 布尔选项，默认为 `false`，如果设为 true，方法会返回一个 *all* 地址解析过的域名数组，参看[#744](https://github.com/iojs/io.js/pull/744) (@silverwind)
* **assert**：
  - `deepEqual()` 方法不再对比 `prototype` 属性，这被认为是 bug，参看[#636](https://github.com/iojs/io.js/pull/636) (@vkurchatkin)
  - 添加方法 `deepStrictEqual()` 功能同 `deepEqual()` 类似，只是在[原型](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)比较时进行严格相等比较，参看[#639](https://github.com/iojs/io.js/pull/639) (@vkurchatkin)
* **tracing**：
  - 如果编译时开启 `--with-lttng` 选项，则会同时编译 [LTTng](http://lttng.org/) (Linux 下一代 Trace 工具)。Trace 分数同 DTrace 和 ETW 相匹配。[#702](https://github.com/iojs/io.js/pull/702) (@thekemkid)
* **docs**：
  - 大量文档更新，具体查看相应提交
  - 新 **Errors** 文档描述了 JavaScript 错误，V8 特定的 和 io.js 特定的错误详情。(@chrisdickinson)
* **npm** 更新到 2.5.1, 简要更新日志：
  - [npm/0e8d473](https://github.com/npm/npm/commit/0e8d4736a1cbdda41ae8eba8a02c7ff7ce80c2ff) [#7281](https://github.com/npm/npm/issues/7281) `npm-registry-mock@1.0.0`: 清理 API，设置 `connection: close`，从而使测试在 io.js 1.1.x 通过。
  ([@robertkowalski](https://github.com/robertkowalski))
  - [npm/f9313a0](https://github.com/npm/npm/commit/f9313a066c9889a0ee898d8a35676e40b8101e7f)
  [#7226](https://github.com/npm/npm/issues/7226) 确保所有的请求设置被复制到 agent 中。
  ([@othiym23](https://github.com/othiym23))
   - [npm/fec4c96](https://github.com/npm/npm/commit/fec4c967ee235030bf31393e8605e9e2811f4a39)
  在环境中允许 `--no-proxy` 覆盖 `HTTP_PROXY` 设置。
  ([@othiym23](https://github.com/othiym23))
  - [npm/9d61e96](https://github.com/npm/npm/commit/9d61e96fb1f48687a85c211e4e0cd44c7f95a38e)
  `npm outdated --long` 添加一列显示依赖的类型。
  ([@watilde](https://github.com/watilde))
* **libuv** 升级到 1.4.0，详情参看 [libuv 更新日志](https://github.com/libuv/libuv/blob/v1.x/ChangeLog)
* 添加贡献者：
  - Aleksey Smolenchuk (@lxe)
  - Shigeki Ohtsu (@shigeki)

### 已知问题

* REPL 中的 Surrogate pair 会导致终端僵死 [#690](https://github.com/iojs/io.js/issues/690)
* io.js 无法作为静态库编译 [#686](https://github.com/iojs/io.js/issues/686)
* `process.send()` 行为并非如文档所说的同步，该问题是在 1.0.2 引入的，参看 [#760](https://github.com/iojs/io.js/issues/760) 和 修复 [#774](https://github.com/iojs/io.js/issues/774) 将会在下个版本发布。

## [2015-02-03, 版本 1.1.0, @chrisdickinson](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-02-03-version-110-chrisdickinson)

### 主要更新

* debug: 修复 v8 post-mortem 调试 bug.
* crypto: publicEncrypt 开始支持受密码保护的私钥.
* crypto: 哈希方法提速 ~30%.
* crypto: 新增 privateEncrypt/publicDecrypt 方法.
* errors
  - 优化 util.inspect 格式化结果
  - fs 抛出的错误, 新增更详细的描述. 这需要一个 `NODE_MODULE_VERSION` bump.
  - http.setHeader 抛出的错误, 新增更详细的描述
* 依赖更新:
  - npm: 更新到 2.4.1
  - http-parser: 回滚到 2.3.0
  - libuv: 更新到 1.3.0
  - v8: 更新到 4.1.0.14
* http.request: 从选项中继承属性
* buffers 新增了可迭代接口 (`for (let byte of buffer.values()) { }`)
* fs: 修复 `fs.createReadStream` 的 fd 泄露. 详情参看 497fd72.
* installer: Windows 平台完成安装后, 触发 WM_SETTINGCHANGE 事件,
    用以让其他运行中进程知晓 PATH 的变化
* 新增贡献者:
  - Vladimir Kurchatkin (@vkurchatkin)
  - Micleușanu Nicu (@micnic)

### 已知问题

* REPL 中的 Surrogate pair 会导致终端僵死 (https://github.com/iojs/io.js/issues/690)
* io.js 无法作为静态库编译 (https://github.com/iojs/io.js/issues/686)

## [2015-01-24, 版本 1.0.4, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-01-24-version-104-rvagg)

### 主要更新

* npm 更新到 2.3.0 修复 Windows "uid is undefined" 错误
* crypto.pseudoRandomBytes() 现在是 crypto.randomBytes() 的别名方法,
  如果没有足够的 entropy 用以产生安全的值则会阻塞. 详情参看 https://github.com/iojs/io.js/commit/e5e5980.
* 给 V8 打补丁, 用于检测 ARMv6; 使程序又能在 ARMv6 上运行 (Raspberry Pi 等.)
* V8 小幅更新 4.1.0.7 to 4.1.0.12
* 'punycode' 核心模块状态, 从不稳定变为稳定
* 新增贡献者:
  - Thorsten Lorenz (@thlorenz)
  - Stephen Belanger (@qard)
  - Jeremiah Senkpiel (@fishrock123)
  - Evan Lucas (@evanlucas)
  - Brendan Ashworth (@brendanashworth)

## [2015-01-20, 版本 1.0.3, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-01-20-version-103-rvagg)

### 主要更新

* V8 从 3.31 升级到 4.1, 这并不是一个大版本升级, 版本号 "4.1" 表示
 与 Chrome 41 保持同步. 3.31 分支 没有与稳定版本保持同步.
* 重新支持 Windows XP / 2003
* npm 更新 2.2.0
* 提高 FreeBSD 支持

### 已知问题

* ARMv6 平台仍然无法编译, V8 的 this 有一个停顿(hold-up), 问题 #283
* Template strings 在 V8 4.1 会导致segfaults, https://codereview.chromium.org/857433004, 问题 #333

## [2015-01-16, 版本 1.0.2, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-01-16-version-102-rvagg)

### 主要更新

* Windows 安装包问题修复
* windows 安装包的 node-gyp 问题修复
* [http_parser v2.4.1 升级](https://github.com/joyent/http-parser/compare/v2.3...v2.4.1)
* [libuv v1.2.1 升级](https://github.com/libuv/libuv/compare/v1.2.0...v1.2.1)

## [2015-01-14, 版本 1.0.1, @rvagg](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#2015-01-14-version-101-rvagg)

因为 1.0.0 版的旧的编译 slave git reflogs 重新编译

* doc: 提高书写一致性 (Rui Marinho)
* win,msi: 修复文档网址链接 (Bert Belder)

--------------------------------------

以下是当前_稳定版_的 Node.js(v0.10.35) 到 io.js(v1.0.0) 的变更概要。v1.0.0 发布时 Node.js 最新的_非稳定版_为 v0.11.14，并正在准备发布 v0.11.15。io.js 的代码是源于 [joyent/node](https://github.com/joyent/node) v0.11 分支，包括其中的大部分变更，因此可视为 v0.11 的扩充。

## [Node.js v0.10.35 到 io.js v1.0.0 的变更概要](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#summary-of-changes-from-nodejs-v01035-to-iojs-v100)

### General

- io.js 内置的 V8 引擎升级幅度很大，从 Node.js v0.10.35 的 3.14.5.9 和 Node.js v0.11.14 升级到 io.js v1.0.0 的 3.31.74.1。他修复了很多 bug 且提升了性能，而且额外增加了新的 ES6 特性。获取更多信息请查看 [io.js ES6 页面](https://iojs.org/es6.html)
- 其他内置的模块也相应升级了：
  - c-ares: 1.9.0-DEV 升级到 1.10.0-DEV
  - http_parser: 1.0 升级到 2.3
  - libuv: 0.10.30 升级到 1.2.0
  - npm: 1.4.28 升级到 2.1.18
  - openssl: 1.0.1j 升级到 1.0.1k
  - punycode: 1.2.0 升级到 1.3.2.
- 所有平台优化了性能和稳定性

### buffer

https://iojs.org/api/buffer.html

- 新增 `buf.writeUIntLE`, `buf.writeUIntBE`, `buf.writeIntLE`, `buf.writeIntBE`, `buf.readUIntLE`, `buf.readUIntBE`, `buf.readIntLE` and `buf.readIntBE` 方法，支持6个字节读写。
- 新增 `Buffer.compare()` 方法，使用 `memcmp()` 对比两个 Buffer 实例的内存区域，实例也有一个 `compare()` 方法。
- 新增 `buffer.equals()` 方法，对比 Buffer 的内容是否一致。
- 新增 `new Buffer(otherBuffer)` 构造函数。
- 调整 `SlowBuffer` 的语义
- 更新 `buffer.toJSON()` 的输出，不再输出数组而是输出一个对象。此对象可被标记为一个 buffer 并且可以传入到 Buffer 构建函数中重新实例化。

### child_process

https://iojs.org/api/child_process.html

- `child_process.exec` 新增了一个 `shell` 的参数。
- 新增一系列同步的方法：`child_process.spawnSync`, `child_process.execSync`, and `child_process.execFileSync`。
- 给 `ENOENT` 错误新增了路径，方便调试。

### console

https://iojs.org/api/console.html

- `console.dir` 新增了一个 `options` 参数。

### cluster

https://iojs.org/api/cluster.html

- 更新了 cluster 模块，在非 Windows 平台默认使用 round-robin 负载均衡算法，该项可以配置。
- 支持了 `--debug` 调试
- 修复了很多 bug

### crypto

https://iojs.org/api/crypto.html

- Added support for custom generator values to `DiffieHellman` (defaulting to 2 for backwards compatibility).
- Added support for custom pbkdf2 digest methods.
- Added support for elliptic curve-based Diffie-Hellman.
- Added support for loading and setting the engine for some/all OpenSSL functions.
- Added support for passing in a passphrase for decrypting the signing key to `Sign.sign()`.
- Added support for private key passphrase in every method that accepts it.
- Added support for RSA public/private encryption/decryption functionality.
- Added support for setting and getting of authentication tags and setting additional authentication data when using ciphers such as AES-GCM.

### dgram

https://iojs.org/api/dgram.html

- 新增支持接受 UDP 空包。

### dns

https://iojs.org/api/dns.html

- 新增 `dns.resolveSoa`, `dns.getServers`, and `dns.setServers` 方法。
- 在错误信息上添加 `hostname`
- 优化错误处理的一致性

### events

https://iojs.org/api/events.html

- 新增 `EventEmitter.setMaxListeners` 的链式调用
- `require('events')` 直接返回 `EventEmitter` 构造函数，可直接使用这个模块，如 `var EventEmitter = require('events')` 而不是 `var EventEmitter = require('events').EventEmitter`。

### fs

https://iojs.org/api/fs.html

- 新增 `fs.access`，弃用 `fs.exists`，请仔细阅读文档。
- NODE_DEBUG 的值非空时显示更多的错误信息以及方法调用的具体位置来优化调试。
- 新增 `fs.watch` 的参数支持子目录递归（只支持 OS X）。
- 修复 callback 不存在会异常的情况，只打印错误。

### http

https://iojs.org/api/http.html

- 新增支持 `response.write` 和 `response.end` 接受一个 callback，当操作完成后被执行。
- 新增 308 状态码的支持（详见 RFC 7238）。
- 新增 `http.METHODS` 数组，列出所有解析器支持的 HTTP 方法。
- 新增 `request.flush` 方法。
- 新增 `response.getHeader('header')` 方法，可以在发送响应头之前调用。
- 新增 `response.statusMessage` 属性。
- 新增客户端 Keep-Alive 行为，在 request 的 options 设置 `keepAlive:true` 可无限重用连接。
- 在 incoming message 新增 `rawHeaders` 和 `rawTrailers` 属性。
- 删除 `DELETE` 和 `OPTIONS` 默认的分块编码。

### net

https://iojs.org/api/net.html

- `net.Server.listen` 变更，当绑定的地址被忽略后，先尝试 IPv6，如果失败再尝试 IPv4。

### os

https://iojs.org/api/os.html

- `os.networkInterfaces` 方法新增 IPv6 的 MAC 地址，网络掩码和范围 ID。
- 更新 Windows 平台的 `os.tmpdir`，当定义临时目录的时候，使用 `%SystemRoot%` 或 `%WINDIR%` 环境变量，而不是硬编码的 `c:\windows`。

### path

https://iojs.org/api/path.html

- 增加了 `path.isAbsolute` 和 `path.parse` 方法。
- 增加了 `path.win32` 和 `path.posix` 对象，他们分别包含了对应平台的 `path` 的实现。
- 提升了 `path.join` 的性能。

### process

https://iojs.org/api/process.html

- 增加了 `beforeExit` 事件。
- 增加了 `process.mainModule` 和 `process.exitCode`。

### querystring

https://iojs.org/api/querystring.html

- stringifying 或者 parsing 一个 query string 的时候可传入自定义的 `encodeURIComponent` 和 `decodeURIComponent` 方法。
- 修复了几个格式化 query string 边缘场景下的问题。

### smalloc

https://iojs.org/api/smalloc.html

`smalloc` 是一个新的核心模块， 用于在 javascript 中 分配、释放和复制(外部的)内存空间。

### streams

https://iojs.org/api/stream.html

streams 的变化没有从 stream1 到 stream2 那样剧烈：它们是对现有想法的改进，让 API 更加友好，同时运行速度更快。所有的这些变更也称为 "stream3"，但是这些变更对大多数使用者来说是透明的，大都不需要太关心。

#### Readable streams

The distinction between "flowing" and "non-flowing" modes has been refined. Entering "flowing" mode is
no longer an irreversible operation&mdash;it is possible to return to "non-flowing" mode from "flowing" mode.
Additionally, the two modes now flow through the same machinery instead of replacing methods. Any time
data is returned as a result of a `.read` call that data will *also* be emitted on the `"data"` event.

As before, adding a listener for the `"readable"` or `"data"` event will start flowing the stream; as
will piping to another stream.

#### Writable streams

The ability to "bulk write" to underlying resources has been added to `Writable` streams. For stream
implementers, one can signal that a stream is bulk-writable by specifying a [_writev](https://iojs.org/api/stream.html#stream_writable_writev_chunks_callback) method.
Bulk writes will occur in two situations:

1. When a bulk-writable stream is clearing its backlog of buffered write requests,
2. or if an end user has made use of the new `.cork()` and `.uncork()` API methods.

`.cork` and `.uncork` allow the end user to control the buffering behavior of writable streams separate
from exerting backpressure. `.cork` indicates that the stream should accept new writes (up to `highWaterMark`),
while `.uncork` resets that behavior and attempts to bulk-write all buffered writes to the underlying resource.

The only core stream API that **currently** implements `_writev` is `net.Socket`.

In addition to the bulk-write changes, the performance of repeated small writes to non-bulk-writable streams
(such as `fs.WriteStream`) has been drastically improved. Users piping high volume log streams to disk should
see an improvement.

For a detailed overview of how streams3 interact, [see this diagram](https://cloud.githubusercontent.com/assets/37303/5728694/f9a3e300-9b20-11e4-9e14-a6938b3327f0.png).

### timers

https://iojs.org/api/timers.html

- 移除 `process.maxTickDepth`, 允许 `process.nextTick` 被无限迭代调用
- 更新 `setImmediate` 允许在一次事件循环处理完整队列, 而不是每次一个.

### tls

https://iojs.org/api/tls.html

- 新增 `detailed` 布尔标志到 `getPeerCertificate` 来返回详细的认证信息 (带有原始 DER 字节).
- 新增 `renegotiate(options, callback)` 方法用于回话 renegotiation.
- 新增 `setMaxSendFragment` 方法用以调整 TLS 碎片大小.
- 新增 `dhparam` 选项 到 DH 密码.
- 新增 `ticketKeys` 选项到 TLS ticket AES 加密钥匙设置.
- 新增异步 OCSP-stapling 回调.
- 新增异步会话存储事件
- 新增异步 SNI 回调.
- 新增多 key 服务器支持 (例如, ECDSA+RSA 服务器).
- 新增可选回调到 `checkServerIdentity` 来让用户手动认证验证
- 新增对 ECDSA/ECDHE 密码支持.
- 用 C++ 实现 TLS 流, 从而提升性能.
- 把 `createCredentials` 移到 `tls` 并重命名为 `createSecureContext`.
- 移除对 SSLv2 和 SSLv3 的支持.

### url

https://iojs.org/api/url.html

- 优化特殊字符的转义.
- 提升解析速度

### util

https://iojs.org/api/util.html

- 新增 `util.debuglog`.
- 新增多个类型检测方法. 查看[文档](https://iojs.org/api/util.html).
- 对 `util.format` 进行了几处更新:
  - `-0` 原样打印, 而不是 `0`.
  - 所有 error 实例 `instanceof Error` 都会被格式化成 error.
  - JavaScript 中的循环引用, 现在被处理为 `%j` 说明符. (TO REVIEW)
  - 允许自定义 `inspect` 方法返回一个对象.
  - 自定义 `inspect` 方法现在会接受所有传给 `util.inspect` 的参数.

## v8

https://iojs.org/api/v8.html

`v8` 是一个全新的核心模块, 用于直接同 V8 引擎交互.

### vm

https://iojs.org/api/vm.html

`vm` 被基于卓越的[Contextify](https://github.com/brianmcd/contextify) native 模块完全重写, 从而工作的更好,
Contextify 所有的功能被加入到了核心模块中, 并进行了优化.

- 新增 `vm.isContext(object)` 方法来确定一个`object` 是否被 contextified.
- 新增 `vm.runInDebugContext(code)` 方法用以在 V8 调试环境编译和执行 `code`.
- 更新 `vm.createContext(sandbox)` 来 "contextify" 沙盒, 使它能够作为 `vm` 脚本的全局环境, 然后返回它. 它不会创建单独的 context 对象
- 更新 `vm` 和 `vm.Script` 的大部分方法, 能接受一个 `options` 对象, 允许用户为脚本自定义 timeout, 错误的展示方式, 以及文件名 (用户栈追踪).
- 修改提供的沙盒对象, 从而可直接用做全局环境, 去除提供的沙盒对象和通过运行 `vm` 模块出现在脚本内部的全局对象之间的错误试探性属性拷贝
关于详细信息, 参看上面的文档链接

### zlib

https://iojs.org/api/zlib.html

- 新增支持 `zlib.flush` 指定特殊的 flush 方法 (默认为 `Z_FULL_FLUSH`).
- 新增支持 `zlib.params` 来在压缩时动态更新压缩级别和策略.
- 新增同步版本的 zlib 方法.

### C++ API Changes

https://iojs.org/api/addons.html

通常情况下, 建议使用 [NAN](https://github.com/rvagg/nan) 作为 addons 的兼容层, 未来他也会帮助处理 V8, 以及 Node/io.js C++ API 的变化.
下面的大部分修改 NAN 都有对应的 wrapper 进行处理.

#### V8 highlights

- Exposed method signature has changed from `Handle<Value> Method(const Arguments& args)` to `void Method(const v8::FunctionCallbackInfo<Value>& args)` with the newly introduced `FunctionCallbackInfo` also taking the return value via `args.GetReturnValue().Set(value)` instead of `scope.Close(value)`, `Arguments` has been removed.
- Exposed setter signature has changed from `void Setter(Local<String> property, Local<Value> value, const v8::AccessorInfo& args)` `void Setter(Local<String> property, Local<Value> value, const v8::PropertyCallbackInfo<void>& args)`.
- Exposed getter signature has changed from `void Getter(Local<String> property, Local<Value> value, const v8::AccessorInfo& args)` `void Setter(Local<String> property, Local<Value> value, const v8::PropertyCallbackInfo<Value>& args)`.
- Exposed property setter signature has changed from `Handle<Value> Setter(Local<String> property, Local<Value> value, const v8::AccessorInfo& args)` `void Setter(Local<String> property, Local<Value> value, const v8::PropertyCallbackInfo<Value>& args)`.
- Exposed property getter signature has changed from `Handle<Value> Getter(Local<String> property, Local<Value> value, const v8::AccessorInfo& args)` `void Setter(Local<String> property, Local<Value> value, const v8::PropertyCallbackInfo<Value>& args)`.
- Similar changes have been made to property enumerators, property deleters, property query, index getter, index setter, index enumerator, index deleter, index query.
- V8 objects instantiated in C++ now require an `Isolate*` argument as the first argument. In most cases it is OK to simply pass `v8::Isolate::GetCurrent()`, e.g. `Date::New(Isolate::GetCurrent(), time)`, or `String::NewFromUtf8(Isolate::GetCurrent(), "foobar")`.
- `HandleScope scope` now requires an `Isolate*` argument, i.e. `HandleScope scope(isolate)`, in most cases `v8::Isolate::GetCurrent()` is OK.
- Similar changes have been made to `Locker` and `Unlocker`.
- V8 objects that need to "escape" a scope should be enclosed in a `EscapableHandleScope` rather than a `HandleScope` and should be returned with `scope.Escape(value)`.
- Exceptions are now thrown from isolates with `isolate->ThrowException(ExceptionObject)`.
- `Context::GetCurrent()` must now be done on an isolate, e.g. `Isolate::GetCurrent()->GetCurrentContext()`.
- `String::NewSymbol()` has been removed, use plain strings instead.
- `String::New()` has been removed, use `String::NewFromUtf8()` instead.
- `Persistent` objects no longer inherit from `Handle` and cannot be instantiated with another object. Instead, the `Persistent` should simply be declared, e.g. `Persistent<Type> handle` and then have a `Local` assigned to it with `handle.Reset(isolate, value)`. To get a `Local` from a `Persistent` you must instantiate it as the argument, i.e. `Local::New(Isolate*, Persistent)`.

#### Node / io.js

- 更新 `node::Buffer::New()` 来直接返回一个 `Handle`, 这样就没有必要再去获取 `handle_` 属性.
- 更新 `node::MakeCallback()` 它需要 `Isolate*` 作为第一个参数. 通常情况 `Isolate::GetCurrent()` 就已经够用.

--------------------------------------

**[之前的更新记录从 joyent/node 项目继承到 io.js 项目中。](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md#20140924-version-01114-unstable)**
