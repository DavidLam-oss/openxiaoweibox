---
title: Obsidian 入门70：文章写完了，用 WeChat Converter 一键发到公众号
date: 2026-07-02
slug: obsidian-70-wechat-converter-publish
excerpt: 注册了公众号，用 Skill 写好了文章，最后一步：一键发到微信后台。
tags:
  - Obsidian
  - WeChat Converter
  - 微信公众号
  - 多平台分发
  - Obsidian插件
obsidianSection: publishing
status: published
---
> 这是一个「Obsidian x AI」系列。
>
> 入门 68 注册了公众号，入门 69 用 Skill 跑完了写作流程。
>
> 文章写好了，怎么发到公众号去？
>
> 这篇来收尾。

## 你可能也有过这种时候

在 Obsidian 里洋洋洒洒写完了一篇，然后打开浏览器，登录公众号后台，新建图文，把内容从 Obsidian 复制过去，调格式，调半天，再传封面图——发布。

这几步，每一步都不难。但合在一起，每次发文章都像在走流程。

WeChat Converter 插件就是来解决这个问题的。

![Obsidian 入门70：文章写完了，用 WeChat Converter 一键发到公众号 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A870%EF%BC%9A%E6%96%87%E7%AB%A0%E5%86%99%E5%AE%8C%E4%BA%86%EF%BC%8C%E7%94%A8%20WeChat%20Converter%20%E4%B8%80%E9%94%AE%E5%8F%91%E5%88%B0%E5%85%AC%E4%BC%97%E5%8F%B7/CleanShot%25202026-07-03%2520at%252007.04.23.webp)


## WeChat Converter 是什么

它是一个 Obsidian 社区插件，核心能力就这些：

- **Markdown 转公众号格式**：标题、列表、引用、代码块、表格，自动转换成公众号编辑器能识别的样式。不会出现发出去格式乱掉的情况。
- **一键发送到草稿箱**：在 Obsidian 里点一下，文章就直接躺进你的微信公众号草稿箱了。不用打开浏览器，不用复制粘贴。
- **本地图片自动上传**：笔记里引用的本地图片，发送时会自动上传到微信素材库。GIF 图片也支持，不用担心动不了。图床链接的图片也能正常识别。
- **数学公式**：LaTeX 行内和块级公式都能正常渲染，不会变成乱码。
- **Callout 和 Mermaid**：Obsidian 的 Callout 引用块和 Mermaid 图表，都能在导出的文章里保留。
- **多主题排版**：内置多套排版主题和样式，你可以按自己的喜好选择，也可以微调。每次发出来的文章风格统一。
- **AI 编排**：如果你对排版拿不准，可以让 AI 帮你重新组织内容的布局和顺序，省去手动调整的功夫。

一句话定位：**你只管在 Obsidian 写，发布的事交给它。**

![Obsidian 入门70：文章写完了，用 WeChat Converter 一键发到公众号 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A870%EF%BC%9A%E6%96%87%E7%AB%A0%E5%86%99%E5%AE%8C%E4%BA%86%EF%BC%8C%E7%94%A8%20WeChat%20Converter%20%E4%B8%80%E9%94%AE%E5%8F%91%E5%88%B0%E5%85%AC%E4%BC%97%E5%8F%B7/CleanShot%25202026-07-03%2520at%252007.05.29.webp)


> 这其实是我自己 vibe coding 的一个 Obsidian 插件，今天也在 Obsidian 入门系列里介绍给大家。

## 怎么装

在社区插件市场搜「WeChat Converter」，找到后安装启用就行。

![Obsidian 入门70：文章写完了，用 WeChat Converter 一键发到公众号 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A870%EF%BC%9A%E6%96%87%E7%AB%A0%E5%86%99%E5%AE%8C%E4%BA%86%EF%BC%8C%E7%94%A8%20WeChat%20Converter%20%E4%B8%80%E9%94%AE%E5%8F%91%E5%88%B0%E5%85%AC%E4%BC%97%E5%8F%B7/CleanShot%25202026-07-03%2520at%252007.00.16.webp)


装好之后，左侧边栏会出现一个魔法棒图标，点开就是插件的主界面 - 在右侧边栏展示公众号排版的预览效果。

