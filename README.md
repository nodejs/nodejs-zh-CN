iojs-cn
----------

参加 Slack 上的实时讨论：[![Join the chat at https://iojs-cn.slack.com](https://iojs-cn.herokuapp.com/badge.svg)](https://iojs-cn.herokuapp.com)

> iojs-cn 组织成立的目的是为了推进 [io.js / Node.js](https://iojs.org/) 在中国的普及，并及时同步英文社区的最新资讯。

## 主要内容

- [io.js 官方网站翻译](https://github.com/nodejs/website/tree/master/content/cn)
- [官方 io.js Tweets 的转发](https://twitter.com/official_iojs)
- [io.js CHANGELOG](https://github.com/nodejs/io.js/blob/v1.x/CHANGELOG.md) [翻译](https://github.com/iojs/iojs-cn/blob/gh-pages/CHANGELOG.md)
- [io.js Weekly](https://medium.com/@iojs) [翻译](https://github.com/nodejs/iojs-cn/tree/gh-pages/articles)
- [io.js 相关文章翻译](https://github.com/nodejs/iojs-cn/tree/gh-pages/articles)
- [更多讨论...](https://github.com/nodejs/iojs-cn/issues)

## 社交媒体帐号

可以关注下列社交媒体帐号来获取 iojs-cn 的最新资讯。

- Twitter [@iojs_cn](https://twitter.com/iojs_cn)
- 微博 [@iojs_cn](http://weibo.com/iojscn)

## 如何参与

请直接前往 [Issue 列表](https://github.com/nodejs/iojs-cn/issues)找到你感兴趣的 Issue 参与讨论，也可申请指派翻译任务。为了保持一致性，提升文档的质量，在翻译之前建议先查阅下[中英文排版规范](https://github.com/sparanoid/chinese-copywriting-guidelines)。请按照以下流程执行，避免浪费人力做相同的事情。

### 提交原文

当找到一篇需要翻译的文章时，新建 issue（标记为 `help wanted`）并提交 PR 添加原文，这样方便以后校译。

可提交到 [articles](https://github.com/nodejs/iojs-cn/tree/gh-pages/articles/_posts) 或 [weekly](https://github.com/nodejs/iojs-cn/tree/gh-pages/weekly/_posts)，文件名的格式为 `YYYY-m-d-title.md`（如 `2012-12-2-how-to-contribute.md`），内容格式为：

```
---
layout: post
title: 原文标题
author: 原文作者
reference: 原文链接
published: false
---

原文正文
```

文章图片放在相应目录的 `images` 子目录下的与标题同名目录中，如 `articles/images/2012-12-2-how-to-contribute/1.png`

### 翻译

在 issue 列表查看需要翻译的文章，可申请翻译并被指派为翻译人（标记为 `in progress`）。翻译人基于原文进行翻译，并提交 PR 进行校译（PR 需要有中英文对比）。

可使用 jekyll 进行本地预览

1. 执行 `$ gem install github-pages` 以安装 Jekyll 和相关插件。
2. 运行网站 `jekyll serve`，jekyll 会自动监控文件的变化。
3. 访问 http://0.0.0.0:4000 来查看效果。

### 校译

提交 PR 后指定 review 人，需要**两个** review 人以 `+1` 或 `LGTM` 的形式同意后才可以合并。

## 贡献者

见[贡献者列表](https://github.com/nodejs/iojs-cn/graphs/contributors)
