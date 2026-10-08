---
title: 不写一行代码，让服务器上的 OpenClaw 自动往我的 Obsidian 里塞笔记
date: 2026-02-17
slug: ai-obsidian-real-time-sync
excerpt: 免费开源方案，让服务器的 OpenClaw 产出的内容实时出现在本地 Obsidian 里。
cover: ""
tags:
  - Obsidian
  - 自动化
  - OpenClaw
  - 笔记同步
  - 效率工具
status: published
---

上次用 rclone 把服务器「挂载」到了本地（[我不懂命令行，但我把 OpenClaw 服务器挂载到了本地](/blog/%E6%88%91%E4%B8%8D%E6%87%82%E5%91%BD%E4%BB%A4%E8%A1%8C%EF%BC%8C%E4%BD%86%E6%88%91%E6%8A%8A%20OpenClaw%20%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%8C%82%E8%BD%BD%E5%88%B0%E4%BA%86%E6%9C%AC%E5%9C%B0)），用了一段时间发现一个问题：我让 OpenClaw 在服务器上整理好一篇素材，打开本地 Obsidian 准备看：空的。等了两三分钟才慢悠悠冒出来。

rclone 的缓存机制决定了它做不到实时。我需要的是：**服务器上 AI 写完东西，本地 Obsidian 秒到。免费，双向，不卡。**

后来找到了 Fast Note Sync，一个开源的 Obsidian 实时同步服务，刚好解决这个问题。

---

## 你只需要准备 4 样东西

在往下读之前，先确认你手上有这些：

1. 你的 OpenClaw 云服务器的 **IP 地址**
2. **SSH 端口**（通常是 22）
3. **登录用**的用户名
4. **SSH 私钥路径**（或者密码）

有了这四样，剩下的全交给 AI。

不懂这些是什么也没关系。如果你之前跟着我的 OpenClaw 系列操作过，这些信息你都有。

---

## Fast Note Sync 是什么

简单说，它做了一件事：让服务器和本地 Obsidian 之间保持一根「热线电话」。

![Fast Note Sync 同步架构示意](/images/posts/%E4%B8%8D%E5%86%99%E4%B8%80%E8%A1%8C%E4%BB%A3%E7%A0%81%EF%BC%8C%E8%AE%A9%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84%20OpenClaw%20%E8%87%AA%E5%8A%A8%E5%BE%80%E6%88%91%E7%9A%84%20Obsidian%20%E9%87%8C%E5%A1%9E%E7%AC%94%E8%AE%B0/20260217223828669.webp)

技术上，它在服务器跑一个同步服务，本地 Obsidian 装一个插件，两边通过 WebSocket 保持长连接。任何一端有改动，另一端立刻同步。

但真正让我心动的是另一个特性：**它提供 REST API，AI 可以直接调用它往 Obsidian 里写笔记。**

我可以将任何我要记录的信息、素材提供给 OpenClaw，不用我动手，它帮我处理后，内容就自动出现在本地 Obsidian 里。

---

## 我让 AI 帮我配的全过程

说实话，我自己也不想去研究那些配置参数。所以我直接把需求丢给了 Claude Code。

### 服务器端：复制这段话给你的 AI

你不需要懂任何技术细节。把下面这整段话复制给你的 OpenClaw（或 Claude Code、Gemini CLI 等任何能连服务器的 AI 助手），把里面的占位符换成你自己的信息，它就会帮你全部配好：

```
请帮我在服务器上部署 Fast Note Sync 服务。这是一个 Obsidian 实时同步工具。

 **部署要求：**
 1. 从 GitHub 下载最新版本：https://github.com/haierkeys/fast-note-sync-service/releases
 2. 创建配置文件 `config/config.yaml`，内容如下：

 server:
   port: 9000
   websocket-port: 9001
 storage:
   path: ./storage
 user:
   register-is-enable: true
 log:
   level: info

 3. 创建 systemd 服务，实现开机自启
 4. 启动服务并确认运行正常

 **我的服务器信息：**
 - IP：`（换成你的服务器 IP）`
 - SSH 端口：`（换成你的端口，通常是 22）`
 - 用户名：`（换成你的用户名）`
 - SSH 私钥路径：`（换成你的私钥路径）`
```

AI 大概两三分钟就能搞完。

唯一需要你自己动手的是：去云服务商的控制台，在安全组里把 **9000** 和 **9001** 两个端口打开。这一步 AI 帮不了你，因为它没有你的云服务商账号权限。

如果你用的是腾讯云，路径是：控制台 → 安全组 → 添加规则 → 端口填 9000 和 9001。

### 本地 Obsidian 插件

这一步有个小坑要提前说：Fast Note Sync 目前**还没上架** Obsidian 官方社区插件商店，所以你在插件市场里搜不到它。

安装方式有两种：

**方式一（推荐）**：用 BRAT 插件安装。如果你之前装过 BRAT（Beta Reviewer's Auto-update Tester），直接在 BRAT 里添加仓库地址 `haierkeys/obsidian-fast-note-sync` 就行。

