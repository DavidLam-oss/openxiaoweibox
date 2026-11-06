---
title: "Obsidian 入门74：PDF 在 Obsidian 里，终于不只是“能看”了"
date: "2026-08-17"
slug: "obsidian-74-pdf-plus-annotation"
excerpt: "PDF 在 Obsidian 里终于不只是“能看”了。选中一段话，链接到笔记，它自动高亮。"
cover: ""
tags:
  - Obsidian
  - Obsidian插件
  - Obsidian入门
status: published
---
>
> 之前聊过怎么把笔记导出成专业 PDF。
> 
> 那是让内容从 Obsidian “出去”：把你的笔记变成一份能分享、能存档的 PDF。
>
> 今天反过来，聊聊让 PDF “进来”：当你手里有一份 PDF，想在 Obsidian 里读它、划重点、批注它，该怎么做。
>
> 如果你还没看过之前那一篇的内容，可以先看 [Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了](/blog/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86)

Obsidian 原生就能打开 PDF，能翻页、能缩放。但等我想给里面一段话划个重点的时候，选中文字……什么反应都没有。

后来我才明白，不是 Obsidian 不行，是“能看”和“能批注”之间，还差着一个插件的距离。这个插件叫 **PDF++**。

![PDF批注插件主视觉](/images/posts/Obsidian%20%E5%85%A5%E9%97%A874%EF%BC%9APDF%20%E5%9C%A8%20Obsidian%20%E9%87%8C%EF%BC%8C%E7%BB%88%E4%BA%8E%E4%B8%8D%E5%8F%AA%E6%98%AF%E2%80%9C%E8%83%BD%E7%9C%8B%E2%80%9D%E4%BA%86/20260817224733327.webp)


## 先搞清楚：PDF 在 Obsidian 里到底能做什么

很多朋友可能和我一样，默认以为 Obsidian 能打开 PDF，就能顺便批注 PDF。其实不是。

Obsidian 原生支持 PDF 查看，这是真的。它的内置查看器基于 PDF.js，打开、翻页、缩放、甚至双页模式都有。

![Obsidian原生PDF查看界面](/images/posts/Obsidian%20%E5%85%A5%E9%97%A874%EF%BC%9APDF%20%E5%9C%A8%20Obsidian%20%E9%87%8C%EF%BC%8C%E7%BB%88%E4%BA%8E%E4%B8%8D%E5%8F%AA%E6%98%AF%E2%80%9C%E8%83%BD%E7%9C%8B%E2%80%9D%E4%BA%86/CleanShot%25202026-08-17%2520at%252022.11.50%25402x.webp)


但“查看”和“批注”是两回事。选中文字划重点、在旁边写笔记、把某句话链接到自己的笔记里，这些原生都做不到。

想要在 Obsidian 里批注 PDF，需要一个插件。而 PDF++ 是目前口碑最好的那个。

## PDF++ 的核心机制：选中一句话，它自动高亮

PDF++ 最让人惊艳的地方，是它的批注方式：**用链接来批注**。

听起来有点绕，我实际走一遍你就明白了：

1. 安装插件（设置 → 第三方插件 → 搜索 `pdf++` → 安装启用）
![第三方插件搜索安装pdf-plus](/images/posts/Obsidian%20%E5%85%A5%E9%97%A874%EF%BC%9APDF%20%E5%9C%A8%20Obsidian%20%E9%87%8C%EF%BC%8C%E7%BB%88%E4%BA%8E%E4%B8%8D%E5%8F%AA%E6%98%AF%E2%80%9C%E8%83%BD%E7%9C%8B%E2%80%9D%E4%BA%86/CleanShot%25202026-08-17%2520at%252022.24.39%25402x.webp)
2. 打开一个 PDF，选中一段想批注的文字
3. 复制链接（快捷键或右键菜单）
4. 把这段链接粘贴到任意一条笔记里
![笔记中粘贴PDF选中文字链接](/images/posts/Obsidian%20%E5%85%A5%E9%97%A874%EF%BC%9APDF%20%E5%9C%A8%20Obsidian%20%E9%87%8C%EF%BC%8C%E7%BB%88%E4%BA%8E%E4%B8%8D%E5%8F%AA%E6%98%AF%E2%80%9C%E8%83%BD%E7%9C%8B%E2%80%9D%E4%BA%86/CleanShot%25202026-08-17%2520at%252022.30.30%25402x.webp)

