---
title: Obsidian 入门60：用 SyncThing 把多台设备织成一张网
date: 2026-06-10
slug: obsidian-syncthing-setup-guide
excerpt: 不需要服务器，不需要插件。两台电脑装上 SyncThing，自动同步你的 Obsidian。
cover: ""
tags:
  - Obsidian
  - 笔记同步
  - Obsidian入门
status: published
---
> 这是一个「Obsidian 入门」系列。
>
> 入门59 讲的是 Fast Note Sync，需要一台服务器当中心节点。这篇讲另一条路，不需要服务器，不需要插件，装上就能用。

入门59 发出来后，有朋友问，我没有服务器，也不想折腾运维，有没有别的办法？

有，SyncThing。

![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/CleanShot%25202026-06-02%2520at%252000.16.28.webp)

其实我现在的 Mac 和服务器之间跑的就是 SyncThing。4 月从 FNS 切过来之后一直用到现在，没出过问题([从 Fast Note Sync 切到 SyncThing：我的 Obsidian 同步终于不用靠 OpenClaw 自由发挥了](/blog/%E4%BB%8E%20Fast%20Note%20Sync%20%E5%88%87%E5%88%B0%20SyncThing%EF%BC%9A%E6%88%91%E7%9A%84%20Obsidian%20%E5%90%8C%E6%AD%A5%E7%BB%88%E4%BA%8E%E4%B8%8D%E7%94%A8%E9%9D%A0%20OpenClaw%20%E8%87%AA%E7%94%B1%E5%8F%91%E6%8C%A5%E4%BA%86))。

它的工作方式跟 FNS 完全相反。FNS 是中心节点模式，你所有的设备都连到一台服务器上。SyncThing 是 P2P 模式，设备之间直连，不需要任何中心服务器。

![fnsvsyncthing](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/20260610095158223.webp)


所以你的门槛很低。不需要买云服务器，不需要装服务端。

两台设备装上 SyncThing，配一下，它们就能自己同步了。

而且它是在操作系统层面监控文件变化，不依赖任何 Obsidian 插件。你在任何一端改了文件，另一端自动收到，不需要手动点同步。

下面直接说怎么装。

---

## Step 1：下载安装

去 SyncThing 官网下载对应系统的版本。

- **Mac**：下载 dmg，拖进 Applications 文件夹，打开就能用
- **Windows**：下载 exe 安装包，下一步下一步
- **Linux**：把 Syncthing 的官网发给 AI，让你的 OpenClaw 或者 Hermes-agent 给你在服务器装好
- **NAS**：群晖的套件中心直接有 SynoCommunity 版本

安装完打开，你会看到一个 Web 界面，默认地址是 `http://127.0.0.1:8384`。这就是 SyncThing 的管理后台，所有操作都在这里完成。

以我的 Mac 为例，安装好之后，在顶部状态栏会显示 Syncthing 的图标。点开之后，能看到基本的一些信息。
![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/CleanShot%25202026-06-10%2520at%252008.21.29.webp)


点击 Open 之后，就能打开 web 界面或者你也可以直接在浏览器输入`http://127.0.0.1:8384`。

![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 配图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/20260610082806980.webp)

---

## Step 2：设备配对

SyncThing 的设备配对方式比较特别。每台设备有一个唯一的 **Device ID**，是一串很长的字符串。你要做的事很简单，把两台设备的 ID 互相告诉对方。

具体操作。

1. 在 Mac 的 SyncThing 管理界面，点右上角「添加远程设备」
2. 输入服务器的设备 ID。如果你的服务器已经安装了 OpenClaw 或者 Hermes-agent，让它帮你装好 Syncthing，并告诉你设备 ID
3. 你在 Mac web 上添加好了服务器的设备 ID 之后。在服务器会有一个一个配对请求，让你的 AI 接受
4. 反过来也做一遍：把你的Mac 设备ID 在服务器添加上去。在右上角，操作的选项菜单中有一个显示 ID 的选项，点击即可看到。

配对完成后，两台设备会出现在彼此的设备列表里，状态显示「已连接」。

![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/CleanShot%25202026-06-10%2520at%252008.30.52.webp)


---

## Step 3：共享文件夹

设备配对好了，接下来告诉 SyncThing 要同步哪些文件夹。

1. 在 Mac 的 SyncThing 上点「添加文件夹」
![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 截图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/CleanShot%25202026-06-10%2520at%252008.46.25.webp)

2. 文件夹路径选你的 Obsidian Vault 目录
3. 给它起个标签，比如「Obsidian Vault」
4. 在共享设备里勾选你的服务器
![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 截图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/CleanShot%25202026-06-10%2520at%252008.44.42.webp)

5. 点保存

这时服务器的 SyncThing 上会询问你是否接受这个共享文件夹。点接受，同步就自动开始了。

>如果还是有问题，那么把你的 Mac 设备 ID 和文件夹 ID 一起提供给服务器上的 AI，让它帮你做好配置。

第一次同步会把整个 Vault 传到对端。文件数量和网络速度不同，耗时不一样。之后每次改动只会同步变化的部分，几秒就完成。

---

## Step 4：配置 .stignore

Obsidian 的 Vault 里不只有你的笔记。还有一个 `.obsidian` 文件夹，里面是插件、主题、缓存之类的配置。这些文件不应该同步到服务器，因为服务器上没有 Obsidian软件，也不需要这些配置。

