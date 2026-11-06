---
title: "Obsidian 入门64：坚果云同步，三步就走完了"
date: "2026-06-21"
slug: "obsidian-64-nutstore-sync"
excerpt: "不用折腾，三步配好坚果云同步 Obsidian"
tags:
  - Obsidian
  - 笔记同步
  - Obsidian入门
status: published
---
> 这是一个「Obsidian x AI」系列。
> 
> 前面介绍了好几种自己折腾同步方案，今天来介绍一下坚果云。

入门63 最后一步聊了同步三档，这篇展开最简单的那个，坚果云。

## 先说两件你可能关心的事

第一，不需要装坚果云桌面端。你只需要在 Obsidian 里装一个插件，叫 Nutstore Sync（读作那次四朵 深克，坚果云同步的英文名）。装好后它会直接和坚果云的云端通信，不走本地同步文件夹那一层。少装一个东西，就少一个可能出问题的环节。

第二，免费版够不够？坚果云免费用户每月 1GB 上传、3GB 下载，按月刷新。如果你的笔记以文字为主，偶尔插图，正常用不会超。如果笔记量大、附件多，或者你在同步配置目录（`.obsidian` 文件夹），流量会跑得快一些。到那个程度再考虑升级专业版，一年 200 块左右，不限流量。

好，说完了。开始配。

## 开始配

先装插件。在 Obsidian 里打开「设置」→「社区插件」→「浏览」，搜索「Nutstore Sync」，安装，启用。

![Obsidian 入门64：坚果云同步，三步就走完了 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A864%EF%BC%9A%E5%9D%9A%E6%9E%9C%E4%BA%91%E5%90%8C%E6%AD%A5%EF%BC%8C%E4%B8%89%E6%AD%A5%E5%B0%B1%E8%B5%B0%E5%AE%8C%E4%BA%86/CleanShot%25202026-06-21%2520at%252010.23.44.webp)


然后进入插件设置界面，默认是单点登录，点击登录按钮，它会弹出一个授权窗口。点「授权坚果云」，浏览器会打开坚果云的登录页。登录之后授权就完成了。

![Obsidian 入门64：坚果云同步，三步就走完了 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A864%EF%BC%9A%E5%9D%9A%E6%9E%9C%E4%BA%91%E5%90%8C%E6%AD%A5%EF%BC%8C%E4%B8%89%E6%AD%A5%E5%B0%B1%E8%B5%B0%E5%AE%8C%E4%BA%86/CleanShot%25202026-06-21%2520at%252010.27.23.webp)


整个流程不到一分钟，不需要输 WebDAV 地址、不需要配第三方应用密码、不需要填任何技术参数。点几下就行。

授权完成后，选一个远程目录存放你的笔记。插件默认会用你的 Vault 名字创建一个新的文件夹，你也可以自己选一个已有的。

![选择远程目录](/images/posts/Obsidian%20%E5%85%A5%E9%97%A864%EF%BC%9A%E5%9D%9A%E6%9E%9C%E4%BA%91%E5%90%8C%E6%AD%A5%EF%BC%8C%E4%B8%89%E6%AD%A5%E5%B0%B1%E8%B5%B0%E5%AE%8C%E4%BA%86/nutstore_select_remote.webp)

点「开始同步」。不过第一次同步前，建议先去插件设置里做三件事：

第一，配好**排除规则**。把不需要同步的文件夹排除掉，比如 `.obsidian` 配置目录、`node_modules` 这些。不然首轮全量上传会把很多没必要的东西也传上去，既慢又占免费流量。

第二，打开**宽松同步模式**（Loose Sync Mode）。这个模式下只传文件名或大小有变化的文件，如果你的笔记库文件很多，性能会好不少。

第三，设一个**大文件跳过阈值**，避免把几百 MB 的附件也传上去。

这些都设好了再点开始同步。第一次会把你的笔记全量上传，时间取决于笔记数量和大小。之后的每一次都是增量同步，只传改动的部分，很快。

手机端也是一样的操作。装 Obsidian → 装 Nutstore Sync → 同一个坚果云账号登录 → 选同一个目录 → 开始同步。步骤完全一样。首次同步慢一些，后面就快了。

![手机端同步](/images/posts/Obsidian%20%E5%85%A5%E9%97%A864%EF%BC%9A%E5%9D%9A%E6%9E%9C%E4%BA%91%E5%90%8C%E6%AD%A5%EF%BC%8C%E4%B8%89%E6%AD%A5%E5%B0%B1%E8%B5%B0%E5%AE%8C%E4%BA%86/nutstore_mobile_sync.webp)



## 实际用下来

坚果云最大的感受就是快。服务器在国内，每次同步基本上秒级完成。如果你的笔记量不大可能没什么感觉，但像有很多笔记或者附件比较多的人，切过来之后能明显感觉到它比 Obsidian Sync 响应快。

