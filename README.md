iojs-cn
----------

参加 Slack 上的实时讨论：[![Join the chat at https://iojs-cn.slack.com](https://iojs-cn.herokuapp.com/badge.svg)](https://iojs-cn.slack.com)

> iojs-cn 组织成立的目的是为了推进 [io.js](https://iojs.org/) 在中国的普及，并及时同步英文社区的最新资讯。


## 主要内容

- [io.js 官方网站翻译](https://github.com/iojs/website/tree/i18n-static/public/i18n/cn)
- [官方 io.js Tweets 的转发](https://twitter.com/official_iojs)
- [io.js CHANGELOG 翻译](https://github.com/iojs/io.js/blob/v1.x/CHANGELOG.md)
- [io.js Weekly 翻译](https://medium.com/@iojs)
- [More...](https://github.com/iojs/iojs-cn/issues)

## 工作流程

0. 所有工作先提交一个 [Issue](https://github.com/iojs/iojs-cn/issues)，加上对应的标签。
0. 将 Issue 指派到对应的人（或者自己）。
0. 完成工作之后如果有内容需要提交到仓库，发起一次 [Pull Request](https://github.com/iojs/iojs-cn/pulls)，并指定 Review 人。
0. Review 通过之后合并，并关闭 Issue。

## 如何参与

请直接前往 [Issue 列表](https://github.com/iojs/iojs-cn/issues)找到你感兴趣的 Issue，然后参与讨论，或者提交 Pull Request。请按照上述的工作流程执行，避免浪费人力做相同的事情。

为了保持一致性，提升文档的质量，在着手工作之前，建议先查阅下：

- [中英文排版规范](https://github.com/sparanoid/chinese-copywriting-guidelines)

我们还会翻译一些 io.js 相关的文章，如果你有阅读到好的文章也欢迎提交。根据上面的工作流程提交 Issue，并以 PR 的形式提交原文，格式如下

```
# 标题

- Authors: 原作者名
- Referer: 原文地址

===

原文内容

```

## 社交媒体帐号

可以关注下列社交媒体帐号来获取 iojs-cn 的最新资讯。

- Twitter [@iojs_cn](https://twitter.com/iojs_cn)
- 微博 [@iojs_cn](http://weibo.com/iojscn)

## 贡献者

见[贡献者列表](https://github.com/iojs/iojs-cn/graphs/contributors)

## 目录规范

- 翻译的文章内容发布到 `articles/_posts` 中，周报发布到 `weekly/_posts` 中。文章的文件名格式为 YYYY-m-d-title.md，如 2012-12-2-how-to-contribute.md，内容格式为：

  ```
  ---
  layout: post
  title: io.js 如何在一天时间内吸引 146 人参与，被翻译成 27 种语言？
  author: mikeal
  reference: https://medium.com/@mikeal/65e5b1c49a62
  ---

  {{正文内容}}
  ```

  其中 `author` 和 `reference` 表示文章的原作者和出处。

- 文章图片放在相应目录的 `images` 子目录下的与标题同名目录中，如 `articles/images/2012-12-2-how-to-contribute/1.png`

- 提交 Pull Request 前推荐先在本地预览最终效果。方式为在项目根目录中：

  1. 执行 `$ gem install github-pages` 以安装 Jekyll 和相关插件；
  2. 运行网站 `jekyll serve`，jekyll 会自动监控文件的变化
  3. 访问 http://0.0.0.0:4000 来查看效果

