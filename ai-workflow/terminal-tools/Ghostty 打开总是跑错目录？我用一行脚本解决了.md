---
title: Ghostty 打开总是跑错目录？我用一行脚本解决了
date: 2026-04-05
slug: ghostty-finder-right-click-fix
excerpt: Ghostty 换了挺顺手，但 Finder 右键打开终端总是落在父级目录。本想换回去，后来想起一句话：万事不决问 AI。发了一下，还真解决了。
cover: /Users/davidlin/Documents/Obsidian/MyVault/Wechat/published/img/cover-combined.jpg
tags:
  - 终端命令行
  - 苹果生态
  - 效率工具
status: published
---

在[别再让你的 Mac 吃灰了：这 16 款神器，让生产力提升 10 倍](/blog/%E5%88%AB%E5%86%8D%E8%AE%A9%E4%BD%A0%E7%9A%84%20Mac%20%E5%90%83%E7%81%B0%E4%BA%86%EF%BC%9A%E8%BF%99%2016%20%E6%AC%BE%E7%A5%9E%E5%99%A8%EF%BC%8C%E8%AE%A9%E7%94%9F%E4%BA%A7%E5%8A%9B%E6%8F%90%E5%8D%87%2010%20%E5%80%8D)里，我介绍过 **MouseBoost Pro**。

它把 Finder 右键菜单增强了一大截，新建文件、复制路径、终端打开，都能在一个右键里搞定。

最近我把终端从 iTerm2 换成了 **Ghostty**。

原因挺简单的：Boris 在用。

Boris 是谁？是 Claude Code 团队那位。不止我，很多人跟着他迁移到了 Ghostty。我倒没有觉得 iTerm2 和 Ghostty 之间有多大差别，但既然大家都在用，那我也选这个。

当然那么多人跟随过去了之后，没有回退肯定是 Ghostty有过人之处。

不过今天我们要来聊的是另外一个问题。

我的 Mac上本来就自带了 Terminal 终端，之前装了一个 Iterm2，现在再装一个 Ghostty，太冗余了！

iTerm2 加上 MouseBoost Pro后，有一个用得很顺的功能：Finder 右键里直接有"Open iTerm Window Here"，点到哪个目录，就从哪个目录打开终端。

![Ghostty 打开总是跑错目录？我用一行脚本解决了 - 截图 1](/images/posts/Ghostty%20%E6%89%93%E5%BC%80%E6%80%BB%E6%98%AF%E8%B7%91%E9%94%99%E7%9B%AE%E5%BD%95%EF%BC%9F%E6%88%91%E7%94%A8%E4%B8%80%E8%A1%8C%E8%84%9A%E6%9C%AC%E8%A7%A3%E5%86%B3%E4%BA%86/CleanShot%25202026-04-05%2520at%252016.08.06.webp)

换到 Ghostty 之后，我想在 MouseBoost Pro 里复现这个体验，结果碰到了一个问题。

## 遇到了一个问题

明明已经在 MouseBoost Pro 里面启用了 Ghostty， 在Finder 里进入了目标目录，右键 Ghostty，它却总跑到上一级父目录去。

![Ghostty 打开总是跑错目录？我用一行脚本解决了 - 截图 2](/images/posts/Ghostty%20%E6%89%93%E5%BC%80%E6%80%BB%E6%98%AF%E8%B7%91%E9%94%99%E7%9B%AE%E5%BD%95%EF%BC%9F%E6%88%91%E7%94%A8%E4%B8%80%E8%A1%8C%E8%84%9A%E6%9C%AC%E8%A7%A3%E5%86%B3%E4%BA%86/CleanShot%25202026-04-05%2520at%252016.10.06.webp)

第一次发生时，我有点怀疑是不是自己操作有问题。试了几次之后才发现，这不是我的问题，是 MouseBoost Pro 的问题：它直接打开 Ghostty App 时，拿到的路径上下文不够准确，经常拿到的是父级目录而不是当前目录。

本来的想法是：算了，大不了把 Ghostty 卸了，换回 iTerm2。

## 后来想起一句话

后来想起之前时常挂在嘴边的那句话：**万事不决问 AI**。

行，那就先问问。

---

没有预设它能给出准确答案，就是抱着"试试看"的心态，把问题描述了一下：

> 我用 MouseBoost Pro 给 Finder 右键加了一个 Ghostty 的入口，但打开后总是落在父级目录而不是当前目录，有没有办法解决？

ChatGPT 给出了一段脚本。

不是纯 Shell，也不是纯 AppleScript，而是两者组合：

```sh
dir=$(osascript <<'APPLESCRIPT'
tell application "Finder"
	if (count of Finder windows) is 0 then
		set p to POSIX path of (desktop as alias)
	else
		set p to POSIX path of (target of front Finder window as alias)
	end if
end tell
return p
APPLESCRIPT
)

cd "$dir"
open -a "Ghostty" .
```

AppleScript 负责问 Finder：当前前台窗口打开的是哪个目录？Shell 负责 cd 到那个目录，然后从那里启动 Ghostty。

![脚本解决问题的场景](/images/posts/Ghostty%20%E6%89%93%E5%BC%80%E6%80%BB%E6%98%AF%E8%B7%91%E9%94%99%E7%9B%AE%E5%BD%95%EF%BC%9F%E6%88%91%E7%94%A8%E4%B8%80%E8%A1%8C%E8%84%9A%E6%9C%AC%E8%A7%A3%E5%86%B3%E4%BA%86/Storyboard_illustration-01_630c6227_20260405.webp)