![Obsidian 入门70：文章写完了，用 WeChat Converter 一键发到公众号 - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A870%EF%BC%9A%E6%96%87%E7%AB%A0%E5%86%99%E5%AE%8C%E4%BA%86%EF%BC%8C%E7%94%A8%20WeChat%20Converter%20%E4%B8%80%E9%94%AE%E5%8F%91%E5%88%B0%E5%85%AC%E4%BC%97%E5%8F%B7/CleanShot%25202026-07-03%2520at%252007.06.14.webp)


## 怎么配

第一次使用需要配置你的公众号。

在插件设置里填入你的公众号 AppID 和 AppSecret。这两个信息微信开发者平台可以找到，另外还需要将你的 IP 配置到微信白名单中。
https://developers.weixin.qq.com/platform

![Obsidian 入门70：文章写完了，用 WeChat Converter 一键发到公众号 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A870%EF%BC%9A%E6%96%87%E7%AB%A0%E5%86%99%E5%AE%8C%E4%BA%86%EF%BC%8C%E7%94%A8%20WeChat%20Converter%20%E4%B8%80%E9%94%AE%E5%8F%91%E5%88%B0%E5%85%AC%E4%BC%97%E5%8F%B7/CleanShot%25202026-07-03%2520at%252007.06.53.webp)


配好之后，以后就不用再动了。每次发文章直接点发送就行。

## 几个关键设置

插件装好之后，下面这几个设置值得看一眼：

**发布前预览**：打开后，发送到草稿箱之前可以先在 Obsidian 里预览公众号效果。标题字号、引用样式、代码块配色，都能提前看到。建议打开。

**图片上传**：如果你的笔记里有本地图片，插件会自动上传到微信素材库。你不需要手动再去公众号草稿箱再手动传一遍。

**多账号管理**：如果你同时运营多个公众号，可以在设置里添加多个账号（最多 5 个账号），发送时选择目标账号。

## 怎么用

安装配置好之后，日常用法很简单。

打开你已经写好的笔记，确认内容没问题。在左侧边栏点开 WeChat Converter 的图标，你可以先预览在公众号里的显示效果。标题层级、引用样式、代码块配色，都能在预览里看到。

预览满意之后，点「发送到微信」。几秒钟后，文章就会出现在你的公众号草稿箱里。

![Obsidian 入门70：文章写完了，用 WeChat Converter 一键发到公众号 - 截图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A870%EF%BC%9A%E6%96%87%E7%AB%A0%E5%86%99%E5%AE%8C%E4%BA%86%EF%BC%8C%E7%94%A8%20WeChat%20Converter%20%E4%B8%80%E9%94%AE%E5%8F%91%E5%88%B0%E5%85%AC%E4%BC%97%E5%8F%B7/CleanShot%25202026-07-03%2520at%252007.12.23.webp)


然后你打开公众号后台，在草稿箱里找到它，做最后的检查：调整封面图、修改摘要、完成基础设置，点「发布」。

![Obsidian 入门70：文章写完了，用 WeChat Converter 一键发到公众号 - 截图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A870%EF%BC%9A%E6%96%87%E7%AB%A0%E5%86%99%E5%AE%8C%E4%BA%86%EF%BC%8C%E7%94%A8%20WeChat%20Converter%20%E4%B8%80%E9%94%AE%E5%8F%91%E5%88%B0%E5%85%AC%E4%BC%97%E5%8F%B7/CleanShot%25202026-07-03%2520at%252007.18.12.webp)


从 Obsidian 写完到公众号发出，整个流程就结束了。

## 几个你可能关心的

**支持多个公众号吗？**

支持。如果你同时运营多个号，可以在设置里添加多个账号，发送时选择目标账号就行。

**除了公众号还能发哪里？**

插件后续版本已经支持一键分发到 20+ 平台，包括飞书、知乎、小红书、微博等。如果你有跨平台分发的需求，可自行体验。

**发送后还能在公众号后台改吗？**

当然。发送到的是草稿箱，不是直接发布。你还有机会在后台调整内容、封面、摘要等。

---

入门 68 注册，入门 69 写作，入门 70 发布。

三篇串在一起，就是一条从零到发布的完整链路。如果现在给你一个新话题，你能不能走完这一圈？

