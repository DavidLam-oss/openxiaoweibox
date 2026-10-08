---
title: Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南
date: 2026-06-16
slug: obshare-feishu-guide
excerpt: 把 Obsidian 笔记同步到飞书，只要 2 个权限就够了。安装→配置→排障，10 分钟配通。
tags:
  - Obsidian
  - Obsidian插件
  - 多平台分发
  - 笔记同步
  - Obsidian入门
status: published
---
> 这是一个「Obsidian x AI」入门系列。
> 
> 前面聊了 [插件升级 2.8.0：以前只有公众号，现在是一键发 20+ 平台](/blog/%E6%8F%92%E4%BB%B6%E5%8D%87%E7%BA%A7%202.8.0%EF%BC%9A%E4%BB%A5%E5%89%8D%E5%8F%AA%E6%9C%89%E5%85%AC%E4%BC%97%E5%8F%B7%EF%BC%8C%E7%8E%B0%E5%9C%A8%E6%98%AF%E4%B8%80%E9%94%AE%E5%8F%91%2020%2B%20%E5%B9%B3%E5%8F%B0)，怎么从 Obsidian 一键发到各类平台。
>
> 这篇聊另一个场景，把笔记同步到飞书文档：3 个坑，一张 checklist，半小时配通。

最近有朋友问我，有没有办法把 Obsidian 的笔记一键发到飞书文档，好给团队共享。

有，用 ObShare 插件。

ObShare 这个插件做的事情很简单。把你的 Obsidian 笔记通过飞书 Open API，一键同步成飞书文档。

这篇文章把从安装到配置的完整流程走一遍，中间把我踩过的坑标出来。你按这个顺序做，半小时内能配通。

---

## 安装 ObShare 插件

GitHub 地址：[https://github.com/xigua222/ObShare](https://github.com/xigua222/ObShare)

有两种安装方式。

1. **插件市场安装**，在 Obsidian 设置 → 社区插件 → 浏览，搜索 `ObShare` 即可安装启用。
2. **BRAT 安装**，如果你已经装了 BRAT 插件，添加仓库 `xigua222/ObShare`，也可以安装。

装完之后，在 Obsidian 左侧栏会出现 ObShare 的图标。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252011.59.59%25402x.webp)


进入插件设置面板，你会看到 4 个空的输入框，App ID、App Secret、文件夹 Token、用户 ID。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252012.00.57%25402x.webp)


接下来就是把这 4 个值填上。要拿到它们，需要在飞书开发者后台做一些配置。

## 第一步：创建飞书自建应用

打开飞书开发者后台。
https://open.feishu.cn/?lang=zh-CN

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.26.50.webp)

创建一个自建应用。
![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.27.44.webp)

自定义命名应用名称没，比方说我把它命名为 WChat conveter
![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.28.47.webp)


创建成功后，点击进入应用详情页。

在**凭证与基础信息**里，可以看到 **App ID** 和 **App Secret**，先把这两个值复制下来，填到 ObShare 插件设置里。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.30.08.webp)



## 第二步：开通「机器人」能力

在应用详情页左侧菜单找到**机器人**，点击开通。这一步是让应用拥有「群机器人」的身份，为后面建群授权做准备。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.31.23.webp)


很多配置教程漏了这一步，会导致后面报 403。

## 第三步：配置云文档权限

在左侧菜单找到**权限管理**，添加以下权限。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.32.32.webp)


给予下方最必要的两个权限（**应用身份和用户身份权限**）：

- `drive:drive` ：云空间读写（让应用能访问你的云盘）
- `docs:document:import` ：导入为文档（让应用能在文件夹里创建文档）

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 9](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.47.47.webp)


这两个就够了，权限给得越小越安全。

如果配置之后发现还是不行，那就在应用身份的 tab 给予所有云文档的权限，并且在用户身份 tab 给予全部权限

## 第四步：创建版本 → 申请发布

这是最容易漏掉的一步。

回到左侧菜单，找到**版本管理与发布** → **创建版本**或者点击顶部的“创建版本”。填一个版本号（如 `1.0.0`），然后点击**申请线上发布**（这个按钮在右上角菜单里）。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 10](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.51.05.webp)


> ⚠️ 勾完权限之后一定记得做这一步，否则权限不会生效。我第一次就是停在这里，反复报错不知道怎么回事。

申请完之后，打开飞书管理后台（https://www.feishu.cn/admin/），在**应用审核**里找到你的应用，**手动审批通过**。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 11](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.54.03.webp)

到这里，你的应用才真正拥有了操作云文档的权限。

## 第五步：获取文件夹 Token

在飞书云盘（https://feishu.cn/drive/home/）里新建一个文件夹，命名随意。建好后打开文件夹，刷新一次页面。在浏览器 URL 末尾那串字符就是**文件夹 Token**。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 12](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252013.58.26.webp)


把它填到 ObShare 设置的第三个输入框里。

## 第六步：获取你的 user_id

