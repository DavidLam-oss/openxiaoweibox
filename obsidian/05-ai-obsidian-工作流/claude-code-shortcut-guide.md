---
title: Obsidian 入门41：那些用 Claude Code 时必须记住的快捷键
date: 2026-05-04
slug: claude-code-shortcut-guide
excerpt: 在终端里用 Claude Code，回车是发送不是换行，贴图也不同系统操作各异。6 个反直觉操作，收藏备用。
cover: ""
tags:
  - 终端命令行
  - Claude Code
  - 效率工具
  - Obsidian入门
  - Obsidian
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 我会从最基础的认知开始，慢慢写到资料整理、写作工作流，再到怎么把 AI 接进来。
>
> 如果你还没看过前几篇，可以先看 [Obsidian 入门40：把我的写作工作流Skill免费分享给你](/blog/Obsidian%20%E5%85%A5%E9%97%A840%EF%BC%9A%E6%8A%8A%E6%88%91%E7%9A%84%E5%86%99%E4%BD%9C%E5%B7%A5%E4%BD%9C%E6%B5%81Skill%E5%85%8D%E8%B4%B9%E5%88%86%E4%BA%AB%E7%BB%99%E4%BD%A0)。

最近，我发现了一个有意思的现象。

很多人都在用 Claude Code，但用法的差距大得吓人。

有的人已经开起了 Agent Team 并行跑任务，有的人到现在还在每步挨个确认，甚至不知道怎么在终端里换行。

昨天看到一个朋友 Prompt 写错了没发现，等开发完了面目全非，准备开始全部再来一遍的时候，我说你咋不用回退。

他来了一句，啥是回退？

![Obsidian 入门41：那些用 Claude Code 时必须记住的快捷键 - 配图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A841%EF%BC%9A%E9%82%A3%E4%BA%9B%E7%94%A8%20Claude%20Code%20%E6%97%B6%E5%BF%85%E9%A1%BB%E8%AE%B0%E4%BD%8F%E7%9A%84%E5%BF%AB%E6%8D%B7%E9%94%AE/20260504103356965.webp)

然后我就懵了。难道只有我知道按两下 Esc 可以回退代码？

仔细想想，意料之外但有点情理之中的感觉。

毕竟 Claude Code 跑在终端里，跟我们平时用的图形化软件完全不同。

很多操作是反直觉的，因为它确实跟我们习惯的那套逻辑不一样。

今天把我自己踩过坑之后总结出来的几个最常用操作整理一下。

针对最容易被卡住的那几个，让你知道至少知道有这么个东西的存在先。

---

## 换行：回车不是换行，是发送

这个是第一个大坑。

在 Word 里、在微信里、在任何一个图形界面里，按回车就是换行，很自然。但在 Claude Code 的终端里，回车＝发送。你写了一大半 Prompt，突然想分段，一按回车，直接发出去了，而故事还没讲完。

这个问题怎么解决？

Mac 用户和 Windows 用户通用的解法是：**Ctrl+J** 或者 **Shift+Ente**r。按下去，换行，但不发送。

![Obsidian 入门41：那些用 Claude Code 时必须记住的快捷键 - 配图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A841%EF%BC%9A%E9%82%A3%E4%BA%9B%E7%94%A8%20Claude%20Code%20%E6%97%B6%E5%BF%85%E9%A1%BB%E8%AE%B0%E4%BD%8F%E7%9A%84%E5%BF%AB%E6%8D%B7%E9%94%AE/ChatGPT%2520Image%2520May%25204%252C%25202026%252C%252010_30_06%2520AM-850.webp)

Mac 用户多一个选择：**Option+回车** 也可以达到同样的效果。

这个操作是我第一批记住的快捷键里最常用的一个。因为写 Prompt 的时候，换行是刚需，分段写比一口气写完清晰得多。

## 清除输入：不用一个字一个字删

第二种情况也特别常见。

你写了一长串，突然发现方向错了，要全部删掉从头来过。很多人会怎么做呢？一个一个退格，慢慢删，删到手指酸。

其实有更快的办法：**Ctrl+U**。

这个快捷键的意思是清掉整行输入。光标在哪个位置都没关系，一按，整行没了，重新打就好了。

我第一次知道这个的时候，第一反应是"这东西怎么不早说"。

## 贴图：Mac 和 Windows 不一样

debug 的时候贴一张报错截图给 AI 看，这个需求太常见了。但很多人在终端里不知道怎么贴图。

先说 Mac，非常简单：**Ctrl+V**。截完图直接粘，跟任何图形软件里一样自然。

Windows 用户要注意，是 **Alt+V**，不是 Ctrl+V。

明明 Ctrl+V 在 Windows 里也是粘贴，但在 Claude Code 里，贴图这个操作要换成 Alt+V；而在 Mac 上需要从Command+V 换成 Ctrl+V。

![Obsidian 入门41：那些用 Claude Code 时必须记住的快捷键 - 配图 3](/images/posts/Obsidian%20%E5%85%A5%E9%97%A841%EF%BC%9A%E9%82%A3%E4%BA%9B%E7%94%A8%20Claude%20Code%20%E6%97%B6%E5%BF%85%E9%A1%BB%E8%AE%B0%E4%BD%8F%E7%9A%84%E5%BF%AB%E6%8D%B7%E9%94%AE/20260504103507742.webp)

