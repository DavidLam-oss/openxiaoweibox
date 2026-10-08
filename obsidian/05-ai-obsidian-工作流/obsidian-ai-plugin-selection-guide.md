---
title: Obsidian 入门 30:将AI集成进Obsidian侧边栏，选哪一个?
date: 2026-04-20
slug: obsidian-ai-plugin-selection-guide
excerpt: 深度对比三款 AI 集成插件，教你如何将终端 AI “缝”进 Obsidian 侧边栏。
cover: ""
tags:
  - Obsidian
  - Claude Code
  - 效率工具
  - Obsidian插件
  - 终端命令行
  - 内容创作
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油”](/blog/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D)。

---

前三篇，我们又是装引擎，又是开“任意门”，最后还顺带去私人加油站加了点“平替油”。

- [Obsidian 入门27：装上Claude Code (CC),开启Obsidian × AI的时代](</blog/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3>)
- [Obsidian 入门28：坐标跳转，让 AI 真正“降临”你的库](/blog/Obsidian%20%E5%85%A5%E9%97%A828%EF%BC%9A%E5%9D%90%E6%A0%87%E8%B7%B3%E8%BD%AC%EF%BC%8C%E8%AE%A9%20AI%20%E7%9C%9F%E6%AD%A3%E2%80%9C%E9%99%8D%E4%B8%B4%E2%80%9D%E4%BD%A0%E7%9A%84%E5%BA%93)
- [Obsidian 入门29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油”](/blog/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D)

到现在为止，你的 Claude Code (CC) 应该已经可以跑得很欢了。

但我猜，如果你是一个追求“沉浸感”的笔记玩家，你一定会发现一个非常不爽的细节：

**你得频繁地在两个窗口之间横跳。**

一个窗口是你的 Obsidian，你在那里思考、写作；另外一个是黑乎乎的终端窗口，你在那里调遣 AI、重构代码。

这感觉就像是你请了一位学富五车的助手，但他却住在你家隔壁。你每次想问他个事，都得推开门，顶着风雨跑到隔壁，问完再跑回来。

虽然他很聪明，但这“推门跑路”的过程，把你的心流全切碎了。

今天，我们要把这位助手，正式请进你的“书房”里，让他直接坐在你的身边。

![Obsidian 入门 30:将AI集成进Obsidian侧边栏，选哪一个? - 配图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A830%EF%BC%9A%E5%B0%86AI%E9%9B%86%E6%88%90%E8%BF%9BObsidian%E4%BE%A7%E8%BE%B9%E6%A0%8F%EF%BC%8C%E9%80%89%E5%93%AA%E4%B8%80%E4%B8%AA/Gemini_Generated_Image_en2aywen2aywen2a_%25E6%2597%25A0%25E6%25B0%25B4%25E5%258D%25B0-850.webp)

---

## 为什么要“缝”进侧边栏？

很多人觉得，切个应用（Alt + Tab）也就一秒钟的事。

但相信我，**“一秒钟的断层”也是断层。**

当你把 AI “缝”进 Obsidian 的侧边栏后，你会发现这不仅仅是省下了一秒钟，而是整个工作流的质变：

你的 Obsidian 不再只是一堆静态的文本，它变成了一个随时可以响应你指令的工作台。你写完一段话，可以直接在旁边让 AI 帮你润色，或者帮你查找某个关联的笔记。

要实现这种“缝合”，目前社区里有三位各具特色的“候选人”。在接下来的三篇里，我会分别手把手教大家怎么配通它们。但在那之前，你需要先做一个小小的“性格测试”，看看哪一位最适合你的书房。

---

## 面试者 A：Claudian（优雅派的“全库助理” —— 首选）

这是我目前最推荐给普通创作者的方案，因为它把底层的命令行，包装成了你最熟悉的模样。

![Obsidian 入门 30:将AI集成进Obsidian侧边栏，选哪一个? - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A830%EF%BC%9A%E5%B0%86AI%E9%9B%86%E6%88%90%E8%BF%9BObsidian%E4%BE%A7%E8%BE%B9%E6%A0%8F%EF%BC%8C%E9%80%89%E5%93%AA%E4%B8%80%E4%B8%AA/CleanShot%25202026-04-19%2520at%252023.50.35.webp)

- **它的性格**：它给黑窗口穿上了“西装”，对话框支持 Markdown 渲染，看起来就像在用微信跟助手聊天。
- **它的绝活**：除了聊天，它最大的杀手锏是**行内编辑（Inline Edit）**。你选中一段文字，按下快捷键，它能直接在原位给你提供修改建议，甚至还能像程序员审阅代码一样，对比修改前后的差异。
- **它的范围**：它默认读取你整个 Obsidian 库作为根目录，你只需要安安静静地写字、提问。
- **它的局限**：目前它专精于 **Claude** 和 **Codex**（极客圈另一个强大的 AI 助手），暂不支持 **Gemini CLI**（Google 出品的终端助手）。另外，即便你内核加了“平替油”，它的界面上可能还是会显示“Opus”。
- **适合谁**：追求美观，希望 AI 能直接在原文上动手，且主要使用 Claude 系模型的写作者。

![Obsidian 入门 30:将AI集成进Obsidian侧边栏，选哪一个? - 配图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A830%EF%BC%9A%E5%B0%86AI%E9%9B%86%E6%88%90%E8%BF%9BObsidian%E4%BE%A7%E8%BE%B9%E6%A0%8F%EF%BC%8C%E9%80%89%E5%93%AA%E4%B8%80%E4%B8%AA/20260419234643121.webp)

---

## 面试者 B：Terminal 插件（硬核派的“原味终端”）

如果你喜欢原汁原味的极客感，不想要任何多余的 UI 修饰，那这位“老兵”是你的首选。

