---
title: Obsidian 入门 29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油”
date: 2026-04-19
slug: obsidian-claude-code-api-switch-guide
excerpt: 揭秘 Claude Code 商业逻辑，教你通过 CC Switch 实现“换油自由”。
cover: ""
tags:
  - Obsidian
  - Claude Code
  - 自动化
  - 编程开发
  - AI模型
  - AI编程
  - 效率工具
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门28：坐标跳转，让 AI 真正“降临”你的库](/blog/Obsidian%20%E5%85%A5%E9%97%A828%EF%BC%9A%E5%9D%90%E6%A0%87%E8%B7%B3%E8%BD%AC%EF%BC%8C%E8%AE%A9%20AI%20%E7%9C%9F%E6%AD%A3%E2%80%9C%E9%99%8D%E4%B8%B4%E2%80%9D%E4%BD%A0%E7%9A%84%E5%BA%93)。

---

前两篇，咱们又是装引擎，又是开“任意门”，终于让 Claude Code (CC) 顺利降临到了你的 Obsidian 库里。

但我猜，不少朋友在兴奋之余，心里正犯嘀咕：

“这玩意儿虽然好，但官方那个 Token 计费看起来好贵啊，而且我还得去折腾海外信用卡才能开订阅……

而且，即使开通了，听说 Claude 可是封号狂魔。可别竹篮打水一场空了！”

如果你也卡在这一步，那今天这篇就是专门为你写的。

我想告诉你一个关于 CC 的真相：**你完全不需要官方订阅，也能开上这辆最顶级的跑车。**

---

## 核心揭秘：一个卖油的，一个造车的

要搞清楚这件事，咱们得先拆解一下 Anthropic（开发 Claude 的那家大公司）背后的商业逻辑。

你可以把 Anthropic 想象成一家巨大的**能源公司**。它真正的产品不是那个黑框框，而是藏在云端的 Claude 模型。它的商业模式非常直接：**卖石油（也就是算力，或者叫 Token）**。

那么，Claude Code (CC) 是什么呢？

**它是为了让你多买它的石油，而精心造的一辆“跑车”。**

Anthropic 发现，如果只是卖石油，大家可能不知道怎么用。于是它干脆造了一辆体验极佳、速度极快、跟程序员和知识创作者极其契合的交通工具，也就是 CC。

![Obsidian 入门 29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油” - 配图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D/20260419085310946.webp)

官方的如意算盘是：车我免费送你开（CC 是开源免费的），但你得加我的“原厂油”（官方订阅）。

但关键就在这里：**车的油箱其实是开放的。**

只要油路是对的，你可以加中石化的油，可以加中石油的油，甚至可以去路边的私人加油站加最便宜的“平替油”。

![Obsidian 入门 29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油” - 配图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D/20260419085532379.webp)

---

## CC Switch：那个神奇的“转换插头”

在[入门27](</blog/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3>) 里，我简要提过一句 **CC Switch**。

它的本质，就是一个安装在你电脑里的“加油站适配器”。它帮跑车伪造了一个“原厂身份”，让车子以为自己还在原厂加官方油，从而完美绕过官方的登录检查。

一头，它紧紧地插在 Claude Code 这辆跑车上；另一头，它可以帮你接通全世界任何一个你想要的加油站（也就是 API 提供商）。

![Obsidian 入门 29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油” - 配图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D/20260419085401966.webp)

有了它，当你敲下 `claude` 时，这辆车以为自己在跟官方服务器说话，但实际上，CC Switch 在中间玩了个“瞒天过海”，把请求偷偷转给了你选好的那个更便宜、更顺手的加油站。

---

## 为什么要换“私家油”？

换句话说，为什么要折腾 CC Switch？理由很简单：

1. **不需要海外信用卡**：国内的加油站（比如 **硅基流动**、MiniMax、智谱 GLM 等）支持支付宝/微信充值，甚至有很多免费额度。
2. **极度便宜**：有时候官方 20 刀一个月的量，在第三方那里可能只要几块钱，甚至免费。
3. **网络更顺滑**：国内的 API 提供商，连接速度往往比跨洋去连官方服务器要快得多。

如果你想找一个靠谱的、适合新手的“私人加油站”，我建议从 [硅基流动](https://siliconflow.cn/) 开始，它不仅有目前最强的 DeepSeek 模型，而且给新用户的免费额度非常大方，足够你开着这辆车跑上几百公里。

![Obsidian 入门 29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油” - 配图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D/20260419085441382.webp)

---

## 实操：如何给车“加私油”？

不管你用哪家的 API，在 CC Switch 那个简洁的界面里，你只需要记住三个通用的概念：

1. **API Key（加油卡）**：这代表了你。你去任何一个 API 平台注册完，都能领到一串长长的字母和数字。
2. **Base URL（加油站地址）**：这代表了加油站在哪。如果你用的是标准的加油站，CC Switch 里往往已经帮你填好了；如果你的模型提供商不在预配置的列表中，你得按要求填个地址。
3. **Model Name（几号汽油）**：这代表了你想加哪种油。是加顶级的“Claude 4.6”，还是加更实惠的“DeepSeek V3.2”或者Minimax m2.7 或者GLM 5.1。

在 CC Switch 里点点鼠标，选好模型，填好 Key，点一下开关。

![Obsidian 入门 29：Claude Code 只是辆“跑车”，你可以给它加任何“便宜的油” - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A829%EF%BC%9AClaude%20Code%20%E5%8F%AA%E6%98%AF%E8%BE%86%E2%80%9C%E8%B7%91%E8%BD%A6%E2%80%9D%EF%BC%8C%E4%BD%A0%E5%8F%AF%E4%BB%A5%E7%BB%99%E5%AE%83%E5%8A%A0%E4%BB%BB%E4%BD%95%E2%80%9C%E4%BE%BF%E5%AE%9C%E7%9A%84%E6%B2%B9%E2%80%9D/CleanShot%25202026-04-19%2520at%252008.56.24.gif)

现在，回到你的终端，再次敲下 `claude`。你会发现，这辆跑车依然跑得飞快，但每一公里的成本，可能已经降到了原本的十分之一。

---

写这一篇，是想破除大家的一个恐惧：**顶级工具，不一定意味着高昂的门槛。**

Anthropic 造了这辆好车，它是免费送给全世界的礼物。我们应该大大方方地把车开起来，哪怕你现在加的是“平替油”，那也比看着跑车在车库里吃灰要强得多。

今天的作业：**去领一个第三方的 API Key，试着用 CC Switch 跑通你的第一条指令。**

下期见！

---

## 进阶阅读

- [Obsidian 入门27：装上Claude Code (CC),开启Obsidian × AI的时代](</blog/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3>)
- [没有 Claude 账号，我也算是用上 Claude Code 了](/blog/%E6%B2%A1%E6%9C%89%20Claude%20%E8%B4%A6%E5%8F%B7%EF%BC%8C%E6%88%91%E4%B9%9F%E7%AE%97%E6%98%AF%E7%94%A8%E4%B8%8A%20Claude%20Code%20%E4%BA%86)
- [AI 时代，普通人怎么拥有自己的 API](/blog/AI%20%E6%97%B6%E4%BB%A3%EF%BC%8C%E6%99%AE%E9%80%9A%E4%BA%BA%E6%80%8E%E4%B9%88%E6%8B%A5%E6%9C%89%E8%87%AA%E5%B7%B1%E7%9A%84%20API)