然后神奇的事发生了：**那段被选中的文字，在 PDF 里自动高亮了**。

也就是说，你的批注不是存在某个隐藏的数据库里，而是变成了一行普通的 markdown 链接，躺在你自己的笔记里。你在笔记里写了什么想法，就跟着这行链接走；点一下链接，直接跳回 PDF 原文。

社区里有人把这种用法总结得很到位：“左边阅读，右边笔记，拖拽即可建立双向链接。每一处感悟都能瞬间回溯原文。”

## 为什么“批注是 markdown”这件事很重要

这个设计看起来简单，其实很聪明。

很多 PDF 批注工具，是把你的批注存在插件自己的数据文件里（甚至是一堆看不懂的 JSON）。哪天插件不维护了、或者 Obsidian 更新把插件搞挂了，你的批注可能就跟着没了。

PDF++ 反过来：批注就是一行 markdown 链接，存在你的笔记里。就算插件哪天不能用了，你的笔记还在、链接还在、PDF 高亮的机制还在（哪怕退化成普通链接），东西丢不了。

![PDF选中文字自动高亮效果](/images/posts/Obsidian%20%E5%85%A5%E9%97%A874%EF%BC%9APDF%20%E5%9C%A8%20Obsidian%20%E9%87%8C%EF%BC%8C%E7%BB%88%E4%BA%8E%E4%B8%8D%E5%8F%AA%E6%98%AF%E2%80%9C%E8%83%BD%E7%9C%8B%E2%80%9D%E4%BA%86/CleanShot%25202026-08-17%2520at%252022.25.31%25402x.webp)


作者有句话说得挺直接：“我不喜欢那些实际上根本不是 markdown 的 .md 文件。markdown 格式的价值不在于文件扩展名！”

这句话我挺认同的。在 Obsidian 这个“以纯文本和 markdown 为生命线”的工具里，批注用 markdown 承载，才是最安心的。

![批注以markdown链接存储](/images/posts/Obsidian%20%E5%85%A5%E9%97%A874%EF%BC%9APDF%20%E5%9C%A8%20Obsidian%20%E9%87%8C%EF%BC%8C%E7%BB%88%E4%BA%8E%E4%B8%8D%E5%8F%AA%E6%98%AF%E2%80%9C%E8%83%BD%E7%9C%8B%E2%80%9D%E4%BA%86/20260817224812030.webp)


## 它不只是批注，还把“看 PDF”这件事也升级了

除了批注，PDF++ 对 Obsidian 内置查看器本身也做了不少增强，挑几个我觉得值得打开的：

- **嵌入裁剪**：把 PDF 嵌入到笔记里时，可以只显示某一段文字，而不是一整页。做读书笔记时特别有用。
- **快捷键**：跳页、缩放、显示大纲，都可以不用鼠标了。
- **颜色标注**：高亮可以选颜色，红色划重点、黄色存疑，一目了然。
- **文字和区域都能批注**：不只是选中文字，PDF 里的某个区域块也能链接批注。

## 和 Zotero 是什么关系？

聊到 PDF 批注，很多朋友会想到 Zotero。这里说清楚：**PDF++ 不是要替代 Zotero，两者是互补的。**

Zotero 是“文献管理航母”，管文献库、抓元数据、生成参考文献，这些是它的主场。

Obsidian + PDF++ 是“知识网络中枢”，你读文献时的想法、摘录、和已有笔记的关联，这些发生在 Obsidian 里。

一个管“我有哪些文献”，一个管“我从文献里得到了什么”。可以配合使用，不冲突。

![Zotero与Obsidian协作示意](/images/posts/Obsidian%20%E5%85%A5%E9%97%A874%EF%BC%9APDF%20%E5%9C%A8%20Obsidian%20%E9%87%8C%EF%BC%8C%E7%BB%88%E4%BA%8E%E4%B8%8D%E5%8F%AA%E6%98%AF%E2%80%9C%E8%83%BD%E7%9C%8B%E2%80%9D%E4%BA%86/20260817224837136.webp)