![Obsidian 入门 30:将AI集成进Obsidian侧边栏，选哪一个? - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A830%EF%BC%9A%E5%B0%86AI%E9%9B%86%E6%88%90%E8%BF%9BObsidian%E4%BE%A7%E8%BE%B9%E6%A0%8F%EF%BC%8C%E9%80%89%E5%93%AA%E4%B8%80%E4%B8%AA/CleanShot%25202026-04-19%2520at%252023.53.44.webp)

它非常直接，就是在你的侧边栏里开一个小窗，把你电脑的终端原样搬了进去。

- **它的性格**：没有任何包装，它就是你电脑终端的镜像。
- **它的绝活**：极其自由。因为它是原生终端，所以它支持最原始的 `cd` 指令。你可以随时在侧边栏里穿梭到库里的任何一个子文件夹，这对于经常要把笔记和代码项目放在一起的人来说，非常顺手。
- **它的优势**：它不挑食。不管你用的是 Anthropic 的 **Claude**，还是 Google 的 **Gemini**，或者是其他的 CLI（命令行助手）工具，只要你在终端能跑通的，它都能在侧边栏里完美呈现。
- **适合谁**：习惯了命令行操作，需要频繁切换工作目录，且希望在一个窗口里跑遍所有助手的硬核玩家。
  ![Obsidian 入门 30:将AI集成进Obsidian侧边栏，选哪一个? - 配图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A830%EF%BC%9A%E5%B0%86AI%E9%9B%86%E6%88%90%E8%BF%9BObsidian%E4%BE%A7%E8%BE%B9%E6%A0%8F%EF%BC%8C%E9%80%89%E5%93%AA%E4%B8%80%E4%B8%AA/20260419234726687.webp)

---

## 面试者 C：Agent Client（全能派的“协议转接头”）

![Obsidian 入门 30:将AI集成进Obsidian侧边栏，选哪一个? - 截图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A830%EF%BC%9A%E5%B0%86AI%E9%9B%86%E6%88%90%E8%BF%9BObsidian%E4%BE%A7%E8%BE%B9%E6%A0%8F%EF%BC%8C%E9%80%89%E5%93%AA%E4%B8%80%E4%B8%AA/CleanShot%25202026-04-19%2520at%252023.56.11.webp)

如果你不仅要用 Claude，还离不开 Gemini 或者其他各种大模型，那么它是目前的终极全能选择。

- **它的性格**：它是一个强大的“协议转接头”，基于 **ACP（Agent Client Protocol）** 协议打造。你可以把 ACP 想象成一套“通用方言”，有了它，即便 AI 助手和笔记软件来自不同的开发者，也能无障碍地沟通。
  ![Obsidian 入门 30:将AI集成进Obsidian侧边栏，选哪一个? - 配图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A830%EF%BC%9A%E5%B0%86AI%E9%9B%86%E6%88%90%E8%BF%9BObsidian%E4%BE%A7%E8%BE%B9%E6%A0%8F%EF%BC%8C%E9%80%89%E5%93%AA%E4%B8%80%E4%B8%AA/20260419234920987.webp)

- **它的绝活**：通吃一切。不管你后台跑的是 Claude Code、Gemini CLI 还是 Codex，它都能通过这套“方言”稳稳地接住。它甚至还能感知你的“当前状态”——你打开了哪篇笔记，它在后台就已经默默知道了。
- **它的范围**：它和 Claudian 一样，也是直接读取你整个库（Vault）作为工作空间。
- **它的门槛**：全能的代价是，它的配置过程会比前两个稍微复杂一点，需要你对端口和协议有一点点耐心。
- **适合谁**：多修玩家，工具控，以及那些必须在侧边栏用上各家助手的用户。

---

## 选型建议：你的决策清单

为了帮你省下折腾的时间，你可以对照下面这个清单做决定：

1.  如果你想**省心、好看**，且非常眼馋“直接在原文上修改”的功能：选 **Claudian**。
2.  如果你习惯敲代码，或者需要**频繁切换子文件夹**：选 **Terminal**。
3.  如果你是 **Gemini 的死忠粉**，或者是个喜欢折腾协议的工具控：选 **Agent Client**。

这三位“候选人”没有绝对的好坏，只有是否契合你的工作习惯。

一旦你选定了其中一位，把那道“物理缝隙”缝补上，你会发现：你的笔记库不再只是一个存放碎片的“仓库”，它成了一个有生命、有互动的“第二大脑”。

---

## 结尾

今天的作业：**根据上面的描述，在心里选定一位你最想请进书房的“面试者”。**

接下来的三篇里，我会分别开启这三位面试者的“保姆级”安装与配置教学。第一篇，我们先从最硬核的 **Terminal 插件** 开始，看看怎么给你的 Obsidian 装上一个真正的“传送阵”。

动手试试，下期见！

---

## 进阶阅读

- [Obsidian 入门29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油”](/blog/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D)
- [保姆级教程：将 Gemini CLI和Claude code集成到 Obsidian](/blog/%E4%BF%9D%E5%A7%86%E7%BA%A7%E6%95%99%E7%A8%8B%EF%BC%9A%E5%B0%86%20Gemini%20CLI%E5%92%8CClaude%20code%E9%9B%86%E6%88%90%E5%88%B0%20Obsidian)
- [我的AI工作流：Obsidian日记库 → Cursor侧写 → Gemini上下文](/blog/%E6%88%91%E7%9A%84AI%E5%B7%A5%E4%BD%9C%E6%B5%81%EF%BC%9AObsidian%E6%97%A5%E8%AE%B0%E5%BA%93%20%E2%86%92%20Cursor%E4%BE%A7%E5%86%99%20%E2%86%92%20Gemini%E4%B8%8A%E4%B8%8B%E6%96%87)
