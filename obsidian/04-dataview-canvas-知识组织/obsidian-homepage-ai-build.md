---
title: 零代码我的 hompage：我的Obsidian魔改之旅—— 如何用AI助手构建会自我进化的数字主页
date: "2025-04-06"
excerpt: >-
  分享如何作为零代码小白，利用 AI 辅助编写 DataviewJS 代码，结合 Homepage 和 Heatmap Tracker 插件，在
  Obsidian 中打造包含热力图、那年今日和随机推荐的“自我进化”数字主页。
tags:
  - Obsidian
  - AI编程
  - 内容创作
---

## 缘起：一场知识管理的觉醒

2024年初，我陷入知识焦虑的泥潭：  
• 有道云笔记、印象笔记、wolai和本地、邮箱等平台散落着2000+碎片笔记  
• 学术文献与灵感随笔在文件夹里交织  
• 最痛心的是——这几年的笔记竟在硬盘深处「沉睡」

直到遇见Obsidian，这个以「双向链接」著称的笔记工具，让我开启了知识管理的范式革命。其本地储存、markdown 格式的特性和丰富的第三方插件生态让我决定后面将 Obsidian 作为笔记助力系统。

今天，决定搭建一个主页并在主页上搭建一些工具去记录和串联 Obsidian 仓库内的所有笔记。最终的效果如下图所示：

![零代码我的 hompage：我的Obsidian魔改之旅—— 如何用AI助手构建会自我进化的数字主页 - 配图 1](/images/posts/202504061912517.webp)

## 技术实现：Obsidian 丰富的插件

主要借助 3 个插件实现：

**1. 主页本页（Homepage插件）**  
• 实时年度进度追踪  
• 跨文档统计看板  
• 智能缓存加速引擎

**2. 创作热力图（Heatmap Tracker插件）**  
• 中英文混合字数统计  
• 创作强度五级可视化  
• 自动/手动刷新数据

**3. 记忆引擎（Dataview插件及）**  
• 时光机：那年今日  
• 量子随机：每日盲盒推荐

## 开发手记：与AI的多次对话

作为零代码小白，我的实现方式如下：

### 热力图的需求拆解

• 给AI投喂Heatmap Tracker example code  
• 用思维导图描述理想中的热力图样式  
• 确定「按字数深浅着色」的核心需求

```css
我希望基于这份代码编写一个我自己的版本。

## 背景

我正在使用 Obsidian 进行日常的写作，记录随笔、日记、学习笔记等，每篇文章的内容、格式和命名都可能不一样。

## 需求

我想基于这份代码实现像 github 热力图类似的效果。具体如下：

- 统计整个仓库的所有内容，而不是固定与某个文件夹。仓库名称为：“MyVault”

- 统计每篇文章的字数，计算Markdown内容的纯文本字数。中文按照字符计算，英文按照单词计算。

- 字数越多，热力图亮度越高；字数越少，热力图亮度越低

    - 0-100 字：最低亮度

    - 100-500 字：低亮度

    - 500-1000 字：中亮度

    - 1000-3000 字：高亮度

    - 3000+ 字：最高亮度

- 以文件创建日期为日期基准。同时考虑文件的修改日期，若文件进行了修改，则只统计修改的字数。

    - 修改的字数的定义为：在原有的字数基础上，增加或者减少的字数的绝对值

- 过滤掉配置文件、模板、插件、主题等文件夹

- 统计最近 3 年的文件（以最新一次修改时间为准计算）

- 在热力图附近的合适位置添加统计信息（考虑美观和空间）

    - 今日码字：xx（当日新增或者修改的总字数）

    - 总共码字：xx（如果数字过长，请考虑合适的展示方式）

    - 平均每日码字：xx


## 补充事项

- 目前主要是使用 Obsidian 的 dataview 插件和 Heatmap Tracker这 2 个插件进行实现。我们不是要写一个新插件，要基于以上 2 个插件进行，所以代码应该为 dataview js 代码

- 若考虑计算修改字数，你可以在 Obsidian 中新建一个本地.md文件。此需求如果过于复杂，则可忽略此需求，关注新建文件即可

- 无需考虑用户配置选项，届时若有需要，我可以直接修改代码里面的配置

- 界面位置无需考虑。将使用以上提到的 2 个插件配合实现

- 刷新机制为实时更新，最后修改为一天更新一次（如果有需要也可以手动刷新）

- 首次使用，加载 loading 即可
```

### 那年今日

同样是将需求和example 的 code 一起投喂给 AI，然后最终的语句如下

```js
// 今天是2025年4月6日，2025 年已经过去了95天。
今天是`=dateformat(date(today), "yyyy年M月d日")`，`=date(today).year` 年已经过去了`=(date(today)-date(date(today).year + "-01-01")).days`天。


// 你总共在42天留下了足迹，继续加油！
dataviewjs
const pages = dv.pages('""')
const dates = [...new Set(pages.map(p => p.file.ctime.toISODate()))]
dv.paragraph(`- 你总共在${dates.length}天留下了足迹，继续加油！`)

// 那年今日table
TABLE WITHOUT ID
    file.link AS "Article",
    dateformat(file.ctime, "yyyy-MM-dd (EEE)") AS "创建时间",
    dateformat(file.mtime, "yyyy-MM-dd HH:mm:ss") AS "最后修改时间"
FROM ""
WHERE dateformat(file.ctime, "MM-dd") = dateformat(date(today), "MM-dd")
SORT file.ctime DESC
LIMIT 100
```

### 今日随机推荐

实现的语句如下

```js
// 获取所有有效笔记（排除模板和系统文件）
const allNotes = dv
  .pages('""')
  .file.filter(
    (f) =>
      f.path.endsWith(".md") &&
      !f.path.includes("Templates/") &&
      !f.path.includes("_attachments/"),
  );

// 基于当天日期生成随机种子（确保每日结果一致）
const today = new Date().toISOString().slice(0, 10); // "YYYY-MM-DD"
const seed = parseInt(today.replace(/-/g, ""));
const randomIndex = Math.floor(Math.sin(seed) * allNotes.length);

// 获取随机笔记
const randomNote = allNotes[randomIndex];

// 显示可点击的链接（带友好提示）
dv.header(2, "今日随机推荐");
dv.paragraph(`[[${randomNote.path}|${randomNote.name}]]`);
dv.paragraph(
  `*"${randomNote.path.split("/").slice(0, -1).join("/")}" 中的笔记*`,
);
```

具体的效果，如一开始的图片所示，希望你也喜欢！
