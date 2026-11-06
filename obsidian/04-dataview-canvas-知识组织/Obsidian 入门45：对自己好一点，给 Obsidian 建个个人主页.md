---
title: Obsidian 入门45：对自己好一点，给 Obsidian 建个个人主页
date: 2026-05-13
slug: obsidian-homepage-dashboard
excerpt: 给自己建个 Obsidian 主页，每次打开都有一个熟悉的起点。
cover: Wechat/published/img/cover-combined.jpg
tags:
  - Obsidian
  - 副业与出海
  - 效率工具
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理和收集、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过上一篇，可以先看 [Obsidian 入门44：YouTube 视频字幕剪藏实战——能看但剪不下来](/blog/Obsidian%20%E5%85%A5%E9%97%A844%EF%BC%9AYouTube%20%E8%A7%86%E9%A2%91%E5%AD%97%E5%B9%95%E5%89%AA%E8%97%8F%E5%AE%9E%E6%88%98%E2%80%94%E2%80%94%E8%83%BD%E7%9C%8B%E4%BD%86%E5%89%AA%E4%B8%8D%E4%B8%8B%E6%9D%A5)。

之前在 Obsidian 入门系列里提过我的个人主页，有朋友留言问是怎么做的。

其实没什么玄乎的，就是装了个插件，再堆几个 Dataview 查询。

但被问起来我才意识到，这个需求很多人都有。笔记越记越多，每次打开软件，不知道从哪看起。

所以分享一下我的做法，给你提供个思路。

---

## 从一个需求开始

先说说我的场景。

我用 Obsidian 写东西，每天的节奏大概是，打开软件，看一眼昨天写了什么，切到项目文件夹，然后继续。

听起来很正常吧？

但问题出在「打开软件」这一步。Obsidian 默认会打开你上次关闭时的文件，这个设计很合理，但我经常搞不清自己上次看到哪了。

而且，如果我只是想「随便看看最近在写什么」，这个默认行为就帮不上忙了。

我的需求很简单，每次打开 Obsidian，第一眼能看到一个全景画面，最近在写什么、写了多少、今天有什么值得回顾的东西。

然后我找到了 HomePage（读作后母佩吉） 这个插件，可以理解为就是主页。

它的核心功能只有两个。一个是设置一个笔记作为启动页，另一个是当你关闭所有标签页时自动回到这个页面。就这么简单，没有多余的功能。装上之后，我把 My Homepage.md 设成了我的大本营。

安装就更简单了，社区插件里搜 HomePage，安装启用。

![Obsidian 入门45：对自己好一点，给 Obsidian 建个个人主页 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A845%EF%BC%9A%E5%AF%B9%E8%87%AA%E5%B7%B1%E5%A5%BD%E4%B8%80%E7%82%B9%EF%BC%8C%E7%BB%99%20Obsidian%20%E5%BB%BA%E4%B8%AA%E4%B8%AA%E4%BA%BA%E4%B8%BB%E9%A1%B5/CleanShot%25202026-05-13%2520at%252008.10.01.webp)

然后在设置里指定你的主页笔记就行。支持指定一个文件做为主页，也可以做其他设定，比如随机笔记、日记或者周记。

没有复杂的配置项，设完就能跑。

我建议把第一个“Open on startup”和“Open when empty”打开，这样的话你启动 Obsidian 或者关闭了所有标签页，就会自动回到设定的主页。

![Obsidian 入门45：对自己好一点，给 Obsidian 建个个人主页 - 截图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A845%EF%BC%9A%E5%AF%B9%E8%87%AA%E5%B7%B1%E5%A5%BD%E4%B8%80%E7%82%B9%EF%BC%8C%E7%BB%99%20Obsidian%20%E5%BB%BA%E4%B8%AA%E4%B8%AA%E4%BA%BA%E4%B8%BB%E9%A1%B5/CleanShot%25202026-05-13%2520at%252008.19.33.webp)

---

## 我的主页长什么样

我的主页分成三个区块，每个区块解决一个具体问题。

![Obsidian 入门45：对自己好一点，给 Obsidian 建个个人主页 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A845%EF%BC%9A%E5%AF%B9%E8%87%AA%E5%B7%B1%E5%A5%BD%E4%B8%80%E7%82%B9%EF%BC%8C%E7%BB%99%20Obsidian%20%E5%BB%BA%E4%B8%AA%E4%B8%AA%E4%BA%BA%E4%B8%BB%E9%A1%B5/CleanShot%25202026-05-13%2520at%252008.37.39.webp)

### 第一个区块：足迹

