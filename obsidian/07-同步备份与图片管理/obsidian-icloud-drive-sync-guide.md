---
title: Obsidian 入门61：苹果用户的零配置方案，iCloud 同步
date: 2026-06-10
slug: obsidian-icloud-drive-sync-guide
excerpt: 苹果全家桶用户的免费同步方案。8 步配好，含最容易被忽略的那个坑。
cover: ""
tags:
  - Obsidian
  - 苹果生态
  - 笔记同步
  - Obsidian入门
status: published
---
> 这是一个「Obsidian x AI」入门系列。
>
> 入门57 的 8 条路里有一条「纯苹果用户的零配置方案」。当时只提了一嘴，这篇把具体步骤拆开。

入门57 发出来后，有苹果用户问，你说的 iCloud Drive 零配置，具体怎么操作？

这篇文章就是回答。

前提是你有 Mac 和 iPhone（或 iPad），登录同一个 Apple ID。满足这两个条件，剩下就是按步骤走一遍。

有一点要先说清楚，这些步骤来自其他用户的实践（参考了 Jay 的教程），我自己没有 iPhone，没法逐条验证。但步骤本身不复杂，跟着做应该不会出问题。

下面是完整流程。

---

## 前置条件

- ✅ 一台 Mac 和一部 iPhone / iPad
- ✅ 登录同一个 Apple ID
- ✅ iCloud 有足够空间（免费 5GB，纯笔记够用。图片多的话可能需要扩容）

---

## Step 1：iPhone 开启 iCloud 同步

设置 → 你的 Apple ID → iCloud → 打开 iCloud Drive。

然后往下翻，在「使用 iCloud 的应用」列表里找到 Obsidian，确保它是打开状态。

这一步的目的是让 iPhone 上的 Obsidian 有权限读写 iCloud Drive。

![iPhone 开启 iCloud 同步](/images/posts/Obsidian%20%E5%85%A5%E9%97%A861%EF%BC%9A%E8%8B%B9%E6%9E%9C%E7%94%A8%E6%88%B7%E7%9A%84%E9%9B%B6%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%8CiCloud%20%E5%90%8C%E6%AD%A5/iphone-icloud-sync.webp)

---

## Step 2：iPhone 创建新 Vault

打开手机 Obsidian，创建一个新的 Vault。

名称必须和你的 Mac 上的 Vault 名称一致。如果你 Mac 上的叫「MyNotes」，这里也要叫「MyNotes」。

![Obsidian 入门61：苹果用户的零配置方案，iCloud 同步 - 配图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A861%EF%BC%9A%E8%8B%B9%E6%9E%9C%E7%94%A8%E6%88%B7%E7%9A%84%E9%9B%B6%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%8CiCloud%20%E5%90%8C%E6%AD%A5/20260610232515396.webp)


**这一步是关键。** 必须在手机上先建一次，iPhone 才会在 iCloud Drive 里生成对应的文件夹结构。很多人第一次没搞通，就是跳过了这一步。

![iPhone 创建新 Vault](/images/posts/Obsidian%20%E5%85%A5%E9%97%A861%EF%BC%9A%E8%8B%B9%E6%9E%9C%E7%94%A8%E6%88%B7%E7%9A%84%E9%9B%B6%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%8CiCloud%20%E5%90%8C%E6%AD%A5/iphone-create-vault.webp)

创建完之后，去 iCloud Drive 检查一下，应该能看到 Obsidian 文件夹里已经有了你的 Vault 目录。

---

## Step 3：iPhone 设置「保持下载」

这一步的目的是防止 iCloud 为了节省空间把文件从本地移除。

设置 → Apple ID → iCloud → iCloud Drive → Obsidian，打开「保持下载」。

![iPhone 保持下载](/images/posts/Obsidian%20%E5%85%A5%E9%97%A861%EF%BC%9A%E8%8B%B9%E6%9E%9C%E7%94%A8%E6%88%B7%E7%9A%84%E9%9B%B6%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%8CiCloud%20%E5%90%8C%E6%AD%A5/iphone-keep-download.webp)

---

## Step 4：Mac 开启 iCloud 同步

系统设置 → Apple ID → iCloud → iCloud Drive → 开启。

点击 iCloud Drive 旁边的选项按钮，确保 Obsidian 在已启用的应用列表里。

![Mac 开启 iCloud 同步](/images/posts/Obsidian%20%E5%85%A5%E9%97%A861%EF%BC%9A%E8%8B%B9%E6%9E%9C%E7%94%A8%E6%88%B7%E7%9A%84%E9%9B%B6%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%8CiCloud%20%E5%90%8C%E6%AD%A5/mac-icloud-sync.webp)

