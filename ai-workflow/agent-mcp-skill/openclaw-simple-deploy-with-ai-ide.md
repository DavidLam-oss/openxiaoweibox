---
title: 用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw
date: 2026-03-04T00:00:00.000Z
slug: openclaw-simple-deploy-with-ai-ide
excerpt: >-
  上次写了腾讯云镜像教程，那篇绑定腾讯云。这次换个思路：如果你有 Claude Code 或 codex，填个表，让 AI
  帮你部署。不绑定腾讯云，阿里云、华为云，甚至自己的电脑都能用。核心思路：你有 AI，就让 AI 帮你装 AI。
cover: ""
tags:
  - OpenClaw
  - 效率工具
  - AI模型
  - 服务器运维
  - 多平台分发
status: published
---

上次写了篇 [适合普通人的 OpenClaw 安装教程：10 分钟就在飞书上跟 AI 对话](/blog/%E9%80%82%E5%90%88%E6%99%AE%E9%80%9A%E4%BA%BA%E7%9A%84%20OpenClaw%20%E5%AE%89%E8%A3%85%E6%95%99%E7%A8%8B%EF%BC%9A10%20%E5%88%86%E9%92%9F%E5%B0%B1%E5%9C%A8%E9%A3%9E%E4%B9%A6%E4%B8%8A%E8%B7%9F%20AI%20%E5%AF%B9%E8%AF%9D)，教你怎么用腾讯云进行部署。

![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 1](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/20260304213938765.webp)

那篇文章发出去后，有个朋友问我：我没有腾讯云，用的是阿里云，怎么办？

我说：也可以啊，就是得自己装。

他说：那你帮我装一下？

我说：我不会。

开个玩笑。我会装，但我不想帮他装。我想做的是：写一个更简单的教程，让他能自己搞定。

这篇文章就是这个教程。

核心思路很简单：**你有 AI，就让 AI 帮你装 AI。**

_这段提示词在后面直接提供给你了。_

![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 2](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/20260304213044662.webp)

---

## 你需要准备什么

只需要 4 样东西：

1. **一台服务器**（或者你自己的电脑）
2. **一个模型 API Key**
3. **（可选）飞书或 Telegram 的凭证**
4. **一个 AI IDE**（Claude Code / Codex / Cursor / 其他都行）

下面详细说每样东西怎么获取。

---

## 如何获取这些信息

### 服务器信息

> 购买服务器的地址如下：
>
> - 腾讯云： https://cloud.tencent.com/act/pro/lighthouse-moltbot
> - 阿里云： https://cn.aliyun.com/benefit/scene/moltbot？from_alibabacloud=
> - 火山引擎： https://www.volcengine.com/activity/clawdbot

_如果嫌麻烦，也可以直接购买预装了 OpenClaw 镜像的服务器，步骤可以参考[适合普通人的 OpenClaw 安装教程：10 分钟就在飞书上跟 AI 对话](/blog/%E9%80%82%E5%90%88%E6%99%AE%E9%80%9A%E4%BA%BA%E7%9A%84%20OpenClaw%20%E5%AE%89%E8%A3%85%E6%95%99%E7%A8%8B%EF%BC%9A10%20%E5%88%86%E9%92%9F%E5%B0%B1%E5%9C%A8%E9%A3%9E%E4%B9%A6%E4%B8%8A%E8%B7%9F%20AI%20%E5%AF%B9%E8%AF%9D)_

如果你买的是云服务器，需要知道三样东西：

- **IP 地址**：在云服务器控制台能找到，是一串数字，比如 123.45.67.89
- **用户名**：通常是 root，如果你没改过的话
- **密码**：买服务器时你设置的那个

**腾讯云怎么找**：打开控制台 → 轻量应用服务器 → 点进去就能看到 IP。密码如果忘了，可以重置。

![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 截图 3](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/CleanShot%25202026-03-04%2520at%252021.33.28.webp)

**阿里云和火山引擎怎么找**：类似，在 ECS 实例列表里。

**如果你用自己的电脑**：不用填这些，AI 会直接在本地部署。

### 模型 API Key

OpenClaw 需要一个「大脑」，就是大模型的 API Key。

去这几家申请都行：

- DeepSeek：platform.deepseek.com
- 智谱 GLM：open.bigmodel.cn
- Kimi：platform.moonshot.cn

