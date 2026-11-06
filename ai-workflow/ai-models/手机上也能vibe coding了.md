---
title: 手机上也能vibe coding了
date: "2026-01-21"
slug: happy-coder-mobile-vibe-coding
excerpt: Happy Coder 让你在手机上实时控制电脑里的 Claude Code，随时随地进行 vibe coding。开源免费，端到端加密。
tags:
  - 效率工具
  - AI模型
  - 开源
---

Vibe coding 真上瘾啊。

每次用 Claude Code 写代码的时候，总有种「心流」的感觉。你只管说想法，它来写代码，配合得像老搭档一样默契。

问题是，这种快乐只能发生在电脑前。

出门遛个弯、等个外卖、躺沙发上刷手机的时候，明明脑子里冒出一个好点子，却只能干瞪眼——因为 Claude Code 在电脑上跑着呢，你够不着。

有没有办法让 vibe coding 随时随地都能进行？

有的。用 Happy Coder。

## Happy Coder 是什么

Happy Coder 是一个开源的移动端客户端，让你可以在手机上实时查看和控制电脑上运行的 Claude Code 或 Codex。

简单说，它就是 Claude Code 的「遥控器」。

核心功能：

- **跨设备无缝切换**：手机上查看进度、发送消息，回到电脑前按下键盘就能接管
- **消息推送**：AI 需要授权或遇到问题时，手机立刻收到通知
- **端到端加密**：用的是和 Signal 一样的加密协议，代码数据全程加密，中继服务器看不到任何内容
- **完全免费 + 开源**：MIT 协议，代码公开，不收一分钱

这个项目是 Slopus 团队做的，和 Anthropic、OpenAI 没有官方关系，是社区的独立作品。

## 怎么安装

### 电脑端

Happy Coder 是手机连接电脑上的 Claude Code，所以前提是电脑上要先装好 Claude Code 或 Codex。

> Gemini CLI 暂时还不支持

安装 CLI 需要 Node.js 18 或更高版本。

Claude Code：

```
npm install -g @anthropic-ai/claude-code
```

Codex：

```
npm install -g @openai/codex
```

然后安装 Happy Coder：

```
npm i -g happy-coder
```

![安装成功截图](/images/posts/%E6%89%8B%E6%9C%BA%E4%B8%8A%E4%B9%9F%E8%83%BDvibe%20coding%E4%BA%86/20260120070704010.webp)

### 手机端

**iOS**：App Store 搜索「Happy」或直接访问：
https://apps.apple.com/us/app/happy-codex-claude-code-app/id6748571505

**Android**：Google Play 搜索「Happy」或直接访问：
https://play.google.com/store/apps/details?id=com.ex3ndr.happy

**网页版**（备选）：
https://app.happy.engineering/

> 推荐用 APP，体验更流畅，而且有推送通知

## 怎么使用

如果你用 Claude Code，原来的启动命令是 `claude`，现在改成：

```
happy
```

如果你用 Codex，原来是 `codex`，现在改成：

```
happy codex
```

输入之后会问你怎么认证，选择 mobile。

![选择 mobile 认证方式](/images/posts/%E6%89%8B%E6%9C%BA%E4%B8%8A%E4%B9%9F%E8%83%BDvibe%20coding%E4%BA%86/20260120071411709.webp)

接着会出现一个二维码，用手机 APP 扫码就完成配对了。

![扫码授权二维码](/images/posts/%E6%89%8B%E6%9C%BA%E4%B8%8A%E4%B9%9F%E8%83%BDvibe%20coding%E4%BA%86/CleanShot%25202026-01-20%2520at%252007.23.51.webp)

配对成功后，手机上就能看到完整的 Claude Code 界面：

![手机端界面](/images/posts/%E6%89%8B%E6%9C%BA%E4%B8%8A%E4%B9%9F%E8%83%BDvibe%20coding%E4%BA%86/8acb6a10b87e1accf0a95cc974928aed.webp)

电脑上的终端则变成这样，显示已经连接：

![电脑端界面](/images/posts/%E6%89%8B%E6%9C%BA%E4%B8%8A%E4%B9%9F%E8%83%BDvibe%20coding%E4%BA%86/CleanShot%25202026-01-20%2520at%252007.27.42.webp)

## 关于语音输入

Happy Coder 自带语音输入功能，可以直接对着手机说话给 Claude 下指令。

不过如果你在国内使用，我更推荐用**豆包输入法**的语音输入。豆包的中文语音识别目前是国内最准的，识别速度快、错字少，比 Happy 自带的语音体验好很多。

用法很简单：在 Happy 的输入框里，切换到豆包输入法，长按语音键说话，说完自动转成文字，然后发送给 Claude 就行了。

## 适合什么场景

- **通勤路上**：地铁里看一眼 Claude 跑到哪了，有问题就用语音回复
- **开会间隙**：不用盯着电脑，手机推送会告诉你什么时候需要介入
- **遛弯散步**：突然想到一个点子，掏出手机就能让 Claude 开工
- **躺平时刻**：沙发上刷着手机，顺便看看代码写得怎么样了

## 别人怎么用它

Reddit 上有个开发者分享了他的工作流：把 Claude Code 跑在云端开发环境里，用 Happy Coder 连接，这样即使电脑关机了，他也能在手机上继续和 AI 协作。

他说：「我最好的点子总是在离开工位的时候冒出来。现在我终于能抓住它们了。」

另一位开发者 Alex Cavender 写了篇详细的使用心得。他用了一周之后总结：

> 周一：启动一个数据库迁移任务，开会期间用手机监控进度，遇到外键约束问题时远程给 Claude 指令。
>
> 周三：通勤路上调试生产问题，引导 Claude 分析日志，到家前就定位到根因了。
>
> 周五：下班前启动优化任务，周末偶尔瞄一眼手机看进度，周一回来发现性能优化全做完了。

他的结论是：Claude Code 的利用率提升了 30%，而且切换回工作状态时几乎不需要重新进入上下文。

---

Vibe coding 的精髓就是：**你负责想，AI 负责干**。

Happy Coder 把这件事从「必须坐在电脑前」变成了「随时随地」。

对了，你现在看到的这篇文章，就是我用 Happy Coder 在手机上完成的。

试试看吧。