---

## Step 5：Mac 设置「保持下载」

和 iPhone 一样，在 Mac 上也要打开「保持下载」。

系统设置 → Apple ID → iCloud → iCloud Drive → Obsidian → 打开「保留下载的文件」。

![Mac 保持下载](/images/posts/Obsidian%20%E5%85%A5%E9%97%A861%EF%BC%9A%E8%8B%B9%E6%9E%9C%E7%94%A8%E6%88%B7%E7%9A%84%E9%9B%B6%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%8CiCloud%20%E5%90%8C%E6%AD%A5/mac-keep-download.webp)

---

## Step 6：复制 Vault 到 iCloud Drive

找到 Mac 上现有的 Vault 文件夹。

**复制它**（不是移动，保留一份备份以防万一），粘贴到 Finder 里 iCloud Drive 的 Obsidian 文件夹中。

![复制 Vault 到 iCloud Drive](/images/posts/Obsidian%20%E5%85%A5%E9%97%A861%EF%BC%9A%E8%8B%B9%E6%9E%9C%E7%94%A8%E6%88%B7%E7%9A%84%E9%9B%B6%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%8CiCloud%20%E5%90%8C%E6%AD%A5/mac-copy-vault.webp)

如果提示有同名文件夹，选「合并」或「覆盖」。

![Obsidian 入门61：苹果用户的零配置方案，iCloud 同步 - 配图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A861%EF%BC%9A%E8%8B%B9%E6%9E%9C%E7%94%A8%E6%88%B7%E7%9A%84%E9%9B%B6%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%8CiCloud%20%E5%90%8C%E6%AD%A5/20260610232552008.webp)


---

## Step 7：验证 Mac

先断开 Mac 上原有的 Vault。

在 Obsidian 界面左下角，点开当前 Vault 名称，选「打开其他 Vault」。然后选择 iCloud Drive 里那个刚复制过去的 Vault，打开。

检查一下。
- 笔记是否全部正常显示
- 插件和主题是否还在

如果发现设置被重置了（插件丢了、主题变了），别慌。这是因为 iCloud 的 Vault 是新创建的，`.obsidian` 设置文件夹是空的。

解决：回到你备份的原始 Vault 文件夹，找到 `.obsidian` 这个隐藏文件夹（按 `Shift + Cmd + .` 可以显示隐藏文件），复制它，粘贴到 iCloud Drive 里的 Vault 中覆盖掉现有的 `.obsidian`。

重新打开 Obsidian，设置应该就恢复了。

---

## Step 8：验证 iPhone

打开手机上的 Obsidian，应该能看到刚才从 Mac 同步过来的 Vault 和笔记。

写一条测试笔记，然后回到 Mac 确认是否能收到。如果双向都正常，说明同步跑通了。

如果手机上看不到新内容，检查一下 iCloud 同步是否处于开启状态，或者等一会儿再刷新，iCloud 的同步不是实时的，偶尔会有几分钟延迟。

---

## 这套方案的优缺点

**优点**：
- 免费（5GB 内）
- 不需要装任何插件
- 苹果原生，不需要额外配置

**缺点**：
- 只适合苹果全家桶用户
- iCloud 在国内的速度看网络心情，偶尔会慢
- 同步不是实时的，有轻微延迟
- Windows 体验很差，不推荐混搭

如果你用的不是纯苹果设备，或者 iCloud 速度不太理想，可以回头看入门58 的 Remotely Save + COS 方案，那条路更稳。

---

## 进阶阅读

- [Obsidian 入门57：找到适合自己的多端同步方案](/blog/Obsidian%20%E5%85%A5%E9%97%A857%EF%BC%9A%E6%89%BE%E5%88%B0%E9%80%82%E5%90%88%E8%87%AA%E5%B7%B1%E7%9A%84%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5%E6%96%B9%E6%A1%88) —— 总篇，8 条路全景图
- [Obsidian 入门58：用 Remotely Save + 腾讯云 COS 实现多端同步](/blog/Obsidian%20%E5%85%A5%E9%97%A858%EF%BC%9A%E7%94%A8%20Remotely%20Save%20%2B%20%E8%85%BE%E8%AE%AF%E4%BA%91%20COS%20%E5%AE%9E%E7%8E%B0%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5) —— 云服务路线，国内更稳定
- [Obsidian 入门60：用 SyncThing 把多台设备织成一张网](/blog/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91) —— P2P 方案，不用服务器
