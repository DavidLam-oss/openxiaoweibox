---
title: Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官
date: 2026-04-22
slug: obsidian-agent-client-ultimate-guide
excerpt: 深度实战 Agent Client 插件，实现一键切换模型与分支对话的终极集成。
cover: ""
tags:
  - Obsidian
  - AI Agent
  - MCP
  - Claude Code
  - 终端命令行
  - AI模型
  - 效率工具
status: published
---

> [!success] 认识一下
>
> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门 32：Claudian 插件实战 ,拥有这个优雅的AI管家](/blog/obsidian-claudian-plugin-tutorial)。

---

这是我们“集成三部曲”的终章。

在经历了 Terminal 的自由和 Claudian 的优雅之后，不少朋友可能会问：

“大卫，如果我想在 Obsidian 侧边栏里全都要怎么办？我既想用 Claude 的逻辑，又想用 Gemini 的博学，偶尔还想换个国产模型调调口味，难道要装一堆插件吗？”

答案就在今天这位“全能翻译官”身上:**Agent Client 插件**。

如果说前两位面试者各有所长，那么这一位就是那种“通吃全场”的顶级连接器。

---

## 核心揭秘：什么是 ACP 协议？

在介绍操作之前，我们得先聊一个听起来有点高级的词：**ACP (Agent Client Protocol)**。

别被吓跑，你只需要记住一句话：**它就是 AI 时代的“普通话标准”。**

以前，每个 AI 助手（如 Claude, Gemini）都有自己的脾气，它们说着不同的方言，笔记软件很难跟它们沟通。

而 ACP 协议就像是一部万能翻译机，只要大家都说这套“普通话”，Obsidian 就能像插拔 U 盘一样，随时更换它的 AI 大脑。

---

## 为什么要折腾这个“全能王”？

虽然配置它比前两位要稍微多花几分钟，但它的回报绝对是“降维打击”级的：

1. **一键换脑**：在同一个界面里，你不需要切窗口。这一刻你可以让 Claude 帮你重构笔记大纲，下一秒切到 Gemini 帮你查个偏门资料。
2. **跨模型联动**：我最喜欢的实战链路是。先让 Gemini 快速生成一堆素材，再一键切换到国产模型（如 MiniMax）进行地道的“去 AI 味”润色。
3. **自动感知（Context）**：它非常聪明，能自动感知你的工作状态。当你点击不同的笔记时，AI 也会自动把目光聚焦在当前这一篇，随时准备基于你手头的文稿开始干活。

最让我感慨的一件事是：这款插件曾经在 Windows 上有个报错，结果开发者直接**让 AI 辅助修复了代码并提交了更新**。

这种“AI 完善 AI 插件”的浪漫，正是我们要拥抱的未来。

---

## 实操：如何连接这根“专线”？

### 第一步：安装

同样建议使用 **BRAT 插件**：

1. 添加地址：`RAIT-09/obsidian-agent-client`。
2. 安装并启用，你会看到侧边栏出现一个可爱的小机器人图标。

### 第二步：一键“点亮”你的 AI

以前配这种插件，最头疼的就是要去终端里找那一长串绝对路径。但现在，Agent Client 的开发者已经帮我们把“活”都干了。

1. 打开 Obsidian 插件设置，找到 **Agent Client**。
2. 划到下面，找到 **「Built-in agents」** 这一栏。
3. 找到你想要的那位助手（比如 Claude Code 或 Codex），点一下它右边的 **「Auto-detect」** 按钮。

![Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98/CleanShot%25202026-04-22%2520at%252022.49.55.webp)

**奇迹发生了**：插件会自动帮你扫描电脑，并把那一长串像“身份证号”一样的路径自动填好。对于 **Claude Code** 和 **Codex** 来说，这一步做完，你的配置工作就宣告结束了。

### 第三步：给 Gemini 的一点小确认

如果你想用的是 **Gemini CLI**，除了点 `Auto-detect` 之外，请多做一个小动作：

点开它下方的 **`Arguments`**（参数）看一眼。你会发现，插件已经提前帮你填好了 `--experimental-acp` 这样的关键口令。

