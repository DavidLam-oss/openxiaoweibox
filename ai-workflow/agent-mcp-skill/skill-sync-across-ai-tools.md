---
title: 一套 Skill 写一处，三个工具同时用
date: 2026-02-12T00:00:00.000Z
slug: skill-sync-across-ai-tools
excerpt: 三个工具，三套 Skill 目录，改一处要改三处。我用软链接让它们共享同一份 Skill。
cover: /Users/davidlin/Desktop/CleanShot 2026-02-12 at 11.22.37.png
tags:
  - 效率工具
  - AI模型
  - 服务器运维
  - 提示词工程
status: published
---

上次写过一篇 [在Claude Code 里用 Skills 要付费？那我用 Gemini CLI 免费白嫖](/blog/%E5%9C%A8Claude%20Code%20%E9%87%8C%E7%94%A8%20Skills%20%E8%A6%81%E4%BB%98%E8%B4%B9%EF%BC%9F%E9%82%A3%E6%88%91%E7%94%A8%20Gemini%20CLI%20%E5%85%8D%E8%B4%B9%E7%99%BD%E5%AB%96)，当时的做法很简单：把 Claude Code 的 Skill 用软链接指到 Gemini CLI 的目录下，两边就通了。

后来 Codex 也加入了日常——它跑异步任务特别顺手，慢慢就离不开了。

三个工具，三套 Skill 目录。有一次我在 Claude Code 里改了 `code-reviewer` 这个 Skill，加了几条新规则，改完挺满意。结果切到 Codex 跑任务，发现它用的还是旧版。

改一个地方，要改三处。这事我忍了大概两天。

> 我的 Gemini CLI被封了...... 正在想办法看看能不能救回来。
> [突发 403！Google 动手了，我的 Antigravity 全线「断供」](/blog/%E7%AA%81%E5%8F%91%20403%EF%BC%81Google%20%E5%8A%A8%E6%89%8B%E4%BA%86%EF%BC%8C%E6%88%91%E7%9A%84%20Antigravity%20%E5%85%A8%E7%BA%BF%E3%80%8C%E6%96%AD%E4%BE%9B%E3%80%8D)

![一套 Skill 写一处，三个工具同时用 - 配图 1](/images/posts/%E4%B8%80%E5%A5%97%20Skill%20%E5%86%99%E4%B8%80%E5%A4%84%EF%BC%8C%E4%B8%89%E4%B8%AA%E5%B7%A5%E5%85%B7%E5%90%8C%E6%97%B6%E7%94%A8/20260212112321289.webp)

---

## 先看看各家的「规矩」

这三个工具都支持自定义 Skill（或者叫指令、规则），但存放的位置各不相同：

| 工具        | 全局目录            | 全局指令文件          | Skill 结构                             |
| ----------- | ------------------- | --------------------- | -------------------------------------- |
| Claude Code | `~/.claude/skills/` | `~/.claude/CLAUDE.md` | 每个 Skill 一个文件夹，入口 `SKILL.md` |
| Codex CLI   | `~/.codex/`         | `~/.codex/AGENTS.md`  | 每个 Skill 一个文件夹，入口 `SKILL.md` |
| Gemini CLI  | `~/.gemini/`        | `~/.gemini/GEMINI.md` | 每个 Skill 一个文件夹，入口 `SKILL.md` |

它们有一个共同点：都是基于文件系统的。

文件在磁盘上，就能用软链接。

![一套 Skill 写一处，三个工具同时用 - 配图 2](/images/posts/%E4%B8%80%E5%A5%97%20Skill%20%E5%86%99%E4%B8%80%E5%A4%84%EF%BC%8C%E4%B8%89%E4%B8%AA%E5%B7%A5%E5%85%B7%E5%90%8C%E6%97%B6%E7%94%A8/20260212112352182.webp)

---

## 唯一真源 + 软链接

**选一个目录当「老大」，其他目录都指向它。**

我选的是 Claude Code 的 `~/.claude/skills/`，原因也简单——它的 Skill 体系最成熟，目录结构最规范，而且官方明确支持软链接。

同步后的关系是这样的：

```
~/.claude/skills/          ← 唯一真源，所有 Skill 的实体文件
     ↓ 软链接
~/.codex/skills/           → ~/.claude/skills/
~/.gemini/skills/          → ~/.claude/skills/   (自建目录)
```

如果你还没有给某个 CLI 创建 skill，可能就还没有 skills目录，例如Gemini CLI 本身没有 `skills/` 目录，但你可以自己建一个，把 Skill 链接过去。

> 不熟悉软链接也没关系。你可以把它理解成 Windows 的「快捷方式」，或者 macOS Finder 里的「替身」。它不是复制，而是一个指向原文件的引用。改了原文件，所有链接自动跟着变。

