---
title: Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了
date: 2026-06-27
slug: obsidian-66-better-export-pdf
excerpt: 想给笔记导出成带目录、带页码的专业 PDF？Better Export PDF 插件一键搞定，单篇批量都行。
tags:
  - Obsidian
  - Obsidian插件
  - 排版与导出
  - 知识管理
status: published
---
>
> 上一篇讲了怎么把笔记一键转 Word 发出去。
> 
> 但有些场景 Word 太重了。今天聊的是导出 PDF，更适合正式分享、存档、打印的格式。
>
> 如果你还没看过前一篇，可以先看 [Obsidian 入门65：把笔记一键转 Word，ToWord 插件三步搞定](/blog/Obsidian%20%E5%85%A5%E9%97%A865%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E4%B8%80%E9%94%AE%E8%BD%AC%20Word%EF%BC%8CToWord%20%E6%8F%92%E4%BB%B6%E4%B8%89%E6%AD%A5%E6%90%9E%E5%AE%9A)

写了一篇笔记，想发给同事或者存档。如果你的笔记里主要是文字、标题、列表这些常规内容，那 Obsidian 内置的 PDF 导出就够了。在笔记右上角的菜单里点「导出为 PDF」，简单快捷，什么都不用装。

但如果你笔记里带了表格、代码块、多级标题，或者想一次性把整个文件夹的笔记合并成一份 PDF，这时候内置的 PDF 导出就不太够用了。它一次只能导一篇，没有目录标签，没有页码。

而这些，就是第三方插件 Better Export PDF 要解决的问题。

## Better Export PDF 是什么

它是 Obsidian 社区插件市场里的一款插件，专门用来把笔记导出成更专业的 PDF 格式。

跟 Obsidian 内置的 PDF 导出相比，它多做了几件事：

- **有目录标签**：导出的 PDF 带书签，点击跳转，内置导出没有这个功能
- **有页眉页脚**：页眉显示笔记名，页脚显示页码，正式感拉满
- **支持批量**：可以把整个文件夹的笔记合并成一个 PDF，也可以每个文件单独导出
- **公式和表格不乱**：LaTeX 公式、Markdown 表格都能正确渲染
- **设置项不多，但够用**：6 个核心选项，改完就不用再动了

一句话说清楚：**它就是你 Obsidian 笔记的"正式出版工具"。**

## 怎么装

打开设置 → 社区插件 → 关掉安全模式（如果你还没关的话）。点「浏览」，在搜索框里输入「Better Export PDF」。找到后点「安装」，等几秒。

![Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86/CleanShot%25202026-06-27%2520at%252021.23.51%25402x.webp)

装完后启用即可，没有额外的依赖，装完启用就能直接用。

插件装好后，设置项可以先不动。等你要导出的时候，再按需调整。

## 导出单篇笔记

选中一篇笔记，右键 →「Better Export PDF」。

注意一点：**默认导出格式是 HTML**，你需要在预览菜单里手动选成「PDF」。这个很容易漏，我第一次用的时候就中招了。

![Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86/CleanShot%25202026-06-27%2520at%252021.27.02%25402x.webp)


选好 PDF 格式后，重点留意这几项：

- **将笔记名作为标题**：打开后，PDF 的文件名直接用笔记标题，不用手动改。
- **页眉**和**页脚**：页眉显示笔记名称，页脚显示页码。正式文档建议两个都打开。
- **横向打印**：默认关闭，只有宽表格或宽图才需要。
- **缩放**：如果笔记内容比较宽，可以调小缩放让所有内容挤进一页。
- **导出后打开**：导出完自动用系统 PDF 阅读器打开，方便检查效果。

点击 Export，选好保存位置。出来的 PDF 左边会有目录标签栏，点击就能跳转到对应章节。公式、表格、代码块都保留得很好。

![Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86/CleanShot%25202026-06-27%2520at%252021.53.29.webp)


我用一篇含有各种特殊格式的笔记，来测试了一下导出为 PDF，发现以下内容都支持导出：

1. 图床的图片
2. 本地图片
3. 数学公式
4. 代码块
5. 表格
6. Mermaid

> [!image-swipe] Swipe to view images
>
> ![Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了 - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86/CleanShot%25202026-06-27%2520at%252021.57.02.webp)
> ![Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86/CleanShot%25202026-06-27%2520at%252021.57.55.webp)
> ![Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了 - 截图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86/CleanShot%25202026-06-27%2520at%252021.58.37.webp)

## 批量导出

批量导出才是它的重头戏。

在文件浏览器的文件夹上右键，你会看到两个选项。

![Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了 - 截图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86/CleanShot%25202026-06-27%2520at%252022.00.33.webp)


**Export folder to PDF**：把文件夹里所有笔记合并成**一个** PDF 文件。适合给客户发完整文档、项目结项报告这种场景。

**Export each file to PDF**：把文件夹里每篇笔记导出为**各自独立**的 PDF。适合归档场景，每篇笔记一份文件。

选第一个的话，插件会先预生成所有内容，文件多的时候需要等一下。等预生成完成，点 Export，出来的 PDF 里各篇笔记的标题会自动成为目录书签层级。

选第二个的话，有一个「Generate TOC.md file」选项值得打开。它会在文件夹里生成一份目录文件，方便你管理。

![Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了 - 截图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86/CleanShot%25202026-06-27%2520at%252022.02.30.webp)


### 什么场景用哪种？

