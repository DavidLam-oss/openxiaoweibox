---
title: Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南
date: 2026-04-04
slug: obsidian-i18n-plugin
excerpt: 双链笔记、PKM 玩家必备：介绍 I18N 插件的云端模式，两步让 Obsidian 插件设置页变成中文，不需要配置 AI、不需要 API Key。
tags:
  - Obsidian
  - 知识管理
  - Obsidian插件
status: published
---

在前面那篇[Obsidian 入门12：国内用户怎么方便地安装第三方插件，告诉你 3 条路](/blog/Obsidian%20%E5%85%A5%E9%97%A812%EF%BC%9A%E5%9B%BD%E5%86%85%E7%94%A8%E6%88%B7%E6%80%8E%E4%B9%88%E6%96%B9%E4%BE%BF%E5%9C%B0%E5%AE%89%E8%A3%85%E7%AC%AC%E4%B8%89%E6%96%B9%E6%8F%92%E4%BB%B6%EF%BC%8C%E5%91%8A%E8%AF%89%E4%BD%A0%203%20%E6%9D%A1%E8%B7%AF)里，我们解决的是第一道门槛：怎么把插件装进去。

但我后来发现，对很多国内小白用户来说，装完插件之后，麻烦才刚开始。

插件明明已经装上了。

可你一点开设置页，里面全是英文。

什么 `Toggle`、`Enable`、`Template`、`Exclude`、`Override`，一屏幕全是英文堆在一起，很容易让人心里发毛。

![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 配图 1](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/20260404093335285.webp)

你会有一种很真实的感觉：

> 它好像就在我面前。
>
> 但又离我很远。

所以今天这篇，我想给大家一个解决方法：安装 `I18N` 这个插件。解决很多人卡在那一整页英文设置上的问题。

---

## I18N 是干嘛的？

如果你第一次看到 `I18N` 这个名字，这个词其实是很有点技术味的。

你可以先把它想简单一点：**它就是给插件设置页配一个“翻译助手”。**

它做的事很具体：专注在插件设置上，帮你把插件的设置项显示为中文。

你开始接触社区插件之后，碰到那些难啃的英文设置页，它会尽量帮你把其中一部分变得更好读。

![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 截图 2](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/CleanShot%25202026-04-04%2520at%252010.03.08.webp)

---

## 小白版用法：先用云端模式就够了

这一篇我们只讲 `I18N` 最简单、最实用、最适合新手的一条路。

### 第一步：先装 BRAT

这里要先纠正一个很关键的点。

`I18N` 这个插件现在**不在官方插件市场里**。

所以你在第三方插件里直接搜 `I18N`，是搜不到的。

这时候最省事的办法，是先装一个叫 **BRAT** 的插件。

你可以先把它理解成一个“GitHub 插件中转站”。

> 有些插件还没正式上架官方市场，但作者已经把代码放在 GitHub 上了。`BRAT` 做的，就是帮你把这些还没上架的插件装进 Obsidian，而且后面更新也会方便很多。

装 `BRAT` 的步骤反而很普通，因为它本身就在官方插件市场里：

1. 打开 `设置`
2. 进入 `Community plugins / 第三方插件`
3. 搜索 `BRAT`
4. 找到 `Obsidian42 - BRAT`
5. 点击「安装」
6. 再点击「启用」

![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 截图 3](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/CleanShot%25202026-04-04%2520at%252010.05.46.webp)

如果你之前完全没装过社区插件，或者卡在国内网络环境，可以先回去看这篇：

[Obsidian 入门12：国内用户怎么方便地安装第三方插件，告诉你 3 条路](/blog/Obsidian%20%E5%85%A5%E9%97%A812%EF%BC%9A%E5%9B%BD%E5%86%85%E7%94%A8%E6%88%B7%E6%80%8E%E4%B9%88%E6%96%B9%E4%BE%BF%E5%9C%B0%E5%AE%89%E8%A3%85%E7%AC%AC%E4%B8%89%E6%96%B9%E6%8F%92%E4%BB%B6%EF%BC%8C%E5%91%8A%E8%AF%89%E4%BD%A0%203%20%E6%9D%A1%E8%B7%AF)

### 第二步：用 BRAT 安装 I18N

`BRAT` 装好之后，打开它的设置页。

里面会有一个类似 `Add Beta plugin` 的按钮。

点进去之后，把 `I18N` 的 GitHub 仓库地址贴进去：

`https://github.com/eondrcode/obsidian-i18n`

然后确认安装。

装完之后，回到 Obsidian 的第三方插件列表，你就能看到 `Obsidian i18n` 了。把它启用就行。

![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 截图 4](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/CleanShot%25202026-04-04%2520at%252010.17.05.gif)

### 第三步：在侧边栏打开 i18n

装好启用之后，左侧栏会多出一个 **i18n** 的入口。

![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 截图 5](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/CleanShot%25202026-04-04%2520at%252010.19.56.webp)

点开它，不用进设置页，云端模式直接就在这里。

界面里有几个关键选项：

- **语言**：切到简体中文
- **云端模式**：打开开关
- **📥 下载应用**：点这个，把翻译拉下来

### 第四步：开启云端模式并下载翻译

操作顺序建议这样：

1. 点击右上角的综合设置，进入插件设置页面。先把目标语言切到简体中文
2. 接着，点击“云端译文”开关
   ![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 截图 6](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/CleanShot%25202026-04-04%2520at%252010.22.07.webp)
3. 选择排名第一的resource（也就是资源）。点击“浏览此仓库资源”。如果打开资源仓库发现无法获取资源，那么就回到插件设置页面，将“加速节点”从直连改成其他的方式。
   ![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 截图 7](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/CleanShot%25202026-04-04%2520at%252010.24.26.webp)

