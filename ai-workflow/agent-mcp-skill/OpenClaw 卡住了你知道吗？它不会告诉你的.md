---
title: OpenClaw 卡住了你知道吗？它不会告诉你的
date: "2026-02-20"
slug: openclaw-rescue-system
excerpt: OpenClaw 卡住时所有通道都断了，你甚至不知道它挂了。我用 Telegram 做了个独立急救 Bot，手机上一条消息就能救回来。
cover: ""
tags:
  - OpenClaw
  - 效率工具
  - 多平台分发
  - 服务器运维
status: published
---

晚上 10 点，手机震了一下。

是之前设的提醒。OpenClaw 那边有个定时任务应该跑完了，我想看看结果。打开飞书，发了条消息过去。

等了一分钟，没回。

又等了两分钟，还是没回。

这时候开始纠结：它是在处理什么复杂的事情，还是已经卡死了？没有任何办法判断。唯一的选择是爬起来，打开电脑，SSH 登录服务器，手动重启。

晚上十点，到了我该睡觉的时间了呀！

我当时就想，这不对。我得给它装个「急救电话」：一个完全独立的通道，让我在手机上就能知道它的状态，必要时一键重启。

之前写过几篇 OpenClaw 的折腾记录：

- 从 [我的 OpenClaw 被攻击了 3000+ 次](/blog/%E6%88%91%E7%9A%84%20OpenClaw%20%E8%A2%AB%E6%94%BB%E5%87%BB%E4%BA%86%203000%2B%20%E6%AC%A1)
- 到 [我的 OpenClaw 还在被攻击，这次我让 AI 帮我装了个「门卫」](/blog/%E6%88%91%E7%9A%84%20OpenClaw%20%E8%BF%98%E5%9C%A8%E8%A2%AB%E6%94%BB%E5%87%BB%EF%BC%8C%E8%BF%99%E6%AC%A1%E6%88%91%E8%AE%A9%20AI%20%E5%B8%AE%E6%88%91%E8%A3%85%E4%BA%86%E4%B8%AA%E3%80%8C%E9%97%A8%E5%8D%AB%E3%80%8D)
- 再到 [不写一行代码，让服务器上的 OpenClaw 自动往我的 Obsidian 里塞笔记](/blog/%E4%B8%8D%E5%86%99%E4%B8%80%E8%A1%8C%E4%BB%A3%E7%A0%81%EF%BC%8C%E8%AE%A9%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84%20OpenClaw%20%E8%87%AA%E5%8A%A8%E5%BE%80%E6%88%91%E7%9A%84%20Obsidian%20%E9%87%8C%E5%A1%9E%E7%AC%94%E8%AE%B0)。

安全防护做了，文件同步做了，这次轮到“运维急救”。

---

先说结论：**你只需要准备两样东西。**

一台跑着 OpenClaw 的服务器，一个 Telegram 或者飞书账号。

配置时间 5 分钟，费用 0 元，内存占用约 16MB。配好之后，手机上发一条消息就能重启 Gateway。

下面说说为什么要做这个，以及过程中踩了哪些坑。

---

## 三个让人头疼的问题

### 不知道它是在干活还是卡了

问 OpenClaw 一个问题，等了 5 分钟没回复。

是在思考怎么处理复杂任务？还是已经卡死了？要不要重启？

没有任何指标可以参考。你只能猜。

![OpenClaw 卡住了你知道吗？它不会告诉你的 - 配图 1](/images/posts/OpenClaw%20%E5%8D%A1%E4%BD%8F%E4%BA%86%E4%BD%A0%E7%9F%A5%E9%81%93%E5%90%97%EF%BC%9F%E5%AE%83%E4%B8%8D%E4%BC%9A%E5%91%8A%E8%AF%89%E4%BD%A0%E7%9A%84/20260220221622818.webp)

### 重启很麻烦

OpenClaw 在 2026.2.13 版本做了一个安全更新：禁止 Bot 自己重启 Gateway。原因可以理解，万一 Bot 进入死循环，不断自我重启，那就更麻烦了。

但代价是：Bot 不能自救了。每次出问题，你都得手动 SSH 登录服务器去重启。

半夜或者凌晨出问题？起床干活。

### 所有通道都断了

这是最坑的一点。Gateway 一旦卡住，飞书收不到消息，Telegram 也收不到消息。小龙虾完全失联。

**你甚至不知道它挂了。**

直到你主动去问它，发现没人应答，才意识到：哦，不知道什么时候就挂了。

---

## 思路：做一个独立的急救通道

思路很简单：再做一个 Bot。就像家里停电了应急手电筒还能亮，这个 Bot 用的是自己的电池：一个独立的 Python 脚本，跑在同一台服务器上，用 Telegram 轮询模式收消息，有自己的 Token，和主 Bot 完全隔离。systemd 管着它，开机自启，崩了自己重启。

