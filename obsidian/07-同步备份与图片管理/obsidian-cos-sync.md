---
title: 搭配腾讯云 COS 让 Obsidian 实现跨设备多端同步
date: "2025-03-30"
excerpt: >-
  详细介绍如何搭配腾讯云 COS 和 Remotely Save 插件，实现 Obsidian 笔记在 Mac、iPad、Android 和 iOS
  多端之间的低成本、高效率同步。
tags:
  - Obsidian
  - 服务器运维
  - 效率工具
---

你在使用 Obsidian 的时候，是否也面临过这样的问题：

- 在 Mac、iPad、Android和 iOS 设备间切换，总是没办法做到如臂使指？

归根结底，是下载了 Obsidian 之后，却没有好的同步工具！

今天我来手把手教你如何搭配腾讯云 COS 从而完美解决以上问题。

## Obsidian 安装 Remotely save 插件

1. 打开 Obsidian 设置，在第三方插件处点击浏览，搜索Remotely save 插件。
   ![Capcha Export 2025-03-30 at 4.45.53 PM.jpg](/images/posts/202503301645080.webp)

2. 点击安装。
   ![Capcha Export 2025-03-30 at 4.45.53 PM.jpg](/images/posts/202503301648382.webp)
3. 安装后打开选项，等待我们在腾讯云COS 拿到相关的信息后再填入。
   ![Capcha Export 2025-03-30 at 4.45.53 PM.jpg](/images/posts/202503301705766.webp)

## 在腾讯云 COS 创建存储桶

1. 直接在腾讯云官网注册，并完成实名认证:
   https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F

2. 根据以下链接找到“创建存储桶”，点击创建。
   https://console.cloud.tencent.com/cos
   ![Capcha Export 2025-03-30 at 4.45.53 PM.jpg](/images/posts/202503301656983.webp)

3. 新建存储桶时，输入存储桶名称（不能重名），并选择访问权限为 “私有读写“。选择与自己就近的区域，如北京、广州。
   ![Capcha Export 2025-03-30 at 4.45.53 PM.jpg](/images/posts/202503301706712.webp)

4. 其他的基本上不用动，因为有些默认勾选的服务是要额外首付的，注意将这些默认勾选的项目给去掉。如果担心版本覆盖的话，可以在第二步勾选“版本控制“，不过这会涉及额外的费用。
   ![Capcha Export 2025-03-30 at 4.45.53 PM.jpg](/images/posts/202503301659642.webp)

5. 创建完成后，切换到概览页面
   ![Capcha Export 2025-03-30 at 4.45.53 PM.jpg](/images/posts/202503301701894.webp)

6. SecretID 和 Key，以及 AppID，需要在 “密钥管理” 页面中新建并获取到（不配置子账号也可以）：https://console.cloud.tencent.com/cam/capi
7. 存储空间名和存储区域，可以在 “存储桶列表” 页面中获取到：https://console.cloud.tencent.com/cos/bucket

## 配置 Remotely save 插件

1. 将上一个步骤中获取的相关信息填入下面的各个选项中
   ![Capcha Export 2025-03-30 at 4.45.53 PM.jpg](/images/posts/202503301705766.webp)

```plaintext
举例来说，假如你拿到的地址是
https://obsidian-12345678.cos.ap-guangzhou.myqcloud.com

那么，
- S3 Endpoint 为：cos.ap-guangzhou.myqcloud.com
- S3 Region 为: ap-guangzhou
- S3 AccessKeyID 为上个步骤获取到的 SecreteID
- S3 SecretAccessKey 则是上个步骤拿到的 SecretKey
- S3 BucketName 则是 obsidian-12345678
```

2. 配置好以上选项后，拉到页面中间位置，会看到一个“检查“的按钮。点击检查，查看链接是否成功。右上角会显示检查链接的状态，如果成功了，则万事俱备。
3. Remotely save 插件的其他设置，自己根据需要进行选择即可。

## 将本地文件同步至腾讯云 COS 存储桶

1. 按快捷键“CMD+P“，输入“remote"，选择开始同步。
   ![Capcha Export 2025-03-30 at 4.45.53 PM.jpg](/images/posts/202503301723707.webp)
2. 此时，右下角会显示同步的进度。显示完成时，就表示你的文件和文件夹都同步到存储桶了。
   > 我有 1000 多个文件，54 个文件夹， 第一次同步大概花了 5 分多钟。

## 配置手机Obsidian

同理，你可以在手机上安装 Remotely save 插件，然后腾讯云 COS 的信息在插件中配置好后，就可以将云端的文件拉到你的手机上了。

以上，就是全部的步骤。当然，使用腾讯云 COS 肯定会涉及到一些费用，但如果是个人使用的话，我认为基本在可接受范围内。为了有余额可以支付产生的费用，建议在开通以上服务的时候可以预先充值 10 块钱，够用很久了。
