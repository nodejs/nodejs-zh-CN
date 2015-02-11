# Getting to know io.js

- Authors: @Ralph Whitbeck
- Referer: [https://developer.atlassian.com/blog/2015/01/getting-to-know-iojs/](https://developer.atlassian.com/blog/2015/01/getting-to-know-iojs/)

===

上个星期, Twitter 上许多在讨论 [io.js](http://iojs.org) 的最初版本. io.js 是一个 npm 平台兼容、 源于 Node.js 并且是 Joyent's [Node.js](http://nodejs.org/) 的 fork 版本.

## 为什么 fork Node.js?

io.js 开发团队主要由 Node.js 的[关键的贡献者](https://github.com/iojs/io.js/blob/v1.x/README.md#current-project-team-members)组成. 在八月份的时候, 该团队创建了 [Node Forward](http://nodeforward.org/), 目的是尝试通过社区来帮助改善Node.js. 

> 一个致力于通过开放合作改善 Node，JavaScript 和其生态系统的社区。

这其中我们可以了解到为什么该社区不得不 fork Nodejs 的原因:

> 在许多人被分散在众多小项目中，需要新的协同空间来成长的时候，出现了需要比传统授权更开放的所有权和贡献权才能解决的问题。对于 Node Forward 而言，要解决这些问题合作才能进行。

结果是, 由于 Node 商标权的限制该社区所做的贡献不能发布, 于是他们决定 fork node.js，然后 io.js 便诞生了.

[Isaac Schlueter](https://twitter.com/izs) 是核心贡献者, [provides a lot of the backstory behind the decision to fork on his personal blog](http://blog.izs.me/post/104685388058/io-js). 一个重要的信息是, io.js 的意图是两个项目能在未来某个时候合并. 

## io.js 做了什么新改动?

首先, io.js 引入了真正的 [语义版本控制 (semver)](http://semver.org/) by tagging the release 1.0.0 because it's such a divergence from Node.js. jQuery 团队在[近期的博客文章](http://blog.jquery.com/2014/10/29/jquery-3-0-the-next-generations/) 中讨论了关于使用 semver 的重要性:

> 其中一个最好的做法是语义版本，或简单称之semver。在实践中，semver给了开发者（以及构建工具）一个避免切换软件版本风险的一个办法。版本号以MAJOR.MINOR.PATCH的形式，其三个组成部分均为整数。在semver中，如果MAJOR变化了，这表示API中有开发者更改需要注意的断层变更。

## 最新的 V8 引擎

io.js 将 V8 JavaScript 引擎更新到了 3.31.74.1，而该版本的 V8 是最显著的支持 ES6 新特性的版本，使用该版本不用再加上 `--harmony` 标志来启用新特性了.

### 可用的 ES6 特性

以下列出 io.js 已经可以使用的，不需要指定任何标志的新特性。

*   [Block scoping (`let`, `const`)](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-let-and-const-declarations)
*   Collections ([`Map`](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-map-objects), [`WeakMap`](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-constructor-properties-of-the-global-object-weakmap), [`Set`](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-set-objects), [`WeakSet`](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-constructor-properties-of-the-global-object-weakset))
*   [Generators](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-generator-function-definitions)
*   [Binary and Octal literals](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-literals-numeric-literals)
*   [Promises](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-promise-jobs)
*   [New String methods](http://www.sitepoint.com/preparing-ecmascript-6-new-string-methods/)
*   [Symbols](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-ecmascript-language-types-symbol-type)
*   [Template strings](https://people.mozilla.org/~jorendorff/es6-draft.html#sec-static-semantics-templatestrings)

### 新 modules

io.js 提供了一些新的实验性的内置模块 (modules):

*   [smalloc](https://iojs.org/api/smalloc.html): 允许你在 JavaScript 中手动进行 raw 内存的分配/释放/拷贝。
*   [v8](https://iojs.org/api/v8.html): 暴露 io.js 中 V8 的事件和接口。

你可以在 [io.js 更新日志](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md) 中看到详细的变动.

## 运行 io.js

运行 io.js 应用与运行 node 应用一样，唯一的区别是可执行文件的名字改变了。

Node.js

    $ node app.js

io.js

    $ iojs app.js

### Node 版本管理器

[Node 版本管理器 (nvm)](https://github.com/creationix/nvm), 是一个用来管理 node.js 版本的工具, 而且现在也支持安装各个版本的 io.js. 如果你已经安装了 nvm 就可以在终端下运行以下命令来列出可用的 io.js 版本:

    $ nvm ls-remote v1
        iojs-v1.0.0
        iojs-v1.0.1
        iojs-v1.0.2
        iojs-v1.0.3

接着你就可以通过其中的某个版本名来安装 io.js 到你的项目文件夹中.

    $ nvm install iojs-v1.0.3

**Note:** 到目前为止, 建议通过 nvm 安装 io.js. 许多早期通过 io.js 官网上的安装文件安装的人表示其是替换安装. 而 nvm 允许你针对不同的项目文件夹设置不同版本的 io.js.

## Trying it out

想要通过 [Atlassian Connect](https://developer.atlassian.com/static/connect/docs/index.html)  扩展来测试 io.js? 你可以快速使用 io.js 运行 HipChat 扩展，并按照以下简单步骤利用如 Generators 的 ES6 新特性：

1.  来到 [HipChat 扩展入门指南](https://www.hipchat.com/docs/apiv2/quick_start?utm_source=dac&amp;utm_medium=blog&amp;utm_campaign=getting-to-know-iojs) 根据教程构建扩展，并运行 [atlassianlabs/ac-koa-hipchat](https://bitbucket.org/atlassianlabs/ac-koa-hipchat?utm_source=dac&amp;utm_medium=blog&amp;utm_campaign=getting-to-know-iojs) 框架（详见入门指南）

2.  `vagrant ssh` 连接到步骤1中设置的 vagrant 服务器. 你可以通过下列命令来安装 nvm:


    curl https://raw.githubusercontent.com/creationix/nvm/v0.23.0/install.sh | bash


该命令会安装 nvm 并更新你的 shell. 接下来你需要输入 `exit` 命令来关闭 ssh 连接并重启 shell.

3.  打开 `package.json` 并编辑 web 选项的脚本，来使用 io.js 替代 Node.js:

    "scripts": {
     "web": "iojs web.js",
     "web-dev": "nodemon --harmony -e js,json,css,hbs web.js"
    },

4.  再次运行 `vagrant ssh` 来重启服务器 shell 并且运行下面的命令来启动应用:

    $ cd project && npm start web

该命令会开启使用 Koa 的 HipChat 扩展服务器，然后你可以通过下列 URL 来给你的扩展注册一个 HipChat 聊天室:

     `https://xxxxxxxx.ngrok.com/addon/capabilities`

      where `xxxxxxxx.ngrok.com` is the url specified in the shell after the  server starts up.

如果你可以在聊天框中输入 `/hello` 之后获得 HipChat 扩展回答的 "Hi" 那么恭喜! 你现在正在利用如 Generators 的 ES6 新特性运行一个 io.js 应用.

## 你会使用 io.js 吗?

你可能会问自己，现在我会用 io.js 来运行我的 Node 扩展吗？眼下 io.js 的年龄刚过一周，在写这篇文章时的最新版本 V1.0.3 仍被贴上“不稳定”的标签。像 nvm 这样的服务还存在 bug。还没有运营商宣布支持它。现在，如果你支持 io.js，并希望看到一个“稳定”版的 io.js，欢迎使用 io.js 测试你的扩展并发现 [issues](https://github.com/iojs/io.js/issues)。归根结底，现在切换到 io.js 还太早，但它值得关注，说不定它会成为最流行的服务端JavaScript平台。