![OpenClaw 卡住了你知道吗？它不会告诉你的 - 配图 2](/images/posts/OpenClaw%20%E5%8D%A1%E4%BD%8F%E4%BA%86%E4%BD%A0%E7%9F%A5%E9%81%93%E5%90%97%EF%BC%9F%E5%AE%83%E4%B8%8D%E4%BC%9A%E5%91%8A%E8%AF%89%E4%BD%A0%E7%9A%84/20260220221702616.webp)

为什么选 Telegram？因为它支持轮询模式——脚本主动去问 Telegram 服务器「有没有新消息」，不需要配 Webhook，不需要开放端口，部署简单。

> 如果你习惯用飞书，逻辑其实是一样的。只是飞书的权限配置，可能要稍微复杂一些。

---

## 踩坑实录

说实话，思路很清晰，但实际配的时候还是踩了不少坑。我是让 OpenClaw Bot 帮我写的代码和配置，但中间来回折腾了好几轮。

第一个坑秒解：systemd 启动服务时找不到 `node` 命令，因为它的环境变量和终端里不一样。在服务文件里手动写上完整的 PATH 就好了。不懂代码没关系，知道有这个坑就行。后面的 Prompt 模板已经帮你处理了。

第二个坑就折腾了。

本来想用 `openclaw gateway restart` 来重启，结果报了个奇怪的错：

```
systemctl --user unavailable: Failed to connect to bus: No medium found
```

我让她查了好几轮，才搞明白：`openclaw gateway restart` 底层依赖 `systemctl --user`，但我们的急救脚本是以系统服务的身份运行的，没有用户级别的 D-Bus 会话。简单说就是：官方的重启命令，在这个场景下走不通。

Bot 给的方案是绕过去——不用官方命令，直接用底层操作：

> 这段是给好奇的人看的，跳过也完全不影响。

```python
# 先停
subprocess.run(["pkill", "-f", "openclaw-gateway"])
time.sleep(3)

# 再启
subprocess.Popen(["/path/to/openclaw", "gateway", "start"], ...)
```

先杀进程，等 3 秒，再重新启动。简单粗暴，但管用。

第三个坑也快：重启后脚本立刻检查进程，Gateway 还没完全起来就误报「启动失败」。就像按了电脑开机键，没等屏幕亮就说电脑坏了。加了个等待和多次检查的逻辑就解决了。

第四个坑最值得说。

Gateway 进程还在跑，端口也在监听，但就是不回消息。怎么判断它是在忙还是卡了？

想了一圈，找到一个关键指标：**日志文件的最后修改时间**。

看懂逻辑就行：日志越久没更新，越可能卡住了：

```python
log_file = f"/tmp/openclaw/openclaw-{date}.log"
last_modified = os.path.getmtime(log_file)
seconds_ago = time.time() - last_modified

if seconds_ago < 60:
    # 日志 1 分钟内更新过，正在工作
elif seconds_ago < 300:
    # 日志 5 分钟没动了，可能卡住
else:
    # 超过 5 分钟，大概率卡了
```

1 分钟内更新过？还在干活，别急。超过 5 分钟没动静？大概率卡了，可以考虑重启。

这个判断逻辑配合 `/status` 命令，终于让我能在手机上看出 Bot 到底是在忙还是挂了。

---

## 最终效果

配好之后，急救 Bot 支持 4 个命令。

### /status 一键体检

发送 `/status`，它会告诉你：

![OpenClaw 卡住了你知道吗？它不会告诉你的 - 配图 3](/images/posts/OpenClaw%20%E5%8D%A1%E4%BD%8F%E4%BA%86%E4%BD%A0%E7%9F%A5%E9%81%93%E5%90%97%EF%BC%9F%E5%AE%83%E4%B8%8D%E4%BC%9A%E5%91%8A%E8%AF%89%E4%BD%A0%E7%9A%84/20260220221822791.webp)

![OpenClaw 卡住了你知道吗？它不会告诉你的 - 配图 4](/images/posts/OpenClaw%20%E5%8D%A1%E4%BD%8F%E4%BA%86%E4%BD%A0%E7%9F%A5%E9%81%93%E5%90%97%EF%BC%9F%E5%AE%83%E4%B8%8D%E4%BC%9A%E5%91%8A%E8%AF%89%E4%BD%A0%E7%9A%84/20260220221916825.webp)

进程在不在、日志活不活跃、端口通不通、系统资源够不够。该知道的都在这了。

### /restart 远程重启

发送 `/restart`，它会自动执行：停止 Gateway → 等待 3 秒 → 重新启动 → 等待 5 秒 → 多次检查确认成功。
![OpenClaw 卡住了你知道吗？它不会告诉你的 - 配图 5](/images/posts/OpenClaw%20%E5%8D%A1%E4%BD%8F%E4%BA%86%E4%BD%A0%E7%9F%A5%E9%81%93%E5%90%97%EF%BC%9F%E5%AE%83%E4%B8%8D%E4%BC%9A%E5%91%8A%E8%AF%89%E4%BD%A0%E7%9A%84/20260220221948867.webp)

