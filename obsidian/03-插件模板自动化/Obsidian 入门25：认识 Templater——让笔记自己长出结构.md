---
title: Obsidian 入门25：认识 Templater——让笔记自己长出结构
date: 2026-04-14
slug: obsidian-templater-tutorial-smart-template
excerpt: 嫌 Obsidian 官方模板太死板？今天带你认识进阶大管家 Templater。别怕写代码，把它当成“智能烤箱”，只需要几个简单指令，就能让你的周记自动汇总当周日记。让笔记自己长出结构！
cover: ""
tags:
  - Obsidian
  - Obsidian插件
  - 自动化
  - 效率工具
  - 知识管理
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门10：从一个模板，到一套真正用得上的模板系统](/blog/Obsidian%20%E5%85%A5%E9%97%A810%EF%BC%9A%E4%BB%8E%E4%B8%80%E4%B8%AA%E6%A8%A1%E6%9D%BF%EF%BC%8C%E5%88%B0%E4%B8%80%E5%A5%97%E7%9C%9F%E6%AD%A3%E7%94%A8%E5%BE%97%E4%B8%8A%E7%9A%84%E6%A8%A1%E6%9D%BF%E7%B3%BB%E7%BB%9F)。

---

记日记这件事，我是[用Calendar在日历上点一下](/blog/Obsidian%20%E5%85%A5%E9%97%A811%EF%BC%9A%E5%86%99%E6%97%A5%E8%AE%B0%E8%BF%99%E4%BB%B6%E4%BA%8B%EF%BC%8C%E5%8F%AF%E8%83%BD%E5%8F%AA%E5%B7%AE%E4%B8%80%E4%B8%AA%20Calendar)解决的。

每天早上打开Obsidian，先打开 Calendar，找到今天的日期，点一下，一篇日记就创建出来了。模板早就配好了，内容只需要填空，五分钟写完。

![Obsidian 入门25：认识 Templater——让笔记自己长出结构 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A825%EF%BC%9A%E8%AE%A4%E8%AF%86%20Templater%E6%8F%92%E4%BB%B6%EF%BC%8C%E8%AE%A9%E7%AC%94%E8%AE%B0%E8%87%AA%E5%B7%B1%E9%95%BF%E5%87%BA%E7%BB%93%E6%9E%84/CleanShot%25202026-03-28%2520at%252016.05.28.gif)

周记也是同理。Calendar 上找到「周」，点一下，一篇周记就出来了。

但问题来了。

日记建好之后，当周的日记会自然积累。但周记呢？点一下是点出来了，打开一看，里面是空的。当周的七天日记，要手动去找，手动一条一条输入双链。

比如我需要输入这个：

```
- [[Diary/2025/Daily/星期一, 4月7日, 2025年.md|星期一, 4月7日, 2025年]]
- [[Diary/2025/Daily/星期二, 4月8日, 2025年.md|星期二, 4月8日, 2025年]]
- ...
```

七条，全靠手敲。

有没有一种方式，让周记在创建的一瞬间，就自动把当周的日记链接进来？

想要实现这种“无中生有”的自动化，就必须请出 Obsidian 里的进阶大管家：**Templater 插件**。

名字听着玄乎，其实它就是在你的笔记里跑一段 JavaScript 脚本（不要被这个名词吓到，接着往下看）。

---

## 为什么核心插件模板不够用了

[入门10](/blog/Obsidian%20%E5%85%A5%E9%97%A810%EF%BC%9A%E4%BB%8E%E4%B8%80%E4%B8%AA%E6%A8%A1%E6%9D%BF%EF%BC%8C%E5%88%B0%E4%B8%80%E5%A5%97%E7%9C%9F%E6%AD%A3%E7%94%A8%E5%BE%97%E4%B8%8A%E7%9A%84%E6%A8%A1%E6%9D%BF%E7%B3%BB%E7%BB%9F) 讲过，核心插件模板可以插入预设好的文字和变量，比如 `{{date}}` 会插入当前日期，`{{time}}` 会插入当前时间。

这是有用的。但它有一个根本的局限：

**它只能插入「写好的内容」，不能根据条件「生成」内容。**

你没法让它判断"这是第几周"，也没法让它去扫描文件夹里的其他文件，更没法让它"找到当周的日记然后生成双链列表"。

想要这些，你需要一个能跑脚本的模板引擎。

---

