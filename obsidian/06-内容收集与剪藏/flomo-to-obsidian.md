---
title: Obsidian 入门51：把 Flomo 碎片笔记也收进你的知识库
date: 2026-05-20
slug: flomo-to-obsidian
excerpt: Flomo 记了很多碎片想法，怎么同步到 Obsidian？Flomo Bridge 一键搞定。
cover: ""
tags:
  - 知识管理
  - Obsidian
  - 笔记同步
  - 效率工具
status: published
---

> 这是一个「Obsidian × AI」系列。
>
> 从网页剪藏到微信读书，再到今天的 Flomo，这个系列一直在聊怎么把散落在各个地方的信息收进 Obsidian。
>
> 如果你还没看过上一篇，可以先看 [Obsidian 入门50：把微信读书的笔记搬进你的第二大脑](/blog/Obsidian%20%E5%85%A5%E9%97%A850%EF%BC%9A%E6%8A%8A%E5%BE%AE%E4%BF%A1%E8%AF%BB%E4%B9%A6%E7%9A%84%E7%AC%94%E8%AE%B0%E6%90%AC%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%BA%8C%E5%A4%A7%E8%84%91)。

你有没有遇到过这种情况，手机上随时记了很多碎片想法，但从来没回过头去翻过。

Flomo(中文名称 - 浮墨) 就是这个场景里做得最好的工具之一。

启动快、有桌面小挂件、支持语音输入，遇到什么灵感掏出来就记。但这种「快」也有代价，碎片进来容易，想整体回顾、整理、跟其他笔记串联起来，就没那么方便了。

Flomo 擅长的事情跟 Obsidian 刚好互补。

---

## Flomo 负责 capture，Obsidian 负责 process

先说说为什么两个工具我都留着用。

Flomo 在手机上比 Obsidian 快太多了。快多少？「一个在天上，一个在地上」那种差距。点一下桌面小挂件就能开始记，支持文字也支持语音。Obsidian 的手机端也很好用，只是它的定位本来就不是随手记。

![Obsidian 入门51：把 Flomo 碎片笔记也收进你的知识库 - 截图 1](/images/posts/Obsidian%20%E5%85%A5%E9%97%A851%EF%BC%9A%E6%8A%8A%20Flomo%20%E7%A2%8E%E7%89%87%E7%AC%94%E8%AE%B0%E4%B9%9F%E6%94%B6%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%9F%A5%E8%AF%86%E5%BA%93/CleanShot%25202026-05-20%2520at%252013.22.50.webp)

Flomo 记的东西还有一个特点，它更接近你的真实想法。因为记的时候没有压力，不需要考虑格式、分类、标签，所以那些灵光一闪的瞬间反而能被捕捉下来。

但问题也在这里。

记完就封存了。Flomo 自己也上了 AI 功能，可以帮你做相关笔记推荐、AI 洞察，一年 99 块也不算贵。

但它始终停留在碎片整理的层面，不适合做大段的二次加工，也不方便跟 Obsidian 里那些「重笔记」串联。

所以最理想的状态是，Flomo 负责快速捕捉，Obsidian 负责整理沉淀。

而连接这两者的，就是今天要聊的这个插件 - Flomo Bridge(读作浮墨布瑞吉)

![Obsidian 入门51：把 Flomo 碎片笔记也收进你的知识库 - 配图 2](/images/posts/Obsidian%20%E5%85%A5%E9%97%A851%EF%BC%9A%E6%8A%8A%20Flomo%20%E7%A2%8E%E7%89%87%E7%AC%94%E8%AE%B0%E4%B9%9F%E6%94%B6%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%9F%A5%E8%AF%86%E5%BA%93/20260520204559175.webp)

## Flomo Bridge：连接 Flomo 和 Obsidian 的桥

Flomo Bridge 是一个 Obsidian 社区插件，作者是 giraffe-tree，目前标星 30 个，版本号 1.0.5。

