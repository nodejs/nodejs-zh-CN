---
layout: post
title: Node.js vs io.js: Why the fork?!?
author: Anand Mani Sankar
reference: http://anandmanisankar.com/posts/nodejs-iojs-why-the-fork/#.VO82hE60PVw.twitter
---

在几个月的沉寂之后，我也回来参与在过去的几个月中已经入侵许多技术讨论区的话题.

**Node.js，这个流行的服务端 JavaScript 运行环境被 fork 了!**

Node.js 已经在过去被 fork 很多了，比如 [JXcore](http://jxcore.com) 为 NodeJS 提供了多线程特性。不过，为何最近的 fork 会引起极大的讨论/争辩？因为，这可不仅仅是普通的代码 fork，同时也可以说是一些 NodeJS 项目的重要贡献者的 fork。[Node 中最重要的5个贡献者](https://github.com/joyent/node/graphs/contributors)其中4个是 [io.js](https://iojs.org) 项目的成员。

关于被 fork 的可能性已经在过去的几个月里被反复讨论了，不过这个 fork 版本的 [io.js](https://iojs.org) 是在2015年一月正式发布了第一个版本。

## Why the fork?

在过去一年左右的时间，Node.js 项目的提交数量一直在稳步下降。

![Node.js commit trend](http://anandmanisankar.com/assets/images/node_commits.png "Node.js commit trend")

更糟糕的是，node 的新版本发布数在 2014 年大幅下降。

![Node.js release trend](http://anandmanisankar.com/assets/images/node_releases.png "Node.js release trend")

但是，fork node.js 的主要原因之一是对于 Joyent 公司处理项目方式的不满。Bryan Cantrill 在他的[博文](https://www.joyent.com/blog/the-power-of-a-pronoun)中阐述了一些观点。

> io.js - Node.js 的 fork 版, 就是不满 Joyent 公司在 Node.js 项目管理工作的结果.

2014年中期，在某些开发者对 Joyent 公司作为 Node.js 项目的管家角色感到不满之后，开始讨论 fork 的可能性。一些核心贡献者试图与 Joyent 公司合作构建一个组织结构，使贡献者和社区可以介入解决各种问题（有的表示通过上面的图表）。为了改善 Node 和它的生态系统，一些贡献者们以 ‘[Node Forward](http://nodeforward.org/)’ 的名义做了一些努力。

但是 [Fedor Indutny](https://github.com/indutny), 一名 Node.js 团队核心成员，厌倦了无处讨论的情况，并开始了从 Node.js 到 io.js 的 fork 工作。其他与 Fedor 相熟的贡献者也自愿加入其中。

Joyent 公司随后通过成立用于开放式管理的 [Node Advisory Board](https://www.joyent.com/blog/node-js-advisory-board) 来应对，不过这似乎有点太晚了。

> 我们不希望只有那些被公司指派的人来参与讨论。我们希望贡献者有更多的控制，以寻求共识。
> 
> <cite>— Mikeal Rogers, io.js 项目团队成员</cite>

其实 fork 只是突出了一个开源项目的“企业赞助商”和“参与贡献的开发者社区”之间的紧张关系。

但对于 Joyent 公司的 CTO Bryan Cantrill 而言，Node 是活跃并且良好的，尽管发展速度放缓。

> 你得关注贡献者的质量，而不是数量。
> 
> <cite>— Bryan Cantrill, CTO, Joyent</cite>

## 现状

### io.js 简介

*   从 Joyent 的 Node.js v0.12 版本 fork 而来
*   与 npm 生态系统完全兼容
*   将采用尽可能快的新的 V8 版本

    *   io.js 基于 V8 的 v4.1.0.14 版本，而 Node 依旧是 v3.28.73
    *   新 V8 带来了许多性能改进和修正
    *   同时, 也支持了更多 [ES6 新特性](https://iojs.org/en/es6.html)
*   新的 (实验性质的) 核心 modules
    *   [V8](https://iojs.org/api/v8.html)：直接与 V8 交互的接口
    *   [smalloc](https://iojs.org/api/smalloc.html)：允许你在 JavaScript 中手动进行 raw 内存的分配/释放/拷贝。
*   语义版本控制 ([semver](http://semver.org/)), 从 v1.0.0 开始
*   每周的生产计划发布
*   Bug 修复，在需要的情况下有选择的从 Node 加入到 io.js 中
*   [开放式管理模式](https://github.com/iojs/io.js/blob/v1.x/GOVERNANCE.md)：贡献者享有更多权利

## 我的看法

io.js 显然已经证明，一个项目可以通过开放治理而更快成长。从2015年1月13日开始到现在（注：2015/2/24），io.js 已经有了10个发布版！

![io.js 的 commit 趋势](http://anandmanisankar.com/assets/images/iojs_commits.png "io.js 的 commit 趋势")

但是情况依旧存在两面性！同一段代码可能是在支持 io.js 但是同时也能对其产生消极的效果。

### 正面性

*   开放式管理，分布式控制
*   更快的版本发布
*   更加新的 V8
*   ES6 优势

### 反面性

*   Node 是相当稳定并且部署稳妥。为什么要换？
*   对于不少人来说，技术集合（更加新的V8、ES6的支持等等）不是足够诱人
*   不是许多公司都在抱怨 Node 更新慢

如果我引用 apache web server、hadoop 或者 linux 作为基金会驱动的开源举措的好例子，有人就会以 Ruby on Rails 或者 Docker 这种单独的公司带动OSS的成功举措作为回应。因此，凡是都是有两面性的！

无论 io.js 是否获得收益，都将源于用户的使用。作为 Uber 首席系统架构师, Matt Ranney 早已发推特讨论将 io.js 投入部署使用。

> 我是最早大规模使用 io.js 作为生产环境的人之一。
> — Matt Ranney ([@mranney](https://github.com/mranney)) [2014/12/3](https://twitter.com/mranney/status/540013975568535553)

<script async="" src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

不过，我认为 fork 只是由 Node 核心社区的一些关键贡献者进行以下意图的探索:

*   Accelerate release of latest advancements in JavaScript as fast as the community feels necessary
*   支持一个开放的管理模式是针对单个企业的管理工作

从用户的角度来看，我相信 io.js 当前 只是解决 Node.js 中的一些 first-world 问题。 It does not yet warrant a switch from Node. 事实上，它只是在忽悠并且迫使用户去做多余的决定。

但是从社区/贡献者的角度来看， **我认为这是一个在正确方向上的 动作 - 如果你将 io.js 视为一个告诉 joyent 如何良好管理一个开源项目的试验品**。 This is one of the reasons I like the ‘OPEN Open Source’ model which [Rod Vagg](https://github.com/rvagg) came up with for the [LevelUp project](https://github.com/rvagg/node-levelup) (a node wrapper for LevelDB).

> 有显著和宝贵的贡献的个人被给予提交权限，并让他们做他们认为适合的贡献。这比起标准森严的开源项目而言更像是一个开放的维基百科。

## 展望：Node 和 io.js 将会合并

有些事情是很清楚的：

*   没有人希望 Node 出现多个 fork 版并使得决策过程更加复杂
*   不论 io.js 还是 node forward 都不存在“创建第二个 Node.js”这个目标
*   维护 fork 版本需要的精力是巨大的

io.js - ‘友好的 fork’, **不打算** 与 Node 竞争。日后，一旦协同决策过程达成协议，io.js 一脉将会与 Node 合并。实际上，[和解进程已经开始](https://medium.com/@iojs/io-js-and-a-node-js-foundation-4e14699fb7be)。Joyent 公司 CEO Scott Hammond 已经邀请了 io.js 技术委员会参加私人会议来讨论 Node 基金会，并且正在带 io.js 回到 node.js 项目。

Node 基金会预计有两个委员会: 基金会董事和技术会员会。技术委员会将会独立操作 foundation board, 给它所需的自由来驱动项目的技术发展。至于技术委员会是否会享有像 io.js 这样开放式的治理模式，目前还尚未明确。([William Bert](https://twitter.com/williamjohnbert) 创建了一个[推特活动](http://nodegovernance.io/) 艾特 Scott Hammond 以表达社区希望 Node 基金会采用 io.js 治理模式)。可能发生的最好的情况是二者合并成功，两全其美。

现在球在 Joyent 的主场！

* * *

#### **更新: 2015/2/27**

[Mikael](https://github.com/mikeal) has created a work-in-progress [‘Reconciliation Proposal’](https://github.com/iojs/io.js/issues/978) that covers topics like technical governance, long-term support, versioning and WG structuring proposals for a future ‘Node’ which re-unites ‘Node.js’ and ‘io.js’.

* * *