## Templater 是什么

如果把 Obsidian 官方自带的模板比作一个“复读机”，你提前录好了什么，它新建笔记时就吐出什么（比如固定的标题格式、或者当天的日期）。

那 Templater 这个社区插件，就是一个“全能智能管家”。它不仅能帮你填字，它还有**逻辑判断**和**执行动作**的能力。

打个生活中的比方：官方模板就像是一个普通的微波炉，你只能按一下“热饭”键。

而 Templater 就像是一个智能烤箱。你可以给它下指令：“管家，先扫一眼烤箱里放的是鸡肉还是牛肉，如果是鸡肉，就烤 20 分钟；顺便看一下现在是不是晚上，如果是，就把厨房的灯打开。”

![Obsidian 入门25：认识 Templater——让笔记自己长出结构 - 配图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A825%EF%BC%9A%E8%AE%A4%E8%AF%86%20Templater%E6%8F%92%E4%BB%B6%EF%BC%8C%E8%AE%A9%E7%AC%94%E8%AE%B0%E8%87%AA%E5%B7%B1%E9%95%BF%E5%87%BA%E7%BB%93%E6%9E%84/20260414223554508.webp)

这个智能管家听得懂的语言，就是大名鼎鼎的 JavaScript。

一听到这个词，很多人可能就想关掉文章了。别怕！其实你根本不用去啃那些厚厚的编程书，我这段时间用下来，翻来覆去也就是让管家干这三件事：

**第一件事：按照我喜欢的口音报时（`tp.date`）**

```text
<% tp.date %>
```

官方的模板只能死板地给你一个格式。但你可以让 Templater 管家变着花样报时，比如不仅有年和月，还要带上“星期几”。

**第二件事：跑腿去拿别人的东西（`tp.file.content`）**

```text
<% tp.file.content %>
```

比如写复盘的时候，你可以让管家跑去另一个文件夹，把前几天写好的目标直接念出来，抄到当前的笔记里。

**第三件事：处理复杂的连环任务（`<%* ... *%>`）**

```javascript
<%*
const today = tp.date.now();
tR += "今天是 " + today;
%>
```

这是管家最厉害的地方。你可以交给他一套完整的行动方案：“管家，先去看看标题是几月份，然后再算算这是今年的第几周，最后去日记本里把这周的日记全都给我搬过来。”

---

## 我的 Templater 实战：让周记自动链接日记

好了，背景交代完了。现在讲讲我是怎么把它用起来的。

### 需求

我的日记存在 `Diary/年份/Daily/` 下面，文件名格式是 `星期一, 4月7日, 2025年.md`。

周记文件名格式是 `第15周，4月，2025年.md`。

我新建一篇周记的时候，希望 Templater 自动做这几件事：

1. 解析周记标题，提取年份和周数
2. 计算这一周从周几到周几
3. 扫描日记文件夹，找到当周的七篇日记
4. 按顺序生成双链列表

### 跟 Gemini 的漫长对话

在去年的时候，这个需求我一开始不知道怎么写。

于是去 Gemini 网页版开了个对话，把日记结构、周记格式、想要实现的效果都跟它说了。

Gemini 给了我一版脚本。贴进去，报错了。

把报错信息复制给 Gemini，它又给了一版。贴进去，还是报错。

每次 Gemini 给完代码，我贴进去，跑不起来，然后把报错截图甩给它，它再给一版……来回大概七八次，才终于跑通了。

那会儿挺烦躁的。还不会用 Cursor 或者 IDE 直接改 Obsidian 的文件夹内容，这是当时我能找到的唯一办法。

最终跑通的那一版的效果，大概是这样的

![Obsidian 入门25：认识 Templater——让笔记自己长出结构 - 截图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A825%EF%BC%9A%E8%AE%A4%E8%AF%86%20Templater%E6%8F%92%E4%BB%B6%EF%BC%8C%E8%AE%A9%E7%AC%94%E8%AE%B0%E8%87%AA%E5%B7%B1%E9%95%BF%E5%87%BA%E7%BB%93%E6%9E%84/CleanShot%25202026-04-14%2520at%252022.27.35.gif)

> **新手别慌**：这段 JavaScript 代码，你**完全不需要看懂**。只需要把它原封不动地复制粘贴到你的“周记模板”里，然后在创建新周记的时候，它就会自己在后台跑起来。

代码脚本在这里：