新用户一般都有免费额度，够你玩一段时间了。

不想自己申请的话，小黄鱼上也有不少人拼车，几块钱就能买到。渠道很多，按自己需求选就好。

### 飞书凭证（可选）

如果你想用飞书跟 AI 对话，需要创建一个飞书应用。

**Step 1：创建应用**

打开飞书开放平台：open.feishu.cn

登录后，点击「创建企业自建应用」。填个名字（比如「我的 AI 助手」）、描述，选个图标。
![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 4](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/20260225222402698.webp)

**Step 2：添加机器人**

进入应用管理页面。左侧找到「添加应用能力」，选择「机器人」，点添加。
![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 5](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/20260225222440062.webp)

**Step 3：复制凭证**

左侧导航找到「凭证与基础信息」，把 App ID 和 App Secret 复制下来，存好。

![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 截图 6](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/CleanShot%25202026-02-25%2520at%252022.25.01.webp)

**Step 4：配置事件**

左侧找到「事件与回调」→ 选择「长连接接收事件」→ 点保存。
![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 截图 7](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/CleanShot%25202026-02-25%2520at%252022.27.26.webp)

然后点「添加事件」→ 搜索「接收消息」→ 确认添加。
再切到「回调配置」页签 → 选择「使用长连接接收回调」→ 保存。

![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 8](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/20260225222936270.webp)

**Step 5：配置权限**

左侧找到「权限管理」→ 点「批量导入权限」。
![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 9](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/20260225223127755.webp)
把下面这段 json 复制进去：

```json
{
  "scopes": {
    "tenant": [
      "im:message",
      "im:message.p2p_msg:readonly",
      "im:message.group_at_msg:readonly",
      "im:message:send_as_bot",
      "im:resource",
      "contact:user.base:readonly",
      "im:message.group_msg",
      "im:message:readonly",
      "im:message:update",
      "im:message:recall",
      "im:message.reactions:read",
      "docx:document:readonly",
      "drive:drive:readonly",
      "wiki:wiki:readonly",
      "bitable:app:readonly",
      "task:task:read",
      "contact:contact.base:readonly",
      "docx:document",
      "docx:document.block:convert",
      "drive:drive",
      "wiki:wiki",
      "bitable:app",
      "task:task:write"
    ],
    "user": []
  }
}
```

点下一步， 确认， 等权限导入完成。
![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 10](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/20260225223203533.webp)
**Step 6：发布应用**

左侧找到「版本管理与发布」→ 点「创建版本」→ 填个版本号（比如 1.0.0）→ 保存并发布。
![publish.png](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/CleanShot%25202026-02-25%2520at%252022.34.10.webp)
如果你是自己创建的企业， 审批人就是你自己， 去 admin.feishu.cn 审批通过就行。

### Telegram（可选，比飞书简单）

如果你更习惯用 Telegram， 这个更简单。

1. 在 Telegram 搜索 **@BotFather**
   ![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 截图 12](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/CleanShot%25202026-03-04%2520at%252021.56.21.webp)

2. 发送 `/newbot`
3. 按提示给 Bot 起个名字
4. 拿到 Bot Token（格式是 `123456:ABC-xxx` 这样的一串字符）

就这些。Telegram 不用配置权限，拿到 Token 就能用。

---

## 复制这个 Prompt，填空，粘贴给你的 AI

准备好了吗？接下来是最爽的部分。
打开你的 AI IDE（Claude Code、Codex、Cursor 都行），把下面的 Prompt 复制进去，**填好你的信息**，然后回车。

### 极简版（只配模型，用网页测试）

如果你暂时不想配置飞书或 Telegram，先用这个版本。部署完可以直接在浏览器里跟 AI 对话。。

```
帮我在服务器上部署 OpenClaw.

## 服务器信息
- IP 地址: [在云服务器控制台能找到，是一串数字,比如 123.45.67.89]
- 用户名: [通常是 root，如果你没改过的话]
- 密码: [买服务器时你设置的那个]

## AI 模型配置
- 模型提供商: [deepseek / zhipu / moonshot / anthropic / openai]
- API Key: [填写你的 API Key]

## 部署要求
1. 连接到服务器
2. 安装 Node.js 22（如果还没有）
3. 安装 OpenClaw： npm install -g openclaw@latest
4. 运行非交互式 onboarding 配置模型
5. 启动 gateway 服务
6. 告诉我怎么打开 Control UI 测试

参考文档: https://docs.openclaw.ai
```