## 几句实在话

PDF++ 也有一面要提前知道：

- 它依赖 Obsidian 的一些内部机制，**Obsidian 大版本更新时，插件可能短暂失效**。作者自己都提醒过这件事。好在批注是 markdown，插件挂了笔记不丢，等作者更新就好。
- 它由一位**没报酬的学生开发者**维护（作者原话）。维护这样一个插件，要研究 Obsidian 未公开的内部机制、PDF 文件格式规范，工作量不小。如果你觉得它好用，可以考虑赞助支持一下（GitHub Sponsors / Buy Me a Coffee），让作者有动力继续维护下去。

---

回到开头那个画面。

现在我在 Obsidian 里打开一份 PDF，选中一段话，链接到笔记，那段话自动亮起来。我可以在笔记里写自己的想法，点一下链接，又跳回原文。

PDF 终于不再是躺在库里、只能翻翻看的“死文件”了。它变成了能和我笔记对话的知识。

如果你也经常在 Obsidian 里读 PDF、做摘录、整理文献，PDF++ 值得装一个试试。安装只要一分钟，体验完全不同。

## 进阶阅读

### PDF 相关
- [Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了](/blog/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86) — 上一篇，把笔记导出成 PDF，让内容"出去"
- [Obsidian 入门67：把笔记「递出去」的更多方式——官方导出 PDF、图片、还有链接](/blog/Obsidian%20%E5%85%A5%E9%97%A867%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E3%80%8C%E9%80%92%E5%87%BA%E5%8E%BB%E3%80%8D%E7%9A%84%E6%9B%B4%E5%A4%9A%E6%96%B9%E5%BC%8F%E2%80%94%E2%80%94%E5%AE%98%E6%96%B9%E5%AF%BC%E5%87%BA%20PDF%E3%80%81%E5%9B%BE%E7%89%87%E3%80%81%E8%BF%98%E6%9C%89%E9%93%BE%E6%8E%A5) — 其他把笔记"递出去"的方式

### 插件安装基础
- [Obsidian 入门12：国内用户怎么方便地安装第三方插件，告诉你 3 条路](/blog/Obsidian%20%E5%85%A5%E9%97%A812%EF%BC%9A%E5%9B%BD%E5%86%85%E7%94%A8%E6%88%B7%E6%80%8E%E4%B9%88%E6%96%B9%E4%BE%BF%E5%9C%B0%E5%AE%89%E8%A3%85%E7%AC%AC%E4%B8%89%E6%96%B9%E6%8F%92%E4%BB%B6%EF%BC%8C%E5%91%8A%E8%AF%89%E4%BD%A0%203%20%E6%9D%A1%E8%B7%AF) — 国内装插件的 3 种方式
- [Obsidian 入门9：别在'插件森林'里迷路，先试试核心插件 - 模板](/blog/Obsidian%20%E5%85%A5%E9%97%A89%EF%BC%9A%E5%88%AB%E5%9C%A8'%E6%8F%92%E4%BB%B6%E6%A3%AE%E6%9E%97'%E9%87%8C%E8%BF%B7%E8%B7%AF%EF%BC%8C%E5%85%88%E8%AF%95%E8%AF%95%E6%A0%B8%E5%BF%83%E6%8F%92%E4%BB%B6%20-%20%E6%A8%A1%E6%9D%BF) — 装插件的入口在哪

### 相关联动
- [Obsidian 入门42：官方出品的剪藏插件，公众号文章也能一键存进你的库](/blog/Obsidian%20%E5%85%A5%E9%97%A842%EF%BC%9A%E5%AE%98%E6%96%B9%E5%87%BA%E5%93%81%E7%9A%84%E5%89%AA%E8%97%8F%E6%8F%92%E4%BB%B6%EF%BC%8C%E5%85%AC%E4%BC%97%E5%8F%B7%E6%96%87%E7%AB%A0%E4%B9%9F%E8%83%BD%E4%B8%80%E9%94%AE%E5%AD%98%E8%BF%9B%E4%BD%A0%E7%9A%84%E5%BA%93) — 把网页文章剪藏进 Obsidian，和 PDF++ 一起组成"资料进库"的组合拳