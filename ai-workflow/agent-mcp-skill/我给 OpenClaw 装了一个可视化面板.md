---
title: 我给 OpenClaw 装了一个可视化面板
date: "2026-03-09"
slug: clawpanel-setup-guide
excerpt: AI 的“黑盒”操作让人不省心？这篇指南帮你给 AI 装上一个透明的“驾驶舱”，顺便解决 Cloudflare 下证书自动续期的烦恼。
cover: ""
tags:
  - OpenClaw
  - 服务器运维
  - 编程开发
  - 效率工具
status: published
---

我又被我的 AI 助理“骗”了。

倒不是说它故意使坏，这家伙干完活之后，汇报说“完成了”，但我压根不知道它在自己的工作目录里是怎么鼓捣的。它的工作区，对我来说就是个“黑盒”。

直到有一次，我让助理 “Jennie” 帮忙整理一份写作流文档。它说搞定了。我鬼使神差地多问了一句：“你把文件放哪了？”

不问不知道，一问吓一跳。它把本该给写作助理“Lyra”的文档，全放在了自己“Jennie”的文件夹里。如果我没多那句嘴，这个错误大概率就永远石沉大海了。

那一刻我清楚地意识到，我需要一个能“看穿”这个黑盒的方法。

![我给 OpenClaw 装了一个可视化面板 - 配图 1](/images/posts/%E6%88%91%E7%BB%99%20OpenClaw%20%E8%A3%85%E4%BA%86%E4%B8%80%E4%B8%AA%E5%8F%AF%E8%A7%86%E5%8C%96%E9%9D%A2%E6%9D%BF/20260309080230129.webp)

这个方法就是我们今天要聊的主角：ClawPanel，一个能让你用浏览器直观管理 AI 工作区的 Web 后台。

![我给 OpenClaw 装了一个可视化面板 - 配图 2](/images/posts/%E6%88%91%E7%BB%99%20OpenClaw%20%E8%A3%85%E4%BA%86%E4%B8%80%E4%B8%AA%E5%8F%AF%E8%A7%86%E5%8C%96%E9%9D%A2%E6%9D%BF/20260309075953753.webp)

---

### **告别黑盒，也告别“人肉运维”**

ClawPanel 的价值很直接：它把命令行里的“黑盒”操作，变成了我们熟悉的、所见即所得的“网盘”式管理。装好之后，我随时能看到 AI 的文件，心里总算踏实了。

但这份踏实感，只持续了不到90天。

一个新的、更烦人的问题浮现了出来：要让这个后台在公网上安全、稳定地访问，就需要配置域名和 HTTPS 证书。

我最初的方案是 `Caddy (服务器) + Cloudflare (DNS)`，这也是很多人的标准配置。但这个方案有个不大不小的麻烦：Cloudflare 的代理（那朵橙色云朵）和 Caddy 默认的证书申请方式 (HTTP-01) 互相冲突。

这导致 HTTPS 证书每隔 90 天就会续期失败，我必须手动登录服务器，关闭代理，续期，再打开。

这让原本为了自动化而生的系统，凭空多出了一项“人肉运维”的工作。这显然不是我们想要的从容。

所以，这篇文章想分享的，不仅是如何安装一个面板，更是如何通过一种名为 `DNS-01` 的验证方式，一劳永逸地解决公网访问和证书自动续期的问题，让你真正获得一个无需操心的 AI 管理后台。

![手摇服务器-clean-850.png](/images/posts/%E6%88%91%E7%BB%99%20OpenClaw%20%E8%A3%85%E4%BA%86%E4%B8%80%E4%B8%AA%E5%8F%AF%E8%A7%86%E5%8C%96%E9%9D%A2%E6%9D%BF/%25E6%2589%258B%25E6%2591%2587%25E6%259C%258D%25E5%258A%25A1%25E5%2599%25A8-clean-850.webp)

---

### **第一站：安装 ClawPanel**

我们先来完成简单的部分，把 ClawPanel 安装起来。

不懂代码也没关系，这里的步骤非常清晰，跟着做就好。

