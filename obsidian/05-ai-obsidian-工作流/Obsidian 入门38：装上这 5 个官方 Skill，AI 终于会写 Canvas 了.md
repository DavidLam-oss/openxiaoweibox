---
title: Obsidian 入门38：装上这 5 个官方 Skill，AI 终于会写 Canvas 了
date: 2026-05-01
slug: obsidian-skills-ai-canvas
excerpt: Obsidian 官方出了 5 个 Skill，专门教 AI 怎么写 Canvas 和数据库。装上一句话就能让 AI 帮你搭知识图谱。
cover: Wechat/published/img/cover-combined.jpg
tags:
  - Obsidian
  - 提示词工程
  - Obsidian插件
  - AI模型
  - 效率工具
status: published
---

## 先看一个效果

![Obsidian 入门38：装上这 5 个官方 Skill，AI 终于会写 Canvas 了 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A838%EF%BC%9A%E8%A3%85%E4%B8%8A%E8%BF%99%205%20%E4%B8%AA%E5%AE%98%E6%96%B9%20Skill%EF%BC%8CAI%20%E7%BB%88%E4%BA%8E%E4%BC%9A%E5%86%99%20Canvas%20%E4%BA%86/CleanShot%25202026-05-01%2520at%252011.19.15.webp)

这不是我画的，也不是我拖进去的...

我跟 AI 说，根据[Obsidian 插件 2.7.3 更新：AI 编排、Mermaid 自动转 PNG，让发布更稳](/blog/Obsidian%20%E6%8F%92%E4%BB%B6%202.7.3%20%E6%9B%B4%E6%96%B0%EF%BC%9AAI%20%E7%BC%96%E6%8E%92%E3%80%81Mermaid%20%E8%87%AA%E5%8A%A8%E8%BD%AC%20PNG%EF%BC%8C%E8%AE%A9%E5%8F%91%E5%B8%83%E6%9B%B4%E7%A8%B3)的内容，生成一张 Canvas。

AI 拿到文章，理解了核心观点和它们之间的逻辑关系，然后直接写了一个 `.canvas` 文件到 vault 里，

```
YourVault/你的文件夹/生成的Canvas.canvas
```

我打开 Obsidian，文件已经在那里了。

没有复制 JSON，没有手动拖文件，没有在任何地方粘贴。

这就是 AI 装上 Skill 之后的真实能力。

---

## 一个 Skill 到底长什么样

在聊五个 Skill 之前，先拆开一个看看里面到底有什么。

拿 json-canvas 来说，它的目录结构简单到只有两层，

```
skills/json-canvas/
├── SKILL.md          # 技能说明书
└── references/
    └── EXAMPLES.md   # 可以直接抄的示例
```

就两个文件，但每一个都管用。

**SKILL.md 是技能说明书。** 它告诉 AI 四件事。

### `.canvas` 文件的基础结构是什么。

两个数组，`nodes` 和 `edges`，一个放节点，一个放连线。就这两样东西，没有别的。

### 节点有哪几种

`text` 是文字卡片，支持 markdown，换行用 `\n` 而不是 `\\n`，这个小细节 AI 经常搞错，Skill 专门写了一句提醒。

`file` 是文件节点，指向 vault 里的笔记或图片，还可以用 `subpath` 指定到某个标题或段落。`link` 是外部链接。`group` 是分组容器，可以把别的节点包进去，配上标签和背景色。

每种节点都有六个必填字段，`id`、`type`、`x`、`y`、`width`、`height`。

ID 是 16 位十六进制随机字符串，坐标和尺寸都是整数。位置没有边界，可以是负数，画布是无限延伸的。

### 怎么连线

每条边要有 `fromNode` 和 `toNode`，引用两个节点的 ID。可以指定从哪一侧出去、从哪一侧进来，top、right、bottom、left 四个方向。可以加箭头，可以加标签。颜色支持六种预设，从红到紫，也可以用十六进制色码。

### 写完之后怎么自查

八条校验规则，ID 不能重复、边必须指向存在的节点、类型只能是 text/file/link/group、颜色只能从预设里选或者用合法 hex、JSON 本身必须能解析。全过了才能交差。

你看，这是在事无巨细地教 AI 「怎么写对一个 Canvas 文件」。

**EXAMPLES.md 是现成的参考答案。** 里面有四个可以直接用的例子，

- 分组看板：To Do / In Progress / Done 三列，用 `group` 节点当容器，`text` 节点当卡片
- 研究画布：文字节点、文件节点、外部链接混在一起，用箭头标出支撑、引用、可视化的关系
- 流程图：Start → Step → Decision，Yes/No 分两条路，失败路径用一个回环箭头指回去

说句心里话，我第一次看到这个结构的时候有点意外。每一条都在解决 AI 真正会犯的错。比如那个 `\n` 和 `\\n` 的提醒，你不写进 Skill，AI 会搞反肯定是十有八九的事情。

