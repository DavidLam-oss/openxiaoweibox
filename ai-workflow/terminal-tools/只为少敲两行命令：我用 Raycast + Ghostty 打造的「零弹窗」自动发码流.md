---
title: "只为少敲两行命令：我用 Raycast + Ghostty 打造的「零弹窗」自动发码流"
date: "2026-07-25"
slug: "raycast-ghostty-auto-license"
excerpt: "每次用户购买都要手动切目录、敲预检、等结果。重复了几十次后，我用 Raycast + Ghostty 把前面的死步骤自动化了。"
tags:
  - Raycast
  - 终端命令行
  - 自动化
  - WeChat Converter
  - 副业与出海
  - 苹果生态
  - 效率工具
status: published
---
## 快乐的烦恼

我一直在维护一款 Obsidian 插件，叫做 Wechat converter ，可以将 Obsidian 的笔记一键同步到微信公众号、小红书、知乎、头条、抖音、飞书等平台。特别是针对公众号，可以实现精美排版后再同步。

![Obsidian WeChat Converter 插件主界面与 Pro 功能](/images/posts/CleanShot%202026-07-25%20at%2023.01.31.webp)


为了维持项目持续运转，在保持公众号发布和飞书同步免费模式的基础上，还加上了 Pro 模式。随着付费用户增加，我遇到了一个快乐的烦恼：**手动签发 License Key**。

每次有用户购买，流程是这样的：

1. 打开终端，`cd` 到项目目录
2. 跑一行预检命令，检查服务在线、鉴权正常
3. 再敲生成命令，填邮箱、备注、有效期

重复了几十次之后，我意识到一件事：**前面两个步骤完全是死步骤，只有最后一步需要我根据用户情况去填参数。**

![手动签发 License Key 的终端命令流程](/images/posts/20260725231611519.webp)


既然前面全是固定动作，为什么不拿 Raycast 把它一键自动化？

## 为什么选择 Raycast?

是因为我一直在我的 mac 上用着 Raycast。

从 [Snippet 快速输入](/blog/Raycast%20%E5%85%A5%E9%97%A8%E6%8C%87%E5%8D%97%EF%BC%9AmacOS%20%E4%B8%8A%E7%9A%84%E6%95%88%E7%8E%87%E7%A5%9E%E5%99%A8) 到翻译、从 IP 检测到各种自动化脚本，Raycast 是我的快捷面板。

所以当遇到下面这个场景时，我的第一反应不是去搜新工具，而是「Raycast 能不能跑一个脚本搞定它？」

---

## 探索一分钟，解决两小时

目标很简单：在 Raycast 里按回车，自动在 Ghostty 中打开项目目录、跑完预检、然后光标留在终端等我敲 Key。

听起来只是两三行脚本的事，但 Ghostty + macOS 这个组合给我上了一课。试了几个方案：

- AppleScript 模拟按键？焦点一飘就打到空气里
- Ghostty 的 `-e` 参数？每次启动弹安全弹窗，要手动点 Allow
- macOS 的 `open -a`？参数被静默忽略，多一个空白 Tab

几个方案各有各的翻车方式。

最后绕回来的思路是：**只要启动 Ghostty 时不带 `-e` 参数，它就认为是在打开一个正常 Shell，安全弹窗 100% 绕过。**

于是有了下面这个脚本。

---

## 最终方案：ZDOTDIR 动态注入 + 静默自毁

```bash
#!/bin/bash

# @raycast.schemaVersion 1
# @raycast.title ob-publisher
# @raycast.mode silent
# @raycast.icon 🔑

PROJECT_DIR="$HOME/code/obsidian-publisher"
GHOSTTY_BIN="/Applications/Ghostty.app/Contents/MacOS/ghostty"

# 创建临时 ZSH 配置目录
TMP_ZDOTDIR=$(mktemp -d /tmp/ghostty_zsh_XXXXXX)

# 写入一次性初始化逻辑
cat << 'EOF' > "$TMP_ZDOTDIR/.zshrc"
[[ -f "$HOME/.zprofile" ]] && source "$HOME/.zprofile"
[[ -f "$HOME/.zshrc" ]] && source "$HOME/.zshrc"

echo "🔍 预检中..."
pnpm license:list --limit 1

# 执行完自毁，不留痕迹
rm -rf "$ZDOTDIR"
unset ZDOTDIR
EOF

# 调起 Ghostty，彻底解耦，防 Raycast 卡死
ZDOTDIR="$TMP_ZDOTDIR" "$GHOSTTY_BIN" --working-directory="$PROJECT_DIR" >/dev/null 2>&1 &
disown
```

脚本做了三件事：

1. 在 `/tmp` 生成一个临时 ZSH 配置文件，里面写好预检命令
2. 通过 `ZDOTDIR` 环境变量让 Ghostty 启动时自动加载它
3. 预检执行完后，临时文件自我销毁

因为 Ghostty 没有收到任何 `-e` 参数，它完全认为自己只是打开了一个正常终端——安全弹窗不存在了。脚本使用 `>/dev/null 2>&1 &` 加 `disown`，Raycast 毫秒级退出，不卡界面。

---

## 用起来的感受

现在有人下单，我只要在任意界面敲 `Option + Space`（唤出 Raycast），输入 `ob-publisher` 回车。

![Raycast 执行 ob-publisher 命令](/images/posts/20260725231639524.webp)


Ghostty 瞬间拉起，预检结果已经打在了屏幕上。我填上买家邮箱、按下回车就能生成授权码，整个过程不到 5 秒。

**以前那些切目录、敲预检、等结果的「仪式感」，全被这个脚本吃掉了。**

剩下的只留给真正需要判断的事情。

*如果你也在用 Raycast，可以看看之前写的 [因为受不了“手动同步”的蠢，我让 Raycast 和 AI 接管了我的博客](/blog/%E5%9B%A0%E4%B8%BA%E5%8F%97%E4%B8%8D%E4%BA%86%E2%80%9C%E6%89%8B%E5%8A%A8%E5%90%8C%E6%AD%A5%E2%80%9D%E7%9A%84%E8%A0%A2%EF%BC%8C%E6%88%91%E8%AE%A9%20Raycast%20%E5%92%8C%20AI%20%E6%8E%A5%E7%AE%A1%E4%BA%86%E6%88%91%E7%9A%84%E5%8D%9A%E5%AE%A2)，思路差不多。*
