---
title: Obsidian 入门 27：装上Claude Code (CC),开启Obsidian × AI的时代
date: 2026-04-18
slug: obsidian-claude-code-install-guide
excerpt: 介绍 Claude Code (CC) 安装教程及国内 CC Switch 丝滑使用方案，开启 AI 编程终端时代。
cover: ""
tags:
  - Claude Code
  - 自动化
  - AI编程
  - Obsidian
  - 终端命令行
  - 效率工具
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门26：想让 AI 读你的 Obsidian？你需要先认识这几个工具](/blog/Obsidian%20%E5%85%A5%E9%97%A826%EF%BC%9A%E6%83%B3%E8%AE%A9%20AI%20%E8%AF%BB%E4%BD%A0%E7%9A%84%20Obsidian%EF%BC%9F%E4%BD%A0%E9%9C%80%E8%A6%81%E5%85%88%E8%AE%A4%E8%AF%86%E8%BF%99%E5%87%A0%E4%B8%AA%E5%B7%A5%E5%85%B7)。

---

上一期我们聊了 CLI 是什么，其实就是用文字跟电脑说话，不需要图形界面。

今天，咱们就把这个听起来有点悬的概念变成现实。我来介绍第一个真实的 CLI 工具：**Claude Code (CC)**。

如果你还没用过它，我建议你今天无论如何要试一下。因为它可能是我见过的，目前全球最强的终端 **AI 编程**工具，没有之一。

---

## CC 其实是什么

CC 是 Claude Code 的简称，Anthropic 官方出品。

它不像网页版的 Claude 只能隔着屏幕聊天。你在终端里敲下一个 `claude`，那一瞬间的感觉很奇妙：你会觉得 Claude 真的「降临」到了你的电脑里。

它不仅仅能聊天，它能直接读懂你当前的整个 Obsidian 库，帮你写笔记、改文件、跑命令。它不是那种只会动嘴皮子的 AI，它是真正能帮你干活的终端 **AI 编程**助手。

其实它就是 CLI 的一种。你在[入门26](/blog/Obsidian%20%E5%85%A5%E9%97%A826%EF%BC%9A%E6%83%B3%E8%AE%A9%20AI%20%E8%AF%BB%E4%BD%A0%E7%9A%84%20Obsidian%EF%BC%9F%E4%BD%A0%E9%9C%80%E8%A6%81%E5%85%88%E8%AE%A4%E8%AF%86%E8%BF%99%E5%87%A0%E4%B8%AA%E5%B7%A5%E5%85%B7) 学过，CLI 就是用文字下指令。而 CC 让这个体验变得极其完整，它把黑乎乎的终端窗口，变成了一个充满智慧的生产力中心。

## 为什么我选 CC

我之前一直在用 Cursor。Cursor 很好，但它本质上是 IDE 加 AI，你还是在点点点。

CC 不太一样，它是纯终端的。那种感觉，就像是你直接把大脑插到了电脑的串口上。

最让我觉得惊艳的是，它跟你当前的工作目录是彻底打通的。网页版 AI，你需要粘贴内容进去，它回答你，然后这事就结束了。

**CC 是你工作流的一部分。**

在 CC 里，你会发现 **AI 编程**不再是一个遥远的概念。你让它改一个文件，它是真的去改。你让它读你整个项目，它会在几秒钟内扫完，然后告诉你：「老板，我理解了，你想做的改动在这里……」。

那种「它真的读懂了我整个文件夹」的实感，是任何网页版产品都给不了的。甚至 VS Code 也可以集成 CC。你在 IDE 里打开终端，输 `claude`，它能瞬间理解你当前复杂的项目结构。用过一次，你可能真的就回不去了。

> 到现在为止，把那种“IDE 和 CLI 只是程序云专属的想法”抛掉，把它当做 Word 一样自然地去使用。

## 安装 CC：先给电脑装个“引擎”

很多非程序员的朋友，看到代码就头大。别怕，CC 的安装其实就两步。

### 第一步：安装 Node.js（电脑的“底座”）

CC 是跑在一个叫 **Node.js** 的环境里的。你可以把它理解为运行 CC 的“底座”或者“引擎”。如果你的电脑没装它，你输入任何命令都会报错。

