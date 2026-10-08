---
title: 没有 Claude 账号，我也算是用上 Claude Code 了
date: "2025-11-01"
excerpt: >-
  分享在没有 Claude 账号的情况下，通过开源项目 claude-code-now 配置 Minimax 等国产大模型 API，成功体验 Claude
  Code 强大编程能力的替代方案。
tags:
  - 效率工具
  - AI模型
  - AI编程
---

今年上半年的时候，就不断地听到人在说 Claude code 很厉害：比 Cursor 强多了，说这是现在最强的 AI 编程工具。

让我这个刚刚把 Cursor 用起来的人，有种 49 年入国军的感觉。

在我这个纯小白的角度，Cursor 已经让我非常惊艳了，Claude code 比 Cursor 还厉害，那不得上天了。

我也想用，但是我没有 Claude 账号，又听说 Claude 封号很疯狂也不敢找代充。只能望洋兴叹，感慨不是臣妾不想，臣妾是真的做不到啊！

### 触动

直到朋友”思潭有话说“最近看了归藏师傅的教程，使用藏师傅的项目 ai-claude-start，不再需要 Claude 而是搭配其他模型（如智谱的 GLM-4.5或者 GLM-4.6）来使用 Claude code。

思潭给我演示了他怎么使用 claude code 搭建了一个写作天团来帮助自己输出文章，顿时惊艳了：思潭太强了，Claude code 太强了。
![没有 Claude 账号，我也算是用上 Claude Code 了 - 配图 1](/images/posts/202511012117823.webp)

于是，我也有强烈的想法：我要在我的电脑装上 Claude code。

### 心动就马上行动！

思潭的项目点醒了我，原来还可以“没有 Claude 账号用 Claude code 的”。这让我想起了我之前看到过一个叫做“Claude code now”的项目，这还是个带UI 界面的。既然原理相通，我要用这个对小白更友好的。

我马上找到了这个项目的 Github 地址
https://github.com/orange2ai/claude-code-now

**我发现，这个项目本身就支持配置其他的 API 模型的，只是我以前一直有路径依赖和畏难情绪，呆在自己的舒适区不出来。所以，人啊，还是需要一些刺激**

接着按照项目指引，将这个项目安装到了我的电脑上。现在，我可以从 3 个地方打开 Claude code 了。

- **Docker 栏**
  ![没有 Claude 账号，我也算是用上 Claude Code 了 - 截图 2](/images/posts/202511012120310.webp)

- **任意文件夹**
  ![没有 Claude 账号，我也算是用上 Claude Code 了 - 截图 3](/images/posts/202511012201440.webp)

- **任意终端**
  ![没有 Claude 账号，我也算是用上 Claude Code 了 - 配图 4](/images/posts/202511012124354.webp)

### 配置API key

现在没有 Claude 的账号和 API，我可以通过配置文件直接来配置自己的API key 了。

我配的是Minimax 刚出的 minimax-m2 模型，现在到 11 月 7 日可以完全免费使用。

而且据说 GPT-5 > Claude sonnet 4.5 > **MiniMax M2** ≈ Claude Opus 4.1 > Claude Sonnet 4.0。是第一个编程能力超越 Claude Sonnet 4.0的国产大模型。

通过以下链接即可申请：
https://platform.minimaxi.com/user-center/basic-information/interface-key
![没有 Claude 账号，我也算是用上 Claude Code 了 - 截图 5](/images/posts/202511012129928.webp)

### 发现问题，又解决了问题

我在配置了我的minimax m2 之后，发现在Claude code now可选择的模型列表中并没有出现我新增加的选项。

于是，我现学现卖，将问题抛给了我手上刚刚配好 m2 模型的 Claude code（_我用其他歪招先解决了上面的问题_）。

不负众望，在（据 Claude Code 自己计算）消耗了 86.21 美金的 token 后，完美解决了问题。并且还支持在全局任意终端可以通过命令查询当前使用的模型，随时可切换至其他已配置模型等。
![没有 Claude 账号，我也算是用上 Claude Code 了 - 配图 6](/images/posts/202511012144179.webp)

---

朋友们，现在 AI 能力的进化日新月异，时常给人一种眼花缭乱学不过来的感觉。

连去年刚出的 Cursor 都给人一种昨日黄花的感觉，但再不行动起来去学 AI、用 AI，去追逐时代的浪潮，以后可能“花”都没得看了。

行动起来！
