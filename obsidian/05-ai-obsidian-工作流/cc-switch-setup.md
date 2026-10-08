---
title: Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来
date: 2026-05-28
slug: cc-switch-setup
excerpt: CC Switch 怎么装、怎么配、怎么跑起来？从下载到测试，10 分钟搞定。
cover: ""
tags:
  - 自动化
  - Claude Code
  - AI模型
  - 效率工具
  - Obsidian入门
  - Obsidian
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 入门54 把模型、入口工具、插件三层关系串成了链条，提到了 CC Switch 是「让国产油能加进去的转换器」。
>
> 这篇把它落地，从下载安装到配好第一个模型，10 分钟跑起来。

如果你看过上一篇文章，应该记得这个比喻：模型是油、Claude Code 是车、CC Switch 是转换器。

这篇就讲一件事，怎么把这个转换器装好、把油管接上，让车真正跑起来。

---

## CC Switch 是什么

简单说，CC Switch 是一个桌面软件。把 Claude Code、Codex、Gemini CLI、OpenClaw 这些工具的配置统一管起来。以前换一个模型要改 JSON、TOML、`.env` 各种格式的文件，改错一个字符就报错。现在点一下界面就好了。

它支持 6 个主流工具：Claude Code、Codex、Gemini CLI、OpenCode、OpenClaw、Hermes Agent。

内置 50 多个 AI 模型提供商，国内常用的 Deepseek、 MiniMax、GLM（智谱）、Kimi（Moonshot）、硅基流动都在里面，直接选就行。不需要海外信用卡也不需要有 claude 或者 ChatGPT 等国外的模型，用国内的 API Key 就能跑。

官网是 **ccswitch.io**，或者直接去 GitHub Releases 页面下载。现在的最新版本是v3.15.0。
https://github.com/farion1231/cc-switch/releases

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.23.18%25402x.webp)

> 我们之前在[Obsidian 入门27：装上Claude Code (CC),开启Obsidian × AI的时代](</blog/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3>)中有简单介绍过 CC switch 的使用。

---

## 下载安装

### macOS

去 GitHub Releases 页面下载 `.dmg` 文件，双击安装。macOS 版已经通过了 Apple 的签名认证，直接装就行，不用额外设置。

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.25.20%25402x.webp)

### Windows

下载 `CC-Switch-v{版本}-Windows.msi` 安装包，或者下载 `-Portable.zip` 的便携版，解压就能用。

装完之后打开，界面是这样的：主界面 + 侧边栏，简洁清晰。右上角有一个加号的按钮，这就是你要点的第一个东西。

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.27.47%25402x.webp)

---

## 添加第一个模型供应商

在上方可以看到一排按钮，从左到右依次是 Claude code CLI、Claude code 桌面版、Codex、Gemini CLI、OpenClaw、Hermes-agent。我们使用 obsidian 的话，最常用的是Claude code CLI和 Codex。

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.29.35%25402x.webp)

以Claude code CLI为例，我们来添加一个模型提供商

### 选择 Provider

点击右上角的加号，CC Switch 会弹出一个列表，里面有 50 多个预设的 Provider。

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.37.38%25402x.webp)

列几个国内常用的：

- DeepSeek。现在好用又便宜的模型，按量付费的。
- **MiniMax** 。国产模型，性价比不错。可以购买包月套餐。
- **GLM（智谱）** 。 国内很活跃的模型平台，也可以购买包月套餐，不过要抢而且基本上抢不到。
- **Kimi（Moonshot）** 。 月之暗面，长上下文能力突出，也有 coding plan 的包月套餐
- **SiliconFlow** 。聚合平台，一个 Key 能调多个模型

选你手上已经有 API Key 的那个，点击一键填充配置模板

### 填入 API Key

从对应的平台复制你的 API Key，粘贴进 CC Switch 的 Key 字段，保存。

如果你还没有 Key，随便选一个平台注册就能拿到免费额度。SiliconFlow 注册实名认证后送 16 元额度，MiniMax 也有新用户福利。

以 DeepSeek 为例，在弹窗中选择了之后，其他选项基本上给你预填好了。你只需要去 DeepSeek API 开放平台充值， 然后把API key 复制过来填入就好了。

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.35.05%25402x.webp)

### 启用

保存之后，在列表中选中这个模型供应商，点击「启用」。然后重启你的终端（或者重启 Claude Code），就能用新配的模型了。

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.39.24%25402x.webp)

**注意**：配好之后第一次使用，建议先在终端里跑一句简单的话测试一下。

比如打开 Claude Code 输入「你好」，如果它正常回复你了，就说明配置生效。如果报错，检查一下 API Key 有没有粘贴完整或者多了空格，或者换个模型供应商试试。

---

## 切换模型 vs 切回官方

切换 Provider 只需要在主界面选择其他的模型供应商点击启用就行，不用改任何配置文件。

如果你想切回官方登录，在 Provider 预设里找到「Official Login」添加，启用后重启终端，再重新走官方的登录流程就可以了。

---

## EchoBird：另一个选择

如果你觉得 CC Switch 的配置还是不够省心，还有一个更「一步到位」的工具叫 **EchoBird**。

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.42.26%25402x.webp)

CC Switch 的逻辑是「你已经有了工具，我帮你统一管理配置」。EchoBird 的逻辑是「你什么工具都没有？我帮你一次性装好」。

它内置了 4 个场景：安装修复 Agent（让 AI 帮你装 Claude Code / OpenClaw 等工具）、一键跑本地大模型、项目管理、应用管理。所有场景共享一个「模型中心」，配一次所有地方都能用。

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 9](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.47.00%25402x.webp)

![Obsidian 入门55：CC Switch 配置指南，10 分钟跑起来 - 截图 10](/images/posts/Obsidian%20%E5%85%A5%E9%97%A855%EF%BC%9ACC%20Switch%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97%EF%BC%8C10%20%E5%88%86%E9%92%9F%E8%B7%91%E8%B5%B7%E6%9D%A5/CleanShot%25202026-05-28%2520at%252022.48.03%25402x.webp)

官网是 **echobird.ai**，安装比 CC Switch 还简单，提供了 GitHub 下载，也提供了百度网盘、夸克云盘等国内用户便于访问的下载渠道。

简单总结：CC Switch 适合「已经有工具，想统一配置管理」的人，EchoBird 适合「什么都没有，想一步到位」的人。两个不冲突，也可以都装。

---

## 10 分钟，你应该已经跑起来了

回顾一下CC switch 的使用：

1. 下载安装 → 找到对应系统的安装包
2. 添加模型供应商 → 从 50 多个预设里选一个国内的
3. 填入 API Key → 复制粘贴，保存
4. 启用 → 点 Enable，重启终端
5. 测试 → 打开工具说句话，看能不能正常回复

到此为止，你的 CC Switch 已经配好了。不用改配置文件、不用记命令、不用折腾环境变量。

油管接好了，车能跑了。

---

## 进阶阅读

- [Obsidian 入门54：DeepSeek 怎么接进来？先把工具串起来说清楚](/blog/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A)
- [Obsidian 入门29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油”](/blog/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D)
- [Obsidian 入门27：装上Claude Code (CC),开启Obsidian × AI的时代](</blog/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3>)