1. **检查一下**：打开你的终端（Mac 按 `Command + Space` 搜“Terminal”，Windows 搜“PowerShell”），输入 `node -v` 然后回车。
2. **如果没有安装**：你会看到一串错误。这时候，去 [Node.js 官网](https://nodejs.org/) 下载那个 **LTS（长期支持版）**。就像装普通软件一样，一路“下一步”到底就行。
   ![Obsidian 入门 27：装上Claude Code (CC),开启Obsidian × AI的时代 - 配图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3/20260418225715329.webp)

### 第二步：一键召唤 CC

装好底座，我们就正式召唤 CC。在终端里复制粘贴下面这行：

```bash
npm install -g @anthropic-ai/claude-code
```

> **小贴士**：如果你是 Mac 用户，可能会遇到“Permission denied”的报错。别担心，在命令前面加个 `sudo`（即 `sudo npm install -g ...`），然后按提示输入你的电脑开机密码就行。

敲下回车，你会看到终端里有很多进度条在飞速跳动。等它停下来，这就装好了。你可以试着敲个 `claude --help`，如果看到一串整齐的指令说明，恭喜你，门已经开了。

![Obsidian 入门 27：装上Claude Code (CC),开启Obsidian × AI的时代 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3/CleanShot%25202026-04-18%2520at%252022.18.34.webp)

---

## 国内用户，CC Switch：你的“隐形入场券”

我知道，官方版需要 Claude 账号和海外信用卡，这把很多人拦在了门外。

如果你不想折腾海外账号，或者想用更便宜的国产模型（比如 SiliconFlow 上的 Claude 或者 DeepSeek），那么 **CC Switch** 就是你的救星。

### 如何配置 CC Switch？

CC Switch 是一个带界面的小工具，完全不需要敲代码。

1. **下载**：去 [GitHub Releases](https://github.com/mushan0x0/cc-switch/releases) 下载适合你电脑的安装包（.dmg 或 .exe）。
   > 地址：https://github.com/farion1231/cc-switch/releases

![Obsidian 入门 27：装上Claude Code (CC),开启Obsidian × AI的时代 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3/CleanShot%25202026-04-18%2520at%252022.39.22.webp)

2. **配置 API Key**：打开软件，你会看到一排 Provider。如果你有硅基流动或者 DeepSeek 的 API Key，直接填进去，选好你想用的模型。
3. **点击 Switch**：点一下开关启用这个模型。现在，你的电脑会以为它正在连接 Anthropic 官网，但实际上，它正通过 CC Switch 连接着你指定的“平替”引擎。
   ![Obsidian 入门 27：装上Claude Code (CC),开启Obsidian × AI的时代 - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3/CleanShot%25202026-04-18%2520at%252022.47.11.webp)

现在，回到终端，再次敲下 `claude`。你会发现，虽然你没买官方订阅，但 CC 依然丝滑地启动了。这种感觉，就像是拿到了一张通往 AI 时代未来的“隐形入场券”。

![Obsidian 入门 27：装上Claude Code (CC),开启Obsidian × AI的时代 - 配图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3/20260418225857736.webp)

## AI 时代，付费是省钱的

最后，我想聊聊 Token 费用。

很多人听到「付费」就本能地抵触。我一开始也这样，总觉得网上有免费的。

但想象一下，你请一个实习生帮你干活，得付工资吧？CC 帮你读代码、改文件、重构项目，它消耗的是真实的、昂贵的算力。

**Token 费用的本质，其实是透明。**

你用了多少，付了多少，这是一种极其公平的交易。更重要的是，你不是在买流量，你是在为节省下来的时间买单。

如果你花几块钱，能让 AI 帮你省掉两小时的机械劳动，你觉得是亏了还是赚了？这个认知，在你开启 **Obsidian × AI** 之旅的第一天，一定要先建立起来。

---

## 结尾

Claude Code (CC) 是你开启终端 AI 时代的钥匙。

今天的作业很简单：**装好它，配好 CC Switch，在终端里敲下 `claude --help` 看到指令说明，就算通关。**

别小看这一步，当你把“引擎”装好，你已经领先了 90% 的 Obsidian 用户。

![Obsidian 入门 27：装上Claude Code (CC),开启Obsidian × AI的时代 - 配图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3/20260418225918809.webp)

下一篇，我会教大家如何用一行简单的命令，“降临”到你的 Obsidian 库里。到时候，你会亲眼看到 AI 是如何瞬间吸收并理解你几百篇笔记的。那才是真正的震撼瞬间。

动手试试，下期见！

---

## 进阶阅读

- [Obsidian 入门26：想让 AI 读你的 Obsidian？你需要先认识这几个工具](/blog/Obsidian%20%E5%85%A5%E9%97%A826%EF%BC%9A%E6%83%B3%E8%AE%A9%20AI%20%E8%AF%BB%E4%BD%A0%E7%9A%84%20Obsidian%EF%BC%9F%E4%BD%A0%E9%9C%80%E8%A6%81%E5%85%88%E8%AE%A4%E8%AF%86%E8%BF%99%E5%87%A0%E4%B8%AA%E5%B7%A5%E5%85%B7)
- [没有 Claude 账号，我也算是用上 Claude Code 了](/blog/%E6%B2%A1%E6%9C%89%20Claude%20%E8%B4%A6%E5%8F%B7%EF%BC%8C%E6%88%91%E4%B9%9F%E7%AE%97%E6%98%AF%E7%94%A8%E4%B8%8A%20Claude%20Code%20%E4%BA%86)
