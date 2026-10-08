---
title: 如何在 Gemini CLI 用上 Gemini 3 pro
date: "2025-11-23"
excerpt: >-
  详细介绍如何申请加入 Google Gemini CLI 的 waitlist，以便在终端中免费使用最新的 Gemini 3 Pro
  模型，并包含启用和切换模型的具体步骤。
tags:
  - AI模型
  - 效率工具
---

在昨天的文章中[保姆级教程：将 Gemini CLI和Claude code集成到 Obsidian](/blog/%E4%BF%9D%E5%A7%86%E7%BA%A7%E6%95%99%E7%A8%8B%EF%BC%9A%E5%B0%86%20Gemini%20CLI%E5%92%8CClaude%20code%E9%9B%86%E6%88%90%E5%88%B0%20Obsidian)，我分享了如何在 Obsidian 里直接调用CLI 工具。但没过多久，我发现之前配置的 Claude code模型额度用完了。

于是，我把目光转向了 Gemini CLI，它每天有 1000 次的免费请求额度，如果当前账号的额度用完，还可以切换账号继续使用。同时，也希望能在第一时间用上最新的 Gemini 3 Pro 模型。
![如何在 Gemini CLI 用上 Gemini 3 pro - 配图 1](/images/posts/202511240600207.webp)

我原本以为可以直接切换，但实际操作下来，发现需要先申请加入等待名单 (waitlist)。

这篇文章就来分享一下具体的申请步骤。

## 哪些用户需要申请

- 如果你已经是付费用户（拥有 Gemini API key、Vertex API key 或 Google AI Ultra 个人订阅），通常会自动获得访问权限，不需要额外申请。
- 其他用户，包括 Google AI Pro、Gemini Code Assist 标准版以及免费用户，则需要通过填写表单来申请。

## 申请入口

- 点击这个网址：`https://goo.gle/geminicli-waitlist-signup`
- 链接会跳转到一个 Google 表单，标题类似 “Access Gemini 3 in Gemini CLI and Gemini Code Assist”，这个表单就是用来收集申请信息的。
  ![如何在 Gemini CLI 用上 Gemini 3 pro - 配图 2](/images/posts/202511240629567.webp)

## 填写一些基本信息

表单内容很简单，按提示填写即可：

- **Google 账号邮箱**：必须是您用来登录 Gemini CLI / AI Studio 的那个。
- **是否为 Google AI Pro 订阅用户**：一个可选项，不是 Pro 用户也可以申请。
- **所在时区**。
- **勾选同意隐私条款**。

提交后，页面会提示你已成功加入等待名单。

## 提交之后会发生什么

提交申请后，Google 会分批次审核和开通权限。根据我的观察，审批的优先级可能和账户类型、所在地区等因素有关，所以等待时间可能会从几天到几周不等。

### 启用 Gemini 3 Pro

收到官方通过审核的邮件后，就可以在 Gemini CLI 里启用 Gemini 3 Pro 了。

你需要通过 `/settings` 命令，将 “Preview Features (e.g., models)” 这个选项切换为 `true`。
![如何在 Gemini CLI 用上 Gemini 3 pro - 配图 3](/images/posts/202511240706744.webp)

按照提示退出设置界面，重新运行 Gemini，就可以用上 Gemini 3 Pro 模型了。

### 切换到 Pro 模型

进入CLI 后默认使用 auto 模式进行模型自动选择。若任务复杂且需要推理，使用/mode 切换到 Pro 模型。
![如何在 Gemini CLI 用上 Gemini 3 pro - 配图 4](/images/posts/202511240716464.webp)

### 重置每日额度

如果当天的免费额度用完了，可以使用 `/auth` 命令，选择 “Login with Google”，浏览器会自动跳转，方便你快速切换个人 Gmail 账户，从而重置额度。
![如何在 Gemini CLI 用上 Gemini 3 pro - 配图 5](/images/posts/202511240729248.webp)

---

Enjoy
