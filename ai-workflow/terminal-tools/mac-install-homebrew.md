---
title: 怎么在 Mac 安装homebrew
date: "2024-12-30"
tags:
  - 苹果生态
  - 终端命令行
excerpt: 本指南将带你快速在 macOS 上安装及配置 Homebrew。内容涵盖了常规安装、使用国内镜像加速，以及安装后的验证方法。
---

### 打开 Terminal

在键盘按 command+ space 打开 spotlight，输入“terminal”将会打开 Mac 的终端

### 输入 Command

输入如下 command

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

如果碰到下面的 error，则需要通过国内镜像来安装

```bash
curl: (7) Failed to connect to raw.githubusercontent.com port 443 after 42 ms: Couldn't connect to server
```

### 使用国内镜像

复制一下命令到终端运行

```bash
export HOMEBREW_BREW_GIT_REMOTE="https://mirrors.ustc.edu.cn/brew.git"
export HOMEBREW_CORE_GIT_REMOTE="https://mirrors.ustc.edu.cn/homebrew-core.git"
export HOMEBREW_BOTTLE_DOMAIN="https://mirrors.ustc.edu.cn/homebrew-bottles"
export HOMEBREW_API_DOMAIN="https://mirrors.ustc.edu.cn/homebrew-bottles/api"
```

接着复制以下命令到终端运行安装脚本

```bash
/bin/bash -c "$(curl -fsSL https://mirrors.ustc.edu.cn/misc/brew-install.sh)"
```

### 将 Homebrew 添加到环境变量中

安装完成后，会有提示说 homebrew 不在环境变量中，需要按照提示添加![怎么在 Mac 安装homebrew - 截图 1](/images/posts/CleanShot-2024-12-30-at-23.04.07@2x.webp)
运行完第一段，等待结束后再运行第二段
![怎么在 Mac 安装homebrew - 截图 2](/images/posts/CleanShot-2024-12-30-at-23.08.23@2x.webp)

### 验证是否安装成功

等待上述命令都跑完后，输入以下去验证

```bash
brew help
```

如果能正常得到结果，那么恭喜你：说明已经安装成功了！