| 场景 | 用哪个 | 原因 |
|---|---|---|
| 项目报告/方案书 | Export folder to PDF | 一篇搞定，目录完整 |
| 学习笔记归档 | Export each file to PDF | 每篇独立，管理方便 |
| 给客户的交付件 | Export folder to PDF | 一本正经，专业感 |

## 几个关键设置

Better Export PDF 的设置项不多，下面这几个最值得关注。

![Obsidian 入门66：把笔记导出为专业 PDF，Better Export PDF 插件够用了 - 截图 9](/images/posts/Obsidian%20%E5%85%A5%E9%97%A866%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E5%AF%BC%E5%87%BA%E4%B8%BA%E4%B8%93%E4%B8%9A%20PDF%EF%BC%8CBetter%20Export%20PDF%20%E6%8F%92%E4%BB%B6%E5%A4%9F%E7%94%A8%E4%BA%86/CleanShot%25202026-06-27%2520at%252022.03.48.webp)

**页眉和页脚的内容是可以改的。** 默认页眉是文件名，页脚是页码。如果你想要更个性化的内容，可以到插件设置的高级区域，用 HTML 模板语法修改。比如你想在页脚显示「第 1 页 / 共 10 页」，可以在 Footer Template 里写：

`第 <span class='pageNumber'></span> 页 / 共 <span class='totalPages'></span> 页`

**关于"文件名添加时间戳"。** 这个选项会在文件名后面加一串 Unix 时间戳，比如 `1763208444668`。虽然精确到秒，但没法直观看出日期。除非你有特殊的版本管理需求，一般不建议开。

**其他选项保持默认就行。** 这个插件的设计理念就是"装好就能用"，不需要折腾。

## 小贴士

**公式多的笔记，Better Export PDF 也能处理好。** 我试过几篇带 LaTeX 公式的笔记，用内置导出偶尔会渲染错位，但 Better Export PDF 稳定很多。

**合并 PDF 时，注意各篇之间的分页。** 目前 Better Export PDF 在合并导出时，各篇笔记之间是连续打印的，不会自动分页。如果你希望每篇都从新一页开始，需要在笔记末尾手动加分页符。

**导出的 PDF 自带目录标签。** 这是这个插件最明显的优势。在 PDF 阅读器里打开，左边就能看到完整的目录层级，点击跳转。不管是自己查阅还是发给别人，体验都好很多。

## 跟 ToWord 怎么选

上一期讲的是 ToWord（导出到 Word），这一期是 Better Export PDF（导出到 PDF）。

简单分一下：

- 对方是日常用 Word 的同事、老板 → **ToWord**
- 正式存档、打印、发客户 → **Better Export PDF**
- 两者不冲突，**建议都装**。同一个笔记，按场景选格式就好。

---

回到开头那个场景：你写了一篇带公式、带表格的笔记，想正式地发出去。

Obsidian 内置的 PDF 导出对日常笔记完全够用。

但如果你有更正式的分享需求，比如合并导出、目录标签、页眉页脚，Better Export PDF 就是那个让 PDF 更像一份正式文档的小工具。

今天的作业很简单：装好 Better Export PDF，选一篇带标题层级的笔记导出成 PDF，看看左边的目录标签是不是能正常跳转。 然后决定一下，你的哪些笔记适合用 PDF 来"递出去"。

动手试试，下期见！

## 进阶阅读

### 笔记分享系列
- [Obsidian 入门65：把笔记一键转 Word，ToWord 插件三步搞定](/blog/Obsidian%20%E5%85%A5%E9%97%A865%EF%BC%9A%E6%8A%8A%E7%AC%94%E8%AE%B0%E4%B8%80%E9%94%AE%E8%BD%AC%20Word%EF%BC%8CToWord%20%E6%8F%92%E4%BB%B6%E4%B8%89%E6%AD%A5%E6%90%9E%E5%AE%9A) — 导出为 Word 格式，适合发给日常用 Office 的人
- [Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南](/blog/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97) — 不想导出文件，直接分享到飞书

### 插件安装基础
- [Obsidian 入门12：国内用户怎么方便地安装第三方插件，告诉你 3 条路](/blog/Obsidian%20%E5%85%A5%E9%97%A812%EF%BC%9A%E5%9B%BD%E5%86%85%E7%94%A8%E6%88%B7%E6%80%8E%E4%B9%88%E6%96%B9%E4%BE%BF%E5%9C%B0%E5%AE%89%E8%A3%85%E7%AC%AC%E4%B8%89%E6%96%B9%E6%8F%92%E4%BB%B6%EF%BC%8C%E5%91%8A%E8%AF%89%E4%BD%A0%203%20%E6%9D%A1%E8%B7%AF) — 国内装插件的 3 种方式
- [Obsidian 入门9：别在'插件森林'里迷路，先试试核心插件 - 模板](/blog/Obsidian%20%E5%85%A5%E9%97%A89%EF%BC%9A%E5%88%AB%E5%9C%A8'%E6%8F%92%E4%BB%B6%E6%A3%AE%E6%9E%97'%E9%87%8C%E8%BF%B7%E8%B7%AF%EF%BC%8C%E5%85%88%E8%AF%95%E8%AF%95%E6%A0%B8%E5%BF%83%E6%8F%92%E4%BB%B6%20-%20%E6%A8%A1%E6%9D%BF) — 装插件的入口在哪

### Better Export PDF 配套插件
- obsidian-tlp-classification 。如果你想给 PDF 加上文档密级标签，这个插件可以与 Better Export PDF 配合，在每页页眉自动生成 TLP 安全等级标记（如 TLP:RED / TLP:GREEN）


