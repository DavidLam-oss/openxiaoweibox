---
title: 文章自动归位 Obsidian 专题页，秘密在前台那几行字
date: "2026-09-01"
slug: obsidian-frontmatter-auto-topic
excerpt: 我的 Obsidian 专题页不用人工维护，秘密藏在每篇文章开头那几行 frontmatter 里。
cover: ""
tags:
  - Obsidian
  - Obsidian插件
  - 多平台分发
  - 知识管理
status: published
---
我的博客有个 [Obsidian 专题页](/blog/obsidian)，它好像不用我管，自己一直在长。

![Obsidian 专题页收录文章截图](/images/posts/%E6%96%87%E7%AB%A0%E8%87%AA%E5%8A%A8%E5%BD%92%E4%BD%8D%20Obsidian%20%E4%B8%93%E9%A2%98%E9%A1%B5%EF%BC%8C%E7%A7%98%E5%AF%86%E5%9C%A8%E5%89%8D%E5%8F%B0%E9%82%A3%E5%87%A0%E8%A1%8C%E5%AD%97/CleanShot%25202026-09-01%2520at%252022.12.35.webp)


新的 Obsidian 文章会自己去到该在的位置，有的进了主学习路径，有的挂在延伸阅读，没人去搬它。仔细想想，这件事已经自动运转很久了。

秘密藏在每篇文章开头那几行 frontmatter 里。

![frontmatter 自动归类规则示例](/images/posts/%E6%96%87%E7%AB%A0%E8%87%AA%E5%8A%A8%E5%BD%92%E4%BD%8D%20Obsidian%20%E4%B8%93%E9%A2%98%E9%A1%B5%EF%BC%8C%E7%A7%98%E5%AF%86%E5%9C%A8%E5%89%8D%E5%8F%B0%E9%82%A3%E5%87%A0%E8%A1%8C%E5%AD%97/20260901215651204.webp)


---

之前写[frontmatter 契约](/blog/obsidian-wechat-e2e-frontmatter-contract)的时候聊过，写作 skill 往 frontmatter 里写 excerpt 和 cover，插件读出来自动填摘要和封面，上下游就这么接上了。

这次是同一套思路，往前走了一步。frontmatter 不止能衔接 AI 和插件，还能衔接文章和专题页。

规则只有三条。

---

第一条，tags 里带上 Obsidian。

```yaml
tags:
  - Obsidian
```

只要这一行，文章就会至少进入专题页的延伸阅读。门槛低到几乎不叫规则，但它保证了 Obsidian 的文章不会漏掉。

第二条，想进主学习路径，标题要用固定格式。

```yaml
title: Obsidian 入门70：文章标题
```

Obsidian 入门，紧跟编号，中间不空格。主站看到这种标题，就知道这是系统教程，会把它放进主学习路径。

第三条，也是我最近在推的一条，加一个 obsidianSection 字段。

```yaml
obsidianSection: publishing
```

这一行告诉主站，文章属于专题页的哪个阶段。publishing 是第八阶段，讲发布、导出和内容分发。这篇文章的 frontmatter 里，就带着这一行。

---

obsidianSection 有八个可选值，对应专题页的八个阶段。列出来感受一下这个分类粒度。

| obsidianSection       | 阶段                   |
| --------------------- | -------------------- |
| first-steps           | 新手起步                 |
| basics                | 笔记基础                 |
| plugins-automation    | 插件、模板与自动化            |
| advanced-organization | 高级组织、Dataview 与知识库结构 |
| ai-workflow           | AI + Obsidian 工作流    |
| collecting            | 内容收集与剪藏              |
| sync-backup           | 同步、备份与图片管理           |
| publishing            | 发布、导出与内容分发           |

阶段定得越细，文章站得越准。读者点进专题页，从新手到进阶一路看下来，不会在「这文章到底该在哪」上犯迷糊。

![Obsidian 专题页八个阶段分类](/images/posts/%E6%96%87%E7%AB%A0%E8%87%AA%E5%8A%A8%E5%BD%92%E4%BD%8D%20Obsidian%20%E4%B8%93%E9%A2%98%E9%A1%B5%EF%BC%8C%E7%A7%98%E5%AF%86%E5%9C%A8%E5%89%8D%E5%8F%B0%E9%82%A3%E5%87%A0%E8%A1%8C%E5%AD%97/20260901215754104.webp)


---

你可能会问，不写 obsidianSection 会怎样？

主站现在也有兜底规则。标题匹配 Obsidian 入门数字，进主路径，title、slug、excerpt、tags 里含 obsidian，进延伸阅读，阶段靠标题编号和关键词猜。

字段写清楚了，主站以后接入精确归类，就是读一下的事。



所以我的习惯变成了这样，写 Obsidian 文章的时候顺手想一下，这篇属于哪个阶段，然后把它写进 frontmatter。成本就一次思考，换来的是专题页长期不用人工维护。

这大概是 frontmatter 最划算的地方，它把「发布后要做的整理」，提前到了「写作时顺手写下」。

规则写在前端，维护留在后端。

---

回头再看开头那个专题页，它之所以整齐，就是每一篇文章开头那几行字，提前替它把位置占好了。完全没有任何的黑科技。

包括你现在看的这篇，它的 frontmatter 里也写着 obsidianSection。

![本篇文章的 frontmatter](/images/posts/%E6%96%87%E7%AB%A0%E8%87%AA%E5%8A%A8%E5%BD%92%E4%BD%8D%20Obsidian%20%E4%B8%93%E9%A2%98%E9%A1%B5%EF%BC%8C%E7%A7%98%E5%AF%86%E5%9C%A8%E5%89%8D%E5%8F%B0%E9%82%A3%E5%87%A0%E8%A1%8C%E5%AD%97/CleanShot%25202026-09-01%2520at%252022.20.59.webp)