最醒目的部分是一张热力图，类似 GitHub 那种绿格子，记录我的写作活动。哪一天写了多少字，颜色深浅一目了然。

这个热力图是我用 Heatmap插件配合 我自己写的一个本地插件实现的。

它读取本地的 activity-log.jsonl 文件，把每天的写作数据汇总成热力图。下面还有几行统计，今日最高字数、总字数、今年活跃了多少天。最底下是一行年份进度：「2026 年已经过去了 X 天」。

说实话，这个实现有点重。我写的时候是因为当时没有现成的方案，现在社区里已经有了更好的选择。

比如 Activity Heatmap 插件，装上就能自动追踪文件变化，生成同样的热力图；

还有 Activity Graph 插件，功能更丰富，支持嵌入到笔记正文、追踪 Tasks 插件的完成情况，还有好几种视图模式可以切换。

如果你也想在主页里放一张热力图，我会建议直接从社区装一个现成的插件，省心很多。

热力图下面还有两行文字，是 Dataview 自动算出来的，今年写了多少天、每天的统计数据。这些都是机器干的活，你只需要写一次查询，它就每天自动更新。

我是用的语法放在下面供你参考。你可以把这一段和你的需求提供给你的 AI，让它参考之后给出你的版本

后面2个区块也是同样的做法：把他们交给你的 AI。

```
今天是`=dateformat(date(today), "yyyy年M月d日")`，`=date(today).year` 年已经过去了`=(date(today)-date(date(today).year + "-01-01")).days`天。


dataviewjs
// --- 配置 ---
const LOG_FILE_PATH = "_internal/activity-log.jsonl"; // 确认日志文件路径

// --- 主逻辑 ---
(async () => {
    let logContent = "";
    try {
        logContent = await dv.io.load(LOG_FILE_PATH);
    } catch (e) {
        dv.paragraph("❌ 无法加载活动日志文件。");
        console.error("Error loading log file for footprint:", e);
        return;
    }

    if (!logContent || logContent.trim() === "") {
        dv.paragraph("- 你今年还没有留下任何足迹。");
        return;
    }

    // 获取当前年份
    const currentYear = moment().format('YYYY'); // 或者 new Date().getFullYear().toString();

    const parsedLogEntries = [];
    const lines = logContent.trim().split('\n');
    for (const line of lines) {
        if (line.trim() === "") continue;
        try {
            const entry = JSON.parse(line);
            // 校验：确保有 date 字段且格式为 YYYY-MM-DD
            if (entry && entry.date && typeof entry.date === 'string' && entry.date.length === 10) {
                 parsedLogEntries.push(entry);
            }
        } catch (e) {
            // console.warn(`Skipping bad JSON line in footprint calculation: ${line}`, e);
        }
    }

    // **修改点：过滤出当年的条目**
    const thisYearEntries = parsedLogEntries.filter(entry => entry.date.startsWith(currentYear + '-'));

    if (thisYearEntries.length === 0) {
        dv.paragraph(`- 你在 ${currentYear} 年还没有留下足迹。`);
        return;
    }

    // 提取当年的所有活跃日期并去重
    const uniqueThisYearDates = new Set(thisYearEntries.map(entry => entry.date));

    // 获取当年唯一活跃日期的数量
    const footprintDaysThisYear = uniqueThisYearDates.size;

    // 显示结果
    dv.paragraph(`- 你在 ${currentYear} 年总共留下了 ${footprintDaysThisYear} 天的足迹，继续加油！`);

})().catch(err => {
    dv.paragraph("❌ 计算当年足迹天数时出错: " + err.message);
    console.error("Error calculating this year's footprint days:", err);
});
```

关于 Dataview，我们之前也介绍过：

