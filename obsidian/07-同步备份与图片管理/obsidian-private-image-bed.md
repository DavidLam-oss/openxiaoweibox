---
title: 如何快速搭建自己的专属图床(Obsidian - 图床+Picgo+OB插件）
date: "2025-03-13"
excerpt: 手把手教你利用腾讯云 COS、PicGo 和 Obsidian 插件搭建专属图床，实现图片自动上传与链接替换，解决 Obsidian 图片分享难题。
tags:
  - Obsidian
  - 服务器运维
  - 效率工具
---

我从去年底开始使用 Obsidian 记录生活、学习及一些探索的过程。

OB 确实好用，但是图片管理实在是很差，特别是想将 OB 用 markdown 格式撰写的内容分享到其他平台的时候，每次都得重新插入图片，非常麻烦和繁琐。

最后发现自己搭建自己的图床是合适的解决方法。下面的 3 张图片就是我搭建图床后所生成的。

![如何快速搭建自己的专属图床 - 配图 1](/images/posts/57f125f49f17261884931b2e269535173a51abb4cef41c59a10f5f13a7af60dc.webp)

![如何快速搭建自己的专属图床 - 配图 2](/images/posts/80f180bc544076e85eec0d0ad57ccad6668e9c920f184d0625bd58bf73021cc5.webp)

![download (1).png](/images/posts/202503131329531.webp)

## 什么是图床

图床（Image Hosting Service）是一个专门用来存储图片的在线服务。通过下面的例子可以更好地理解：

1. **拍了一张照片**：比如你拍了一张可爱的猫咪照片，想分享给朋友。
2. **上传到图床**：你把这张照片上传到一个图床网站（比如 Imgur、SM.MS 等）。
3. **获取图片链接**：上传后，图床会给你一个链接，比如 `https://example.com/cat.jpg`。
4. **分享链接**：你可以把这个链接发给朋友，或者放在你的博客里。别人点击链接就能看到你的猫咪照片了。

更通俗地来理解，图床就是一个在线网盘，图片传上去之后就可以通过在线链接的形式将图片分享到别的地方或者给别人。对于平常有自己的笔记系统想要迁移的人来说，图床更加便于你迁徙到别的笔记软件中去。

## 常见的图床服务：

- **Imgur**：国外很流行的图床，免费且简单易用。
- **SM.MS**：国内常用的图床，支持免费上传。
- **腾讯云COS、阿里云OSS**：适合需要大量存储和高稳定性的用户，通常是付费的。

我们今天使用腾讯云 COS 来作为图床，再搭配其他的一些工具实现在 OB 中自动将插入的图片转化为在线链接，大致分为 3 步：

1. 建立存储桶buket，实现手动上传图片；
2. 配置 Picgo 软件，实现自动上传图片；
3. 设置 Obsidian，实现在 Obsidian 中自动上传图片。

> 为什么不用 SM.MS，大家可以去搜一下 SM 域名回收事件，大概就知道原因了。

## 建立存储桶 buket

直接在腾讯云官网注册，并完成实名认证:
https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F

根据以下链接找到“创建存储桶”，点击创建。
https://console.cloud.tencent.com/cos

![如何快速搭建自己的专属图床(Obsidian - 图床+Picgo+OB插件） - 配图 4](/images/posts/202503131428306.webp)

新建存储桶时，输入存储桶名称（不能重名），并选择访问权限为 “公有读私有写” 或“公有读写”，其它无需更改。
![如何快速搭建自己的专属图床(Obsidian - 图床+Picgo+OB插件） - 配图 5](/images/posts/202503131429562.webp)

其他的基本上不用动，因为有些默认勾选的服务是要额外首付的，注意将这些默认勾选的项目给去掉。

待存储通创建完毕后并进入其中后，就可以手动上传文件了。不过因为腾讯云 COS 是收费的， 建议充值10 块钱，听说可以用很久。
![如何快速搭建自己的专属图床(Obsidian - 图床+Picgo+OB插件） - 配图 6](/images/posts/202503131433212.webp)

## 安装和配置Picgo

**Picgo**是一款**免费开源**的软件，可以通过链接去下载：

- GitHub Release： [https://github.com/Molunerfinn/PicGo/releases](https://github.com/Molunerfinn/PicGo/releases)
- 如果没有条件，就搜索引擎搜索吧，也能下载到的。

安装好 Picgo 之后，我们需要先为它配置好图床信息。
![如何快速搭建自己的专属图床(Obsidian - 图床+Picgo+OB插件） - 配图 7](/images/posts/202503131450042.webp)

需要配置的信息，分为三类：

- COS 版本，选择 V5；
- SecretID 和 Key，以及 AppID，需要在 “密钥管理” 页面中新建并获取到：https://console.cloud.tencent.com/cam/capi
- 存储空间名和存储区域，可以在 “存储桶列表” 页面中获取到：https://console.cloud.tencent.com/cos/bucket
- 在 Picgo 中，你可以设定 “存储路径”，来指定将图片上传到某个具体的文件夹。设置时，请务必记得在末尾加上斜杠 / 。

设置好之后，打开上传主界面，并将图床选择为 “腾讯云 COS”。
![如何快速搭建自己的专属图床(Obsidian - 图床+Picgo+OB插件） - 配图 8](/images/posts/202503131455553.webp)

此时，可以尝试上传一张图片看看是否设置成功，如果一切都设置好了的话在存储桶里面能马上看到你刚刚上传的图片。

## 使用插件在Obsidian中自动上传图片

在 Obsidian 的插件市场中搜索“**Image auto upload plugin**“，安装后，保持默认设置无序做任何更改
![如何快速搭建自己的专属图床(Obsidian - 图床+Picgo+OB插件） - 配图 9](/images/posts/202503131457685.webp)
此时，当你拖拽一张图片或者粘贴一张图片到 Obsidian 中，将会自动上传到腾讯云存储中并且自动将生成的链接插入你刚刚放图片的位置。

> 如果不想使用腾讯云 COS 作为图床，也可以参考这篇教程将Cloudflare R2作为图床并且用 WebP Cloud 优化图片体积。
> https://sspai.com/post/90170

Enjoy！