**方式二**：手动安装。去 GitHub Releases 页面下载最新版本，解压后放到你的 `.obsidian/plugins/` 目录里。

装好之后，在插件设置里填入：

- 服务地址：`http://你的服务器IP:9000`
- WebSocket 端口：`9001`

第一次连接时，需要先在浏览器里打开 `http://你的服务器IP:9000`，注册一个账号。然后用这个账号登录 Obsidian 插件。

连上之后，试着在本地新建一个笔记。如果服务器那边也出现了，说明同步已经跑起来了。

> [!tips]
> 注册完账号后，记得回去把配置文件里的 `register-is-enable` 改成 `false`，防止别人也来注册。这一步可以让 AI 帮你改。

### 让 AI 直接往 Obsidian 里写东西

同步跑通之后，接下来才是真正好玩的部分。

Fast Note Sync 提供了 REST API——你的 AI 助手可以通过一个「接口」，直接把内容写进你的 Obsidian。

先在网页端（`http://你的服务器IP:9000`）登录，拿到你的 Token（一串验证身份的字符串）。

然后，跟服务器部署一样，把下面这段话复制给你的 AI：

```
请帮我在服务器上创建一个 Fast Note Sync 的 API 客户端脚本，用于往 Obsidian 写入笔记。

 **要求：**
 1. 安装依赖：`pip install requests`
 2. 创建脚本文件 `fast_note_sync_client.py`，功能是调用 Fast Note Sync 的 REST API 创建/更新笔记
 3. 脚本需要包含一个 `create_note(path, content)` 函数，参数是笔记路径和内容
 4. 再写一个 `create_inbox_note(title, content, tags)` 便捷函数，自动加日期前缀和 frontmatter，存到 Inbox 目录

 **我的配置信息：**
 - API 地址：`http://（你的服务器 IP）:9000`
 - Token：`（换成你在网页端拿到的 Token）`
 - Vault 名称：`（换成你在插件里创建的仓库名）`

 **完成后，帮我跑一个测试：创建一篇标题为「测试笔记」的笔记，确认本地 Obsidian 能收到。**
```

AI 会帮你写好脚本、装好依赖、跑完测试。你在本地 Obsidian 看到「测试笔记」出现，就说明整条通路打通了。

---

## 我现在怎么用这套系统

配好之后，我的日常工作流变成了这样：

在手机上看到一篇好文章，转发给 OpenClaw。它帮我提取要点、整理格式，然后通过 API 直接写入 Obsidian。

我打开电脑，笔记已经躺在那了。按照我的文件夹结构，分门别类放好。

素材收集、自动归档、本地查看。整个过程没有一步需要我手动操作。

说实话，配完那天晚上我试了好几次，就为了看那个「笔记突然冒出来」的效果。有点像小时候往信箱里塞信，然后跑到另一头去看它掉出来。

---

## 和其他方案比一下

| 方案               | 实时性   | 双向同步 | 成本         | 适合谁               |
| ------------------ | -------- | -------- | ------------ | -------------------- |
| rclone 挂载        | 有延迟   | 单向为主 | 免费         | 偶尔改改远程文件     |
| iCloud / Dropbox   | 实时     | 双向     | 付费或有限制 | 个人多设备同步       |
| Obsidian Sync      | 实时     | 双向     | $4/月        | 不想折腾的用户       |
| **Fast Note Sync** | **实时** | **双向** | **免费**     | **服务器 + AI 集成** |

怎么选？看你的场景。手机和电脑之间同步笔记，Obsidian Sync 或者 iCloud 就够了，没必要折腾。但如果你像我一样，服务器上跑着 AI，需要它产出的内容自动进入 Obsidian。那 Fast Note Sync 是我目前找到的最合适的方案。

---

## 配完之后别忘了这几件事

1. **关闭注册**：前面提过了，注册完把 `register-is-enable` 改成 `false`。你的同步服务暴露在公网上，不关注册等于给陌生人开了门。

2. **加 HTTPS**：如果你在意传输安全，可以用 Nginx 反向代理加上 Let's Encrypt 证书。这个也可以让 AI 帮你配，一句话的事。

3. **备份**：Fast Note Sync 的数据存在服务器的 `storage` 目录里。定期备份这个目录就行，跟备份其他文件没区别。

---

## 说几句实话

Fast Note Sync 目前还是 Beta 状态，不是一个「成熟到闭着眼用」的产品。我用了这段时间没碰到什么问题，但不代表它不会出问题。

好在它是开源的，数据存在你自己的服务器上，最坏的情况也就是同步断了，笔记本身不会丢。

从 rclone 挂载到 Fast Note Sync，我的 OpenClaw 工作流算是补上了最后一块拼图。服务器上的 AI 产出的东西，终于能实时出现在我的 Obsidian 里了。

不用手动复制，不用等缓存，不用花钱。

现在每次打开 Obsidian，笔记已经在那了。