- [Obsidian 入门22：认识 Dataview 插件，给你 3 段直接复制的指令，打造全自动仪表盘](/blog/Obsidian%20%E5%85%A5%E9%97%A822%EF%BC%9A%E8%AE%A4%E8%AF%86%20Dataview%20%E6%8F%92%E4%BB%B6%EF%BC%8C%E7%BB%99%E4%BD%A0%203%20%E6%AE%B5%E7%9B%B4%E6%8E%A5%E5%A4%8D%E5%88%B6%E7%9A%84%E6%8C%87%E4%BB%A4%EF%BC%8C%E6%89%93%E9%80%A0%E5%85%A8%E8%87%AA%E5%8A%A8%E4%BB%AA%E8%A1%A8%E7%9B%98)
- [Obsidian 入门23：别让待办烂在笔记里！用 Dataview 自动汇总你所有的 TODO](/blog/Obsidian%20%E5%85%A5%E9%97%A823%EF%BC%9A%E5%88%AB%E8%AE%A9%E5%BE%85%E5%8A%9E%E7%83%82%E5%9C%A8%E7%AC%94%E8%AE%B0%E9%87%8C%EF%BC%81%E7%94%A8%20Dataview%20%E8%87%AA%E5%8A%A8%E6%B1%87%E6%80%BB%E4%BD%A0%E6%89%80%E6%9C%89%E7%9A%84%20TODO)
- [Obsidian 入门24：不会写 Dataview 代码？教你一招，让 AI 成为你的专属“程序员”](/blog/Obsidian%20%E5%85%A5%E9%97%A824%EF%BC%9A%E4%B8%8D%E4%BC%9A%E5%86%99%20Dataview%20%E4%BB%A3%E7%A0%81%EF%BC%9F%E6%95%99%E4%BD%A0%E4%B8%80%E6%8B%9B%EF%BC%8C%E8%AE%A9%20AI%20%E6%88%90%E4%B8%BA%E4%BD%A0%E7%9A%84%E4%B8%93%E5%B1%9E%E2%80%9C%E7%A8%8B%E5%BA%8F%E5%91%98%E2%80%9D)

### 第二个区块：那年今日

这个区域是一个 Dataview 查询，找出所有创建日期是「今天」的笔记，按时间倒序排列。

效果很奇妙。比如今天打开 Obsidian，看到「一年前的今天我写了一篇关于 X 的文章」「三年前的今天我刚开始学 Y」。有时候你会惊讶，原来我那时候就在想这个事情了。

这个功能不复杂，就几行 Dataview 代码。但它带来的体验是一种连续感，你的笔记库像一条流动的河，每一天都被过去某一天的自己提醒着。

````
## 那年今日
今天是 `=dateformat(date(today), "yyyy年M月d日")`，那年今日，你曾记录过：

```dataview
TABLE WITHOUT ID
    file.link AS "Article",
    dateformat(file.ctime, "yyyy-MM-dd (EEE)") AS "创建时间",
    dateformat(file.mtime, "yyyy-MM-dd HH:mm:ss") AS "最后修改时间"
FROM ""
WHERE dateformat(file.ctime, "MM-dd") = dateformat(date(today), "MM-dd")
SORT file.ctime DESC
LIMIT 100
````

### 第三个区块：今日随机推荐

这个是我最喜欢的一个小设计。

如果从现有笔记里随机抽一篇，你今天可能看到任何东西。但问题是，如果每次刷新都换一篇，那就没有「今天」的感觉了。

所以我的做法是，基于当天日期生成一个随机种子。今天打开，看到的是笔记 A。明天打开，看到的是笔记 B。同一天内，不管你刷新多少次，看到的都是同一篇。这就形成了一个有趣的组合，稳定性加上意外性。

有时候你会翻到自己都快忘记写过的笔记，然后重新读一遍，还挺有意思的。

```
dataviewjs
// 获取所有有效笔记（排除模板和系统文件）
const allNotes = dv.pages('""').file
    .filter(f => f.path &&
           f.path.endsWith(".md") &&
           !f.path.includes("Templates/") &&
           !f.path.includes("_attachments/"));

// 显示标题
dv.header(2, "今日随机推荐");

// 检查是否有可用笔记
if (!allNotes || allNotes.length === 0) {
    dv.paragraph("*没有找到符合条件的笔记*");
} else {
    try {
        // 基于当天日期生成随机种子（确保每日结果一致）
        const today = new Date().toISOString().slice(0, 10); // "YYYY-MM-DD"
        const seed = parseInt(today.replace(/-/g, ""));

        // 确保随机索引在有效范围内
        let randomIndex = Math.abs(Math.floor(Math.sin(seed) * allNotes.length)) % allNotes.length;
        if (randomIndex < 0 || randomIndex >= allNotes.length) {
            randomIndex = 0; // 如果索引无效，使用第一个笔记
        }

        // 获取随机笔记
        const randomNote = allNotes[randomIndex];

        // 确保随机笔记存在并有有效的路径
        if (randomNote && randomNote.path) {
            // 显示可点击的链接（带友好提示）
            dv.paragraph(`[[${randomNote.path}|${randomNote.name || randomNote.basename || "未命名笔记"}]]`);

            // 提取并显示笔记所在的文件夹路径
            const folderPath = randomNote.path.split("/").slice(0, -1).join("/");
            dv.paragraph(`*"${folderPath || "根目录"}" 中的笔记*`);
        } else {
            dv.paragraph("*无法获取随机笔记信息*");
        }
    } catch (error) {
        // 显示错误信息
        dv.paragraph(`*生成随机推荐时出错: ${error.message}*`);
        console.error("随机笔记生成错误:", error);
    }
}

