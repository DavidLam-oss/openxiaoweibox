---
title: Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家
date: 2026-04-22
slug: obsidian-claudian-plugin-tutorial
excerpt: 拒绝复制粘贴！手把手带你配通 Claudian 插件，开启“选中文本即识别”的精准 AI 协作。掌握外部文件夹挂载技巧，让 AI 拥有“跨库”上帝视角。
cover: ""
tags:
  - Obsidian
  - Obsidian插件
  - Claude Code
  - 效率工具
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门 31：Terminal 插件实战, 开启你的“传送阵”](/blog/obsidian-terminal-plugin-advanced-guide)。

---

上一篇，我们请出了那位自由而硬核的“老兵”：Terminal 插件。

今天，我们要请出另一位面试者，她是目前整个社区里颜值最高、最懂礼貌，也最适合小白用户的**Claudian 插件**。

如果说 Terminal 是一个不修边幅的特种兵，那么 Claudian 就是一位穿着考究、温文尔雅的“全职管家”。

![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/CleanShot%25202026-04-21%2520at%252022.53.51.webp)

---

## 为什么要请这位“管家”？

站在我个人的角度，我更喜欢像 Terminal 这种精准控制的插件。但当我对比完所有的集成方案后，我必须说：**Claudian 确实是目前对新人最友好的。**

理由很简单：**它把黑窗口彻底藏了起来。**

你在侧边栏看到的，是一个精美的、支持 Markdown 渲染的聊天界面。有头像、有对话气泡、有排版，那种“有来有回”的沟通感，会让你觉得 AI 就像你的微信好友一样。

![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/CleanShot%25202026-04-21%2520at%252022.54.41.webp)

---

## 实操：如何把管家请进门？

### 第一步：安装

由于 Claudian 目前更新飞快且没有上架社区插件市场，我建议直接用 **BRAT 插件**进行安装：

1. 打开 BRAT 设置，点击 **Add Beta plugin**。
2. 填入这个地址：`YishenTu/claudian`。
3. 点击 **Add Plugin**，并启用它。

![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/CleanShot%25202026-04-21%2520at%252022.58.37.webp)

这时候，你的侧边栏就会出现一个可爱的机器人气泡图标。

![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/CleanShot%25202026-04-21%2520at%252022.59.17.webp)

> 如果你还不不会安装 BRAT插件，请看这下面这 2 篇：
>
> - [Obsidian 入门12：国内用户怎么方便地安装第三方插件，告诉你 3 条路](/blog/Obsidian%20%E5%85%A5%E9%97%A812%EF%BC%9A%E5%9B%BD%E5%86%85%E7%94%A8%E6%88%B7%E6%80%8E%E4%B9%88%E6%96%B9%E4%BE%BF%E5%9C%B0%E5%AE%89%E8%A3%85%E7%AC%AC%E4%B8%89%E6%96%B9%E6%8F%92%E4%BB%B6%EF%BC%8C%E5%91%8A%E8%AF%89%E4%BD%A0%203%20%E6%9D%A1%E8%B7%AF)
> - [Obsidian（双链笔记｜PKM）入门17：插件配置全程中文指南](/blog/Obsidian%EF%BC%88%E5%8F%8C%E9%93%BE%E7%AC%94%E8%AE%B0%EF%BD%9CPKM%EF%BC%89%E5%85%A5%E9%97%A817%EF%BC%9A%E6%8F%92%E4%BB%B6%E9%85%8D%E7%BD%AE%E5%85%A8%E7%A8%8B%E4%B8%AD%E6%96%87%E6%8C%87%E5%8D%97)

### 第二步：配置

接着打开 Claudian 插件的设置页面，你需要去插件设置里对准你的”引擎”路径：

- **Mac**：运行 `which claude` 获取路径
- **Windows**：运行 `where claude` 获取路

以 Mac 为例，打开电脑自带的终端，接着运行命令“Which claude”，你会得到一个路径：
![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/CleanShot%25202026-04-21%2520at%252023.09.04.webp)

把这个路径填入到 Claudian 插件设置中 Claude CLI 路径的位置。
![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 截图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/CleanShot%25202026-04-21%2520at%252023.01.51.webp)

这里有一个小细节，很多朋友会卡住：

> **“大卫，为什么下面显示的还是 Opus、Sonnet 这种官方名字？我加的明明是 DeepSeek 这种便宜的‘私油’啊。”**

别纠结。

因为 Claudian 做了一层深度的 UI 包装，它界面上的那些名字更像是一个“代号”。只要你底层用 **CC Switch** 配好了模型，无论 UI 上显示什么，跑的都是你最爱的那款“平替油”。

---

## 哪里不会“点”哪里

这是我最近发现的一个非常惊喜的功能。

![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 配图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/20260421234604758.webp)

以前我们要改一段话，总得手动复制，然后告诉 AI：“嘿，看这段，帮我润色一下。”