逻辑很清晰：路径由脚本自己算，不依赖右键菜单默认传过来的模糊上下文，Ghostty 只负责"在这个路径启动"。

## 接下来，配置

接下来就是把它配置进 MouseBoost Pro。步骤不复杂：

![Ghostty 打开总是跑错目录？我用一行脚本解决了 - 配图 4](/images/posts/Ghostty%20%E6%89%93%E5%BC%80%E6%80%BB%E6%98%AF%E8%B7%91%E9%94%99%E7%9B%AE%E5%BD%95%EF%BC%9F%E6%88%91%E7%94%A8%E4%B8%80%E8%A1%8C%E8%84%9A%E6%9C%AC%E8%A7%A3%E5%86%B3%E4%BA%86/20260405161700119.webp)

### Step 1

打开 MouseBoost Pro，点击左侧「Command Scripts」菜单，切换到「Shell」标签页，点击左下角的「+」新增一个脚本。

### Step 2

把上面的脚本完整粘贴进去。

### Step 3

在名称栏自定义一个名字，比如「Ghostty here」。图标也可以自定义，我找了一张小图片传上去，看起来比默认的舒服。

![Ghostty 打开总是跑错目录？我用一行脚本解决了 - 截图 5](/images/posts/Ghostty%20%E6%89%93%E5%BC%80%E6%80%BB%E6%98%AF%E8%B7%91%E9%94%99%E7%9B%AE%E5%BD%95%EF%BC%9F%E6%88%91%E7%94%A8%E4%B8%80%E8%A1%8C%E8%84%9A%E6%9C%AC%E8%A7%A3%E5%86%B3%E4%BA%86/CleanShot%25202026-04-05%2520at%252016.14.55.webp)

### Step 4

保存之后，回到 Command Scripts 列表，找到刚创建的这一行，在右侧「Add to Main Menu」列打勾。这样右键菜单里才会出现这个选项。

![Ghostty 打开总是跑错目录？我用一行脚本解决了 - 截图 6](/images/posts/Ghostty%20%E6%89%93%E5%BC%80%E6%80%BB%E6%98%AF%E8%B7%91%E9%94%99%E7%9B%AE%E5%BD%95%EF%BC%9F%E6%88%91%E7%94%A8%E4%B8%80%E8%A1%8C%E8%84%9A%E6%9C%AC%E8%A7%A3%E5%86%B3%E4%BA%86/CleanShot%25202026-04-05%2520at%252016.17.25.webp)

### Step 5

回到 Main menue选项下，在列表里可以直接上下拖动，调整这个脚本在右键菜单里出现的顺序。

---

配置完试了一下。

在 Finder 里点进一个目录，右键，选 Ghostty here——

这次直接落在了当前目录，和 iTerm2 的体验完全一样。

![Ghostty 打开总是跑错目录？我用一行脚本解决了 - 截图 7](/images/posts/Ghostty%20%E6%89%93%E5%BC%80%E6%80%BB%E6%98%AF%E8%B7%91%E9%94%99%E7%9B%AE%E5%BD%95%EF%BC%9F%E6%88%91%E7%94%A8%E4%B8%80%E8%A1%8C%E8%84%9A%E6%9C%AC%E8%A7%A3%E5%86%B3%E4%BA%86/CleanShot%25202026-04-05%2520at%252016.22.27.gif)

### 事情不大，但有意思的是

事情不大，但这个解决过程让我挺有感触的。

不是先去研究 MouseBoost Pro 的文档，不是去翻 Ghostty 的论坛，而是直接问 AI，抱着"不对就拉倒"的心态试了一下。结果还真解决了。

**万事不决问 AI**，这句话我之前在[老师让明天带手抄报？还好我能搬AI救兵](/blog/%E8%80%81%E5%B8%88%E8%AE%A9%E6%98%8E%E5%A4%A9%E5%B8%A6%E6%89%8B%E6%8A%84%E6%8A%A5%EF%BC%9F%E8%BF%98%E5%A5%BD%E6%88%91%E8%83%BD%E6%90%ACAI%E6%95%91%E5%85%B5)里也写过。每次真的用它解决了一个具体问题，体验都比"听了一句话"要真实得多。

所以遇到问题，先问问 AI，也不亏什么呀！

在这个浪潮汹涌的时代，也许这才是正确地解决问题方式......

---

相关旧文：

- MouseBoost Pro 基础介绍：[别再让你的 Mac 吃灰了：这 16 款神器，让生产力提升 10 倍](/blog/%E5%88%AB%E5%86%8D%E8%AE%A9%E4%BD%A0%E7%9A%84%20Mac%20%E5%90%83%E7%81%B0%E4%BA%86%EF%BC%9A%E8%BF%99%2016%20%E6%AC%BE%E7%A5%9E%E5%99%A8%EF%BC%8C%E8%AE%A9%E7%94%9F%E4%BA%A7%E5%8A%9B%E6%8F%90%E5%8D%87%2010%20%E5%80%8D)
- "万事不决问 AI"心态的由来：[老师让明天带手抄报？还好我能搬AI救兵](/blog/%E8%80%81%E5%B8%88%E8%AE%A9%E6%98%8E%E5%A4%A9%E5%B8%A6%E6%89%8B%E6%8A%84%E6%8A%A5%EF%BC%9F%E8%BF%98%E5%A5%BD%E6%88%91%E8%83%BD%E6%90%ACAI%E6%95%91%E5%85%B5)