```javascript
<%*
// --- 配置区域 ---
const dailyNoteRootFolder = "Diary"; // 包含年份文件夹的根目录名
const weeklyNoteTitleFormat = "第W周，M月，YYYY年"; // 你的周记标题格式

// --- 脚本逻辑 ---

// 1. 设置 Moment.js 使用中文语言包
moment.locale('zh-cn');

// 2. 解析周记标题获取年份和周数
const weeklyNoteTitle = tp.file.title;
const titleMatch = weeklyNoteTitle.match(/第(\d{1,2})周，\d{1,2}月，(\d{4})年/);

if (!titleMatch) {
  new Notice(`错误：周记标题 "${weeklyNoteTitle}" 不符合 "${weeklyNoteTitleFormat}" 格式。`, 10000);
  return;
}

const week = parseInt(titleMatch[1], 10);
const year = parseInt(titleMatch[2], 10);

// 3. 确定本周的开始和结束日期
const weekStart = moment().year(year).isoWeek(week).startOf('isoWeek');
const weekEnd = moment().year(year).isoWeek(week).endOf('isoWeek');
const weekStartStr = weekStart.format("YYYY-MM-DD");
const weekEndStr = weekEnd.format("YYYY-MM-DD");

// 4. 构建当年的【日记】文件夹路径
const currentYearDailyFolder = `${dailyNoteRootFolder}/${year}/Daily`;

// 5. 获取 Vault 中的所有 Markdown 文件
const allFiles = app.vault.getMarkdownFiles();

// 6. 筛选出指定年份【日记】文件夹内、且日期在本周范围内的日记文件
const dailyNotesInWeek = allFiles.filter(file => {
  // 检查文件是否在正确的年份【日记】文件夹内
  if (!file.path.startsWith(currentYearDailyFolder + "/")) {
    return false;
  }

  // --- 日记文件名解析逻辑 ---
  // !! 使用你确认的格式："dddd, M月D日, YYYY年" (注意英文逗号) !!

  // 方式A: 解析 "dddd, M月D日, YYYY年" 格式 (已取消注释)
  const dailyNoteTitleFormat = "dddd, M月D日, YYYY年"; // 使用英文逗号
  const fileDateMoment = moment(file.basename, dailyNoteTitleFormat, 'zh-cn', true); // 严格模式

  if (fileDateMoment.isValid()) {
      const fileDateStr = fileDateMoment.format("YYYY-MM-DD");
      // 检查日期是否在本周范围内
      return fileDateStr >= weekStartStr && fileDateStr <= weekEndStr;
  } else {
      // 如果解析失败，打印错误信息到控制台 (可选)
      console.log(`无法解析文件 "${file.basename}" 使用格式 "${dailyNoteTitleFormat}"`);
  }


  // 方式B: 解析 YYYY-MM-DD 开头的格式 (已被注释掉)
  /*
  const dateMatch = file.basename.match(/^(\d{4}-\d{2}-\d{2})/);
  if (dateMatch) {
    const fileDateStr = dateMatch[1];
    const fileDateMoment = moment(fileDateStr, "YYYY-MM-DD", true);
    if (fileDateMoment.isValid()) {
      return fileDateStr >= weekStartStr && fileDateStr <= weekEndStr;
    }
  }
  */
  // --- 结束：日记文件名解析逻辑 ---

  return false; // 解析失败或不在范围内，则排除
});

// 7. 按日期排序日记 (使用 moment 对象进行比较)
dailyNotesInWeek.sort((a, b) => {
    const dailyNoteTitleFormat = "dddd, M月D日, YYYY年"; // 确保格式一致
    const dateA = moment(a.basename, dailyNoteTitleFormat, 'zh-cn', true);
    const dateB = moment(b.basename, dailyNoteTitleFormat, 'zh-cn', true);
    // 比较有效的 moment 对象
    if (dateA.isValid() && dateB.isValid()) {
      return dateA.diff(dateB); // 返回毫秒差，用于排序
    } else if (dateA.isValid()) { return -1; } // A 有效，排前面
    else if (dateB.isValid()) { return 1; }  // B 有效，排前面
    return 0; // 都无效，保持原顺序
});


// 8. 生成 Markdown 链接列表
const links = dailyNotesInWeek.map(file => `- [[${file.path}|${file.basename}]]`).join('\n');

// --- 模板最终输出 ---
tR += `*本周时间范围: ${weekStart.format("YYYY年M月D日 dddd")} 至 ${weekEnd.format("YYYY年M月D日 dddd")}*\n\n`;
if (links) {
  tR += links;
} else {
  tR += `*在本周 (${weekStartStr} 到 ${weekEndStr}) 的文件夹 "${currentYearDailyFolder}" 中没有找到符合 "${dailyNoteTitleFormat}" 格式的日记文件。*\n`; // 更新了提示中的格式
  tR += `*(请检查该文件夹下是否存在日记文件、文件名格式是否严格匹配)*`;
}

%>
```