4. 以我们之前介绍过的“Calendar”插件为例，搜索这个插件，接着下载资源。

![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 截图 8](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/CleanShot%25202026-04-04%2520at%252010.31.14.webp)

5. 回到一开始进来的页面，点击应用
   ![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 截图 9](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/CleanShot%25202026-04-04%2520at%252010.36.22.webp)

插件会自动从社区翻译资源库把对应的汉化文件拉到你的本地。

你可以把它理解成：

别人已经先把一部分常用插件的翻译整理好了，你直接拿来用就行。

不需要做任何其他的复杂操作！

### 第五步：回到目标插件里确认效果

回到你要的目标插件的设置页。

现在看起来应该顺眼多了。

比如你之前卡在某个任务插件、日记插件、模板插件的英文设置页。

现在回去看一眼。

有些原本只能靠猜的词，现在看得明白是什么意思了。

可以看到，原本“Calendar”插件全部是英文的设置界面，现在已经都是中文了。

![Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南 - 截图 10](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/CleanShot%25202026-04-04%2520at%252010.45.11.webp)

所以，像 `Date format`、`Template`、`Enable` 这种常见设置，原来你可能只知道它“像是有用”，但不太敢点。

现在你至少能更快判断：

- 这个是在改日期格式
- 这个是在设模板
- 这个是在开关某个功能

它未必能把所有地方都翻得很完美。

但只要你不再需要一边翻译一边猜I18N这个插件就已经帮上忙了。

---

## AI 这一步先跳过

`I18N` 设置里面也有和机器翻译、AI 相关的设置。

这一篇我建议你先跳过。

如果你只是想先把插件设置页看明白一点，云端模式已经足够作为起点。

等以后我们真的讲到怎么在 Obsidian 里接 AI、怎么配置模型、怎么填 API Key，再回头看这些进阶能力，会更顺。

现在先不用管那么多。

先把最眼前这道门槛跨过去。

---

## 先敢点设置页，再说别的

我用得越久，越觉得 Obsidian 对新手不太友好的地方，在于它太自由了。

自由到很多人面对一个插件设置页时，会不知道该从哪里下手。

`I18N` 这种工具的价值，只是帮你把第一屏英文先处理掉。

这一步很基础。

也很重要：

**让你敢开始用。**

![697](/images/posts/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97/Project_Obsidian%25E5%2585%25A5%25E9%2597%25A817_I18N%25E6%258F%2592%25E4%25BB%25B6_illustration-04_7a91b4d0_20260403.webp)

如果你最近正好装了几个社区插件，却一直没认真配置过，不妨先试试这个方法。

先别研究 AI。

先把设置页看懂。

很多后面的路，都是从这一点点“看懂了，所以敢点了”开始长出来的。

## 进阶阅读

如果你想顺着这条线继续往下学，可以先接着看这几篇：

**入门系列相关：**

- 安装插件是前置步骤：[Obsidian 入门12：国内用户怎么方便地安装第三方插件，告诉你 3 条路](/blog/Obsidian%20%E5%85%A5%E9%97%A812%EF%BC%9A%E5%9B%BD%E5%86%85%E7%94%A8%E6%88%B7%E6%80%8E%E4%B9%88%E6%96%B9%E4%BE%BF%E5%9C%B0%E5%AE%89%E8%A3%85%E7%AC%AC%E4%B8%89%E6%96%B9%E6%8F%92%E4%BB%B6%EF%BC%8C%E5%91%8A%E8%AF%89%E4%BD%A0%203%20%E6%9D%A1%E8%B7%AF)
- 搭配 I18N 汉化效果最好：[Obsidian 入门11：写日记这件事，可能只差一个 Calendar](/blog/Obsidian%20%E5%85%A5%E9%97%A811%EF%BC%9A%E5%86%99%E6%97%A5%E8%AE%B0%E8%BF%99%E4%BB%B6%E4%BA%8B%EF%BC%8C%E5%8F%AF%E8%83%BD%E5%8F%AA%E5%B7%AE%E4%B8%80%E4%B8%AA%20Calendar)
- 另一个常用插件+I18N 汉化的例子：[Obsidian 入门14：在笔记中也可以做任务管理(todo)全流程](</blog/Obsidian%20%E5%85%A5%E9%97%A814%EF%BC%9A%E5%9C%A8%E7%AC%94%E8%AE%B0%E4%B8%AD%E4%B9%9F%E5%8F%AF%E4%BB%A5%E5%81%9A%E4%BB%BB%E5%8A%A1%E7%AE%A1%E7%90%86(todo)%E5%85%A8%E6%B5%81%E7%A8%8B>)

**延伸折腾方向：**

- Calendar + 模板 + 搜索的联动：[Obsidian 入门16：用 Obsidian 做日周复盘，三件套串起一套习惯](/blog/obsidian-beginner-16-daily-weekly-review)
- 折腾党向，AI 进 Obsidian：[保姆级教程：将 Gemini CLI 和 Claude code 集成到 Obsidian](/blog/保姆级教程：将 Gemini CLI和Claude code集成到 Obsidian)
- 想深度定制或自己写插件：[被官方 Bot 打回 10 次后，我终于摸清了 Obsidian 插件上架的所有"潜规则"](/blog/obsidian-plugin-submission-guide)
- 折腾 Obsidian 转公众号格式：[我做了个插件，让公众号排版不用离开 Obsidian](/blog/%E6%88%91%E5%81%9A%E4%BA%86%E4%B8%AA%E6%8F%92%E4%BB%B6%EF%BC%8C%E8%AE%A9%E5%85%AC%E4%BC%97%E5%8F%B7%E6%8E%92%E7%89%88%E4%B8%8D%E7%94%A8%E7%A6%BB%E5%BC%80%20Obsidian)

记得关注，我们下期见。