### 完整版（配模型 + 飞书/Telegram）

如果你想把 AI 接到飞书或 Telegram， 用这个版本。

```
帮我在服务器上部署 OpenClaw.
## 服务器信息
- IP 地址: [填写]
- 用户名: [填写]
- 密码: [填写]

## AI 模型配置
- 模型提供商: [填写]
- API Key: [填写]

## 通道配置（选一个）
我想用 [飞书 / Telegram] 跟 AI 对话:
### 飞书
- App ID: [填写]
- App Secret: [填写]

### 或者 Telegram
- Bot Token: [填写]

## 部署要求
1. 连接到服务器
2. 安装 Node.js 22（如果还没有）
3. 安装 OpenClaw
4. 配置模型和通道
5. 启动 gateway 服务
6. 告诉我怎么配对
参考文档: https://docs.openclaw.ai
```

把方括号里的内容换成你自己的信息，粘贴给 AI，剩下的就是等待。

---

## 配对：第一次对话前的最后一步

部署完成后，第一次跟 AI 对话需要「配对」。这是 OpenClaw 的安全机制，防止陌生人乱用你的机器人。

### 飞书配对

1. 打开飞书， 搜索你刚创建的机器人，发一条消息（比如「hi」）
2. 它会回复一个配对码，比如 `ABC123`
   ![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 截图 13](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/CleanShot%25202026-03-04%2520at%252022.08.18.webp)

3. 回到你的 AI IDE，告诉它：「帮我批准配对码 ABC123」

### Telegram 配对

1. 在 Telegram 找到你的 Bot，发一条消息
2. 它会回复配对码(与飞书类似)
3. 同样让 AI 帮你批准，或者自己运行命令
   配对完成后，就可以正常对话了。

---

## 第一次对话：领养仪式

配对好之后，发一条消息试试。

它会回复你一段话，大意是：

> 「我刚上线，啥都没有，名字、性格、记忆全是空白的。你叫什么？我怎么称呼你？给我起个名字吧？」

这是 OpenClaw 的 onboarding 流程。

每个人的第一次对话都是这样的——它是一张白纸，等你来定义。

给它起个名字，告诉它怎么称呼你，设定它的性格。

这个过程有点像领养了一只电子宠物，挺有仪式感的。

从这一刻起，它就是你的了。
![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 14](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/20260225223640429.webp)

---

## 它能帮你干什么

跑起来之后，你会发现它的能力远超一个聊天机器人。

分享几个我自己在用的场景：

**每日定制日报。** 我设了一个定时任务，让它每天早上去网上
搜索我关注的领域，整理成一份日报发给我。每天早上打开手机，就能看到一份按我口味定制的资讯摘要。
![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 15](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/20260225223740242.webp)

**社交媒体「养号」** 。我让它在即刻上注册了一个账号，每天浏览帖子、点赞、写评论。第一次看到它自己去即刻上逛、发帖、跟人互动的时候，有一种「它成精了」的感觉。
![用 AI 部署 AI：一个提示词 10 分钟装好 OpenClaw - 配图 16](/images/posts/%E7%94%A8AI%E9%83%A8%E7%BD%B2AI%EF%BC%9A%E4%B8%80%E4%B8%AA%E6%8F%90%E7%A4%BA%E8%AF%8D10%E5%88%86%E9%92%9F%E8%A3%85%E5%A5%BDOpenClaw/e50fa9337727c8eb0b8f97312b374eac.webp)

**随时随地记笔记。** 我用了 Obsidian 的 Fast Note Sync 插件，把 OpenClaw 和本地笔记打通了。走在路上、等电梯的时候，一条消息发给它，它就自动帮我存到 Obsidian 里。

---

上次那篇教程，是教你怎么「买」一个现成的。

这篇教程，是教你怎么「造」一个自己的。

买的好处是省心，造的好处是自由。

你有阿里云、华为云，甚至一台旧电脑？都能部署。

你不想绑定某个云厂商？随时迁移。

**你有了 AI，就不用再被「会不会」卡住了。**

有问题，问你的 AI。它会帮你搞定。