SyncThing 在编辑文件夹的弹窗上提供了一个叫忽略模式的机制。在里面添加上。

```
.obsidian/
.DS_Store
*.tmp
```

或者任何你不想要同步的文件夹、文件等。

![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 截图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/CleanShot%25202026-06-10%2520at%252008.48.54.webp)

这样 `.obsidian`、`.DS_Store` 和临时文件就不会被同步过去了。同步过来的就是干净的笔记文件。

如果你之后改了 `.stignore`，SyncThing 会自动重新评估规则，不需要重启。

---

## Step 5：版本控制（可选但推荐）

SyncThing 自带版本控制功能。我最推荐的是 **Staggered File Versioning**，中文叫阶段版本控制。

它的工作方式很像 macOS 的 Time Machine：

- 最近 1 小时内，每 30 秒保留一个版本
- 最近 1 天内，每小时保留一个
- 超过 30 天的，每周保留一个

这些历史版本会存在一个隐藏的 `.stversions` 文件夹里。万一同步出错把文件覆盖了，去那里翻一下就能找回旧版本。

开启方式很简单，在文件夹设置里找到「文件版本控制」，选“阶段版本控制”，其他保持默认。

![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 截图 9](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/CleanShot%25202026-06-10%2520at%252008.51.53.webp)


---

## 看看同步状态

SyncThing 的管理界面很直观。打开就能看到

- 所有已配对的设备，在线还是离线
- 每个文件夹的同步进度
- 如果有文件冲突或同步失败，会显示具体原因

![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 截图 10](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/CleanShot%25202026-06-10%2520at%252008.53.19.webp)


如果某台设备离线了，它会持续重试。等设备上线后自动补上错过的同步，不需要手动干预。

---

## FNS（Fast Note Sync) vs SyncThing，怎么选

两篇文章都写完了，放在一起对比更清楚。

| 对比项 | FNS（入门59） | SyncThing（这篇） |
|---|---|---|
| 需不需要服务器 | 需要 7×24 在线 | 不需要，P2P 直连 |
| 需不需要插件 | Obsidian 插件 | 不需要，系统级同步 |
| 安装门槛 | 装服务端 + 配客户端 | 装 App + 配设备 |
| 数据流向 | 经过你的服务器 | 设备直连 |
| 版本控制 | 无 | 内置交错版本控制 |

**选 FNS 如果**：你有服务器，想要手机端也能实时同步，不介意装服务端。

**选 SyncThing 如果**：你没有服务器，或者只想在电脑之间同步，不想装任何 Obsidian 插件。

---

SyncThing 和 FNS 其实不冲突。我现在就是两者都用：

- **Mac ↔ 服务器**：SyncThing（文件系统级双向同步，自动）
- **Mac ↔ 手机**：FNS（Obsidian 插件，推送到手机。手机改了后，也能同步回 Mac）。其实我打算后面也换成 Syncthing，只是现在懒癌发作不想折腾_-

SyncThing 负责把服务器和 Mac 拉齐，FNS 负责把 Mac 的变化推给手机。各司其职，互补得很好。

![Obsidian 入门60：用 SyncThing 把多台设备织成一张网 - 配图 11](/images/posts/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91/20260610100021399.webp)


从入门57 的总篇开始，到 入门58 的云服务、入门59 的自建中心节点，再到 入门60 的 P2P 直连，三条路都拆完了。

你按自己的条件选一条，走下去就行。

---

## 进阶阅读

- [Obsidian 入门59：用 Fast Note Sync 自建一套多端同步](/blog/Obsidian%20%E5%85%A5%E9%97%A859%EF%BC%9A%E7%94%A8%20Fast%20Note%20Sync%20%E8%87%AA%E5%BB%BA%E4%B8%80%E5%A5%97%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5) —— 前一篇，需要服务器的方案
- [Obsidian 入门58：用 Remotely Save + 腾讯云 COS 实现多端同步](/blog/Obsidian%20%E5%85%A5%E9%97%A858%EF%BC%9A%E7%94%A8%20Remotely%20Save%20%2B%20%E8%85%BE%E8%AE%AF%E4%BA%91%20COS%20%E5%AE%9E%E7%8E%B0%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5) —— 云服务路线
- [Obsidian 入门57：找到适合自己的多端同步方案](/blog/Obsidian%20%E5%85%A5%E9%97%A857%EF%BC%9A%E6%89%BE%E5%88%B0%E9%80%82%E5%90%88%E8%87%AA%E5%B7%B1%E7%9A%84%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5%E6%96%B9%E6%A1%88) —— 总篇，8 条路全景图
- [从 Fast Note Sync 切到 SyncThing：我的 Obsidian 同步终于不用靠 OpenClaw 自由发挥了](/blog/%E4%BB%8E%20Fast%20Note%20Sync%20%E5%88%87%E5%88%B0%20SyncThing%EF%BC%9A%E6%88%91%E7%9A%84%20Obsidian%20%E5%90%8C%E6%AD%A5%E7%BB%88%E4%BA%8E%E4%B8%8D%E7%94%A8%E9%9D%A0%20OpenClaw%20%E8%87%AA%E7%94%B1%E5%8F%91%E6%8C%A5%E4%BA%86) —— 4 月写的迁移故事
