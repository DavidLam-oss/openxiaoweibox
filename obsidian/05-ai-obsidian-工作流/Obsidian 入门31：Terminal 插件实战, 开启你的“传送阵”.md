---
title: Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵”
date: 2026-04-21
slug: obsidian-terminal-plugin-advanced-guide
excerpt: 拒绝全库乱扫！手把手带你配通 Obsidian Terminal 插件，解决 command not found 顽疾。实现“Wechat 车间”级精准 AI 协作，让侧边栏成为你指挥多模型的“全能统帅部”。
cover: ""
tags:
  - Obsidian
  - Obsidian插件
  - Claude Code
  - 终端命令行
  - Codex
  - 效率工具
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门30:将AI集成进Obsidian侧边栏,选哪一个?](/blog/obsidian-ai-plugin-selection-guide)

---

上一篇，我们给三位侧边栏的“面试者”做了选型对比。

今天，我们要请出其中最自由、最硬核的那位“老兵”：**Terminal 插件**。

虽然它的长相平平无奇，就是一个黑框框，但在我心里，它是不可替代的。因为它能给你一种“掌控全世界”的自由。

---

## 为什么我们需要一个“手动挡”？

很多人不理解：既然有专门的 AI 插件，为什么还要在侧边栏装个终端？

我有两个必须用它的理由。

第一，是“专注”。我的 Obsidian 库很大，包含了我生活、工作的方方面面。但我平时花精力最多的地方，其实是那个叫 `Wechat` 的子文件夹。

如果你直接在库的根目录运行 AI，它会像个好奇宝宝一样到处乱看，既浪费 Token，又容易被一些无关紧要的文件干扰了判断。

第二，是“精准”。我在 `Wechat` 目录下定义了专门的写作、生图 Skill，还有一份专属的 `claude.md` 指令。我只有通过 `cd` 命令（还记得那个[任意门](/blog/obsidian-terminal-navigation-guide)吗？）钻进这个特定的“写作车间”，AI 才能瞬间“附身”，变成我的首席编辑。

---

## 实操：两步跨越“配置鸿沟”

很多小白装完 Terminal 插件，兴冲冲敲下 `claude`，结果跳出一个巨大的错误：`command not found`。

那一刻，挫败感通常会让你想直接点那个“卸载”按钮。

**别怕，这是因为 Obsidian 还没拿到你电脑的“地图”。**

### 第一步：安装

在 Obsidian 插件市场搜索 **Terminal**，安装并启用。

![Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵” - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D/CleanShot%25202026-04-20%2520at%252009.06.54.webp)

### 第二步：给黑窗口注入“灵魂”

装完之后，如果你直接在侧边栏敲 `claude`，大概率会看到那个讨厌的错误：`command not found`。

这是因为 Obsidian 作为一个图形软件，它默认是“看不见”你系统里的那些高级工具的。它就像一个被关在房间里的客人，找不到去地下室工具间的路。

我们要做的，是给它画一张精确的“地图”。

#### 1. 找到“门牌号”

打开你电脑自带的终端（注意，不是 Obsidian 里的，是系统原生的），敲下这一行：

```bash
npm config get prefix
```

如果返回的是 `/opt/homebrew` 或 `/usr/local`，记住这个地址。
![Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵” - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D/CleanShot%25202026-04-20%2520at%252009.30.43.webp)

#### 2. 打个“环境补丁”

这是最关键的一步，我们要把这个地址告诉系统的“总管”：

1. 在终端输入 `nano ~/.zshrc`，打开你的配置文件。
2. 划到最下面，新起一行，贴入这句代码：
   `export PATH="$PATH:/opt/homebrew/bin"` （如果第一步返回的是别的地址，请对应修改）。
   ![Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵” - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D/CleanShot%25202026-04-20%2520at%252009.31.28.webp)

3. 按 `Ctrl + O` 保存，再按 `Ctrl + X` 退出。
4. 最后敲一句 `source ~/.zshrc` 让它立即生效。
   ![Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵” - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D/CleanShot%25202026-04-20%2520at%252009.33.09.webp)

#### 3. 检查“登录模式”

回到 Obsidian 的 Terminal 插件设置里：

1. 点击 **「配置 (Profiles)」** 右侧的列表图标，编辑你的默认配置。
2. 找到 **「参数 (Arguments)」** 这一行。
3. **检查一下**：正常情况下，插件的预设应该已经帮你填好了 **`--login`**（或者 `-l`）。如果已经有了，你就不用管它；如果这一行是空的，请手动点“+”号填上去。
   ![Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵” - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D/CleanShot%25202026-04-20%2520at%252009.34.08.gif)

