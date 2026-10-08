---
title: 我让 AI 和插件签了份「契约」，从此发文一键搞定
date: 2026-02-09T00:00:00.000Z
slug: obsidian-wechat-e2e-frontmatter-contract
excerpt: 写作 skill、生图 skill、发布插件，三件套齐了。但它们之间怎么衔接？靠两个 frontmatter 字段。
tags:
  - Obsidian
  - 内容创作
  - 效率工具
  - 编程开发
status: published
---

上一篇写了[免费生图的配图流水线](/blog/0%20%E5%85%83%E7%94%9F%E5%9B%BE%E6%88%90%E6%9C%AC%EF%BC%8C7%20%E6%AD%A5%E5%85%A8%E8%87%AA%E5%8A%A8%EF%BC%9A%E6%88%91%E7%9A%84%20AI%20%E9%85%8D%E5%9B%BE%E6%B5%81%E6%B0%B4%E7%BA%BF%E5%8D%87%E7%BA%A7%E8%AE%B0)，再上一篇写了[一键同步到微信草稿箱的插件](/blog/%E5%8F%97%E5%A4%9F%E4%BA%86%E5%A4%8D%E5%88%B6%E7%B2%98%E8%B4%B4%EF%BC%8C%E6%88%91%E6%8A%8A%20Obsidian%20%E7%9B%B4%E6%8E%A5%E6%8E%A5%E8%BF%9B%E4%BA%86%E5%BE%AE%E4%BF%A1%E5%90%8E%E5%8F%B0)。

写作 skill 有了，生图 skill 有了，插件也有了。

但它们之间怎么衔接？

今天补上这一环。

---

## 完整链路长什么样

现在我的发布流程是这样的：

1. 在 Obsidian 里写完文章
2. 用写作 skill 根据文章内容生成摘要
3. 用配图 skill 生成封面，图片路径自动写入 frontmatter
4. 点一下「同步到草稿箱」，插件读取 frontmatter，自动填充摘要和封面
5. 发送成功后，本地封面图自动清理

中间不用切出去找图、不用手动填摘要、不用事后清理文件。

![流水线闭环](/images/posts/%E6%88%91%E8%AE%A9%20AI%20%E5%92%8C%E6%8F%92%E4%BB%B6%E7%AD%BE%E4%BA%86%E4%BB%BD%E3%80%8C%E5%A5%91%E7%BA%A6%E3%80%8D%EF%BC%8C%E4%BB%8E%E6%AD%A4%E5%8F%91%E6%96%87%E4%B8%80%E9%94%AE%E6%90%9E%E5%AE%9A/Project_Obsidian%25E5%2585%25AC%25E4%25BC%2597%25E5%258F%25B7E2E%25E5%258F%2591%25E5%25B8%2583%25E6%25B5%2581%25E7%25A8%258B_illustration-01_e20e4a87_20260209.webp)

---

## 核心：Frontmatter 契约

这套流程能跑通，靠的是一个简单的约定：**Frontmatter 契约**。

上游（写作 skill、配图 skill）负责往 frontmatter 里写入两个字段：

```yaml
excerpt: "一句话摘要"
cover: "img/cover.jpg"
```

下游（插件）负责读取这两个字段，自动填充到发送弹窗里。

就这么简单。

上游管产出，下游管发送，通过 frontmatter 这个「契约」衔接。

![契约握手](/images/posts/%E6%88%91%E8%AE%A9%20AI%20%E5%92%8C%E6%8F%92%E4%BB%B6%E7%AD%BE%E4%BA%86%E4%BB%BD%E3%80%8C%E5%A5%91%E7%BA%A6%E3%80%8D%EF%BC%8C%E4%BB%8E%E6%AD%A4%E5%8F%91%E6%96%87%E4%B8%80%E9%94%AE%E6%90%9E%E5%AE%9A/Project_Obsidian%25E5%2585%25AC%25E4%25BC%2597%25E5%258F%25B7E2E%25E5%258F%2591%25E5%25B8%2583%25E6%25B5%2581%25E7%25A8%258B_illustration-02_607e14e2_20260209.webp)

---

## 一个具体场景

假设你本地有一张图片，希望它始终作为封面。

操作很简单：把图片路径告诉 AI，让 AI 写入 frontmatter 的 `cover` 字段就行。

这个用法适合两类人：

- **懒人**：一张图片打天下，省心省力
- **想打造个人 IP 的人**：一张图片长期作为封面，强化品牌识别

不管你是哪种，只要 frontmatter 里有 `cover` 字段，插件就会自动读取。

![一图打天下](/images/posts/%E6%88%91%E8%AE%A9%20AI%20%E5%92%8C%E6%8F%92%E4%BB%B6%E7%AD%BE%E4%BA%86%E4%BB%BD%E3%80%8C%E5%A5%91%E7%BA%A6%E3%80%8D%EF%BC%8C%E4%BB%8E%E6%AD%A4%E5%8F%91%E6%96%87%E4%B8%80%E9%94%AE%E6%90%9E%E5%AE%9A/Project_Obsidian%25E5%2585%25AC%25E4%25BC%2597%25E5%258F%25B7E2E%25E5%258F%2591%25E5%25B8%2583%25E6%25B5%2581%25E7%25A8%258B_illustration-03_f21328d3_20260209.webp)

---

## 插件的安全设计

说到自动清理，我最怕的是删错东西。

所以我在插件里做了几个兜底：

1. **清理时机**：只有「创建草稿成功」后才会触发清理，不会出现「草稿没发成功但图片已经删了」的情况
2. **回收站兜底**：清理默认走系统回收站，出错可找回
3. **失效字段自动清理**：如果清理目录包含了 frontmatter 里的 `cover` 路径，插件会自动把这个字段清空，避免留下无效引用

宁可多一个 warning，也不要偷偷做不可逆动作。

---

## 给也在折腾的朋友

如果你也在搭类似的流程，我的建议是：

1. **先定义最小契约字段**：比如 `excerpt`、`cover`，够用就行
2. **把「内容生产」和「发布动作」解耦**：上游专注产出，下游专注发送
3. **自动化默认保守**：能走回收站就走回收站，能给 warning 就给 warning

---

整条链路打通了。

从 Obsidian 写完，到躺进微信草稿箱，现在真的可以一气呵成。

链路闭环了，剩下的就是写。干起来！