但在 Claudian 里，你只需要做一个动作：**在笔记里选中那段文字。**

当你选中一段文本后，再去看侧边栏，你会发现它已经“读心”般地提取了你选中的内容和当前的笔记上下文。

在对话框处，会显示有多少行被选中了。如果你在笔记中没有选中文本，则不会显示这个提醒文字（如果它反应慢了，你在对话框里点一下鼠标就能唤醒它的注意力）。

![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 截图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/CleanShot%25202026-04-21%2520at%252023.12.58.webp)

这种“外科手术级”的精准打击，效率极高。它不再是盲目地扫描全库，而是把所有的算力都集中在你鼠标选中的那几行字上。

---

## 打破“库”的边界

在侧边栏对话框的最下方，有一个不起眼的小文件夹图标。

这个功能非常强悍：**它可以帮你挂载库（Vault）以外的文件夹。**

因为 Claudian 会默认将你的 Obsidian 的 Vault 也就是你的库当做整个项目的根目录，如果你想将库以外的文件或者文件夹作为对话的补充，那么可以通过这种方式挂载进来。

如果你有一堆参考资料在桌面上，又不想费劲地搬进 Obsidian 库里，你只需要点一下那个图标，把桌面文件夹拉进来。AI 瞬间就拥有了“上帝视角”，能同时看到你库内的笔记和库外的资料。

![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 截图 9](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/CleanShot%25202026-04-21%2520at%252023.18.39.webp)

## @你想要的文章

也可以通过对话框中的@符号，搜索和贴入你想要放入对话中的其他文章，作为此次对话的上下文。

不用再去左侧文件列表中，找到文章再贴入了。在 Claudian 对话框中，一次完成。
![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 截图 10](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/CleanShot%25202026-04-22%2520at%252007.28.08.webp)

---

今天的作业：**装好 Claudian 插件，选中你最近写的一段话，让它在侧边栏帮你生成一个金句总结。**

**进阶挑战**：试着点一下那个小文件夹图标，挂载一个你桌面的参考文件夹，看看 AI 是不是真的能同时读到库内和库外的资料。

![Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家 - 配图 11](/images/posts/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6/20260421234643074.webp)

虽然它只是换了一身“西装”，但这种视觉上的亲和力和交互上的便利，会让你的 AI 协作体验从“我在调命令”变成“我在聊创作”。

下一篇，我们来聊聊这一系列的最后一位“全能翻译官”：**Agent Client 插件**。

下期见！

---

## 进阶阅读

**入门系列（前置知识）**

- [Obsidian 入门 31：Terminal 插件实战, 开启你的"传送阵"](/blog/obsidian-terminal-plugin-advanced-guide)（Claudian 的兄弟插件）
- [Obsidian 入门 30：将AI集成进Obsidian侧边栏，选哪一个](/blog/obsidian-ai-plugin-selection-guide)（选型对比）
- [Obsidian 入门 27：装上Claude Code (CC),开启Obsidian × AI的时代](/blog/obsidian-claude-code-install-guide)（基础概念）
- [Obsidian 入门 29：Claude Code 只是辆"跑车"，你可以给它加任何"便宜的油"](/blog/obsidian-claude-code-api-switch-guide)（省钱技巧）

**免费替代方案**

- [不花一分钱，让豆包、Kimi、Deepseek住进Obsidian](/blog/%E4%B8%8D%E8%8A%B1%E4%B8%80%E5%88%86%E9%92%B1%EF%BC%8C%E8%AE%A9%E8%B1%86%E5%8C%85%E3%80%81Kimi%E3%80%81Deepseek%E4%BD%8F%E8%BF%9BObsidian)
- [没有 Claude 账号，我也算是用上 Claude Code 了](/blog/%E6%B2%A1%E6%9C%89%20Claude%20%E8%B4%A6%E5%8F%B7%EF%BC%8C%E6%88%91%E4%B9%9F%E7%AE%97%E6%98%AF%E7%94%A8%E4%B8%8A%20Claude%20Code%20%E4%BA%86)

**扩展玩法**

- [受够了复制粘贴，我把 Obsidian 直接接进了微信后台](/blog/%E5%8F%97%E5%A4%9F%E4%BA%86%E5%A4%8D%E5%88%B6%E7%B2%98%E8%B4%B4%EF%BC%8C%E6%88%91%E6%8A%8A%20Obsidian%20%E7%9B%B4%E6%8E%A5%E6%8E%A5%E8%BF%9B%E4%BA%86%E5%BE%AE%E4%BF%A1%E5%90%8E%E5%8F%B0)（与你写作流的对接）
- [Obsidian 入门 26：想让 AI 读你的 Obsidian？你需要先认识这几个工具](/blog/Obsidian 入门26：想让 AI 读你的 Obsidian？你需要先认识这几个工具)
