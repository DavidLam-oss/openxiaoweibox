---
title: "Obsidian 入门73：别人家的 Obsidian 为什么那么好看？秘密就在这篇里"
date: "2026-07-29"
slug: "obsidian-73-themes-css-customization"
excerpt: "Obsidian 默认主题不难看，但它还能长成别样的样子。从点一下换个社区主题，到写一行 CSS 改个小细节，再到让 AI 帮你生成一个专属主题。"
tags:
  - Obsidian
  - Obsidian插件
  - 编程开发
  - Obsidian入门
  - AI模型
status: published
---

> 这是一个「Obsidian x AI」系列。
>
> 入门 3 讲了怎么换主题，但只提了一嘴。这篇把它讲透：从直接装一个别人的主题，到动动手改点小东西，再到让 AI 帮你做一个属于自己的主题。
>
> Obsidian 默认主题不难看，但很多人不知道它还能长成别的样子。

先给你看两张图。

第一张，是社区里的人用 Obsidian 的方式：

![Esther Inspired 主题效果图，思谭有话说制作](/images/posts/20260729191429822.webp)

*思谭有话说用 AI 做了一套 Obsidian + Typora 双版本的中文写作主题「Esther Inspired」，已经在 GitHub 开源。，并且上架到了Obsidian 的主题市场。

第二张，是群友深小乐的 Obsidian 首页：

![深小乐定制的 Obsidian 首页效果](/images/posts/CleanShot%202026-07-29%20at%2019.16.16%402x.webp)

*他花了两个小时，给自己做了个带绿植背景图的首页。*

它们都是 Obsidian。和你电脑上装的是同一个软件。

区别只是**主题**。

而且，这一切都不需要你会写代码。

---

## 最快的方式：点一下，换个主题

换主题是让 Obsidian 变脸最快的方式，不需要任何技术，三步搞定。

**怎么换。**

1. 打开设置 → 外观 → 主题
![Obsidian 外观设置界面，主题切换入口](/images/posts/CleanShot%202026-07-29%20at%2019.20.11%402x.webp)

2. 点「管理」，进入社区主题市场
![Obsidian 社区主题市场，按下载量排序](/images/posts/CleanShot%202026-07-29%20at%2019.25.11%402x.webp)

3. 挑一个喜欢的，点「安装并启用」



主题市场里有成千上百个主题，按下载量排序就能看到最受欢迎的。每一个都有预览图，看着喜欢就装上试试。

**换主题会影响我的笔记吗？**

完全不会。主题只改变外观，不改你一个字的内容。不喜欢的话，点一下切换回默认主题，一切恢复原样。

随便试。

---

## 不想换整个主题，只想改几个小地方：CSS Snippets（读作死你劈死）

有时候你选了一个主题，整体喜欢，就一两个小地方不满意。比如标题颜色不是你想要的，或者行距太挤了。

这时候不需要换主题，也不用改主题文件。Obsidian 有一个叫 **CSS Snippets** 的功能，可以让你在不碰主题的情况下，单独覆盖几个样式。

**怎么用。**

1. 打开设置 → 外观
2. 往下翻到「CSS 代码片段」
![CSS 代码片段设置路径：设置→外观→CSS 代码片段](/images/posts/CleanShot%202026-07-29%20at%2019.28.15%402x.webp)

3. 点文件夹图标，打开 snippets 文件夹
4. 在里面放一个 `.css` 文件，内容就是你想改的样式
5. 回到 Obsidian，在设置里点一下刷新，然后启用它

**给你几个可以直接复制粘贴的例子。**

把标题改成你喜欢的颜色：

```css
h1 { color: #e06c75; }
h2 { color: #61afef; }
```

加大正文的行距，读起来更舒服：

```css
body { line-height: 1.8; }
```

**我自己也在用。**

我装的是 Baseline 主题，整体很喜欢，但有两处不太满意：浅色模式下的代码块灰灰的看不清，另外各个层级的标题不够有区分度。

于是我自己写了两个 CSS Snippet 来补：

一个把代码块在浅色模式下变成深色背景：
```css
body.theme-light pre {
  background-color: #1e1e1e !important;
  border: 1px solid #2d2d2d !important;
  border-radius: 8px !important;
}
```

另一个给 6 级标题分别上色，从深蓝渐变到浅蓝，层一目了然：
```css
.theme-light {
  --h1-color: hsl(216, 88%, 26%);
  --h2-color: hsl(212, 100%, 33%);
  --h3-color: hsl(210, 86%, 39%);
  --h4-color: hsl(208, 58%, 49%);
  --h5-color: hsl(209, 70%, 62%);
  --h6-color: hsl(209, 65%, 72%);
}
```

两个文件放进 snippets 文件夹，刷新启用，Baseline 就变成了我自己舒服的样子。

![Baseline 主题使用 CSS Snippet 微调后的效果](/images/posts/20260729200725157.webp)


你不需要理解 CSS 语法。网上搜「Obsidian CSS snippets 好看」能找到大量别人写好的现成代码段，复制到文件里就能用。

---