写完这个脚本之后，我新建周记就是点一下，等几秒，七条链接全出来了。

---

## Templater vs 核心插件模板：怎么选

说到这里，很多新手可能晕了：我到底什么时候该用官方的，什么时候用 Templater？

说白了，如果是填个当天的日期、时间这种“死数据”，老老实实用官方自带的模板足够了，别给自己找不痛快去折腾 Templater 的代码。

但如果你要的是“无中生有”、“自动计算”（比如：判断今天是今年的第几周、扫描文件夹把今天的任务自动拉出来），那 Templater 就是唯一的解。

---

## 把最难的事，丢给最强的大脑

看到这里，你可能会说：“这么复杂、动不动就几十行的脚本，我一个小白怎么可能写得出来？哪怕报错了我也看不懂啊！”

确实。如果你不会写代码，在两年前，我绝对不会写这篇教程推荐你去用 Templater。因为那意味着你为了记个笔记，还要去学 JavaScript，完全本末倒置。

但现在时代变了。

连我这种懂点代码的人，都懒得自己去手敲这几十行逻辑了。因为现在，**我们有 AI**。

![Obsidian 入门25：认识 Templater——让笔记自己长出结构 - 配图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A825%EF%BC%9A%E8%AE%A4%E8%AF%86%20Templater%E6%8F%92%E4%BB%B6%EF%BC%8C%E8%AE%A9%E7%AC%94%E8%AE%B0%E8%87%AA%E5%B7%B1%E9%95%BF%E5%87%BA%E7%BB%93%E6%9E%84/20260414223651052.webp)

前面我讲过，即使是我自己写那个周记的脚本，也是丢给 Gemini 帮我来回改了七八轮才跑通的。

朋友们，把 AI 用起来！

---

## 进阶阅读

- [Obsidian 入门10：从一个模板，到一套真正用得上的模板系统](/blog/Obsidian%20%E5%85%A5%E9%97%A810%EF%BC%9A%E4%BB%8E%E4%B8%80%E4%B8%AA%E6%A8%A1%E6%9D%BF%EF%BC%8C%E5%88%B0%E4%B8%80%E5%A5%97%E7%9C%9F%E6%AD%A3%E7%94%A8%E5%BE%97%E4%B8%8A%E7%9A%84%E6%A8%A1%E6%9D%BF%E7%B3%BB%E7%BB%9F)
- [Obsidian 入门11：写日记这件事，可能只差一个 Calendar](/blog/Obsidian%20%E5%85%A5%E9%97%A811%EF%BC%9A%E5%86%99%E6%97%A5%E8%AE%B0%E8%BF%99%E4%BB%B6%E4%BA%8B%EF%BC%8C%E5%8F%AF%E8%83%BD%E5%8F%AA%E5%B7%AE%E4%B8%80%E4%B8%AA%20Calendar)
- [Obsidian 入门16：用 Obsidian 做日周复盘，三件套串起一套习惯](/blog/obsidian-beginner-16-daily-weekly-review)
- [Obsidian 入门22：认识 Dataview 插件，给你 3 段直接复制的指令，打造全自动仪表盘](/blog/Obsidian%20%E5%85%A5%E9%97%A822%EF%BC%9A%E8%AE%A4%E8%AF%86%20Dataview%20%E6%8F%92%E4%BB%B6%EF%BC%8C%E7%BB%99%E4%BD%A0%203%20%E6%AE%B5%E7%9B%B4%E6%8E%A5%E5%A4%8D%E5%88%B6%E7%9A%84%E6%8C%87%E4%BB%A4%EF%BC%8C%E6%89%93%E9%80%A0%E5%85%A8%E8%87%AA%E5%8A%A8%E4%BB%AA%E8%A1%A8%E7%9B%98)