1.  **下载 ClawPanel**: 从它的 [GitHub Releases](https://github.com/openclaw/clawpanel/releases) 页面找到最新版的二进制文件，下载到你的服务器上。
2.  **创建服务**: 为了让它能在后台长期运行，我们为它创建一个 `systemd` 服务。
3.  **启动服务**: 启动它，并设置为开机自启。

这个过程，你可以直接把下面的指令复制给你的 AI 助理，让它帮你完成。

```
请帮我完成 ClawPanel 的基础安装：

1. 从 https://github.com/openclaw/clawpanel/releases 下载最新版的二进制文件。
2. 将其安装到 /opt/clawpanel/ 目录。
3. 为它创建一个 systemd 服务，并确保启动时传入 OpenClaw 的路径作为环境变量。
4. 启动服务并设置为开机自启。
```

完成后，ClawPanel 应该已经在你服务器的 `19527` 端口上运行了。

---

### **第二站：配置 Caddy (核心环节)**

现在，我们来处理核心的部分：让 Caddy 作为我们面板的代理，并配置好永久自动续期的 HTTPS。

#### 1. 准备一个带“插件”的 Caddy

常规的 Caddy 是不支持 DNS-01 验证的，我们需要一个包含了 Cloudflare DNS 插件的“特供版”。

好在 Caddy 官网就提供了下载服务，直接运行下面的命令，就能下载到这个特供版 Caddy。（如果你的 AI 助理提示 Go 版本过低无法编译，用这个方法可以完美跳过问题。）

```bash
curl -sL "https://caddyserver.com/api/download?os=linux&arch=amd64&p=github.com%2Fcaddy-dns%2Fcloudflare" -o /tmp/caddy-cf
# 下载后替换你服务器上原有的 Caddy 二进制文件即可
# sudo mv /tmp/caddy-cf /usr/local/bin/caddy
# sudo chmod +x /usr/local/bin/caddy
```

#### 2. 申请一个 Cloudflare API Token

这是整个流程中最关键的一步。我们需要在 Cloudflare 创建一个 API Token，并只给它最小的必要权限。

- 登录 Cloudflare -> 我的个人资料 -> API 令牌 -> 创建令牌。
- 选择“创建自定义令牌”。
- **权限设置**：
  - `区域 (Zone)` → `DNS` → `编辑 (Edit)`
- **区域资源**：
  - `包括 (Include)` → `特定区域 (Specific zone)` → 选择你的域名

创建成功后，把生成的 Token 复制下来，**这是它唯一一次完整显示**。

#### 3. 配置 Caddy

现在，我们把刚刚的 Token告诉 Caddy。

首先，创建一个环境变量文件：

```bash
# 创建并编辑
sudo vim /etc/caddy/caddy.env
```

把你的 Token 写进去：

```
CLOUDFLARE_API_TOKEN=你刚刚复制的Token
```

然后，修改 Caddy 的主配置文件 `Caddyfile`，为你的 ClawPanel 添加一段这样的配置：

```caddy
clawpanel.你的域名.top {
    tls {
        dns cloudflare {env.CLOUDFLARE_API_TOKEN}
    }
    reverse_proxy 127.0.0.1:19527
}
```

这段配置的核心是 `tls` 块，它告诉 Caddy：在为这个域名申请证书时，请使用 Cloudflare 的 DNS 来进行验证，验证时需要的 API 令牌，请从我刚刚设置的环境变量 `CLOUDFLARE_API_TOKEN` 中读取。

#### 4. 重启 Caddy 并验证

最后一步，我们需要让 Caddy 在启动时加载我们设置的环境变量文件。

编辑 Caddy 的 `systemd` 服务文件：

```bash
sudo systemctl edit caddy
```

在打开的编辑器里，输入以下内容，它会覆盖掉默认的启动指令：

```ini
[Service]
ExecStart=
ExecStart=/usr/local/bin/caddy run --environ --config /etc/caddy/Caddyfile --envfile /etc/caddy/caddy.env
```

> **实战小贴士：**
> 为什么不直接修改原始的 `caddy.service` 文件？因为使用 `systemctl edit` 创建的覆盖文件，在 Caddy 升级后依然会保留，更为稳妥。这也是之前踩过的一个坑，直接修改原文件，升级后配置就没了。

现在，重新加载并重启 Caddy：

```bash
sudo systemctl daemon-reload
sudo systemctl restart caddy
```

等待片刻，访问 `https://clawpanel.你的域名.top`，你应该能看到 ClawPanel 的登录界面了，而且浏览器地址栏的锁应该是安全状态。

---

### **给你的 AI 配上“遥控器”**

走到这一步，我们已经完成了一个相当稳妥的部署。

更有趣的是，我们可以把整个过程“封装”成一个指令，交给你的 AI 助理来完成。以后给新服务器部署时，你只需要把下面的话复制给它。

这比我们自己对着文档操作，又多了一份从容。

> **复制这段话给你的 OpenClaw 助理：**
>
> ```
> 请帮我部署 ClawPanel 并通过 Caddy 的 DNS-01 方式配置好公网访问。
>
> **我的环境:**
> - 域名: [填写你的域名]
> - 已安装: OpenClaw, Caddy
> - Cloudflare: DNS 已托管
>
> **执行步骤:**
> 1.  参考本文，完成 ClawPanel 的安装和服务配置。
> 2.  参考本文，下载带 Cloudflare 插件的 Caddy。
> 3.  请向我申请 Cloudflare API Token，我会提供给你。
> 4.  创建 `/etc/caddy/caddy.env` 文件并填入 Token。
> 5.  修改 `Caddyfile`，为 `clawpanel.你的域名` 添加反向代理和 DNS-01 的 tls 配置。
> 6.  通过 `systemctl edit caddy` 更新服务，加载环境变量文件。
> 7.  重启 Caddy，并验证 `https://clawpanel.你的域名` 是否可访问。
>
> 请开始执行，有问题随时问我。
> ```

---

### **从“黑盒”到“驾驶舱”**

现在，每当 AI 助理在服务器上完成一项任务，我不再需要追问“你改了哪里？”，而是可以从容地打开浏览器，进入 ClawPanel 这个“驾驶舱”，直观地看到所有文件的变化。晚上也终于能睡个安稳觉，不用担心第二天醒来，AI 又不知把什么东西搞丢了。

从一个充满不确定性的“黑盒”，回归到一个可掌控、确定性更高的工作流——这才是真正的“一劳永逸”，之前那些都只能算半成品。

毕竟，掌控感，才是我们玩技术最重要的事情。

![我给 OpenClaw 装了一个可视化面板 - 配图 4](/images/posts/%E6%88%91%E7%BB%99%20OpenClaw%20%E8%A3%85%E4%BA%86%E4%B8%80%E4%B8%AA%E5%8F%AF%E8%A7%86%E5%8C%96%E9%9D%A2%E6%9D%BF/20260309080338987.webp)