## 更进一步：让 AI 帮你做个主题

如果你想要的不只是改几个颜色，而是一整套属于自己的视觉风格：标题用什么字体、引用用什么底色、代码块什么配色、表格什么样。可以考虑自己做一个主题。

以前做主题需要懂 CSS，现在有 AI 了。

我的朋友 **思谭有话说** 就是这么干的。他把自己喜欢的配色和风格描述给 AI，AI 生成了一套完整的主题，取名叫 **Esther Inspired**，支持 Obsidian 和 Typora 两个平台，已经在 GitHub 开源，也已经上架 Obsidian 主题市场。

![想法变成了一个真实的主题](/images/posts/20260729200845910.webp)


如果你也想试试，可以给他一个 prompt 模板，大概长这样（在里面描述你喜欢的风格）：

> 帮我生成一个 Obsidian 主题 CSS 文件。我喜欢的风格是：简约、暖色调、字体用苹方或思源宋体、标题用深橙色、引用块用浅黄色底、行距 1.8、代码块用深色背景。帮我生成完整的 `obsidian.css` 文件。

把这段发给 Claude 或者 ChatGPT，它会把完整的主题文件返回给你。把文件放到 Obsidian 的 snippets 文件夹里启用就行。

当然，不可能第一版就做出满意的样子。我相信这是一个一来一回的过程，你可以在和 AI 的来回中让它不断去优化和改进，并且你也能更加明确自己的需求。

做出来之后， **你是唯一一个拥有这个主题的人。**

---

主题这件事，没有对错，只有喜欢和不喜欢。

如果你一直觉得 Obsidian 默认外观差点意思，但不知道怎么下手，今天就可以开始。先从社区主题市场翻翻看，装一个试试。不花时间，也没有风险。

如果你的 Obsidian 还没变成你喜欢的样子，今晚就可以开始动起来了。

---

## 进阶阅读

### 本系列基础篇
- [Obsidian 入门3：先把它调顺眼，再开始认真用](/blog/Obsidian%20%E5%85%A5%E9%97%A83%EF%BC%9A%E5%85%88%E6%8A%8A%E5%AE%83%E8%B0%83%E9%A1%BA%E7%9C%BC%EF%BC%8C%E5%86%8D%E5%BC%80%E5%A7%8B%E8%AE%A4%E7%9C%9F%E7%94%A8) — 入门 3 提到换主题，这篇终于填坑了
- [Obsidian 入门19：认识笔记属性，你的笔记「身份证」和「配料表」](/blog/Obsidian%20%E5%85%A5%E9%97%A819%EF%BC%9A%E8%AE%A4%E8%AF%86%E7%AC%94%E8%AE%B0%E5%B1%9E%E6%80%A7%EF%BC%8C%E4%BD%A0%E7%9A%84%E7%AC%94%E8%AE%B0%E3%80%8C%E8%BA%AB%E4%BB%BD%E8%AF%81%E3%80%8D%E5%92%8C%E3%80%8C%E9%85%8D%E6%96%99%E8%A1%A8%E3%80%8D) — 笔记结构基础

### 主题与美化
- [插件升级：排版微调 + 自定义 CSS，这次是两个用户说「想要」的功能](/blog/%E6%8F%92%E4%BB%B6%E5%8D%87%E7%BA%A7%EF%BC%9A%E6%8E%92%E7%89%88%E5%BE%AE%E8%B0%83%20%2B%20%E8%87%AA%E5%AE%9A%E4%B9%89%20CSS%EF%BC%8C%E8%BF%99%E6%AC%A1%E6%98%AF%E4%B8%A4%E4%B8%AA%E7%94%A8%E6%88%B7%E8%AF%B4%E3%80%8C%E6%83%B3%E8%A6%81%E3%80%8D%E7%9A%84%E5%8A%9F%E8%83%BD) — 文章排版也可以自定义 CSS
- [Obsidian 入门45：对自己好一点，给 Obsidian 建个个人主页](/blog/Obsidian%20%E5%85%A5%E9%97%A845%EF%BC%9A%E5%AF%B9%E8%87%AA%E5%B7%B1%E5%A5%BD%E4%B8%80%E7%82%B9%EF%BC%8C%E7%BB%99%20Obsidian%20%E5%BB%BA%E4%B8%AA%E4%B8%AA%E4%BA%BA%E4%B8%BB%E9%A1%B5) — 如果你也想做一个像深小乐那样的首页

### 相关工具
- [Obsidian 入门34：搞懂 Agent、MCP、Skill，看懂 AI 打工团队](/blog/Obsidian%20%E5%85%A5%E9%97%A834%EF%BC%9A%E6%90%9E%E6%87%82%20Agent%E3%80%81MCP%E3%80%81Skill%EF%BC%8C%E7%9C%8B%E6%87%82%20AI%20%E6%89%93%E5%B7%A5%E5%9B%A2%E9%98%9F) — 如果看不懂上面的代码，先看懂 AI 的架构

---

*如果你也有好看的 Obsidian 主题或者首页配置想分享，欢迎在评论区贴出来。*
