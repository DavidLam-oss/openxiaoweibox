---
title: Gemini system instruction 的优化
date: "2025-09-13"
excerpt: >-
  介绍 Gemini 的 Personal Context 功能更新，分享如何利用 Cursor 分析个人日记生成心理侧写，从而优化 System
  Instruction，让 AI 更懂你的个性。
tags:
  - AI模型
  - 提示词工程
  - 生活随笔
  - 效率工具
---

## Saved info升级为Personal context

在之前的[如何让 Gemini 拥有关于“我”的专属记忆](/blog/%E5%A6%82%E4%BD%95%E8%AE%A9%20Gemini%20%E6%8B%A5%E6%9C%89%E5%85%B3%E4%BA%8E%E2%80%9C%E6%88%91%E2%80%9D%E7%9A%84%E4%B8%93%E5%B1%9E%E8%AE%B0%E5%BF%86)中介绍了如何通过设置 Saved info 设置 Gemini 的 system instruction 去让 Gemini 拥有专属于“我”的记忆，从而在沟通中获得更符合自己特性的回答。

今天发现 Saved info 已经更新成为 Personal context。可以通过打开 your past chats with Gemini 的开关，让Gemini 可以从我们过去的chat 中去更好地理解用户以及用户的语言风格等，从而能提供更好的回答。

![Gemini system instruction 的优化 - 配图 1](/images/posts/202509161503811.webp)

当然你如果你有隐私方面的担忧，也可以选择关闭。或者可以点击上面的“Gemini Apps Activity"之后进入下面这个页面，将 on 更改成 off。不过即使更改成 off 了，过去 72 小时的 chat 还是会被用来作为回复的引用。
![Gemini system instruction 的优化 - 配图 2](/images/posts/202509161506589.webp)

当然，也可以通过下面的 delete 手动删除你的 activity。

![Gemini system instruction 的优化 - 配图 3](/images/posts/202509161509499.webp)

## 怎么让 Gemini 知道我的 personality？

原本的 system instructions 依然在那里，我上次是添加了”显性记忆“以及”隐形记忆”的system instruction。我今天想在这个基础上去添加我自己的一些特性，主动去让 Gemini 先了解我是一个什么样的人，而不是让他通过 chat 去学习我是怎样的。

我自己其实也不太了解我是一个怎么样的人，好在我前几年有写日记的习惯而且我的日记已经全部搬到 Obsidian 中作为 markdown 文件本地存储了，那么我在想我是否可以提供我的日记给 Gemini 让他来帮我分析呢？

中间经过了一些探索：

- 用 Gemini 来，做一次最多只能传 10 个附件
- 我接着在想是能否把我的各个 markdown 文件合并成一个 PDF 呢？这是一种方式，但是太过麻烦了。
- 后来我想到去 Obsidian 里面用 Copilot 工具分析我的日记并输出内容，结果效果不太好，它只能基于一定的上下文进行分析，不能分析我所有甚至大部分的日记。

最后面发现，我用 Cursor 不就行了吗？

于是我把 Obsidian 的库文件夹丢进 cursor 里面，结合之前获得的一个心理侧写 Prompt 丢给它，让它分析我的日记文件，最后输出了对应的我个人特质的内容给我。我把这些内容放到 Personal Contexts 里面，现在 Gemini 就是我个人独有的 Gemini 了。