在飞书管理后台(第四步的URL) → **组织架构** → **成员与部门**，找到你自己，查看详情。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 13](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252014.00.39.webp)

里面有一个 **User ID**（格式如 `abc1234`）。
![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 14](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252014.01.29.webp)


把它填到 ObShare 设置的第四个输入框里。

> ⚠️ 注意这里要填的是 `user_id`，**不是 `open_id`（`ou_xxx` 开头）或 `union_id`（`on_xxx` 开头）**。ObShare 用这个字段是在文档创建后把所有权转给你，而不是给那个机器人 App。

## 第七步：建群并授权

这是整个配置里**最反人类**的一步。

打开飞书客户端，新建一个群组（随便叫什么，一个人也能建群）。
![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 15](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252014.15.42.webp)

然后把你的应用拉进来。在群设置 → **群机器人** → 添加机器人，搜索你的应用名称并添加。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 16](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252014.17.56.webp)

点击设置后，会展开完整的窗口。点击群机器人。
![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 17](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252014.18.29.webp)

选择我们在一开始创建的应用。
![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 18](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252014.21.08.webp)

添加机器人成功后，返回群租，能看到下面的信息。
![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 19](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252014.24.40.webp)


建好群之后，回到飞书云盘，找到你在第五步新建的文件夹，点击分享，在弹窗的邀请协作者输入框中输入你刚刚创建的群租，例如我创建的群租叫做测试，右侧的权限选择「可管理」。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 截图 20](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/CleanShot%25202026-06-16%2520at%252014.28.22.webp)


> 分享给群时权限一定要选「可管理」，不是「只读」或「可编辑」。另外分享完等几秒再测试，飞书的权限下发有延迟。

这一步的本质是，飞书云文档的分享面板不认识「应用」，只能分享给用户或群组。所以「建群 → 加机器人 → 分享给群」是把应用伪装成群成员来获得文件夹访问权。

如果你按「分享文档给同事」的直觉来理解这个步骤，一定会懵。

## 测试：终于可以同步了

现在回到 ObShare 设置面板，4 个输入框应该已经填好了。

| 输入框 | 对应值 | 获取位置 |
|--------|--------|---------|
| App ID | `cli_xxxxxxxx` | 飞书开发者后台 → 凭证与基础信息 |
| App Secret | `xxxxxxxx` | 同上（创建时复制） |
| 文件夹 Token | `xxxxxxxx` | 云盘文件夹 URL 末尾 |
| 用户 ID | `abc1234` | 管理后台 → 成员与部门 → 你的详情 |

先点**测试连接**，确认提示成功。然后打开一篇 Obsidian 笔记，点击 ObShare 图标，选择发送。

![Obsidian 入门62：把 Obsidian 笔记同步到飞书文档，ObShare 配置指南 - 配图 21](/images/posts/Obsidian%20%E5%85%A5%E9%97%A862%EF%BC%9A%E6%8A%8A%20Obsidian%20%E7%AC%94%E8%AE%B0%E5%90%8C%E6%AD%A5%E5%88%B0%E9%A3%9E%E4%B9%A6%E6%96%87%E6%A1%A3%EF%BC%8CObShare%20%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8D%97/6475b222877666570c3524012aad3677.webp)


如果报 **400 或 403**，大概率是前面的某一步没做完。
1. 应用有没有发布？
2. 后台有没有审批？
3. 机器人有没有拉进群？
4. 文件夹有没有分享给群？

400 和 403 的根因是一样的，应用没获得文件夹访问权。区别只是 403 在访问文件夹时就拒了，400 在导入为文档那一步才拒。解法是同一套，把上面四步重新检查一遍。

## 一份 checklist

如果你也在配 ObShare，按这个顺序走。

- [ ] 安装 ObShare（插件市场 or BRAT）
- [ ] 飞书开发者后台创建自建应用
- [ ] 开通「机器人」能力
- [ ] 勾选云文档权限：`drive:drive` + `docs:document:import`
- [ ] **创建版本 → 申请线上发布**
- [ ] 飞书管理后台审批应用
- [ ] 复制 App ID 和 App Secret → 填到 ObShare
- [ ] 云盘新建文件夹，记下 token → 填到 ObShare
- [ ] 管理后台获取自己的 user_id → 填到 ObShare
- [ ] **飞书客户端建群，把应用拉进来**
- [ ] 把文件夹分享给那个群，权限「可管理」
- [ ] 点测试连接 → 选一篇笔记发送

配完 ObShare 之后，我理解了一件事。飞书的身份体系分得很细，App、Bot、群机器人、User、user_id、open_id、union_id，每一种都对应一套资源访问权。这给企业级用户最大的灵活性，但对只想「把笔记同步过去」的小用户非常不友好。

ObShare 本身能做的优化其实有限，它依赖的飞书 Open API 就是这个模型。能做的只是把「该填什么」和「该去哪儿找」讲得更清楚。

希望这篇文章帮你10 分钟配通，不用再走我踩过的那 55 分钟弯路。