![拆解 Skill 结构](/images/posts/Obsidian%20%E5%85%A5%E9%97%A838%EF%BC%9A%E8%A3%85%E4%B8%8A%E8%BF%99%205%20%E4%B8%AA%E5%AE%98%E6%96%B9%20Skill%EF%BC%8CAI%20%E7%BB%88%E4%BA%8E%E4%BC%9A%E5%86%99%20Canvas%20%E4%BA%86/Project_Obsidian%25E5%25AE%2598%25E6%2596%25B9Skill_illustration-01_170c80e5_20260501.webp)

---

## 官方一共五个 Skill

Obsidian 官方维护了一个仓库，[kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)。

它的逻辑很简单，大模型知道 Obsidian 是什么，但不知道怎么写 Obsidian 的各种专属文件。这个仓库给 AI 写了专项教材，让 AI 真正会操作，而不是只会描述。

目前一共五个，

**json-canvas**，`.canvas` 可视化画布。你让它生成一张 Canvas，它就直接写一个文件给你，可以是知识图谱、看板或者流程图。这就是我们刚刚用来演示的那个skill。

**obsidian-markdown**，Obsidian 的专属语法。wikilink `[[笔记]]`、callout `> [!note]`、embed 、frontmatter 属性。这些普通 AI 经常写错格式，Skill 教它写对。

**obsidian-bases**，`.base` 数据库视图。可以根据标签、属性、文件夹自动筛选笔记，按表格、看板、列表或者地图展示。你跟 AI 说「帮我生成一个数据库视图，把所有状态是草稿的笔记都抓出来」，它就帮你写好这个视图文件。

**obsidian-cli**，Obsidian 的命令行接口。可以让 AI 帮你读笔记、创建笔记、搜索 vault 内容，或者在插件开发时让 AI 帮你 reload 插件、截屏看效果。

**defuddle**，网页内容提取。帮 AI 把网页里的广告和导航栏去掉，输出干净的 markdown。你丢一个链接给 AI，AI 自己抓内容，省 token，也省去你复制粘贴的麻烦。

![五个 Skill 卡片](/images/posts/Obsidian%20%E5%85%A5%E9%97%A838%EF%BC%9A%E8%A3%85%E4%B8%8A%E8%BF%99%205%20%E4%B8%AA%E5%AE%98%E6%96%B9%20Skill%EF%BC%8CAI%20%E7%BB%88%E4%BA%8E%E4%BC%9A%E5%86%99%20Canvas%20%E4%BA%86/Project_Obsidian%25E5%25AE%2598%25E6%2596%25B9Skill_illustration-02_eb2f3299_20260501.webp)

---

## 怎么装上

装起来很简单，把这个 Prompt 复制给你的 AI 工具（Claude Code、Copilot、Cursor 都行），它会自动帮你把五个 Skill 全部装好，

```
请帮我把 Obsidian 官方 Skill 安装到我的 Obsidian vault：

1. 访问 https://github.com/kepano/obsidian-skills
2. 帮我安装这 5 个Obsidian的官方 skill 到当前项目的 Skills目录下
3. 确认这五个 Skill 都已就位：json-canvas、obsidian-markdown、obsidian-bases、obsidian-cli、defuddle
4. 我的 Obsidian Vault的路径是：[填写你的 Obsidian 库的文件夹路径]
```

装完之后，你就可以像开头演示的那样，直接跟 AI 说「根据这篇文章生成一张 Canvas」，或者「帮我把所有草稿笔记整理成一个 bases 视图」。

![一键安装](/images/posts/Obsidian%20%E5%85%A5%E9%97%A838%EF%BC%9A%E8%A3%85%E4%B8%8A%E8%BF%99%205%20%E4%B8%AA%E5%AE%98%E6%96%B9%20Skill%EF%BC%8CAI%20%E7%BB%88%E4%BA%8E%E4%BC%9A%E5%86%99%20Canvas%20%E4%BA%86/Project_Obsidian%25E5%25AE%2598%25E6%2596%25B9Skill_illustration-03_5dc4d3d4_20260501.webp)

如果你用的是 Claude Code或者其他 CLI 工具，Skill 会被自动发现的。

---

Skill 让 AI 从「懂概念」变成「会操作」。

它让 AI 真正理解你每天在用的东西是什么样子：Canvas 文件怎么写、Bases 怎么配置、wikilink 怎么连，AI 知道之后，你说的每一句话就不再是描述，而是指令。

这篇文章选了 json-canvas 来演示，因为它最直观。obsidian-bases 其实同样值得试试，它能让 AI 帮你生成数据库视图，把符合特定条件的笔记都抓出来，按表格或者看板展示。

回到开头那张图。我当时的第一反应是，我之前怎么不知道可以这样做，哈哈！

希望你也是。

![老友分享](/images/posts/Obsidian%20%E5%85%A5%E9%97%A838%EF%BC%9A%E8%A3%85%E4%B8%8A%E8%BF%99%205%20%E4%B8%AA%E5%AE%98%E6%96%B9%20Skill%EF%BC%8CAI%20%E7%BB%88%E4%BA%8E%E4%BC%9A%E5%86%99%20Canvas%20%E4%BA%86/Project_Obsidian%25E5%25AE%2598%25E6%2596%25B9Skill_illustration-04_48c227b9_20260501.webp)
