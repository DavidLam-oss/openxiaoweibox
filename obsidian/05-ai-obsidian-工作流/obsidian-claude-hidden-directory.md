---
title: Obsidian 入门35：装完的 Skill 去哪了？揭秘 .claude 隐藏目录
date: 2026-04-25
slug: obsidian-claude-hidden-directory
excerpt: 跟着教程装完 Skill，但在 Obsidian 里死活找不到？它其实藏在一个你看不见的文件夹里。
cover: ""
tags:
  - Obsidian
  - Claude Code
  - 编程开发
  - 提示词工程
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门34：搞懂 Agent、MCP、Skill，看懂 AI 打工团队](/blog/Obsidian%20%E5%85%A5%E9%97%A834%EF%BC%9A%E6%90%9E%E6%87%82%20Agent%E3%80%81MCP%E3%80%81Skill%EF%BC%8C%E7%9C%8B%E6%87%82%20AI%20%E6%89%93%E5%B7%A5%E5%9B%A2%E9%98%9F)。

---

你有没有想过，Claude Code 每次开工前，它是怎么知道"该怎么帮你"的？

它不是靠猜的。每次开工前，它都会先读一份文件。

那份文件里写了你想让它怎么工作、你希望它注意什么、你有没有什么特别的要求。这份文件就像它的"工作手册"，读完才开工。

这份工作手册放在哪里？

放在一个叫 **`.claude`** 的文件夹里。

## 这个文件夹在哪？

大多数人的第一反应是去 Obsidian 里找。结果翻了一圈，没有。

打开 Finder 或文件资源管理器，也看不到。好像根本不存在。

它确实存在。只是，它是一个**隐藏文件夹**。

你可能觉得这有点奇怪：为什么要藏起来？

设计师是这么想的：电脑上装了很多软件，每个软件都有自己的配置文件，这些文件你平时不需要看到，也不需要去改，所以系统默认把它们"收"到一个看不见的地方，省得你误删或者乱动。这是 macOS 和 Windows 的共同设计。

所以 `.claude` 这个文件夹，就在电脑的某个角落里，只是默认不在屏幕上显示。

![揭开隐藏](/images/posts/Obsidian%20%E5%85%A5%E9%97%A835%EF%BC%9A%E8%A3%85%E5%AE%8C%E7%9A%84%20Skill%20%E5%8E%BB%E5%93%AA%E4%BA%86%EF%BC%9F%E6%8F%AD%E7%A7%98%20.claude%20%E9%9A%90%E8%97%8F%E7%9B%AE%E5%BD%95/Project_Obsidian%25E5%2585%25A5%25E9%2597%25A835_claude%25E7%259B%25AE%25E5%25BD%2595_illustration-02_30ca24df_20260425.webp)

## 它在哪？

- **Mac 用户**：在你的用户主目录里，路径是 `~/.claude`（波浪线代表你的用户文件夹）
- **Windows 用户**：在 `C:\Users\你的用户名\.claude` 这个位置

找到它不难。Mac 用户在 Finder 里按 `Command + Shift + G`，然后输入 `~/.claude`，回车，就会直接跳进去。Windows 用户直接在这个路径 `C:\Users\你的用户名\.claude` 后面加上 `\`，粘贴到地址栏回车就行。

进去之后会看到三个东西：

- **CLAUDE.md**：这是给 AI 看的"工作手册"，AI 每次开工前都会先读一遍
- **settings.json**：Claude Code 的设置，比如你用的是什么模型
- **skills/**：你装的所有 Skill，都放在这里

Skill 装完之后，就藏在 `skills/` 里面。

所以你跟着教程装了 Skill，文件确实放进去了，但你在 Obsidian 里看不到它，在 Finder 里也看不到它。不是丢了，是藏在这里了。

## 那改了配置，怎么知道有没有生效？

最简单的方式：直接打开那个文件，看看里面是不是你写的内容。改之前打开看一遍，改之后再打开看一遍，一致，就生效了。

或者更直接：直接问 AI「你现在读的 CLAUDE.md 在哪个路径？」它会告诉你它用的是哪一份。

---

还有一个关键的事要知道：`.claude` 目录有两处。

一处是你用户主目录里的那份，这是**全局级**的，意思是这台电脑上所有 Claude Code 实例都会读这一份。

另一处在你的 Obsidian 库根目录下面，这是**项目级**的，只对这个库有效。

两套是**分开独立**的。你改了主目录里的那份，不会影响这个库里的 AI；反过来也一样。

就像同一套工具，在不同的房间贴着不同的说明书。AI 在哪个房间，就读哪张纸。改错了地方，自然不起作用，很多人卡在这里就是这个原因。

![双重维度](/images/posts/Obsidian%20%E5%85%A5%E9%97%A835%EF%BC%9A%E8%A3%85%E5%AE%8C%E7%9A%84%20Skill%20%E5%8E%BB%E5%93%AA%E4%BA%86%EF%BC%9F%E6%8F%AD%E7%A7%98%20.claude%20%E9%9A%90%E8%97%8F%E7%9B%AE%E5%BD%95/Project_Obsidian%25E5%2585%25A5%25E9%2597%25A835_claude%25E7%259B%25AE%25E5%25BD%2595_illustration-01_f6eba1f9_20260425.webp)

---

现在你知道了：Skill 在哪、CLAUDE.md 在哪、全局和项目有什么区别、怎么验证修改有没有生效。

不过每次都要找到那个隐藏的文件夹再进去改，确实有点麻烦。

下一期我会介绍一种方法，让你在 Obsidian 里直接看到这些文件，像管理普通笔记一样管理它们，不需要每次都去翻隐藏文件夹。

这个方法对 Claude Code、Codex、Gemini 都适用。

---

## 进阶阅读

- [Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家](/blog/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6)
- [Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官](/blog/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98)
- [Obsidian 入门34：搞懂 Agent、MCP、Skill，看懂 AI 打工团队](/blog/Obsidian%20%E5%85%A5%E9%97%A834%EF%BC%9A%E6%90%9E%E6%87%82%20Agent%E3%80%81MCP%E3%80%81Skill%EF%BC%8C%E7%9C%8B%E6%87%82%20AI%20%E6%89%93%E5%B7%A5%E5%9B%A2%E9%98%9F)

---

下次你装完 Skill 找不到的时候，记住它不是丢了，是藏在一个你还没注意到的地方。