这就意味着，对于绝大多数用户来说，你的配置动作其实只有两个：**找对应的 AI -> 点 Auto-detect**。

只要这两个小动作做完，你的侧边栏机器人就会瞬间被点亮。

![Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98/CleanShot%25202026-04-22%2520at%252023.05.09.webp)

---

## 终极形态：它为什么是“翻译官”？

配通之后，你一定要花几分钟感受一下 Agent Client 的独特魅力。这些功能，是它作为“终极集成方案”的底气：

### 库即世界

和Claudian一样，它默认将你的整个 Obsidian 库（Vault）作为项目的根目录。这意味着，它不仅能读你眼前的笔记，它能看穿你整个知识库的连接。

### 读心术（自动上下文）

这是我最喜欢的细节。

当你正在编辑某篇笔记时，对话框会自动把这篇笔记加进上下文。你不需要手动 Add，直接提问，AI 永远知道你现在在想什么。
![Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98/CleanShot%25202026-04-22%2520at%252023.06.18.webp)

### Session 统帅部

![Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官 - 配图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98/20260422231056094.webp)

把鼠标移到对话框顶部，你会发现新大陆：

- **加号**：随时开启一段跟当前 agent 全新的对话。
- **历史记录**：点开那个“时钟”图标，你可以给对话起名字，或者随时“穿越”回某次对话继续聊。
  ![Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98/CleanShot%25202026-04-22%2520at%252023.11.48.webp)

- **Fork（分支）对话**：在历史记录弹窗中，可以看到这个在其他插件里都没见过的功能。它可以把现有的对话“岔开”，开启一个新分支。就像河流分叉一样，你可以在保留原思路的同时，拉出一个新想法去测试，互不干扰。
  ![Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官 - 配图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98/20260422234506428.webp)

### 一键换脑

在顶部列表里，你可以随时在 Claude Code、Codex 和 Gemini 之间切换。如果你喜欢用 OpenCode，也可以在插件设置里面点“Add Custom Agent”把它请进来。
![Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官 - 截图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98/CleanShot%25202026-04-22%2520at%252023.13.28.webp)

### 对话即笔记（导出功能）

顶部有一个保存按钮。点一下，它会把你们聊的所有内容包括你的提问、AI 的回答，甚至 AI 的 Thinking（思考过程）全部导出一份 Markdown 文件，自动存在库里一个叫“Agent Client”的文件夹里。

![Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官 - 截图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98/CleanShot%25202026-04-22%2520at%252023.00.32.webp)

**这种“对话产生价值，价值沉淀为笔记”的闭环，才是真正的 Obsidian 玩法。**

---

至此，我们的“Obsidian x AI 集成三部曲”就全部讲完了。

不管你选择的是硬核的 **Terminal**，优雅的 **Claudian**，还是全能的 **Agent Client**，我们的目标始终只有一个：**让 AI 彻底消失在你的工作流中，让它成为你如影随形、触手可及的“第二大脑”。**

![Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官 - 配图 9](/images/posts/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98/20260422234537012.webp)

今天的作业：**尝试用 Agent Client 连接你的第一个模型，并试着让它基于你当前的笔记提一个建议。**

下期见！

---

## 进阶阅读

- [Obsidian 入门 30:将AI集成进Obsidian侧边栏,选哪一个?](/blog/obsidian-ai-plugin-selection-guide)
- [Obsidian 入门 31：Terminal 插件实战, 开启你的“传送阵”](/blog/obsidian-terminal-plugin-advanced-guide)
- [我的AI工作流：Obsidian日记库 → Cursor侧写 → Gemini上下文](/blog/%E6%88%91%E7%9A%84AI%E5%B7%A5%E4%BD%9C%E6%B5%81%EF%BC%9AObsidian%E6%97%A5%E8%AE%B0%E5%BA%93%20%E2%86%92%20Cursor%E4%BE%A7%E5%86%99%20%E2%86%92%20Gemini%E4%B8%8A%E4%B8%8B%E6%96%87)