dataviewjs
const getSafeTitle = (note) => {
    if (note?.frontmatter?.title) return note.frontmatter.title;
    if (note?.name) return note.name.replace(".md", "");
    return note?.path?.split("/").pop()?.replace(".md", "") || "随机笔记";
};

dataviewjs
const getSafeTitle = (note) => {
    if (note?.frontmatter?.title) return note.frontmatter.title;
    if (note?.name) return note.name.replace(".md", "");
    return note?.path?.split("/").pop()?.replace(".md", "") || "随机笔记";
};
```

---

## 你可以从哪开始

如果你也想在 Obsidian 里建一个主页，我的建议是，不用一步到位。

最简单的版本，装 HomePage 插件，新建一个笔记，在里面放几个你最常用的链接。比如「每日笔记」「项目文件夹」「正在写的文章」。

这就够了。

你的主页只有一个功能，让你每次打开 Obsidian 都知道从哪开始。

等你习惯了有一个主页，再慢慢加东西。

想看看最近改了什么，加一个 Dataview 的最近修改列表。

想统计写作情况，再加一个热力图插件。不要一上来就想做得跟我一样，先想清楚一件事，**我每天打开 Obsidian 最想看什么**。

这个问题的答案，就是你的主页应该放的东西。

---

说到底，建个人主页跟技术关系不大。

你不需要会写代码，不需要懂 Dataview 的语法，甚至不需要用跟我一样的插件。你只需要想清楚一件事，每次打开 Obsidian，你最想看到的那个画面是什么。

对我来说，是热力图上慢慢连成片的绿格子。是那年今日里突然跳出来的旧笔记。

对你来说，可能是完全不同的东西。

但重要的是，每次打开 Obsidian，你都有一个熟悉的起点，一个带着你个人痕迹的地方。

工具是次要的。找到自己的方式，才重要。

---

## 进阶阅读

- [Obsidian 入门22：认识 Dataview 插件，给你 3 段直接复制的指令，打造全自动仪表盘](/blog/Obsidian%20%E5%85%A5%E9%97%A822%EF%BC%9A%E8%AE%A4%E8%AF%86%20Dataview%20%E6%8F%92%E4%BB%B6%EF%BC%8C%E7%BB%99%E4%BD%A0%203%20%E6%AE%B5%E7%9B%B4%E6%8E%A5%E5%A4%8D%E5%88%B6%E7%9A%84%E6%8C%87%E4%BB%A4%EF%BC%8C%E6%89%93%E9%80%A0%E5%85%A8%E8%87%AA%E5%8A%A8%E4%BB%AA%E8%A1%A8%E7%9B%98)
- [Obsidian 入门23：别让待办烂在笔记里！用 Dataview 自动汇总你所有的 TODO](/blog/Obsidian%20%E5%85%A5%E9%97%A823%EF%BC%9A%E5%88%AB%E8%AE%A9%E5%BE%85%E5%8A%9E%E7%83%82%E5%9C%A8%E7%AC%94%E8%AE%B0%E9%87%8C%EF%BC%81%E7%94%A8%20Dataview%20%E8%87%AA%E5%8A%A8%E6%B1%87%E6%80%BB%E4%BD%A0%E6%89%80%E6%9C%89%E7%9A%84%20TODO)
- [Obsidian 入门24：不会写 Dataview 代码？教你一招，让 AI 成为你的专属“程序员”](/blog/Obsidian%20%E5%85%A5%E9%97%A824%EF%BC%9A%E4%B8%8D%E4%BC%9A%E5%86%99%20Dataview%20%E4%BB%A3%E7%A0%81%EF%BC%9F%E6%95%99%E4%BD%A0%E4%B8%80%E6%8B%9B%EF%BC%8C%E8%AE%A9%20AI%20%E6%88%90%E4%B8%BA%E4%BD%A0%E7%9A%84%E4%B8%93%E5%B1%9E%E2%80%9C%E7%A8%8B%E5%BA%8F%E5%91%98%E2%80%9D)
- [Obsidian 入门40：把我的写作工作流Skill免费分享给你](/blog/Obsidian%20%E5%85%A5%E9%97%A840%EF%BC%9A%E6%8A%8A%E6%88%91%E7%9A%84%E5%86%99%E4%BD%9C%E5%B7%A5%E4%BD%9C%E6%B5%81Skill%E5%85%8D%E8%B4%B9%E5%88%86%E4%BA%AB%E7%BB%99%E4%BD%A0)