作业很简单：**装好 WeChat Converter，把你根据入门 69 写的那篇文章从 Obsidian 发到你的公众号草稿箱。**

动手试试，下期见。

---

## 进阶阅读

### 关于 WeChat Converter
- [受够了复制粘贴，我把 Obsidian 直接接进了微信后台](/blog/%E5%8F%97%E5%A4%9F%E4%BA%86%E5%A4%8D%E5%88%B6%E7%B2%98%E8%B4%B4%EF%BC%8C%E6%88%91%E6%8A%8A%20Obsidian%20%E7%9B%B4%E6%8E%A5%E6%8E%A5%E8%BF%9B%E4%BA%86%E5%BE%AE%E4%BF%A1%E5%90%8E%E5%8F%B0) — 插件从预览到一键发布的进化故事
- [我做了个插件，让公众号排版不用离开 Obsidian](/blog/%E6%88%91%E5%81%9A%E4%BA%86%E4%B8%AA%E6%8F%92%E4%BB%B6%EF%BC%8C%E8%AE%A9%E5%85%AC%E4%BC%97%E5%8F%B7%E6%8E%92%E7%89%88%E4%B8%8D%E7%94%A8%E7%A6%BB%E5%BC%80%20Obsidian) — 插件的起源
- [插件升级 2.8.0：以前只有公众号，现在是一键发 20+ 平台](/blog/%E6%8F%92%E4%BB%B6%E5%8D%87%E7%BA%A7%202.8.0%EF%BC%9A%E4%BB%A5%E5%89%8D%E5%8F%AA%E6%9C%89%E5%85%AC%E4%BC%97%E5%8F%B7%EF%BC%8C%E7%8E%B0%E5%9C%A8%E6%98%AF%E4%B8%80%E9%94%AE%E5%8F%91%2020%2B%20%E5%B9%B3%E5%8F%B0) — 多平台分发能力
- [插件升级｜2.9.0：现在可以把 Obsidian 文章一键发布到飞书云文档了](/blog/%E6%8F%92%E4%BB%B6%E5%8D%87%E7%BA%A7%EF%BD%9C2.9.0%EF%BC%9A%E7%8E%B0%E5%9C%A8%E5%8F%AF%E4%BB%A5%E6%8A%8A%20Obsidian%20%E6%96%87%E7%AB%A0%E4%B8%80%E9%94%AE%E5%8F%91%E5%B8%83%E5%88%B0%E9%A3%9E%E4%B9%A6%E4%BA%91%E6%96%87%E6%A1%A3%E4%BA%86) — 插件最新升级

### 本系列前篇
- [Obsidian 入门68：攒了满 Obsidian 的内容，把它递给更广的人群](/blog/Obsidian%20%E5%85%A5%E9%97%A868%EF%BC%9A%E6%94%92%E4%BA%86%E6%BB%A1%20Obsidian%20%E7%9A%84%E5%86%85%E5%AE%B9%EF%BC%8C%E6%8A%8A%E5%AE%83%E9%80%92%E7%BB%99%E6%9B%B4%E5%B9%BF%E7%9A%84%E4%BA%BA%E7%BE%A4) — 注册公众号
- [Obsidian 入门 69：拿到 Skill 之后，怎么用它写完一篇文章](/blog/Obsidian%20%E5%85%A5%E9%97%A8%2069%EF%BC%9A%E6%8B%BF%E5%88%B0%20Skill%20%E4%B9%8B%E5%90%8E%EF%BC%8C%E6%80%8E%E4%B9%88%E7%94%A8%E5%AE%83%E5%86%99%E5%AE%8C%E4%B8%80%E7%AF%87%E6%96%87%E7%AB%A0) — 用 Skill 写稿
- [Obsidian 入门40：把我的写作工作流Skill免费分享给你](/blog/Obsidian%20%E5%85%A5%E9%97%A840%EF%BC%9A%E6%8A%8A%E6%88%91%E7%9A%84%E5%86%99%E4%BD%9C%E5%B7%A5%E4%BD%9C%E6%B5%81Skill%E5%85%8D%E8%B4%B9%E5%88%86%E4%BA%AB%E7%BB%99%E4%BD%A0) — 把我的写作 skill 分享给你