免费的 1GB 流量，目前如果是纯文字笔记完全够用。额度每个月刷新，也不用操心。

## 内置 AI 助手

顺便一提，Nutstore Sync 插件内置了一个 AI 助理入口。如果你有自己的 API Key（比如硅基流动、OpenAI），配进去之后可以在 Obsidian 里直接让 AI 帮你总结、润色、排版。

![Obsidian 入门64：坚果云同步，三步就走完了 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A864%EF%BC%9A%E5%9D%9A%E6%9E%9C%E4%BA%91%E5%90%8C%E6%AD%A5%EF%BC%8C%E4%B8%89%E6%AD%A5%E5%B0%B1%E8%B5%B0%E5%AE%8C%E4%BA%86/CleanShot%25202026-06-21%2520at%252010.31.37.webp)

不过这个跟同步没关系。不配 API Key 的话，插件只做同步，不受影响。对 AI 有兴趣的话，之前聊过 [[Obsidian 入门32：Claudian 插件实战，拥有这个优雅的AI管家|Claudian]] 和 [DeepSeek 接入](/blog/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A)，你可以看看哪个更适合你。

---

最后说一个该注意的事。

同步前先把笔记备份一次。坚果云本身有版本历史，但多一层备份总不会错。另外，尽量不要同时在两台设备上改同一篇笔记。电脑上改完，等几秒让同步完成，再在手机上打开。这个习惯养好了，同步基本不会出问题。

回到入门63 的那三档
- 有钱、怕折腾 → Obsidian Sync
- 求简单、国内用 → 坚果云
- 想省钱、愿意折腾 → 自建

我选的是第三档，是因为我天生爱折腾。

如果是你来选择的话，依据自己的情况选择一个适合自己的方案就行了，适合自己的才是最好的！

## 进阶阅读

### 同步方案系列
- [入门57：同步总览](/blog/Obsidian%20%E5%85%A5%E9%97%A857%EF%BC%9A%E6%89%BE%E5%88%B0%E9%80%82%E5%90%88%E8%87%AA%E5%B7%B1%E7%9A%84%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5%E6%96%B9%E6%A1%88) ， 8 种方案一张表对号入座
- [入门58：Remotely Save + COS](/blog/Obsidian%20%E5%85%A5%E9%97%A858%EF%BC%9A%E7%94%A8%20Remotely%20Save%20%2B%20%E8%85%BE%E8%AE%AF%E4%BA%91%20COS%20%E5%AE%9E%E7%8E%B0%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5)
- [入门59：Fast Note Sync 自建](/blog/Obsidian%20%E5%85%A5%E9%97%A859%EF%BC%9A%E7%94%A8%20Fast%20Note%20Sync%20%E8%87%AA%E5%BB%BA%E4%B8%80%E5%A5%97%E5%A4%9A%E7%AB%AF%E5%90%8C%E6%AD%A5)
- [入门60：SyncThing 织网](/blog/Obsidian%20%E5%85%A5%E9%97%A860%EF%BC%9A%E7%94%A8%20SyncThing%20%E6%8A%8A%E5%A4%9A%E5%8F%B0%E8%AE%BE%E5%A4%87%E7%BB%87%E6%88%90%E4%B8%80%E5%BC%A0%E7%BD%91)
- [入门61：iCloud 同步](/blog/Obsidian%20%E5%85%A5%E9%97%A861%EF%BC%9A%E8%8B%B9%E6%9E%9C%E7%94%A8%E6%88%B7%E7%9A%84%E9%9B%B6%E9%85%8D%E7%BD%AE%E6%96%B9%E6%A1%88%EF%BC%8CiCloud%20%E5%90%8C%E6%AD%A5)
- [入门62：飞书 ObShare](/blog/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97)

### 前文回顾
- [入门63：6 步上手](/blog/Obsidian%20%E5%85%A5%E9%97%A863%EF%BC%9A%E6%96%B0%E6%89%8B%E5%85%A5%E9%97%A8%E6%8C%87%E5%8D%97%EF%BC%8C%E4%BB%8E%E4%B8%8B%E8%BD%BD%E5%88%B0%E7%94%A8%E8%B5%B7%E6%9D%A5%EF%BC%8C6%20%E6%AD%A5%E5%B0%B1%E5%A4%9F%E4%BA%86) — 坚果云就是这篇提到的「求简单」路线

### AI 插件
- [入门32：Claudian](/blog/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6)
- [入门54：接入 DeepSeek](/blog/Obsidian%20%E5%85%A5%E9%97%A854%EF%BC%9ADeepSeek%20%E6%80%8E%E4%B9%88%E6%8E%A5%E8%BF%9B%E6%9D%A5%EF%BC%9F%E5%85%88%E6%8A%8A%E5%B7%A5%E5%85%B7%E4%B8%B2%E8%B5%B7%E6%9D%A5%E8%AF%B4%E6%B8%85%E6%A5%9A)
