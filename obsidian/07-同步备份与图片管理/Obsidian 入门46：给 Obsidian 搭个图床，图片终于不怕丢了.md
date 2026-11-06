---
title: Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了
date: 2026-05-15
slug: obsidian-image-bed-setup
excerpt: 给 Obsidian 搭个图床，同步再也不用等图片加载了。
cover: Wechat/published/img/cover-combined.jpg
tags:
  - Obsidian
  - 排版与导出
  - 效率工具
  - Obsidian入门
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理和收集、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过上一篇，可以先看 [Obsidian 入门45：对自己好一点，给 Obsidian 建个个人主页](/blog/Obsidian%20%E5%85%A5%E9%97%A845%EF%BC%9A%E5%AF%B9%E8%87%AA%E5%B7%B1%E5%A5%BD%E4%B8%80%E7%82%B9%EF%BC%8C%E7%BB%99%20Obsidian%20%E5%BB%BA%E4%B8%AA%E4%B8%AA%E4%BA%BA%E4%B8%BB%E9%A1%B5)。

有朋友问我，你在 Obsidian 里贴了那么多图片，库会不会很臃肿？

会。而且不只是臃肿的问题。

## 图片在 Obsidian 里是怎么存的

你在 Obsidian 里拖进一张图片，它不会像在 Word 里一样嵌入到文档里。Obsidian 会把图片文件复制到你的 vault 目录下的某个附件文件夹，然后在文档里写一行 `![[图片.png]]` 来引用它。

> 关于附件的使用，可以阅读[Obsidian 入门8：附件与图片管理，给你的笔记装上「附件收纳术」](/blog/Obsidian%20%E5%85%A5%E9%97%A88%EF%BC%9A%E9%99%84%E4%BB%B6%E4%B8%8E%E5%9B%BE%E7%89%87%E7%AE%A1%E7%90%86%EF%BC%8C%E7%BB%99%E4%BD%A0%E7%9A%84%E7%AC%94%E8%AE%B0%E8%A3%85%E4%B8%8A%E3%80%8C%E9%99%84%E4%BB%B6%E6%94%B6%E7%BA%B3%E6%9C%AF%E3%80%8D)

这是 Markdown 的工作方式，本身没问题。

但问题出在，当你开始大量用图的时候，情况就变了。

一张手机拍的截图大概 2-3MB，一篇教程文章放 5-6 张图很正常，一篇文章光是图片就占了十几 MB。如果你的库有几十篇文章，几百张图，很快就会变成一个本地的巨大仓库。

然后你会遇到三个很现实的问题。

第一个，同步变慢了。如果你用 Obsidian Sync、iCloud 多端同步或者其他同步方案，每张图片都要上传下载。在自己电脑上还好，但在手机上看，等图片加载完的那几秒，足够让你失去阅读耐心。

第二个，存储空间膨胀。Obsidian Sync 是按流量计费的，iCloud 的空间也不是无限的。

第三个，管理混乱。所有图片都堆在一个附件文件夹里，时间一长根本分不清谁是谁。

所以衡量下来很不划算，更好的解决方案是使用**图床**。

![多设备同步困境](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/Project_ImageBed_46_illustration-01_04b483ee_20260515.webp)

图床是一个在线的图片存储服务，你把图片传上去，拿到一个链接，贴到 Obsidian 里。图片实际存在云端，本地只留一个文本链接。

好处很明显。同步的时候只传几 KB 的文字，不传图片。手机打开文章，图片从 CDN 加载，比自己库里的附件还快。所有的图片都在图床的管理后台，跟文章完全解耦。

接下来我直接说怎么搭。

---

## 开始搭：Mac 版

我会用腾讯云 COS 作为图床，搭配 PicGo（读作匹克够，Mac 上的一个软件） 和 Image Auto Upload Plugin（读作一米鸡 阿噗楼 普拉金， Obsidian 的一个插件），在 Mac 上跑通这条链路。

这套方案我自己用了一年多了，很稳。

### 第一步：注册腾讯云 COS

腾讯云的对象存储（COS）是国内最常用的图床方案之一。优点是稳定、国内访问快、有免费额度。缺点是实名认证稍微有点门槛。