> **为什么这么折腾？**：这一整套动作，其实是给了终端一张“通关绿卡”。参数里的 `--login` 负责告诉终端：请像一个真正的用户一样“登录”我的电脑。而我们刚才在 `.zshrc` 里打的补丁，则是为它准备好的“地图”。
>
> 只有地图和绿卡都到位了，你在侧边栏里敲 `claude`、`gemini` 还是 `opencode`，它们才会真正听你使唤。

![Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵” - 配图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D/20260420095846126.webp)

---

## 高光时刻：瞬移进你的“车间”

一般来说，在左边侧边连，点击即可快速启动 Terminal 窗口。

在这里，你可以通过CD 命令（具体参考[Obsidian 入门28：坐标跳转，让 AI 真正“降临”你的库](/blog/obsidian-terminal-navigation-guide)) 跳转到具体的某个子文件夹，例如写作目录。
![Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵” - 截图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D/CleanShot%25202026-04-21%2520at%252008.51.01.gif)

不过，这里还有一个更直观、连设置都不用翻、CD 命令都不需要输入的办法：

1. 在 Obsidian 左侧的文件列表（File Explorer）里，找到你的 **`Wechat`** 文件夹。
2. 对着它点**右键**。
3. 选那个 **「在此处打开终端 (Open terminal here)」**。

**奇迹发生了**：侧边栏的小黑窗会自动跳出来，而且它的“当前位置”已经稳稳地停在了你的 `Wechat` 目录下。

![Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵” - 截图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D/CleanShot%25202026-04-20%2520at%252009.35.54.gif)

现在，你只需要敲下一句：

```bash
claude
```

Claude 这一次会立刻读取你 `Wechat` 目录下的专属技能。它知道你现在的身份是一名博主，准备开始一场硬核的写作马拉松。这种“局部感知”的效率，是任何全库扫描插件都给不了的。

---

## 多模型大乱斗：在这个窗口里，你是国王

侧边栏终端最大的魅力，就在于这种“全能切换”的自由。

![Obsidian 入门31：Terminal 插件实战, 开启你的“传送阵” - 配图 9](/images/posts/Obsidian%20%E5%85%A5%E9%97%A831%EF%BC%9ATerminal%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E5%BC%80%E5%90%AF%E4%BD%A0%E7%9A%84%E2%80%9C%E4%BC%A0%E9%80%81%E9%98%B5%E2%80%9D/20260420095909036.webp)

我平时会打一套“组合拳”：

- **Claude Code**：虽然我加的是 MiniMax 或 GLM 的“平替油”，但它重构笔记的逻辑依然很稳。
- **Gemini CLI**：当我需要 Google 家那种博学多才的视角时，敲一下 `gemini` 就能无缝接力。
- **OpenCode**：因为这个插件就是电脑原生终端的镜像，所以我还可以非常方便地在这里运行 OpenCode，可以使用一些 OpenCode 提供的一些免费模型。
- **Codex**：如果前面的都卡壳了，我还会请出 ChatGPT 的 Codex 救急。

在这个小小的侧边栏里，你不再是被插件定义的用户，你是指挥这些顶级 AI 的国王。

---

今天的作业：**成功装好 Terminal 插件，并尝试用 `cd` 命令进入一个子文件夹跑通 `claude`。**

> [!note]
> 如果你在 `cd` 进入文件夹时报错，记得检查一下文件夹名字的大小写，终端对这个可是非常敏感的。

别小看这个黑窗口。当你学会了在笔记侧边栏直接操控全世界的 AI，你会发现：你离“数字游民”那种随心所欲的自由，又近了一步。

下一篇，我们来聊聊那个更美观、更适合大多数人的方案：**Claudian 插件**。

动手试试，下期见！

---

## 进阶阅读

- [Obsidian 入门 30:将AI集成进Obsidian侧边栏,选哪一个?](/blog/obsidian-ai-plugin-selection-guide)
- [Obsidian 入门 28：坐标跳转，让 AI 真正“降临”你的库](/blog/obsidian-terminal-navigation-guide)
- [保姆级教程：将 Gemini CLI和Claude code集成到 Obsidian](/blog/%E4%BF%9D%E5%A7%86%E7%BA%A7%E6%95%99%E7%A8%8B%EF%BC%9A%E5%B0%86%20Gemini%20CLI%E5%92%8CClaude%20code%E9%9B%86%E6%88%90%E5%88%B0%20Obsidian)
