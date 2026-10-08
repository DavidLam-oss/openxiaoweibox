---
title: Obsidian 入门48：为什么剪藏到 Obsidian 的文章，图片过段时间就没了？
slug: obsidian-web-clipper-image-localization
excerpt: 剪藏的文章过段时间图片就裂了？两步让你的图片真正归你。
date: 2026-05-17
cover: Wechat/published/img/cover-main.jpg
tags:
  - Obsidian
  - Web剪藏
  - 排版与导出
  - Obsidian插件
  - Obsidian入门
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理和收集、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过上一篇，可以先看 [Obsidian 入门47：不想用图床？本地图片也能管得井井有条](/blog/Obsidian%20%E5%85%A5%E9%97%A847%EF%BC%9A%E4%B8%8D%E6%83%B3%E7%94%A8%E5%9B%BE%E5%BA%8A%EF%BC%9F%E6%9C%AC%E5%9C%B0%E5%9B%BE%E7%89%87%E4%B9%9F%E8%83%BD%E7%AE%A1%E5%BE%97%E4%BA%95%E4%BA%95%E6%9C%89%E6%9D%A1)。

群里有人问：剪藏到 Obsidian 的文章，为什么过一段时间图片就不显示了？

这个问题问到了点上。你刚用 Web Clipper 剪藏完一篇文章，文字都在，排版也还行。过了几周打开一看，图片位置只剩一个裂开的占位符。

不是你的笔记出了问题。问题出在图片还在别人家的服务器上。

---

## 图片为什么会失效

原因有三层。

第一层，剪藏工具保存的是图片链接，不是图片本身。`![Obsidian 入门48：为什么剪藏到 Obsidian 的文章，图片过段时间就没了？ - 配图 1](https://example.com/pic.jpg)` 这张图没有进你的库，只是借了别人的服务器给你看。哪天对方关了防盗链、换了域名，图片就跟着没了。

第二层，微信公众号的限制。微信文章里的图片，刚剪藏下来可能还能显示，过段时间就会失效。这是微信对外链展示的控制手段。

第三层，懒加载。公众号的图片是滚到哪才加载到哪。如果你打开文章直接剪藏，根本没滚到底，后面的图插件根本没拿到。

![[Wechat/published/attachments/7a738ea49cff5a2c52ac50c1bb0a5d59_MD5.jpg|400]]

---

## 剪藏前：先让图片全部加载出来

如果是剪藏公众号文章，在用 Web Clipper 插件的剪藏按钮之前，有一个动作非常关键。

打开公众号文章，从头滚到底。确认文章里的图片都正常显示了，再执行剪藏。

就这么简单一个动作，能避免大部分"剪藏后图片缺失"的问题。

---

## 第一步：Local Images Plus 把图片下载到本地

现在图片已经全部加载并剪藏进 Obsidian 了，但链接还是指向原平台的服务器。

这时候需要 Local Images Plus。这个插件的核心作用，是把笔记里所有远程图片链接下载下来，存到本地附件文件夹，然后自动把链接替换成本地引用。

安装很简单。在社区插件市场搜索 Local Images Plus，点安装就行。

![插件](/images/posts/Obsidian%20%E5%85%A5%E9%97%A848%EF%BC%9A%E4%B8%BA%E4%BB%80%E4%B9%88%E5%89%AA%E8%97%8F%E5%88%B0%20Obsidian%20%E7%9A%84%E6%96%87%E7%AB%A0%EF%BC%8C%E5%9B%BE%E7%89%87%E8%BF%87%E6%AE%B5%E6%97%B6%E9%97%B4%E5%B0%B1%E6%B2%A1%E4%BA%86%EF%BC%9F/CleanShot%25202026-05-17%2520at%252009.45.46.webp)

装好后打开设置。如果你的 Obsidian 已经设置了附件图片是跟随笔记起一个新的 folder 的话，那就不需要去特别地进行设置，保持默认就行了。

因为这样图片会存放在当前笔记旁边的文件夹里，方便管理。

![插件设置](/images/posts/Obsidian%20%E5%85%A5%E9%97%A848%EF%BC%9A%E4%B8%BA%E4%BB%80%E4%B9%88%E5%89%AA%E8%97%8F%E5%88%B0%20Obsidian%20%E7%9A%84%E6%96%87%E7%AB%A0%EF%BC%8C%E5%9B%BE%E7%89%87%E8%BF%87%E6%AE%B5%E6%97%B6%E9%97%B4%E5%B0%B1%E6%B2%A1%E4%BA%86%EF%BC%9F/CleanShot%25202026-05-17%2520at%252009.51.35.webp)
关键操作在这里。打开一篇刚剪藏好的文章，按 Ctrl+P 打开命令面板，搜索「Localize attachments for the current note」。这里可以看到有两个选项：

1. Plugin Folder：会在你当前笔记的位置。
2. Obsidian Folder：会去到 Obsidian 的根目录。

插件会扫描这篇笔记里的所有远程图片，一张张下载到本地。它只处理你当前打开的这篇，不会动其他笔记。

![插件命令](/images/posts/Obsidian%20%E5%85%A5%E9%97%A848%EF%BC%9A%E4%B8%BA%E4%BB%80%E4%B9%88%E5%89%AA%E8%97%8F%E5%88%B0%20Obsidian%20%E7%9A%84%E6%96%87%E7%AB%A0%EF%BC%8C%E5%9B%BE%E7%89%87%E8%BF%87%E6%AE%B5%E6%97%B6%E9%97%B4%E5%B0%B1%E6%B2%A1%E4%BA%86%EF%BC%9F/CleanShot%25202026-05-17%2520at%252010.01.38.webp)