打开腾讯云官网，注册并完成实名认证。

> 腾讯云 COS 的网址：https://console.cloud.tencent.com/cos

![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.08.03.webp)

然后在控制台里找到「对象存储」，创建一个存储桶（就是存储图片的文件夹）。创建的时候注意几个设置：

- **存储桶名称**：随便起一个，但不能重名
- **访问权限**：选「公有读私有写」。这样别人能看到你的图片，但只有你自己能上传和删除。
- **其他选项**：保持默认就行。注意取消那些默认勾选的额外服务，那些是单独收费的。

![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.10.31.webp)

创建完之后，你会看到一个存储桶列表页面。记下两个信息：**存储桶名称** 和 **存储区域**，后面配置 PicGo 要用。

然后去「密钥管理」页面，新建一个密钥。这里会生成一对 **SecretID** 和 **SecretKey**，相当于你的账号密码。

充值 10 块钱，可以用很久很久。我充了 10 块钱，用了一年多了还剩 2 块钱。

> 具体的操作截图我之前写过一篇详细的教程，你可以参考里面的截图对照操作：
> [如何快速搭建自己的专属图床(Obsidian - 图床+Picgo+OB插件）](/blog/%E5%A6%82%E4%BD%95%E5%BF%AB%E9%80%9F%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E4%B8%93%E5%B1%9E%E5%9B%BE%E5%BA%8A%28Obsidian%20-%20%E5%9B%BE%E5%BA%8A%2BPicgo%2BOB%E6%8F%92%E4%BB%B6%EF%BC%89)

### 第二步：安装 PicGo

去 PicGo 的 GitHub Release 页面下载 macOS 版本，或者直接搜索引擎搜 PicGo 下载。

> PicGo 官网：https://picgo.app/
> PicGo Github release 页面：https://github.com/Molunerfinn/PicGo/releases

现在最新版是 v2.5.3（2026 年 3 月发布），macOS 版本已经在 v2.4.2 之后做了签名认证，安装时不会再提示「未识别的开发者」了。

![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.05.24.webp)

安装好之后打开，你会看到一个简洁的界面。

先做关键的一步：配置腾讯云 COS。

在 PicGo 的设置里找到「图床设置」→「腾讯云 COS」，填写刚才记下的信息：

- **COS 版本**：选 V5
- **SecretID**：刚才新建的
- **SecretKey**：刚才新建的
- **存储 bucket 名称**
- **存储区域**
- **存储路径**（可选）：如果你想上传到指定文件夹，可以填。注意末尾要加斜杠 `/`
  ![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.14.12.webp)

填完之后点确定，然后切换到「上传区」，把图床切换成腾讯云 COS。拖一张图进去试试，如果上传成功，去 COS 的存储桶里查看。能看到这张图了，那就说明整条路已经通了。

如果上传失败或者报错，记得查看顶部我框出来这个位置，记得要切换为腾讯云 COS。

![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.16.21.webp)

如果你经常在多台电脑之间切换，PicGo 还有一个值得一提的新功能：**PicGo Cloud**。它可以把你的图床配置、上传历史同步到云端，换电脑后登录就能恢复配置，不用每台机器重新输入一遍 SecretKey。

> [!image-swipe] 左右滑动查看图片
>
> ![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.23.46.webp)
> ![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.24.26.webp)

### 第三步：配置 Obsidian

在 Obsidian 的社区插件市场搜索 **Image Auto Upload Plugin**，安装启用。

![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 9](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.27.20.webp)

什么都不用配，默认设置就行。

现在你回到 Obsidian，拖一张图片或者截图粘贴进去，你会发现图片自动上传到腾讯云 COS，然后链接自动插入到你的文档里。整个过程在 1-2 秒内完成，几乎无感。

如果你还想让图片名字整齐一些，可以再加一个 **Paste Image Rename** 插件。它会在粘贴图片时弹出一个命名窗口，你可以给图片起一个有意义的名字，比如「图床搭建-配置 PicGo.png」或者比如按「文章标题+时间戳」，而不是一串乱码。

如果你觉得每次插入的图片尺寸太大了，你可以在 Image auto upload 插件的设置中，更改图片大小后缀，这样的话在插入图片后会约束他的展示尺寸。比如我设置的就是`|400`。

![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 10](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.31.13.webp)

---

## 市面上还有哪些插件方案

上面我用了 Image Auto Upload Plugin，但不是只有这一个选择。在 Obsidian 里做「粘贴→自动上传」这件事，其实有好几条路可以走。我列几个主流的，你根据自己情况选。

### Image Uploader

一个更轻量的选择。不需要外部客户端，支持直接配置 S3 兼容的存储服务（腾讯云 COS、阿里云 OSS、AWS S3 等都在此列）。插件内置了上传功能，你在 Obsidian 里粘贴图片，它直接帮你传到云上。

优点是少装一个软件。缺点是配置起来稍微复杂一点，而且每个存储服务的配置项都不一样。

### 我为什么选了 Image Auto Upload + PicGo

试了一圈之后，我回到这个组合。原因很简单。

插件做得越少，出问题的概率越小。Image Auto Upload 只做一件事，拦截粘贴事件，调用系统里的图床客户端上传。上传这件事，交给 PicGo 来做。

![选择适合自己的方案](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/Project_ImageBed_46_illustration-02_ff5d9554_20260515.webp)

PicGo 是一个独立的图床客户端，支持 macOS 和 Windows。它最方便的地方是，它提供了一个系统级的上传区域，你可以在任何软件里截图，然后按快捷键上传到图床，不只限于在 Obsidian 里用。

还有一个原因：PicGo 支持插件扩展。你不想用腾讯云，可以选择阿里云、又拍云、GitHub 图床，甚至 WebDAV，装一个对应的插件就行。

---

## Windows 上也来一遍

Windows 上的流程和 Mac 基本一致，只有几个差异点。

PicGo 有 Windows 版本，安装包在同一个 GitHub Release 页面可以下载，安装后界面和配置方式一模一样。你只需要在第一步配置 COS 时输入同样的信息就行。

一个值得注意的区别是：Windows 上 PicGo 安装后默认会开机自启，这在 Mac 上需要手动设置。如果你不想让它每次开机都启动，可以到 PicGo 的设置里关掉。

还有一个细节是快捷键。

PicGo v2.5.0 之后，**默认的上传快捷键统一改成了 `Cmd Or Ctrl + Shift + U`**。也就是说 Mac 上用 `Cmd + Shift + U`，Windows 上用 `Ctrl + Shift + U`。旧版的 `Ctrl+Shift+P` 已经不再作为默认值了。你可以在 PicGo 设置里按自己的习惯修改。

如果你用的是微信截图或者 Snipaste，PicGo 也支持这些截图工具的快捷键配合使用。

还有一个好消息是，之前提到的 **PicGo Cloud** 配置同步功能是跨平台的。

你在 Mac 上配置好的 COS 信息和上传历史，登录同一个 PicGo Cloud 账号，在 Windows 上也能直接同步过来。两台电脑不用各配一遍。

---

## 不止腾讯云 COS

上面我用腾讯云 COS 做了演示，但 PicGo 能用的图床远不止这一种。

PicGo 有一个插件市场。在 PicGo 的「插件设置」里搜索安装对应的插件，就能连接到不同的存储服务。

![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 截图 12](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/CleanShot%25202026-05-15%2520at%252022.40.31.webp)

**想要免费的**，可以试试 WebDAV。

很多 NAS 用户和私人云盘都支持 WebDAV 协议。只要你的云服务商提供了 WebDAV 地址，在 PicGo 里装一个 webdav 插件就能直接上传。对于已经买了 NAS 的人来说，这是最省钱的方案。

**已经在用阿里云的**，PicGo 也有对应的阿里云 OSS 插件，配置方式和 COS 基本一致，换汤不换药。

**想要全球加速的**，可以看看 AWS S3 或者 Cloudflare R2。R2 还有免费额度，对个人用户很友好。

不管你用哪种云服务，配置逻辑都是一样的：装插件 → 填密钥 → 开始用。PicGo 的插件生态覆盖了市面上大部分主流的存储方案。

---

## 到底值不值得折腾

搭图床不是为了炫技。

如果你只是偶尔在笔记里放一两张图，那本地附件完全够用，不用折腾。

但如果你和我一样，经常写教程类的文章，需要大量截图；

或者你的笔记库在多台设备之间同步；

又或者你只是不想某天打开 Obsidian 发现自己的库已经膨胀到几个 G。那花 10 分钟搭一个图床，是一个长期受益的投入。

10 分钟之后，你再也不用管图片的事了。粘贴、自动上传、自动链接。

![Obsidian 入门46：给 Obsidian 搭个图床，图片终于不怕丢了 - 配图 13](/images/posts/Obsidian%20%E5%85%A5%E9%97%A846%EF%BC%9A%E7%BB%99%20Obsidian%20%E6%90%AD%E4%B8%AA%E5%9B%BE%E5%BA%8A%EF%BC%8C%E5%9B%BE%E7%89%87%E7%BB%88%E4%BA%8E%E4%B8%8D%E6%80%95%E4%B8%A2%E4%BA%86/20260515234222007.webp)

它就在那稳稳地接住你...

_上面这句话是我故意改成 ChatGPT 风格的-\_-幽你一默，哈哈哈哈_

---

## 进阶阅读

- [Obsidian 入门40：把我的写作工作流Skill免费分享给你](/blog/Obsidian%20%E5%85%A5%E9%97%A840%EF%BC%9A%E6%8A%8A%E6%88%91%E7%9A%84%E5%86%99%E4%BD%9C%E5%B7%A5%E4%BD%9C%E6%B5%81Skill%E5%85%8D%E8%B4%B9%E5%88%86%E4%BA%AB%E7%BB%99%E4%BD%A0)
- [Obsidian 入门8：附件与图片管理，给你的笔记装上「附件收纳术」](/blog/Obsidian%20%E5%85%A5%E9%97%A88%EF%BC%9A%E9%99%84%E4%BB%B6%E4%B8%8E%E5%9B%BE%E7%89%87%E7%AE%A1%E7%90%86%EF%BC%8C%E7%BB%99%E4%BD%A0%E7%9A%84%E7%AC%94%E8%AE%B0%E8%A3%85%E4%B8%8A%E3%80%8C%E9%99%84%E4%BB%B6%E6%94%B6%E7%BA%B3%E6%9C%AF%E3%80%8D)
- [Obsidian 入门12：国内用户怎么方便地安装第三方插件，告诉你 3 条路](/blog/Obsidian%20%E5%85%A5%E9%97%A812%EF%BC%9A%E5%9B%BD%E5%86%85%E7%94%A8%E6%88%B7%E6%80%8E%E4%B9%88%E6%96%B9%E4%BE%BF%E5%9C%B0%E5%AE%89%E8%A3%85%E7%AC%AC%E4%B8%89%E6%96%B9%E6%8F%92%E4%BB%B6%EF%BC%8C%E5%91%8A%E8%AF%89%E4%BD%A0%203%20%E6%9D%A1%E8%B7%AF)
- [Obsidian 入门5：别被「Markdown」吓到，它只是为了让你写得更爽](/blog/Obsidian%20%E5%85%A5%E9%97%A85%EF%BC%9A%E5%88%AB%E8%A2%AB%E3%80%8CMarkdown%E3%80%8D%E5%90%93%E5%88%B0%EF%BC%8C%E5%AE%83%E5%8F%AA%E6%98%AF%E4%B8%BA%E4%BA%86%E8%AE%A9%E4%BD%A0%E5%86%99%E5%BE%97%E6%9B%B4%E7%88%BD)
- [6MB 图片变 100KB？我只用了 2 步](/blog/6MB%20%E5%9B%BE%E7%89%87%E5%8F%98%20100KB%EF%BC%9F%E6%88%91%E5%8F%AA%E7%94%A8%E4%BA%86%202%20%E6%AD%A5)
- [如何快速搭建自己的专属图床(Obsidian - 图床+Picgo+OB插件）](/blog/%E5%A6%82%E4%BD%95%E5%BF%AB%E9%80%9F%E6%90%AD%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%E4%B8%93%E5%B1%9E%E5%9B%BE%E5%BA%8A%28Obsidian%20-%20%E5%9B%BE%E5%BA%8A%2BPicgo%2BOB%E6%8F%92%E4%BB%B6%EF%BC%89)
