---
title: Obsidian入门37：让隐藏的配置「显形」——Symlink 那座桥
date: 2026-04-26
slug: obsidian-symlink-hidden-config
excerpt: Finder里找不到`.claude`目录，每次改Skill配置都要翻终端？用Symlink在Obsidian里建一座桥，让你像管笔记一样管AI配置。
cover: ""
tags:
  - Obsidian
  - 效率工具
  - 编程开发
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门35：装完的 Skill 去哪了？揭秘 .claude 隐藏目录](/blog/Obsidian%20%E5%85%A5%E9%97%A835%EF%BC%9A%E8%A3%85%E5%AE%8C%E7%9A%84%20Skill%20%E5%8E%BB%E5%93%AA%E4%BA%86%EF%BC%9F%E6%8F%AD%E7%A7%98%20.claude%20%E9%9A%90%E8%97%8F%E7%9B%AE%E5%BD%95)。

---

[入门35](/blog/Obsidian%20%E5%85%A5%E9%97%A835%EF%BC%9A%E8%A3%85%E5%AE%8C%E7%9A%84%20Skill%20%E5%8E%BB%E5%93%AA%E4%BA%86%EF%BC%9F%E6%8F%AD%E7%A7%98%20.claude%20%E9%9A%90%E8%97%8F%E7%9B%AE%E5%BD%95)留了个尾巴：`.claude` 目录找到了，但 Finder 里看不到，每次改配置都要翻终端。

![开篇痛点——找不到的文件夹](/images/posts/Obsidian%E5%85%A5%E9%97%A837%EF%BC%9A%E8%AE%A9%E9%9A%90%E8%97%8F%E7%9A%84%E9%85%8D%E7%BD%AE%E3%80%8C%E6%98%BE%E5%BD%A2%E3%80%8D%E2%80%94%E2%80%94Symlink%20%E9%82%A3%E5%BA%A7%E6%A1%A5/Project_Obsidian%25E5%2585%25A5%25E9%2597%25A837_Symlink%25E6%2589%2593%25E9%2580%259AObsidian%25E4%25B8%258EAI%25E5%25B7%25A5%25E4%25BD%259C%25E7%259B%25AE%25E5%25BD%2595_illustration-01_9cb3bb21_20260426.webp)

这个问题确实麻烦。

有没有一种方法，让你在 Obsidian 的文件列表里直接看到这些文件，像管笔记一样管它们？

有的！

用 Symlink。

## Symlink 是什么？

你可以把它理解成一个「映射」，就是在某个位置放一个「指向标」，指向真正文件所在的地方。它不是复制文件，你点开这个指向标，系统自动带你到原文件。

macOS 叫它「替身」，Windows 叫它「快捷方式」，Linux/macOS 终端里叫 Symlink（符号链接）。名字不同，原理一样。

关键是：改了原文件，所有映射过去的地方都生效。你不需要改三份，只改一份就行。

说个具体场景。

你搬进了新办公楼，工位在 A栋 3层 302。前台把工位地址记在本子第一页。找你的人打前台，前台查本子，带他们过去。

后来你换了工位，只需要告诉前台更新这一行字。所有的人还是打前台，前台自动带他们去新地址。

这个「前台本子上的一行字」，就是 Symlink。它本身不是你的工位，但它指向你的工位。你换了工位，改这一行字就够了，所有人自动跟着找到新地方。

![前台比喻——Symlink映射可视化](/images/posts/Obsidian%E5%85%A5%E9%97%A837%EF%BC%9A%E8%AE%A9%E9%9A%90%E8%97%8F%E7%9A%84%E9%85%8D%E7%BD%AE%E3%80%8C%E6%98%BE%E5%BD%A2%E3%80%8D%E2%80%94%E2%80%94Symlink%20%E9%82%A3%E5%BA%A7%E6%A1%A5/Project_Obsidian%25E5%2585%25A5%25E9%2597%25A837_Symlink%25E6%2589%2593%25E9%2580%259AObsidian%25E4%25B8%258EAI%25E5%25B7%25A5%25E4%25BD%259C%25E7%259B%25AE%25E5%25BD%2595_illustration-02_aeaa35c9_20260426.webp)

