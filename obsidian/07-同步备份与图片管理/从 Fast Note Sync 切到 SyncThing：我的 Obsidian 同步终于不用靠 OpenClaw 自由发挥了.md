---
title: 从 Fast Note Sync 切到 SyncThing：我的 Obsidian 同步终于不用靠 OpenClaw 自由发挥了
date: 2026-04-08
slug: obsidian-syncthing-migration
excerpt: 很多自动化流程跑不通，其实是坏在了「同步」这一环。Fast Note Sync 很轻量，但它的「被动属性」让同步全看 OpenClaw 的自由发挥。我换到了 SyncThing，终于实现了一个在哪改都自动一致的笔记系统。
cover: ""
tags:
  - Obsidian
  - 笔记同步
  - 效率工具
  - OpenClaw
  - 自动化
  - 服务器运维
status: published
---

上次写了一篇[不写一行代码，让服务器上的 OpenClaw 自动往我的 Obsidian 里塞笔记](/blog/%E4%B8%8D%E5%86%99%E4%B8%80%E8%A1%8C%E4%BB%A3%E7%A0%81%EF%BC%8C%E8%AE%A9%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84%20OpenClaw%20%E8%87%AA%E5%8A%A8%E5%BE%80%E6%88%91%E7%9A%84%20Obsidian%20%E9%87%8C%E5%A1%9E%E7%AC%94%E8%AE%B0)，讲的是怎么用 Fast Note Sync 把服务器上的笔记同步到本地。

> [!FAST Note Sync]
> 想要了解 FNS 细节的朋友，可以看下面：
>
> - 服务端：https://github.com/haierkeys/fast-note-sync-service
> - Obsidian 插件：https://github.com/haierkeys/obsidian-fast-note-sync

效果还不错。

但用着用着，有个不舒服的地方一直在那里。像鞋里进了一颗小石子，不影响吃饭睡觉，但就是觉得硌得慌。

## 核心痛点：FNS 的「被动同步」宿命

在讲具体的尴尬之前，得先看清 Fast Note Sync 的技术底色：**它本质上是一个基于 Obsidian 插件的同步工具。**

这意味着，同步的发生必须依赖「Mac 端的 Obsidian 插件感知到了变化」。如果变化发生在没有 GUI、没有 Obsidian 界面运行的服务器上，FNS 服务端就是睁眼瞎。

![从 Fast Note Sync 切到 SyncThing：我的 Obsidian 同步终于不用靠 OpenClaw... - 配图 1](/images/posts/%E4%BB%8E%20Fast%20Note%20Sync%20%E5%88%87%E5%88%B0%20SyncThing%EF%BC%9A%E6%88%91%E7%9A%84%20Obsidian%20%E5%90%8C%E6%AD%A5%E7%BB%88%E4%BA%8E%E4%B8%8D%E7%94%A8%E9%9D%A0%20OpenClaw%20%E8%87%AA%E7%94%B1%E5%8F%91%E6%8C%A5%E4%BA%86/Project_SyncThing_Obsidian-illustration-01.webp)

这种「被动」属性，直接导致了我在使用中的两个抓狂瞬间：

### 1. 同步全靠 AI 的「自觉」

我的工作流是这样的：OpenClaw 在服务器上跑一个任务 → 生成一篇笔记 → 然后得有人把笔记推送到 Mac 上。

以前负责推送的是 Fast Note Sync。流程虽然通，但有个隐患：**每次任务跑完，AI 得记得调用推送脚本，笔记才会出现在服务器本地，Mac 才收得到。**

听起来是自动化，其实还是靠「自觉」。

因为 AI 模型并不是每次都老老实实执行这一步。有的模型遵循度高，有的低。我同时跑好几个任务的时候，经常发生这个推了、那个没推的情况。

人也会忘。尤其是同时盯着好几件事，「等一下...我好像忘了点什么」这种事真的会发生。

不触发，它就不动。

### 2. 服务器成了「单向黑洞」

第二个问题更麻烦一点：FNS 的同步逻辑很难做到真正的实时双向。

本地 Mac 往服务器推，没问题。但反过来，如果我在服务器上改了一个错字，Mac 这边是收不到的。

这是因为服务器上没有运行着的 Obsidian，FNS 插件根本没法工作。它没法主动告诉服务端「我改了」。单向同步成了这种场景下的天然限制。

有时候我在服务器上让 OpenClaw 改了点东西，改完才想起来：诶，Mac 上显示的还是老版本。

