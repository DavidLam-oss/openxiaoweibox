---
title: Obsidian 入门58：用 Remotely Save + 腾讯云 COS 实现多端同步
date: 2026-06-02
slug: obsidian-remotely-save-cos-sync
excerpt: 同一个 COS 存储桶，管图床也管同步。10 分钟配好，多端用同一个 Obsidian。
cover: ""
tags:
  - Obsidian
  - 笔记同步
  - 排版与导出
  - Obsidian入门
status: published
---
> 这是一个「Obsidian x AI」系列。
>
> 入门57 给了 8 条路的全景图。这篇拆开其中一条来走：Remotely Save + 腾讯云 COS。
>
> 选这条路先讲，原因很简单，如果你之前跟着入门46 搭过图床，那你的腾讯云 COS 存储桶已经在了，直接复用就行。

[入门 57](/blog/Obsidian%20%E5%85%A5%E9%97%A857%EF%BC%9A%E6%89%BE%E5%88%B0%E9%80%82%E5%90%88%E8%87%AA%E5%B7%B1%E7%9A%84%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5%E6%96%B9%E6%A1%88) 发出来后，有朋友问：8 条路里性价比最高的是哪条？

我的答案是 Remotely Save + 腾讯云 COS。原因有三个。

第一，便宜。个人笔记同步的用量很少，基本花不了几个钱。我之前预充了 10 块，用了一年多还剩 2 块。

第二，国内访问快。服务器就在国内，不像 Obsidian Sync 或 iCloud 偶尔还要看网络心情。

第三，如果你之前跟着入门46 搭过图床，那你腾讯云的账号已经注册好了，密钥已经有了，存储桶已经建好了，这些东西可以直接复用，不用再折腾一遍。

![Obsidian 入门58：用 Remotely Save + 腾讯云 COS 实现多端同步 - 配图 1](/images/posts/20260602235535322.webp)

所以这篇教程你可能只需要花 10 分钟：5 分钟装插件配好，5 分钟等第一次同步完成。

阿里云 OSS 的用户也不用急，步骤完全一样，只是控制台不同。我会在最后单独说一下。

---

## Step 1：安装 Remotely Save

打开 Obsidian，进入设置 → 第三方插件 → 社区插件市场，搜索 **Remotely Save**。

![在社区插件市场搜索 Remotely Save](/images/posts/202503301645080.webp)

点进插件卡片，点击安装，然后启用。

![点击安装 Remotely Save](/images/posts/202503301648382.webp)

启用之后，左侧工具栏会出现一个 Remotely Save 的图标，后面如果想要手动触发同步，可以点击这个图标。

现在，点进去插件设置页面，能看到对应的配置选项。不过现在基本都是空的，我们先去腾讯云那边准备好信息再回来填。

## Step 2：腾讯云 COS 创建存储桶

如果你已经跟着入门46 搭过图床，这一步可以跳过，直接用已有的存储桶就行。

还没弄过的朋友，跟着走一遍。

打开腾讯云官网，注册并完成实名认证。然后在控制台找到「对象存储」，创建一个存储桶。

创建时注意几个设置。

- **存储桶名称**：随便起，但不能重名
- **所属地域**：选离你最近的，比如广州、上海、北京
- **访问权限**：选 **私有读写**。这一点跟入门46 的图床不同。图床需要公有读私有写，同步必须私有，因为你的笔记文件不应该被公开访问

![新建存储桶界面](/images/posts/202503301706712.webp)

创建页面底部可能会有一些默认勾选的额外付费服务，记得取消掉。

![取消默认勾选的额外付费服务](/images/posts/202503301659642.webp)


创建完成后，记下两个信息。

1. **存储桶名称** ：在存储桶列表里能看到
2. **所属区域** ：格式类似 `ap-guangzhou`、`ap-beijing`

这两个信息等下配置 Remotely Save 时要填。

## Step 3：获取 API 密钥

去腾讯云的「密钥管理」页面（控制台 → 访问管理 → 密钥管理），新建一个密钥。

系统会生成一对 **SecretID** 和 **SecretKey**。把它们复制下来，安全和密钥一样重要，不要泄露给别人。

## Step 4：配置 Remotely Save

现在回到 Obsidian 的 Remotely Save 设置页面。

把 **同步方式** 切换到 **S3 或兼容 S3 的对象存储**。然后填入以下信息。

