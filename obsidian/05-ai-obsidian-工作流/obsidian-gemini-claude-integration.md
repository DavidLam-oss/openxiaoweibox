---
title: 保姆级教程：将 Gemini CLI和Claude code集成到 Obsidian
date: "2025-11-23"
tags:
  - Obsidian
  - 效率工具
  - AI模型
  - 编程开发
excerpt: >-
  我分享了将 Gemini CLI 和 Claude Code 集成到 Obsidian 的实践。记录了从 Python 弯路到 Node.js
  正确安装，以及解决 Obsidian 终端 PATH 问题的关键步骤，希望能助你避坑。
---

## 背景

我的目标很简单：希望在 Obsidian 里，能够直接调用 Google 的 `Gemini` 和 Anthropic 的 `Claude code`，让 AI 辅助更自然地融入日常的写作和记录流程。

不过，这个过程比预想的要曲折一些。我先是尝试了 Python 的安装方式，遇到些麻烦后才转向 Node.js，最后解决了 Obsidian 内部环境变量（PATH）的识别问题。这篇文章想做的，就是把这个过程分享出来，希望能让有类似需求的朋友更顺利一些。

## 第一阶段：关于 Python 的一次弯路和反思

**最初的想法：过于依赖 AI 建议**

事情的开端，是我向 AI (Comet) 询问“如何安装 Gemini CLI”，它提供了一条基于 Python (`pip`) 的安装指引。出于习惯和信任，我便按照这个路径开始了尝试。

但很快，过程变得不那么顺利：

1.  **系统权限的限制**：在 macOS 上直接使用 `pip install` 时，会因为系统对 Python 环境的保护而报错。
2.  **棘手的版本兼容**：我尝试用 `pipx` 来创建一个独立环境，但又遇到了 Python 3.14 和 `protobuf` 库之间的兼容问题。
3.  **找错了对象**：花了不少功夫，通过调整 Python 版本总算安装成功后，却发现这个 `gemini-cli` 并非 Google 官方版本，而是一个社区早期的项目。

**一个重要的提醒：与 AI 协作，也需要独立判断**

后来，我暂时离开 AI 对话框，直接用 Google 搜索 "gemini cli"，搜索结果的第一条就是官方的 GitHub 仓库，里面清楚地说明了安装方式是基于 Node.js。

这件事让我有了一个很重要的提醒：AI 是个很有用的助手，但在协作中，我们自己还是需要保留一些主动性和验证的习惯。当 AI 给出的方案变得越来越复杂，或者报错越来越多的时候，或许说明我们该停下来，检查一下最初的方向。有时候，回到官方文档这种最朴素的查询方式，反而效率更高。

**尽信书则不如无书，尽信 AI 则不如无 AI**

## 第二阶段：正确的安装路径 (Node.js)

如果你的设备是 Mac，可以参考下面的步骤。

### 1. 全局安装 CLI 工具

在系统的终端（Terminal 或 iTerm）里，分别运行：

```bash
# 安装 Google Gemini CLI
npm install -g @google/gemini-cli

# 安装 Claude Code
npm install -g claude-code
```

### 2. 验证安装

安装完成后，在系统终端里输入下面的命令，如果能顺利进入各自的交互界面，就说明安装好了。

```bash
gemini
# 或
claude code
```

## 第三阶段：在 Obsidian 中集成（关键的一步）

这是很多人容易遇到的一个环节。即便系统终端可以正常使用了，Obsidian 的插件里可能还是会提示找不到命令。

### 第一步：安装 Terminal 插件

在 Obsidian 的“设置” -> “第三方插件” -> “社区插件市场”中，搜索并安装 **"Terminal"** 插件，然后启用它。

### 第二步：问题分析与修正

在 Obsidian 的 Terminal 插件里输入 `gemini`，如果提示 `zsh: command not found: gemini`，这通常是因为插件启动的 Shell 环境，没有加载到系统完整的环境变量（PATH）。

**解决方案：**

1.  **找到工具的实际安装路径**：在系统终端运行 `npm config get prefix`。如果使用 Homebrew 安装的 Node，路径通常是 `/opt/homebrew`。
2.  **修正 PATH**：将下方这行配置，添加到你所使用的 Shell 配置文件中（例如 `.zshrc` 或 `.bash_profile`）。这样可以确保每次启动 Shell 时，都能找到正确的路径。

    ```bash
    export PATH="$PATH:/opt/homebrew/bin"
    ```

但是上面的方法在每次关闭 OB 的 terminal 窗口后，再次开启需要又输入一遍上面的命令。

通过以下方法可以实现不用在终端里每次临时输入 `export` 命令，**一劳永逸**：

1. **编辑配置文件**： 在系统终端（或者 Obsidian 终端）中输入：

   ```
   nano ~/.zshrc
   ```

2. **添加路径**： 使用键盘方向键移到文件最底部，新起一行，粘贴以下内容：

   ```
   export PATH="$PATH:/opt/homebrew/bin"
   ```

3. **保存并退出**：
   - 按 `Ctrl + O` （写入保存），然后按 `Enter` 确认文件名。
   - 按 `Ctrl + X` （退出编辑器）。

4. **立即生效**： 执行以下命令让配置立即生效：

   ```
   source ~/.zshrc
   ```

### 第三步：检验成果

重启 Obsidian 和它的 Terminal 插件，再次输入 `gemini`。这时候，那个熟悉的像素风格 LOGO 应该就会显示出来了。

## 最终的效果

现在，我可以在 Obsidian 里随时唤起：

1.  **Claude Code**：帮我构思代码、分析项目。
    ![保姆级教程：将 Gemini CLI和Claude code集成到 Obsidian - 配图 1](/images/posts/202511230721592.webp)

2.  **Gemini**：用来做一些信息查询或快速的文本生成。
    ![保姆级教程：将 Gemini CLI和Claude code集成到 Obsidian - 配图 2](/images/posts/202511230721554.webp)

整个过程都在同一个窗口内完成，不再需要切换和复制粘贴，实现了自己设想中那种“All-in-One”的工作流。

> **结尾的一点想法**：有时候我们花时间去了解一些技术细节，目的不是技术本身，而是为了搭建一个更顺畅、更舒服的工作流。而在如今的环境下，在参考 AI 建议的同时，也保持独立的审视和判断，或许是一个值得我们慢慢养成的好习惯。