解决办法也有，比如在服务器上装个 FNS 客户端。但问题是它必须依附于 Obsidian 才能跑，服务器上没桌面环境，这条路走不通。

## 所以我换了 SyncThing

SyncThing 不是新工具，我之前就装过，但一直没下决心迁移。这次切过来，主要是因为它解决了上面两个问题。

![从 Fast Note Sync 切到 SyncThing：我的 Obsidian 同步终于不用靠 OpenClaw... - 配图 2](/images/posts/%E4%BB%8E%20Fast%20Note%20Sync%20%E5%88%87%E5%88%B0%20SyncThing%EF%BC%9A%E6%88%91%E7%9A%84%20Obsidian%20%E5%90%8C%E6%AD%A5%E7%BB%88%E4%BA%8E%E4%B8%8D%E7%94%A8%E9%9D%A0%20OpenClaw%20%E8%87%AA%E7%94%B1%E5%8F%91%E6%8C%A5%E4%BA%86/20260408222721021.webp)

### 真正的双向同步，不靠人记

SyncThing 走的是文件系统监控的路线。你在任何一端改了文件，另一端**自动**收到，不需要任何主动触发。

OpenClaw 工作流写了一个文件 → SyncThing 检测到变化 → Mac 这边自动同步过来。全程没有「记得调用」这个环节。

**AI 不用自觉了，我也不用记了。**

![AI 不用自觉，我也不用记](/images/posts/%E4%BB%8E%20Fast%20Note%20Sync%20%E5%88%87%E5%88%B0%20SyncThing%EF%BC%9A%E6%88%91%E7%9A%84%20Obsidian%20%E5%90%8C%E6%AD%A5%E7%BB%88%E4%BA%8E%E4%B8%8D%E7%94%A8%E9%9D%A0%20OpenClaw%20%E8%87%AA%E7%94%B1%E5%8F%91%E6%8C%A5%E4%BA%86/Project_SyncThing_Obsidian_illustration-02_0c45169f_20260408.webp)

这跟 Fast Note Sync 的区别在于：SyncThing 是在**操作系统层面**监控变化。这里其实涉及到一个思维转变。

Fast Note Sync 的同步是**命令式**的。你改了文件，还得命令插件去同步。

而 SyncThing 是**声明式**的：它监控的是文件系统的最终状态。只要文件出现在文件夹里，SyncThing 的任务就是保证两边一致。它不关心是谁写的，只关心结果。这种解耦，才让流程真正变得健壮。

### 所以现在的完整架构是这样的

- **Mac ↔ 服务器**：SyncThing（双向，文件系统级监控）
- **Mac → 手机**：Fast Note Sync（单向，本地变化触发）。

两者各司其职。SyncThing 负责把服务器和 Mac 拉齐，FNS 负责把 Mac 的变化推给手机。

缺了 SyncThing，FNS 根本不知道服务器改了东西；缺了 FNS，手机就收不到通知了。

### 透明，出了问题一眼就知道在哪

SyncThing 有一个管理界面，能看到所有设备、每个文件夹的同步状态。

文件没同步成功？上面写着原因。是网络不通，还是某个文件被 `.stignore` 拦了，一目了然。

![从 Fast Note Sync 切到 SyncThing：我的 Obsidian 同步终于不用靠 OpenClaw... - 截图 4](/images/posts/%E4%BB%8E%20Fast%20Note%20Sync%20%E5%88%87%E5%88%B0%20SyncThing%EF%BC%9A%E6%88%91%E7%9A%84%20Obsidian%20%E5%90%8C%E6%AD%A5%E7%BB%88%E4%BA%8E%E4%B8%8D%E7%94%A8%E9%9D%A0%20OpenClaw%20%E8%87%AA%E7%94%B1%E5%8F%91%E6%8C%A5%E4%BA%86/CleanShot%25202026-04-08%2520at%252022.31.18.webp)

### `.stignore`让同步过来的就是干净的笔记

Obsidian vault 里不只有 Markdown 文件，还有 `.obsidian/` 文件夹（放了插件配置、主题缓存等）。

SyncThing 自带 `.stignore`，配置起来很直观：

```
.obsidian/
.DS_Store
*.tmp
```

同步过来的就是干净的笔记，不带任何 Obsidian 的内部文件。

### 支持全平台

