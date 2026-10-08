---
title: 怎么在 Mac 安装 Stable Diffusion
date: "2025-01-02"
excerpt: >-
  保姆级教程：手把手教你在 Mac 上安装 Stable Diffusion WebUI
  (Automatic1111)，涵盖环境配置、国内镜像加速及常见问题解决。
tags:
  - 内容创作
  - 苹果生态
  - 服务器运维
---

## 准备工作

- 确保 macOS 版本为 12.3 或更高
- 安装 homebrew，若还未安装可参考[怎么在 Mac 安装homebrew](/blog/怎么在%20Mac%20安装homebrew)
- 安装 Python 3.10

---

### 安装Python 3.10

通过以下命令安装 python 3.10

```bash
brew install python@3.10
```

等待命令跑完后，运行以下命令查看 Python 的版本

```bash
python3.10 --version
```

如果输出的不是 3.10，那么可以通过以下命令查看Python 3.10 的安装路径

```bash
which python3.10
```

通常通常，Homebrew 安装的 Python 3.10 路径为 `/usr/local/opt/python@3.10/bin/python3.10`

运行以下命令查看这个路径里面的 Python 是否 3.10 了

```bash
/opt/homebrew/bin/python3.10 --version
```

如果得到的结果是 `Python 3.10.x`，说明 Python 3.10 已正确安装。

## 克隆 Automatic1111 Web UI 仓库

运行以下命令

```bash
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

如果速度非常慢，甚至没有速度，这通常是由于 GitHub 的服务器位于国外，国内访问时可能受到网络限制或延迟的影响。可以使用国内镜像进行克隆

```
git clone https://gitclone.com/github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

## 安装和运行 Automatic1111 Web UI

1. 进入项目目录

```bash
cd stable-diffusion-webui
```

2. 创建 Python 3.10 虚拟环境

```bash
python3.10 -m venv venv
source venv/bin/activate
```

3. 安装依赖

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

4. 启动 web UI

```bash
./webui.sh
```

## 启动 web UI

### stable-diffusion-webui-assets

启动后，会首先克隆克隆 stable-diffusion-webui-assets， 如果碰到问题或者没有速度，需要替换为国内的镜像。
按照以下步骤操作：

- 打开路径： `/stable-diffusion-webui/modules/launch_utils.py`。 找到`launch_utils.py`，双击打开。
- 找到以下代码

```bash
assets_repo = "https://github.com/AUTOMATIC1111/stable-diffusion-webui-assets.git"
```

- 将 url 替换为国内镜像

```bash
assets_repo = "https://gitclone.com/github.com/AUTOMATIC1111/stable-diffusion-webui-assets.git"
```

### stablediffusion

接着会克隆stablediffusion， 如果碰到和上述一样的问题，重复类似的步骤，将 url 替换为国内镜像。

```bash
stable_diffusion_repo = "https://gitclone.com/github.com/Stability-AI/stablediffusion.git"
```

### generative-models

接着克隆generative-models，如果碰到和上述一样的问题，重复类似的步骤，将 url 替换为国内镜像。

```bash
stable_diffusion_xl_repo = "https://gitclone.com/github.com/Stability-AI/generative-models.git"
```

### k-diffusion

接着克隆k-diffusion，如果碰到和上述一样的问题，重复类似的步骤，将 url 替换为国内镜像。

```bash
k_diffusion_repo = "https://gitclone.com/github.com/crowsonkb/k-diffusion.git"
```

### BLIP

接着克隆BLIP，如果碰到和上述一样的问题，重复类似的步骤，将 url 替换为国内镜像。

```bash
blip_repo = "https://gitclone.com/github.com/salesforce/BLIP.git"
```

**请记住，上述启动 web UI 的步骤中克隆仓库的动作，每次修改后都需要启动 web UI 继续刚刚失败的动作**

```bash
cd stable-diffusion-webui
./webui.sh

```

启动成功后，将会调用浏览器打开 web UI 界面，如下图所示
![attachments/CleanShot%202025-01-02%20at%2021.23.23](/images/posts/CleanShot-2025-01-02-at-21.23.23.webp)
可以输入prompt，然后点击“Generate”去生成图像，此时电脑将全速跑起来进行计算。
在 terminal 窗口，能看到图像生成的进度。
![attachments/CleanShot%202025-01-02%20at%2021.27.07](/images/posts/CleanShot-2025-01-02-at-21.27.07.webp)
以下是我刚刚生成的图像。
![attachments/00001-3382828513](/images/posts/00001-3382828513.webp)

## 退出web UI

- 关闭浏览器标签页。
- 同时，关闭 terminal 即可退出。