![Flomoe-bridge](/images/posts/Obsidian%20%E5%85%A5%E9%97%A851%EF%BC%9A%E6%8A%8A%20Flomo%20%E7%A2%8E%E7%89%87%E7%AC%94%E8%AE%B0%E4%B9%9F%E6%94%B6%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%9F%A5%E8%AF%86%E5%BA%93/CleanShot%25202026-05-20%2520at%252013.18.08.webp)

它的工作方式很简单，通过 Flomo 的 API 把你所有的笔记拉到 Obsidian 里，每条笔记生成一个独立的 Markdown 文件。

### 来看看它能做什么

同步方式有三种：

- 第一次全量拉取所有笔记
- 之后每次只同步新增或修改过的。
- 也可以打开自动同步，设置一个间隔，它会自己在后台跑。

附件会跟着笔记一起下载到本地，图片和音频都有。你在 Flomo 里用过的 `[[互引]]`，同步后会自动转成 Obsidian 的内部链接格式。如果 Flomo 那边删了笔记，下次同步时本地对应的文件也会一起清理掉。

所有数据只存在本地，你的 Token 和笔记内容不会上传到任何服务器。

这一套功能基本覆盖了「把 Flomo 笔记搬进 Obsidian」的所有需求。

## 怎么装怎么用

安装不复杂，有两种方式。

**手动安装**：去 GitHub 的 Releases 页面下载三个文件，`main.js`、`manifest.json`、`styles.css`。然后在你的 Obsidian 库的 `.obsidian/plugins/` 下新建一个 `flomo-bridge` 文件夹，把这三个文件放进去。重启 Obsidian，在设置里启用插件就行了。

**用 BRAT 安装**：如果你装了 BRAT 插件，可以直接用它的方式安装。在 BRAT 设置里添加仓库地址 `giraffe-tree/flomo-bridge`，但要注意选对版本。我尝试的时候，不选版本号的话会提示找不到 `manifest.json`。选择最新的 **1.0.5** 版本就能正常安装了。

然后需要配置一个 Token。

![Obsidian 入门51：把 Flomo 碎片笔记也收进你的知识库 - 截图 4](/images/posts/Obsidian%20%E5%85%A5%E9%97%A851%EF%BC%9A%E6%8A%8A%20Flomo%20%E7%A2%8E%E7%89%87%E7%AC%94%E8%AE%B0%E4%B9%9F%E6%94%B6%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%9F%A5%E8%AF%86%E5%BA%93/CleanShot%25202026-05-20%2520at%252013.32.38.webp)

打开 v.flomoapp.com/mine 登录你的 Flomo 账号，按 F12 打开开发者工具，切换到 Network 标签。

刷新页面或者点一条笔记，找到一个 API 请求，在 Request Headers 里找到 Authorization 那一行，复制 Bearer 后面的那串字符。那就是你的 Token。

![Obsidian 入门51：把 Flomo 碎片笔记也收进你的知识库 - 截图 5](/images/posts/Obsidian%20%E5%85%A5%E9%97%A851%EF%BC%9A%E6%8A%8A%20Flomo%20%E7%A2%8E%E7%89%87%E7%AC%94%E8%AE%B0%E4%B9%9F%E6%94%B6%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%9F%A5%E8%AF%86%E5%BA%93/CleanShot%25202026-05-20%2520at%252020.30.34.webp)

把 Token 粘贴到插件设置里，设置一个同步目录（默认是 `flomo/）`，马上就会开始进行第一次全量同步。

![Obsidian 入门51：把 Flomo 碎片笔记也收进你的知识库 - 截图 6](/images/posts/Obsidian%20%E5%85%A5%E9%97%A851%EF%BC%9A%E6%8A%8A%20Flomo%20%E7%A2%8E%E7%89%87%E7%AC%94%E8%AE%B0%E4%B9%9F%E6%94%B6%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%9F%A5%E8%AF%86%E5%BA%93/CleanShot%25202026-05-20%2520at%252020.33.03.webp)

插件会在概览 tab 显示一个同步状态，最近一次同步时间和进度一目了然。

