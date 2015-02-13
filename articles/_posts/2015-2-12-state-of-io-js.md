---
layout: post
title: io.js 的现状
author: mikeal
reference: https://medium.com/node-js-javascript/state-of-io-js-2b3094e6f923
---

> 这是我有生之年经历过的最积极与开放的开源项目。

io.js 发布后的这几个月间发生了许多事。我们把一个非常重要的发布日期定在 **Fedor 的生日**，也就是 1 月 13 日。在一大群人的努力工作后，虽然剩下的时间不多，但我们最终完成了这个雄心壮志的目标。☺

第一个 io.js 释出版本，加上 4 个补丁（patch）版本，总共被下载了**超过 40 万**次。

参与项目的代码贡献者数量在所有人的预料之外。由于 [Chris Dickinson](https://github.com/chrisdickinson) 与 [Colin Ihrig](https://github.com/cjihrig) 的杰出贡献，最先被加入到了 [技术委员会（TC）](https://github.com/iojs/io.js/blob/v1.x/GOVERNANCE.md#iojs-project-governance) (这个技术委员会负责项目的运作)，后来，我们又邀请了 [Domenic Denicola](https://github.com/domenic) ———— 他同时也是 [v8](https://twitter.com/rvagg/status/558378711624343552) 与 **TC39** 的优秀贡献者 ———— 作为非投票参与者加入到了技术委员会的会议中来。除此之外，我和 [Rod Vagg](https://github.com/rvagg) 也是非投票参与者的其中成员。

值得注意的是，在 node.js™ 的开发过程中从未超过 8 位活跃贡献者。但仅在上周，**Chris Dickinson** 就招募了 [8 位新的代码贡献者](https://github.com/iojs/io.js/issues/234#issuecomment-71097752) 加入 io.js 的开发，他们将要参与到本周的其他开发计划中去。

本次 io.js 释出版本是基于**确定标记为稳定版 v8 引擎**发布的，这个版本的 v8 引擎将于**三月上旬**跟随新版本的 Chrome 一齐发布。从此开始，我们会同时存在两个版本，稳定版本的 io.js 打包上一个稳定版本的 v8 引擎，而不稳定分支会包含 v8 计划开发中的更新。简单来说，**可以认为 io.js 在三月份就会有稳定版本释出**。而同时不稳定分支会继续开发和测试包括 io.js 和 v8 的新功能特性。

核心开发以外的一些任务也已经发展到一定阶段，他们有必要拥有自己的小组和贡献者。除了起初伴随项目建立的 [构建小组](https://github.com/iojs/build) 之外，我们还新建了 [网站小组](https://github.com/iojs/website) 和 [stream 开发小组](https://github.com/iojs/readable-stream)，与此同时，我们也希望未来一段时间能有其他投入到 **io.js 宣传布道, 文档建设, i18n 本地化工作, [nan](https://github.com/rvagg/nan) 开发,** 与 **roadmap 制定** 等工作上去，这些工作更宽泛，也需要社区的更多贡献者参与进来。

起初当我们筹划 io.js 项目时，最大的顾虑就是缺乏 node.js™ 的贡献者。但现在，面对众多参与到项目中的贡献者，io.js 的最大问题是如何将项目中方方面面的工作，有效地分配给他们。从这个角度来说，io.js 虽然不如**现在的** node.js™，但比它**刚起步时**，要健康得多。而这仅仅是个开始。