### /logs 查看日志

发送 `/logs`，显示最近 50 行日志。排查问题的时候很有用。
![OpenClaw 卡住了你知道吗？它不会告诉你的 - 截图 6](/images/posts/OpenClaw%20%E5%8D%A1%E4%BD%8F%E4%BA%86%E4%BD%A0%E7%9F%A5%E9%81%93%E5%90%97%EF%BC%9F%E5%AE%83%E4%B8%8D%E4%BC%9A%E5%91%8A%E8%AF%89%E4%BD%A0%E7%9A%84/CleanShot%25202026-02-20%2520at%252022.20.20%25402x.webp)

### /help 帮助信息

显示所有可用命令。
![OpenClaw 卡住了你知道吗？它不会告诉你的 - 配图 7](/images/posts/OpenClaw%20%E5%8D%A1%E4%BD%8F%E4%BA%86%E4%BD%A0%E7%9F%A5%E9%81%93%E5%90%97%EF%BC%9F%E5%AE%83%E4%B8%8D%E4%BC%9A%E5%91%8A%E8%AF%89%E4%BD%A0%E7%9A%84/20260220222122648.webp)

---

## 怎么部署：复制一段话就行

先准备两样东西：在 Telegram 找 `@BotFather` 创建一个新 Bot，拿到 Bot Token；再找 `@userinfobot` 拿到你的 User ID。两分钟的事。

然后是核心步骤：把下面这段 Prompt 复制给你的 OpenClaw Bot，把方括号里的内容替换成你自己的信息：

```
请帮我配置一个独立的 Telegram 急救系统，用于在 OpenClaw Gateway 卡住时远程重启。

要求：
1. 创建 Python 脚本 /root/.openclaw/workspace/scripts/emergency_telegram.py
2. 使用轮询模式（不需要 Webhook）
3. 支持以下命令：
   - /status - 显示详细状态（进程、日志活跃度、端口、系统资源）
   - /restart - 重启 Gateway（pkill + 重新启动 + 多次检查）
   - /logs - 查看最近 50 行日志
   - /help - 帮助信息
4. 创建 systemd 服务 /etc/systemd/system/telegram-rescue.service
5. 配置开机自启和自动重启

我的配置：
- Bot Token: [你的 Bot Token]
- User ID: [你的 User ID]
- OpenClaw 路径: /root/.nvm/versions/node/v22.22.0/bin/openclaw

关键点：
- 必须在 systemd 服务里设置完整的 PATH 环境变量
- 重启逻辑：pkill -f openclaw-gateway → sleep 3 → 启动 → sleep 5 → 多次检查
- 状态检查：包括日志最后修改时间（判断是否卡住）
- 完全独立，不依赖 OpenClaw Gateway

请帮我完成配置并启动服务。
```

这段 Prompt 里已经把前面踩过的坑全部写进去了。PATH 环境变量、pkill 替代方案、重启检查逻辑、日志活跃度判断。你的 Bot 会按照这些要求来配置，不用再踩一遍。

配好之后，在 Telegram 给急救 Bot 发个 `/status`，看到状态信息就说明成了。

---

## 用起来什么感觉

有天晚上，问了 Bot 一个问题，等了好几分钟没回。以前遇到这种情况只能干瞪眼，这次我打开 Telegram，给急救 Bot 发了个 `/status`：

```
Gateway 运行中
  CPU: 0.1% | 内存: 28.4%
日志较旧（5分钟前更新）
端口 18789 正在监听
```

日志 5 分钟没更新，CPU 几乎为零。不用猜了，卡了。

发了个 `/restart`，十几秒后回到 Telegram 再问一遍，Bot 活过来了。

![OpenClaw 卡住了你知道吗？它不会告诉你的 - 配图 8](/images/posts/OpenClaw%20%E5%8D%A1%E4%BD%8F%E4%BA%86%E4%BD%A0%E7%9F%A5%E9%81%93%E5%90%97%EF%BC%9F%E5%AE%83%E4%B8%8D%E4%BC%9A%E5%91%8A%E8%AF%89%E4%BD%A0%E7%9A%84/20260220221736199.webp)

如果重启之后还是不对劲，还可以发 `/logs` 看最近的日志，找找线索。

整个过程不超过 30 秒。不用开电脑，不用 SSH，不用记命令。

---

**这才是 AI 助手应该有的样子。你睡你的，它干它的。出了问题，一条消息就能救回来。**

如果你也在用 OpenClaw，建议花 5 分钟配一个。毕竟，急救系统这种东西，你永远希望它用不上。但真用上的那一刻，你会庆幸自己装了。

如果在配置过程中碰到问题，欢迎加我交流：linauwawa。