| 配置项 | 从哪里拿 | 示例 |
|--------|----------|------|
| **Endpoint** | 存储桶的所属地域，格式为 `cos.{region}.myqcloud.com` | `cos.ap-guangzhou.myqcloud.com` |
| **Region** | 存储桶的所属区域 | `ap-guangzhou` |
| **AccessKeyID** | 上一步拿到的 SecretID | `AKIDxxxxxxxx` |
| **SecretAccessKey** | 上一步拿到的 SecretKey | `xxxxxxxx` |
| **BucketName** | 存储桶名称 | `obsidian-12345678` |

填完之后，拉到页面下方，点 **检查** 按钮。如果看到绿色的「连接成功」提示，说明配置没问题。

![Remotely Save 配置页面](/images/posts/202503301705766.webp)

如果检查失败，最可能的原因是。

- Endpoint 格式写错了。注意是 `cos.{region}.myqcloud.com`，不是存储桶的访问域名
- SecretID 或 SecretKey 复制多了空格
- 存储桶名称写错了

## Step 5：首次同步

配置成功后，按 `Cmd + P`（Windows 用 `Ctrl + P`），输入 `remote`，选择 **Remotely Save：开始同步**。

第一次同步会把你的整个 Vault 上传到 COS。文件数量不同，耗时不一样。我自己的库那个时候有 1000 多个文件，第一次同步大概 5 分钟。

![选择同步命令](/images/posts/202503301723707.webp)

同步完成后，打开腾讯云 COS 的存储桶页面，你应该能看到你的笔记文件已经在里面了。

## Step 6：手机端也配上

iPhone 或 Android 上的操作一样。

安装 Obsidian 和 Remotely Save 插件，填入同样的 COS 信息。然后点同步，所有文件就会从云端拉到手机上了。

之后你在电脑上改了笔记，点一下同步，手机上就能看到最新版本。反过来也一样。

![Obsidian 入门58：用 Remotely Save + 腾讯云 COS 实现多端同步 - 配图 8](/images/posts/20260602235610361.webp)


## 不想用腾讯云？阿里云 OSS 也可以

整体步骤完全一样，只是控制台不同。

1. 在阿里云控制台开通对象存储 OSS，创建 Bucket
2. 在 RAM 访问控制里创建 AccessKey
3. Endpoint 格式是 `oss-{region}.aliyuncs.com`，比如 `oss-cn-hangzhou.aliyuncs.com`
4. Region 填对应的区域代码，比如 `cn-hangzhou`

其他配置项一一对应，填到 Remotely Save 里就行。检查连接通过后，就可以开始同步了。

## 费用

腾讯云 COS 新用户通常有免费额度，但过了优惠期是按量计费。好在纯笔记同步的文件都是文本，体量很小。

我自己的使用情况供参考：入门46 搭了图床、这篇配了同步，同一个存储桶跑了一年多，加上 CDN 流量，总共花了不到 10 块钱。

建议注册时预充 10 块，打开账单告警。头几个月留意一下用量，心里有数就好。

---

Remotely Save + COS 配好之后，Obsidian 的多端同步就解决了。

入门46 的时候，腾讯云 COS 存储桶帮你管图片。现在，同一个 COS 存储桶帮你同步笔记。一个桶干两件事，不用额外开任何服务。

之前在 Mac 上写了一半的笔记，打开手机，同步一下，接着写。那种感觉谈不上惊喜，就是松了一口气。

![Obsidian 入门58：用 Remotely Save + 腾讯云 COS 实现多端同步 - 配图 9](/images/posts/20260602235648499.webp)


下篇会拆另一条路，看你想先走哪个。

## 进阶阅读

- [Obsidian 入门57：找到适合自己的多端同步方案](/blog/Obsidian%20%E5%85%A5%E9%97%A857%EF%BC%9A%E6%89%BE%E5%88%B0%E9%80%82%E5%90%88%E8%87%AA%E5%B7%B1%E7%9A%84%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5%E6%96%B9%E6%A1%88)，全景图，8 条路对号入座
- [Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了](/blog/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86)，同一个 COS 存储桶，图床就是这么搭的
- [搭配腾讯云 COS 让 Obsidian 实现跨设备多端同步](/blog/%E6%90%AD%E9%85%8D%E8%85%BE%E8%AE%AF%E4%BA%91%20COS%20%E8%AE%A9%20Obsidian%20%E5%AE%9E%E7%8E%B0%E8%B7%A8%E8%AE%BE%E5%A4%87%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5)，去年写的旧版教程，步骤框架一样，界面可能有变化