几分钟后，图片就从别人家的服务器搬到了你的硬盘上。

比方说我刚才用这个命令跑了一下，那么我这篇笔记里面的那些图片，就出现在了我当前笔记的旁边的文件夹中。

而且自动把文章中的远程图床链接替换为了本地路径引用。

![attachment](/images/posts/Obsidian%20%E5%85%A5%E9%97%A848%EF%BC%9A%E4%B8%BA%E4%BB%80%E4%B9%88%E5%89%AA%E8%97%8F%E5%88%B0%20Obsidian%20%E7%9A%84%E6%96%87%E7%AB%A0%EF%BC%8C%E5%9B%BE%E7%89%87%E8%BF%87%E6%AE%B5%E6%97%B6%E9%97%B4%E5%B0%B1%E6%B2%A1%E4%BA%86%EF%BC%9F/CleanShot%25202026-05-17%2520at%252010.04.05.webp)

---

## 第二步：Image Auto Upload 上传到自己的图床

图片到本地了，稳了。但如果你跟我一样，图片全部走图床（参考 [Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了](/blog/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86)），还可以再往前走一步。

Image Auto Upload 这个插件做的事情是：你在笔记里粘贴或拖入图片时，它会自动把图片上传到你配好的图床，然后把链接替换成图床地址。

那怎么让已经下载到本地的图片也触发这个上传机制呢？有两个做法。

方法一：在 Obsidian 的文件管理里，找到刚下载的本地图片，直接拖回笔记正文区域。Image Auto Upload 检测到图片拖入操作，会自动上传并替换链接。

方法二：Image Auto Upload 有一个命令叫「Upload all images」，运行后会扫描库里的图片上传到图床。不过这个命令会处理整个库，不只是当前笔记。如果你只想处理刚下载的几张图，用方法一拖回去更精准。

![拖动](/images/posts/Obsidian%20%E5%85%A5%E9%97%A848%EF%BC%9A%E4%B8%BA%E4%BB%80%E4%B9%88%E5%89%AA%E8%97%8F%E5%88%B0%20Obsidian%20%E7%9A%84%E6%96%87%E7%AB%A0%EF%BC%8C%E5%9B%BE%E7%89%87%E8%BF%87%E6%AE%B5%E6%97%B6%E9%97%B4%E5%B0%B1%E6%B2%A1%E4%BA%86%EF%BC%9F/CleanShot%25202026-05-17%2520at%252010.32.54.webp)

两种方法都行，看你怎么顺手。

所以整条链路是这样的：

![Obsidian 入门48：为什么剪藏到 Obsidian 的文章，图片过段时间就没了？ - 配图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A848%EF%BC%9A%E4%B8%BA%E4%BB%80%E4%B9%88%E5%89%AA%E8%97%8F%E5%88%B0%20Obsidian%20%E7%9A%84%E6%96%87%E7%AB%A0%EF%BC%8C%E5%9B%BE%E7%89%87%E8%BF%87%E6%AE%B5%E6%97%B6%E9%97%B4%E5%B0%B1%E6%B2%A1%E4%BA%86%EF%BC%9F/20260517141144271.webp)

每一步都会自动替换笔记里的引用，图片始终正常显示，只是来源从别人的服务器变成了你的硬盘，再从你的硬盘变成了你的云端。

![[Wechat/published/attachments/fadc35befae23311d0ef0a5e5ade9bff_MD5.jpg|400]]

---

## 三种方案，你选哪种？

上面这个流程走完，是最完整的方案。但不是每篇剪藏都需要这么折腾。

临时扫一眼的文章，保留原链就行，挂了也不心疼。真正重要的文章才值得走完整套流程。

三种方案的区别在这里：

| 方案        | 稳定性 | 库体积 | 适合场景                 |
| ----------- | ------ | ------ | ------------------------ |
| 保留原链接  | 低     | 最小   | 临时资料、不重要的网页   |
| 下载到本地  | 高     | 较大   | 需要长期保存的重要文章   |
| 本地+上图床 | 高     | 最小   | 多端同步、需要发布的内容 |

你自己判断，哪些内容值得"真正拥有"。

---

## 进阶阅读

- [Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了](/blog/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86)
- [Obsidian 入门47：不想用图床？本地图片也能管得井井有条](/blog/Obsidian%20%E5%85%A5%E9%97%A847%EF%BC%9A%E4%B8%8D%E6%83%B3%E7%94%A8%E5%9B%BE%E5%BA%8A%EF%BC%9F%E6%9C%AC%E5%9C%B0%E5%9B%BE%E7%89%87%E4%B9%9F%E8%83%BD%E7%AE%A1%E5%BE%97%E4%BA%95%E4%BA%95%E6%9C%89%E6%9D%A1)
- [Obsidian 入门8：附件与图片管理，给你的笔记装上「附件收纳术」](/blog/Obsidian%20%E5%85%A5%E9%97%A88%EF%BC%9A%E9%99%84%E4%BB%B6%E4%B8%8E%E5%9B%BE%E7%89%87%E7%AE%A1%E7%90%86%EF%BC%8C%E7%BB%99%E4%BD%A0%E7%9A%84%E7%AC%94%E8%AE%B0%E8%A3%85%E4%B8%8A%E3%80%8C%E9%99%84%E4%BB%B6%E6%94%B6%E7%BA%B3%E6%9C%AF%E3%80%8D)
