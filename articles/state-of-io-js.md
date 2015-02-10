# io.js 的现状

- Authors: @mikeal
- Referer: https://medium.com/node-js-javascript/state-of-io-js-2b3094e6f923

===

这是我有生之年经历过的最积极与开放的开源项目。

io.js 发布后的这几个月间发生了许多事。我们把一个非常重要的发布日期定在 **Fedor 的生日**，也就是 1 月 13 日。在一大群人的努力工作后，虽然剩下的时间不多，但我们最终完成了这个雄心壮志的目标。☺

第一个 io.js 释出版本，加上 4 个补丁（patch）版本，总共被下载了 **超过 40 万** 次。

参与项目的代码贡献者数量在所有人的预料之外。由于 [Chris Dickinson](https://github.com/chrisdickinson) 与 [Colin Ihrig](https://github.com/cjihrig) 的杰出贡献，最先被加入到了技术委员会 [TC](https://github.com/iojs/io.js/blob/v1.x/GOVERNANCE.md#iojs-project-governance) (这个技术委员会负责项目的运作)，后来，我们又邀请了 [Domenic Denicola](https://github.com/domenic) ———— 他同时也是 [v8](https://twitter.com/rvagg/status/558378711624343552) 与 **TC39** 的优秀贡献者 ———— 作为非投票参与者加入到了技术委员会的会议中来。除此之外，我和 [Rod Vagg](https://github.com/rvagg) 也是非投票参与者的其中成员。

值得注意的是，在 node.js™ 的开发过程中从未超过 8 位活跃贡献者。但仅在上周，**Chris Dickinson** 就招募了 [8 位新的代码贡献者](https://github.com/iojs/io.js/issues/234#issuecomment-71097752) 加入 io.js 的开发，他们将要参与到本周的其他开发计划中去。

Current releases of io.js are releases of v8 slated to be marked **stable** and released in Chrome in **early March**. From that point on we will have a stable channel, using the latest stable v8, and an unstable channel with the next line of v8 development. This means that **you can expect io.js to be marked stable in March**. The unstable line will [continue and be used for testing](https://github.com/iojs/io.js/pull/630) new features in both io.js and v8.

Some tasks outside of core development have already grown to the point that they necessitate their own project teams and committers. In addition to the [build](https://github.com/iojs/build) group which was established when we launched there is now a [website](https://github.com/iojs/website) group and a [streams](https://github.com/iojs/readable-stream) group. We expect to see working groups form around **evangelism, documentation, i18n, nan,** and the **roadmap** in the future. These groups offer a much wider range of participation from the community.

When io.js began the largest concern was the lack of contributors to node.js™. Now io.js’ biggest problem is keeping up with the flood of contributors coming in, participating in every facet of the project. io.js isn’t just healthier than node.js™ **today**, it’s healthier than node.js™ **ever was** and this is only the beginning.