效果：

- 新写一个 Skill，只放在 `~/.claude/skills/` 里
- Codex 和 Gemini CLI 自动就能用
- 改了一处，三处都生效

---

## 该同步什么，不该同步什么

这里有个前提：我只同步**全局级别**的 Skill。

什么是全局 Skill？就是不依赖任何特定项目的通用能力。比如 `brainstorming`（头脑风暴）、`code-reviewer`（代码审查）、`skill-creator`（创建新 Skill）这些，不管在哪个项目里都用得上。

项目级别的 Skill 呢？不需要同步。

因为 Claude Code、Codex 这些工具启动时，会同时读取全局目录和项目目录：

```
全局：~/.claude/skills/          ← 通用 Skill（同步的）
项目：<project>/.claude/skills/  ← 项目专属 Skill（独立的）
```

> 不懂代码也没关系，这段的意思就是：通用的统一管，专用的各管各。

所以分工很清楚：

| 级别 | 管理方式          | 举例                         |
| ---- | ----------------- | ---------------------------- |
| 全局 | 唯一真源 + 软链接 | brainstorming、code-reviewer |
| 项目 | 保持独立，不同步  | wechat-writer、项目特定规则  |

如果某个 Skill 想跨项目复用但不放全局，同样可以用软链接指过去。

---

## 实操：一键同步

手动一个一个建软链接当然可以，但 Skill 多了之后还是麻烦。

我用 Raycast 写了两个快捷命令：

- **Sync AI Skills**：扫描 `~/.claude/skills/` 下所有 Skill，为 Codex 和 Gemini CLI 批量创建软链接
- **Clean Broken Links**：清理那些指向已删除 Skill 的失效链接

核心逻辑就是一个循环：

```bash
# 遍历源目录下的每个 Skill
for skill in ~/.claude/skills/*/; do
    skill_name=$(basename "$skill")
    # 为每个目标工具创建软链接
    ln -s "$skill" ~/.codex/skills/"$skill_name"
    ln -s "$skill" ~/.gemini/skills/"$skill_name"   # 自建目录
done
```

> 这段代码是简化版，实际脚本还有安全检查。不想看代码的话，知道「一个循环搞定」就行。

有几个细节值得注意：

1. **不覆盖实体目录**：如果目标位置已经有一个真实的 Skill 文件夹（不是软链接），保持原样，不动它
2. **跳过未安装的工具**：如果你没装 Codex，脚本不会报错，直接跳过
3. **定期清理**：删掉一个 Skill 后，其他工具那边的软链接就「断了」，需要清理

同步完成后，目录长这样：

```
~/.claude/skills/
├── brainstorming/        ← 实体目录
├── code-reviewer/        ← 实体目录
├── skill-creator/        ← 实体目录
└── ...

~/.codex/skills/
├── brainstorming → ~/.claude/skills/brainstorming
├── code-reviewer → ~/.claude/skills/code-reviewer
├── skill-creator → ~/.claude/skills/skill-creator
└── ...

~/.gemini/skills/
├── brainstorming → ~/.claude/skills/brainstorming
├── code-reviewer → ~/.claude/skills/code-reviewer
└── ...                       (自建目录，手动链接)
```

一边是实体，另外两边全是软链接。改了实体，链接自动跟着变。

顺便提一句：Codex 对 Skill 文件夹的软链接支持没问题，但对单独的 `.md` 文件有个已知的小 bug，偶尔会读不到。所以建议把 Skill 组织成文件夹而不是散装的 `.md` 文件，这样最稳。

我用的是 Raycast 来触发，但这不是唯一的方式。你可以用 Alfred、用 Shell alias、用 cron 定时任务，甚至直接手动跑脚本——选自己顺手的就好。

![一套 Skill 写一处，三个工具同时用 - 配图 3](/images/posts/%E4%B8%80%E5%A5%97%20Skill%20%E5%86%99%E4%B8%80%E5%A4%84%EF%BC%8C%E4%B8%89%E4%B8%AA%E5%B7%A5%E5%85%B7%E5%90%8C%E6%97%B6%E7%94%A8/20260212112428624.webp)

## 写在最后

从最早只用 Claude Code 一个工具，到后来加了 Gemini CLI，再到现在 Codex 也加入日常，工具确实越来越多。

但管理方式反而越来越简单了。

现在每次写完一个新 Skill，跑一下同步，三个工具同时就位。这种「改一处，处处生效」的感觉，用过就回不去了。

说到底就四个字：**一处维护，处处生效。**

工具会继续变多，但加一个工具不过是脚本里多一行路径的事。