SyncThing 支持 Windows、Mac、Linux。安卓端也有成熟的官方 App。我的场景是服务器 + Mac 两个节点，够了。

### 意外惊喜：比回收站更强的时间机器

相比 Fast Note Sync 简单的「覆盖」，SyncThing 自带了多种版本控制模式。我目前最推荐的是 **Staggered File Versioning（交错版本控制）**。

以前最怕工作流跑偏，把整篇草稿给洗了。现在 SyncThing 会在本地维护一个隐藏的 `.stversions` 文件夹，它像 macOS 的 Time Machine 一样：

- 最近 1 小时内，每 30 秒存一个版本；
- 最近 1 天内，每小时存一个；
- 超过 30 天的，每周存一个。

我把天数设为了 180 天。这意味着哪怕我今天手滑在 Mac 上删了库，或者服务器脚本写崩了，我也能找回半年前任何一天的状态。这种「物理级」的安全感，是轻量插件给不了的。

![物理级的安全感（时间机器）](/images/posts/%E4%BB%8E%20Fast%20Note%20Sync%20%E5%88%87%E5%88%B0%20SyncThing%EF%BC%9A%E6%88%91%E7%9A%84%20Obsidian%20%E5%90%8C%E6%AD%A5%E7%BB%88%E4%BA%8E%E4%B8%8D%E7%94%A8%E9%9D%A0%20OpenClaw%20%E8%87%AA%E7%94%B1%E5%8F%91%E6%8C%A5%E4%BA%86/Project_SyncThing_Obsidian_illustration-03_eeadb96b_20260408.webp)

---

## 代价也得说清楚

没有完美的方案。SyncThing 相对于 Fast Note Sync，有几个地方是需要接受的：

**要装客户端**。FNS 只需要一个脚本运行在服务器上。SyncThing 需要两边都装一个常驻进程，配置多一点。

**不需要担心网络环境**。SyncThing 优先尝试 P2P 直连。只有当两端都在严密的防火墙后，才会走官方的中继服务器。不管你在哪，它都能保证 100% 的连通性。即便没有公网 IP，同步速度通常也能跑满带宽。

**不会做格式转换**。SyncThing 就是纯文件同步，原样来原样去。Obsidian 笔记本身是 Markdown，不涉及转换，这个对我来说也不是问题。

---

## 实战小贴士：快速上手

如果你也在用 Mac + 云服务器，想要类似的体验，基本步骤如下：

1. **服务器**：下载 Linux 版，把二进制文件放到 PATH 里。建议使用 `systemctl enable syncthing@your_user.service` 启动，保证文件权限一致。
2. **Mac**：去官网下载 GUI 版，装好之后打开。
3. **互相添加**：两边各拿自己的 Device ID，互相添加到对方的设备列表里。
4. **创建共享文件夹**：在两边各创建一个文件夹，Folder ID 填一样的，本地路径各自填自己的。
5. **开启版本控制**：在文件夹设置里选「Staggered File Versioning」，最大保留天数设为 90 或 180 天。记得在两端都开启一次，实现双重保险。
6. **开始同步**：等它们自动握手连接，GUI 显示「Up to Date」就是成功了。

SyncThing 官网有详细的图文文档，细节可以看 [docs.syncthing.net](https://docs.syncthing.net)。

如果你已经有 OpenClaw 运行在服务器上了，完全可以让它帮你配置。

---

工具选型这件事，从来都没有银弹。

Fast Note Sync 很轻量，如果是设备之间都能安装插件，它做得很好。但我的场景变了。我需要真正的双向同步，需要「改了就是改了」，不需要我去记、去触发。

SyncThing 是我权衡之后的答案。它多了安装配置的步骤，多了跑后台进程的开销，但换来了我真正想要的东西：**一个在哪改都自动一致的笔记系统。**

鞋里的这颗小石子，终于倒出来了，爽呀！

![随处一致的笔记系统](/images/posts/%E4%BB%8E%20Fast%20Note%20Sync%20%E5%88%87%E5%88%B0%20SyncThing%EF%BC%9A%E6%88%91%E7%9A%84%20Obsidian%20%E5%90%8C%E6%AD%A5%E7%BB%88%E4%BA%8E%E4%B8%8D%E7%94%A8%E9%9D%A0%20OpenClaw%20%E8%87%AA%E7%94%B1%E5%8F%91%E6%8C%A5%E4%BA%86/Project_SyncThing_Obsidian_illustration-04_fd7589a6_20260408.webp)