还有一点也顺便说一下：贴图不需要先保存成文件再拖进去，截图之后直接 Ctrl+V 或者 Alt+V 粘贴，Claude Code 会自动读取。

一开始我不知道这个操作的时候，只会把图片存在本地，然后把图片路径告诉 Claude code，实在是显得愚蠢且麻烦。

现在算是起飞了。

## 搜索历史：之前打过的命令找回来

有时候你会想复用之前打过的一个很长的 Prompt，但忘了具体内容是什么。

重新打一遍太费时间了。其实可以搜：**Ctrl+R**。

按下去之后，输入关键词，就能找到之前打过的命令历史。用上下键可以切换不同的匹配结果，找到想用的之后按回车就填充进去了。

![Obsidian 入门41：那些用 Claude Code 时必须记住的快捷键 - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A841%EF%BC%9A%E9%82%A3%E4%BA%9B%E7%94%A8%20Claude%20Code%20%E6%97%B6%E5%BF%85%E9%A1%BB%E8%AE%B0%E4%BD%8F%E7%9A%84%E5%BF%AB%E6%8D%B7%E9%94%AE/CleanShot%25202026-05-04%2520at%252011.01.03.webp)

这个在连续对话里特别有用，比如你想回到某个特定时刻的指令，直接 Ctrl+R 搜一下就行。

## 快速翻查历史：用方向键上下找

有的时候你想复用之前打过的某个 Prompt，用 Ctrl+R 搜关键词是一种方式，但有时候你记得刚才说过什么，只是想快速找回来。

直接按**方向键的上和下**，可以在历史记录里快速翻查。上一条、下一条，找起来很快。

这个在连续对话里特别有用，比如你想回到某个特定时刻的指令，直接上下翻就好了，比 Ctrl+R 更直觉。

![Obsidian 入门41：那些用 Claude Code 时必须记住的快捷键 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A841%EF%BC%9A%E9%82%A3%E4%BA%9B%E7%94%A8%20Claude%20Code%20%E6%97%B6%E5%BF%85%E9%A1%BB%E8%AE%B0%E4%BD%8F%E7%9A%84%E5%BF%AB%E6%8D%B7%E9%94%AE/CleanShot%25202026-05-04%2520at%252011.25.00.gif)

---

## 取消与回退：Esc 两下，还有 /rewind

最后说一个很多人不知道的。

输入到一半发现不对，想撤销整个输入，不要用退格键一直删。**连按两下 Esc** 可以触发 /rewind，就是回退。

而且现在的 /rewind 还可以选择只回退代码、只回退对话，或者两个都回退。

这个对做实验的时候特别有用。让 Claude 试一种新方案，不行的话代码回退，对话留着，Claude 还记得你刚才聊了什么，知道这条路不通，可以直接换方向，不用重新解释一遍需求。

以前遇到这种情况我都是含泪 git reset。现在有了 /rewind，真的回不去了。

![Obsidian 入门41：那些用 Claude Code 时必须记住的快捷键 - 配图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A841%EF%BC%9A%E9%82%A3%E4%BA%9B%E7%94%A8%20Claude%20Code%20%E6%97%B6%E5%BF%85%E9%A1%BB%E8%AE%B0%E4%BD%8F%E7%9A%84%E5%BF%AB%E6%8D%B7%E9%94%AE/20260504103530363.webp)

---

说到底，终端里的操作逻辑跟图形界面不一样，这本身不是问题。只要知道那几个关键的区别，剩下的就跟用普通软件一样顺了。

下次有人问你 Claude Code 怎么用，你就把上面这些教给他。至于其他的，边用边学就好了！

---

### 进阶阅读

- [Obsidian 入门40：把我的写作工作流Skill免费分享给你](/blog/Obsidian%20%E5%85%A5%E9%97%A840%EF%BC%9A%E6%8A%8A%E6%88%91%E7%9A%84%E5%86%99%E4%BD%9C%E5%B7%A5%E4%BD%9C%E6%B5%81Skill%E5%85%8D%E8%B4%B9%E5%88%86%E4%BA%AB%E7%BB%99%E4%BD%A0)
- [Obsidian 入门39：怎么创建自己的 Skill？我把五步拆给你看](/blog/Obsidian%20%E5%85%A5%E9%97%A839%EF%BC%9A%E6%80%8E%E4%B9%88%E5%88%9B%E5%BB%BA%E8%87%AA%E5%B7%B1%E7%9A%84%20Skill%EF%BC%9F%E6%88%91%E6%8A%8A%E4%BA%94%E6%AD%A5%E6%8B%86%E7%BB%99%E4%BD%A0%E7%9C%8B)
- [Obsidian 入门34：搞懂 Agent、MCP、Skill，看懂 AI 打工团队](/blog/Obsidian%20%E5%85%A5%E9%97%A834%EF%BC%9A%E6%90%9E%E6%87%82%20Agent%E3%80%81MCP%E3%80%81Skill%EF%BC%8C%E7%9C%8B%E6%87%82%20AI%20%E6%89%93%E5%B7%A5%E5%9B%A2%E9%98%9F)
- [Obsidian 入门27：装上Claude Code (CC),开启Obsidian × AI的时代](</blog/Obsidian%20%E5%85%A5%E9%97%A827%EF%BC%9A%E8%A3%85%E4%B8%8AClaude%20Code%20(CC)%2C%E5%BC%80%E5%90%AFObsidian%20%C3%97%20AI%E7%9A%84%E6%97%B6%E4%BB%A3>)