Obsidian 里建 Symlink，就是把这个前台本子放在 Obsidian 的文件列表里，让你能看见、能改这一行字。

## Mac 上怎么做

在 Obsidian 库根目录建一个文件夹，用终端命令把它链接到 `.claude/`。

假设你的 Obsidian 库在 `~/Documents/MyVault/`，用户名是 `david`。

```bash
# 第一步：在 Obsidian 库根目录建一个可见的文件夹
mkdir -p ~/Documents/MyVault/_ai_configs

# 第二步：把 CLAUDE.md 映射进来
ln -s ~/.claude/CLAUDE.md ~/Documents/MyVault/_ai_configs/CLAUDE.md

# 第三步：把 skills 目录映射进来
ln -s ~/.claude/skills ~/Documents/MyVault/_ai_configs/skills
```

解释一下：

- `mkdir -p` 是新建一个文件夹，`-p` 的意思是「如果已存在就不报错」
- `ln -s` 是创建符号链接，`-s` 代表 symbolic（符号的）
- 格式是：`ln -s 目标路径 链接存放路径`
- `~/.claude/` 是用户主目录下的 `.claude` 文件夹，`~` 是 macOS 表示「我的文件夹」的简写

完成后，打开 Obsidian，在文件列表里就能看到 `_ai_configs/` 这个文件夹，点进去，CLAUDE.md 和 skills/ 都在里面。

你直接双击打开，编辑，保存。AI 工具下一秒读到的就是改过的内容。

## Windows 上怎么做

Windows 10/11 需要先确认开启了「开发者模式」，否则创建符号链接会报权限错误。开启方式：开始菜单 → 设置 → 隐私与安全 → 开发者选项 → 开启「开发者模式」。

假设你的 Obsidian 库在 `C:\Users\david\Documents\MyVault\`。

```powershell
# 第一步：在 Obsidian 库根目录建一个可见的文件夹（用命令提示符或 PowerShell）
# 打开命令提示符，输入：

mkdir C:\Users\david\Documents\MyVault\_ai_configs

# 第二步：把 CLAUDE.md 映射进来
mklink C:\Users\david\Documents\MyVault\_ai_configs\CLAUDE.md C:\Users\david\.claude\CLAUDE.md

# 第三步：把 skills 目录映射进来（/D 表示目录链接）
mklink /D C:\Users\david\Documents\MyVault\_ai_configs\skills C:\Users\david\.claude\skills
```

解释一下：

- `mklink` 是 Windows 创建链接的命令
- 不加参数是创建文件的符号链接，加 `/D` 是创建目录的符号链接
- 路径要用 Windows 的完整格式 `C:\Users\...\`

如果你用的是 PowerShell，语法相同。如果报错「权限不足」，先去设置里开启开发者模式。

## 让 AI 帮你建好这一切

上面的命令不复杂，但你也不用自己跑。

你现在有 AI 了，直接让它帮你执行就行。把下面这段话复制给 Claude Code / Codex / Gemini CLI：

![AI帮你执行命令](/images/posts/Obsidian%E5%85%A5%E9%97%A837%EF%BC%9A%E8%AE%A9%E9%9A%90%E8%97%8F%E7%9A%84%E9%85%8D%E7%BD%AE%E3%80%8C%E6%98%BE%E5%BD%A2%E3%80%8D%E2%80%94%E2%80%94Symlink%20%E9%82%A3%E5%BA%A7%E6%A1%A5/Project_Obsidian%25E5%2585%25A5%25E9%2597%25A837_Symlink%25E6%2589%2593%25E9%2580%259AObsidian%25E4%25B8%258EAI%25E5%25B7%25A5%25E4%25BD%259C%25E7%259B%25AE%25E5%25BD%2595_illustration-04_61e4bfc8_20260426.webp)

> **Prompt（直接复制使用）：**
>
> ```
> 请帮我做以下操作：
>
> 第一步：在 [~/Documents/MyVault/] 这个目录下新建一个文件夹，叫 [_ai_configs]
>
> 第二步：用 Symlink 把 [~/.claude/] 里的 [CLAUDE.md] 和 [skills/] 链接到 [_ai_configs] 里
>
> 如果遇到权限问题，提示我给予相应的权限。
> ```

不管 Mac 还是 Windows，建好之后效果是一样的。

打开 Obsidian 文件列表，你会看到一个 `_ai_configs/` 文件夹（你可以叫它「AI配置」或者其他顺眼的名字）：

```
_ai_configs/
├── CLAUDE.md          ← 你之前要翻终端才能找到的文件
└── skills/            ← 点进去是你的 Skill 列表
    ├── wechat-writer/
    ├── brainstorm/
    └── ...