![Obsidian 入门51：把 Flomo 碎片笔记也收进你的知识库 - 截图 7](/images/posts/Obsidian%20%E5%85%A5%E9%97%A851%EF%BC%9A%E6%8A%8A%20Flomo%20%E7%A2%8E%E7%89%87%E7%AC%94%E8%AE%B0%E4%B9%9F%E6%94%B6%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%9F%A5%E8%AF%86%E5%BA%93/CleanShot%25202026-05-20%2520at%252020.36.18.webp)

同步完成后，你的 Flomo 笔记就会以独立 Markdown 文件的形式出现在你指定的目录里。点开一看，Frontmatter 里记着创建时间、标签、来源，正文就是你的原始内容，干净利落。附件也自动下载到本地了，不会裂图。

---

## 同步后的效果

每条笔记是一个独立的文件，文件名格式是 `{日期}_{标签}_{内容摘要}_{slug}.md`。文件头包含 Frontmatter，记录了 slug、创建时间、更新时间、标签等信息。

附件会存到 `attachments/` 子目录里，按日期归类。图片和音频都下载到本地，不会因为链接失效而丢失。

![Obsidian 入门51：把 Flomo 碎片笔记也收进你的知识库 - 配图 8](/images/posts/Obsidian%20%E5%85%A5%E9%97%A851%EF%BC%9A%E6%8A%8A%20Flomo%20%E7%A2%8E%E7%89%87%E7%AC%94%E8%AE%B0%E4%B9%9F%E6%94%B6%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%9F%A5%E8%AF%86%E5%BA%93/20260520203739568.webp)

如果你在 Flomo 里用过 `[[互引]]` 功能，同步后这些链接会自动转换成 Obsidian 的内部链接格式，跟你在 Obsidian 里写的双链一样工作。

## Flomo + Obsidian = 完整的工作流

说到底，Flomo 和 Obsidian 是搭档，各司其职的那种。

Flomo 负责那 80% 的「轻记录」，走在路上想到一个点子、听完播客冒出一个感悟、开会时灵光一闪。

这些内容在 Flomo 里记下来，丢给 Flomo Bridge 同步到 Obsidian，然后在你写长文、做复盘、建知识体系的时候，它们自然就被串联起来了。

那些碎片想法，不应该只在手机里躺平。

---

## 进阶阅读

- [Obsidian 入门50：把微信读书的笔记搬进你的第二大脑](/blog/Obsidian%20%E5%85%A5%E9%97%A850%EF%BC%9A%E6%8A%8A%E5%BE%AE%E4%BF%A1%E8%AF%BB%E4%B9%A6%E7%9A%84%E7%AC%94%E8%AE%B0%E6%90%AC%E8%BF%9B%E4%BD%A0%E7%9A%84%E7%AC%AC%E4%BA%8C%E5%A4%A7%E8%84%91)
- [Obsidian 入门49：从官方剪藏到社区增强，飞书B站公众号都能剪了](/blog/Obsidian%20%E5%85%A5%E9%97%A849%EF%BC%9A%E4%BB%8E%E5%AE%98%E6%96%B9%E5%89%AA%E8%97%8F%E5%88%B0%E7%A4%BE%E5%8C%BA%E5%A2%9E%E5%BC%BA%EF%BC%8C%E9%A3%9E%E4%B9%A6B%E7%AB%99%E5%85%AC%E4%BC%97%E5%8F%B7%E9%83%BD%E8%83%BD%E5%89%AA%E4%BA%86)
- [Obsidian 入门43：给剪藏插件加上 AI，剪藏完自动写摘要、打标签](/blog/Obsidian%20%E5%85%A5%E9%97%A843%EF%BC%9A%E7%BB%99%E5%89%AA%E8%97%8F%E6%8F%92%E4%BB%B6%E5%8A%A0%E4%B8%8A%20AI%EF%BC%8C%E5%89%AA%E8%97%8F%E5%AE%8C%E8%87%AA%E5%8A%A8%E5%86%99%E6%91%98%E8%A6%81%E3%80%81%E6%89%93%E6%A0%87%E7%AD%BE)
