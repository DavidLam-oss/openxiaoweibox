---
title: "纯文本模型也能识图？我让 DeepSeek 长出了「眼睛」"
date: "2026-06-17"
slug: "deepseek-vision-mcp"
excerpt: "给 DeepSeek 配个 MCP「外挂」，三步获得识图能力"
tags:
  - AI模型
  - MCP
  - 自动化
status: published
---
在昨天的介绍 [Reasonix](/blog/%E6%88%91%E6%98%AF%E6%80%8E%E4%B9%88%E5%81%9A%E5%88%B0%E7%94%A8%20DeepSeek%20%E8%BE%BE%E5%88%B0%20100%25%20%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87%E7%9A%84%EF%BC%9F)的 文章中讲到，DeepSeek 的文本能力我很满意。中文理解到位，指令跟得紧，价格也便宜。

但它是纯文本模型，不能识图。给截图、表格照片、手绘图，它都看不到。在写作、办公、日常信息处理这些场景里，确实不方便。

![纯文本模型也能识图？我让 DeepSeek 长出了「眼睛」 - 配图 1](/images/posts/%E7%BA%AF%E6%96%87%E6%9C%AC%E6%A8%A1%E5%9E%8B%E4%B9%9F%E8%83%BD%E8%AF%86%E5%9B%BE%EF%BC%9F%E6%88%91%E8%AE%A9%20DeepSeek%20%E9%95%BF%E5%87%BA%E4%BA%86%E3%80%8C%E7%9C%BC%E7%9D%9B%E3%80%8D/20260617231107409.webp)


## 哪些场景需要识图

举个例子：想分析公众号文章的配图设计？它看不到。要从聊天记录截图里提取文字？它看不到。画了流程图想检查逻辑？同样看不到。

类似的不便还有很多：

- 收到名片想自动录入通讯录，不行
- 拍了白板上的会议纪要，它识别不了
- 海报上的活动时间和地点，它提取不出来
- 软件报错了，截个图想查解决方案，更是不可能

如果你也遇到过这种「就差一张图」的尴尬，那下面这个方案应该能帮到你。

## 解决方案：MCP「外挂」

MCP 全称 Model Context Protocol，简单说，就是让模型可以调用外部工具。

DeepSeek 本身不能看图，但你可以给它配一个「外挂」，一个专门负责看图的多模态模型。当遇到图片时，DeepSeek 通过 MCP 协议把任务转发给外挂，拿到分析结果后继续处理。

![纯文本模型也能识图？我让 DeepSeek 长出了「眼睛」 - 配图 2](/images/posts/%E7%BA%AF%E6%96%87%E6%9C%AC%E6%A8%A1%E5%9E%8B%E4%B9%9F%E8%83%BD%E8%AF%86%E5%9B%BE%EF%BC%9F%E6%88%91%E8%AE%A9%20DeepSeek%20%E9%95%BF%E5%87%BA%E4%BA%86%E3%80%8C%E7%9C%BC%E7%9D%9B%E3%80%8D/20260617225813819.webp)


我用的外挂是硅基流动（SiliconFlow）上的 Qwen3.5-397B 多模态模型。中文图片识别能力好，价格也便宜。

这个方法不挑工具。不管你用的是 [Reasonix](/blog/%E6%88%91%E6%98%AF%E6%80%8E%E4%B9%88%E5%81%9A%E5%88%B0%E7%94%A8%20DeepSeek%20%E8%BE%BE%E5%88%B0%20100%25%20%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87%E7%9A%84%EF%BC%9F)、Claude Code、Codex 还是其他支持 MCP 的 agent，只要你的 agent 跑的是 DeepSeek，用同样的方法配一个 Vision MCP，都能让它具备识图能力。

## 配置步骤：复制一段 prompt 就行

如果你也在用 DeepSeek 且需要识图能力，配置起来很简单。不用记那些技术步骤，把下面这段 prompt 发给你的 agent 就行，把方括号里的内容换成你的信息：

```text
请帮我配置一个 Vision MCP 服务，使用以下信息：

平台名称：[你的平台，如 硅基流动/SiliconFlow]
模型名称：[多模态模型名称，如 Qwen/Qwen3.5-397B-A17B]
API Key：[你的 API Key]

请完成以下步骤：
1. 创建 MCP server 目录
2. 安装 @modelcontextprotocol/sdk 依赖
3. 编写 index.js，实现 analyze_image 工具
4. 注册到 MCP 配置中
5. 验证可用
```

Agent 收到后会帮你把整个 MCP 服务搭好。你不需要知道怎么装 Node.js，不需要写代码，也不需要手动改配置文件。

你只需要自己填三样东西：
- 用哪个平台（比如硅基流动、OpenAI、Anthropic）
- 用哪个多模态模型
- 你的 API Key

![纯文本模型也能识图？我让 DeepSeek 长出了「眼睛」 - 配图 3](/images/posts/%E7%BA%AF%E6%96%87%E6%9C%AC%E6%A8%A1%E5%9E%8B%E4%B9%9F%E8%83%BD%E8%AF%86%E5%9B%BE%EF%BC%9F%E6%88%91%E8%AE%A9%20DeepSeek%20%E9%95%BF%E5%87%BA%E4%BA%86%E3%80%8C%E7%9C%BC%E7%9D%9B%E3%80%8D/20260617225920190.webp)


配好之后，给 DeepSeek 发一张图片路径，它就会自动调用 Vision MCP 来分析。

对用户来说，就像 DeepSeek 自己突然能看图了一样。

![纯文本模型也能识图？我让 DeepSeek 长出了「眼睛」 - 配图 4](/images/posts/%E7%BA%AF%E6%96%87%E6%9C%AC%E6%A8%A1%E5%9E%8B%E4%B9%9F%E8%83%BD%E8%AF%86%E5%9B%BE%EF%BC%9F%E6%88%91%E8%AE%A9%20DeepSeek%20%E9%95%BF%E5%87%BA%E4%BA%86%E3%80%8C%E7%9C%BC%E7%9D%9B%E3%80%8D/20260617230343499.webp)


## 实测体验

这套配置我已经用了好几天，实测表现不错。

识别配图中的文字、分析聊天记录截图、检查流程图逻辑，都能准确完成。

![纯文本模型也能识图？我让 DeepSeek 长出了「眼睛」 - 截图 5](/images/posts/%E7%BA%AF%E6%96%87%E6%9C%AC%E6%A8%A1%E5%9E%8B%E4%B9%9F%E8%83%BD%E8%AF%86%E5%9B%BE%EF%BC%9F%E6%88%91%E8%AE%A9%20DeepSeek%20%E9%95%BF%E5%87%BA%E4%BA%86%E3%80%8C%E7%9C%BC%E7%9D%9B%E3%80%8D/CleanShot%25202026-06-17%2520at%252023.11.33%25402x.webp)


而且 MCP 的好处是配好之后完全无感。你不需要手动切换工具，DeepSeek 遇到图片会自动调用。

如果你也想给 DeepSeek 装上「眼睛」，试试这个方案。整个配置过程就是复制一段 prompt、填好三个信息、发给你的 agent，然后等着它帮你搞定。

我用的硅基流动有免费试用额度，如果你还没选好平台，可以先从它试起。