```

直接双击修改，保存。AI 工具读到的就是新内容。

![Obsidian里的效果——文件夹出现](/images/posts/Obsidian%E5%85%A5%E9%97%A837%EF%BC%9A%E8%AE%A9%E9%9A%90%E8%97%8F%E7%9A%84%E9%85%8D%E7%BD%AE%E3%80%8C%E6%98%BE%E5%BD%A2%E3%80%8D%E2%80%94%E2%80%94Symlink%20%E9%82%A3%E5%BA%A7%E6%A1%A5/Project_Obsidian%25E5%2585%25A5%25E9%2597%25A837_Symlink%25E6%2589%2593%25E9%2580%259AObsidian%25E4%25B8%258EAI%25E5%25B7%25A5%25E4%25BD%259C%25E7%259B%25AE%25E5%25BD%2595_illustration-03_120537cf_20260426.webp)

这个文件夹只在 Obsidian 里显示，不会出现在 Finder 或文件资源管理器里，它是 Obsidian 和真实目录之间的「桥」。

## 适用这些工具，不只 Claude Code

Symlink 这个方法不挑工具。任何放在「隐藏目录」里的配置文件，都可以用同样的思路在 Obsidian 里建一个入口：

| 工具                  | 隐藏配置目录 |
| --------------------- | ------------ |
| Claude Code           | `~/.claude/` |
| Codex                 | `~/.codex/`  |
| Gemini CLI            | `~/.gemini/` |
| Obsidian Agent Client | `.agent/`    |

做法都一样：在 Obsidian 库里建一个文件夹，把对应的目录链接过去。

## 有两点需要注意

**不要删除原文件**。删 symlink 本身不影响原文件（它只是个指向标），但要小心：你在 Obsidian 里通过这个桥**编辑**的内容，直接改的是 `.claude/` 下的原始文件，不是副本。所以不要顺手把 `.claude/` 里的文件删掉。那才是真正会出问题的操作。

**链接断了会怎样**。如果你移动了 Obsidian 库，或者重装了系统，链接可能会失效。Obsidian 会显示这个文件夹打不开。重建即可，只需要让 AI 再重新帮你配一次就行了。

---

所以，下次改 Skill 配置，不用翻文件夹了，在 Obsidian 里直接找到它就行。

## 进阶阅读

- [Obsidian 入门32：Claudian 插件实战 ,拥有这个优雅的AI管家](/blog/Obsidian%20%E5%85%A5%E9%97%A832%EF%BC%9AClaudian%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%20%2C%E6%8B%A5%E6%9C%89%E8%BF%99%E4%B8%AA%E4%BC%98%E9%9B%85%E7%9A%84AI%E7%AE%A1%E5%AE%B6)
- [Obsidian 入门33：Agent Client 插件实战, 你的全能AI辅助官](/blog/Obsidian%20%E5%85%A5%E9%97%A833%EF%BC%9AAgent%20Client%20%E6%8F%92%E4%BB%B6%E5%AE%9E%E6%88%98%2C%20%E4%BD%A0%E7%9A%84%E5%85%A8%E8%83%BDAI%E8%BE%85%E5%8A%A9%E5%AE%98)
- [Obsidian 入门35：装完的 Skill 去哪了？揭秘 .claude 隐藏目录](/blog/Obsidian%20%E5%85%A5%E9%97%A835%EF%BC%9A%E8%A3%85%E5%AE%8C%E7%9A%84%20Skill%20%E5%8E%BB%E5%93%AA%E4%BA%86%EF%BC%9F%E6%8F%AD%E7%A7%98%20.claude%20%E9%9A%90%E8%97%8F%E7%9B%AE%E5%BD%95)
