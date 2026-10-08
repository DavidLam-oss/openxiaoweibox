---
title: 如何搭建不需要魔法也能使用的Gemini（保姆级教程）
date: "2025-10-30"
excerpt: >-
  手把手教你利用 Koyeb 免费部署 Gemini CLI 反代服务，配合 Google OAuth 认证，实现无需魔法、无频率限制地调用 Gemini
  API，并集成到 Cherry Studio 和手机端。
tags:
  - AI模型
  - 编程开发
  - 服务器运维
  - 效率工具
---

现在很多朋友在申请了 Google AI studio 的免费 API 在使用，但是有2个问题：

- 基本上在 call 这些 API 的时候都需要挂上魔法
- Rate limit 有限，限制了每分钟的次数和 token 上限等。

我之前在 Cherry studio 配置了Gemini 的API 之后，时不时的就会碰到红色报错。

于是，我在网上搜索了很多的资料想搞清楚怎么去解决这个问题，也跟 AI 聊了很多轮怎么去解决这个问题。

最终发现可以部署 Gemini 反代，部署成功后用部署后的 API key 和 API 地址去调用，就可以尽可能地规避以上 2 个问题。

我查到的主流教程大都基于 Render 平台，但我在实践中发现，Render 对 IP 纯净度要求很高，容易触发绑定信用卡，不够‘丝滑’。

经过进一步的测试，我找到了一个更稳定、更简单的免费平台：Koyeb。 下面，就是我基于 Koyeb跑通的保姆级教程（**真·有手就行！**）。

### 注册 Koyeb 账号

1，注册/登录Koyeb

地址： https://app.koyeb.com/auth/signup

建议直接使用Github或者用邮件创建并登Koyeb。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 1](/images/posts/202510301517431.webp)

根据提示登录或者完成认证。登录后需要回答 4 个问题，你可以随便回答或者点击"Skip“跳过，完成这个步骤之后，会进入如下页面。保持在这页面，先不要关闭。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 2](/images/posts/202510301523964.webp)

### 获取Google认证OAuth文件

#### 1. 确认你的Google账号中存在至少一个项目

打开链接： https://console.cloud.google.com/ 使用 Google 账号登录。最好你的Google 账号开启了两步验证，这样可以确保你的谷歌账号绝对安全。

> 关于如何开启 Google 账号 两步验证，可参考以下公众号的文章：（此处插入文章）

部分人的Google账号中没有项目，所以可以先检查一下或者创建一个项目。若没有项目，选择我左上角的项目选择器即可，点开，新建一个项目。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 3](/images/posts/202510301531049.webp)

**如果你之前的Google账号已经提取过API key，或者自己创建过项目，这里就直接忽略下方的创建项目内容，跳转到下一步 `获取认证链接`**

#### 2. 访问认证网站

我们通过sukaka老师搭建的认证网站来获取凭证。通过这个方法获取凭证，整个的操作步骤几乎被简化到极致。

访问认证网站： [http://gcli-auth.sukaka.top:7861/](http://gcli-auth.sukaka.top:7861/)

输入访问密码： `pwd`

即可进入Google OAuth认证页面。

![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 4](/images/posts/202510301535042.webp)

#### 3. 获取认证链接

在页面中，你可以直接点击 `获取认证链接` 按钮，来获取认证链接

也可以点击 `高级选项` 部分输入你的项目ID，如果你不知道这个是什么，就不要输入，让系统自己检测。

点击了获取认证链接后，会出现一个很长的链接，点击打开。如图：
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 5](/images/posts/202510301540799.webp)

#### 4. Google账号认证

点击上一步获取到的那条很长的链接。点击后，会让你登录你的Google账号，请根据提示自行登录。

登录完成后会出现一个 `错误页面` 。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 6](/images/posts/202510301542054.webp)

我们需要更改一下地址栏（浏览器中输入网址的地方）的链接。

将地址中的 `localhost` 更改为 `gcli-auth.sukaka.top` （直接复制下面的地址也行）

```ts
gcli - auth.sukaka.top;
```

![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 7](/images/posts/202510301546952.webp)

> **注意：localhost 后方的冒号也需要保留，只需替换 localhost 即可。其他的任何地方都不要改**

更改完成后，按回车访问这个地址。

会出现 `OAuth authentication successful!` （如果没出现的话，确定网址你没有改错，然后可以刷新几次试试）。如图：

![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 8](/images/posts/202510301547159.webp)

#### 5. 获取认证文件

返回到上一个标签页，点击页面中的`获取认证文件`，稍等片刻，会显示`步骤二：认证成功`

我们先点击 `下载认证文件`，将认证文件下载下来。

![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 9](/images/posts/202510301552037.webp)

这个页面不用关闭，等下直接复制那一串认证的内容也可以的。

至此Google认证已经完成。

### 部署 CLI 反代

在Koyeb 中，点击`Web service`，接着选择`Docker`。我们将部署gzzhongqi 老师的 geminicli2api项目，根据实践，这个项目更加简单和稳定。

![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 10](/images/posts/202510301559694.webp)

下一步，Docker image 填下面这个地址，接着点击下一步。

```ts
ghcr.io/gzzhongqi/geminicli2api:latest
```

![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 11](/images/posts/202510301618623.webp)

到下一步，默认是会显示中间的“CPU Standard”。我们切换到“CPU Eco”,选择第一个“Free”也就是免费。Region 选择“Washington DC”
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 12](/images/posts/202510301619665.webp)

下一步，我们要配置环境变量，填完一个之后点击”Add another"填下一个。分别是：

- GEMINI_CREDENTIALS：需要复制刚刚你获取的Google OAuth认证文件中的内容，如果你没有关闭刚刚的认证文件，可以直接复制填入。（花括号也要）
- PORT：填”8888“
- GEMINI_AUTH_PASSWORD：请自行填写一个密码，这将是你调用API的密钥。

确认无误后，点击“Deploy”。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 13](/images/posts/202510301621319.webp)

**切记将下方的“Ports"从默认的 8000 改成我们需要的”8888“。**

点击“Deploy后，请稍作等待，页面会跳到下一个界面。此界面无需进行任何操作。等待约一分钟，系统将自动跳转至下方界面。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 14](/images/posts/202510301640551.webp)

如果一直没有反应，可以刷新页面或者再继续等待一会。完成后将得到下面的页面，红框框起来的位置就是你的公网地址，也就是后续我们要用到的 API base url。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 15](/images/posts/202510301701299.webp)

### 设置Koyeb 服务保活

因为我们使用的是Koyeb 的免费服务，在 1 个小时没有活动后服务会自动陷入休眠。我们需要设置一个定时任务定期的去访问才能避免休眠。

#### 1. 注册Uptimerobot

打开以下链接注册，注册后会发送一封激活邮件。
[https://dashboard.uptimerobot.com/sign-up](https://dashboard.uptimerobot.com/sign-up)

#### 2. 创建Monitor

完成后他会引导你创建第一个 monitor。在 URL to monitor 中输入你在 Koyeb 获取到的 public address，在地址后加/docs。例如你的地址是：abc.koyeb.app。那么此时你应该输入 abc.koyeb.app/docs

可以参考下面这张图进行设置。email通知不想要的话，就取消勾选。我设置了 50 分钟间隔去触发一次访问上面的 URL，你可以根据你的需要和意愿进行选择。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 16](/images/posts/202510301752702.webp)

最后，点击创建就可以了

#### 更改项目设置

在控制面板中，点击打开你刚刚创建的 monitor。检查设置是否都正确，特别是检查一下 url 是否有出入，如果有要修改的地方，点击右上角”Edit“即可进行修改。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 17](/images/posts/202510301758033.webp)

### 在Cherry studio进行设置

在 Cherry studio 中，打开设置->模型服务，点击下方的“添加”。提供商名称你可以自己命名即可，类型选择“OpenAI”。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 18](/images/posts/202510301800888.webp)

填入 API 密钥和API 地址：

- API 密钥：就是我们在部署 Koyeb 服务时，其中一个变量 - GEMINI_AUTH_PASSWORD的值。
- API 地址：填写你的Koyeb 服务的公网地址。复制过来之后记得将 url 最后的“/”去掉。
  ![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 19](/images/posts/202510301809964.webp)

点击下方的“管理”按钮，即可添加模型。 我们一般选择 gemini-2.5-pro 和 gemini-2.5-flash。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 20](/images/posts/202510301811042.webp)

设置好后，我们进入聊天窗口进行测试，测试成功！
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 21](/images/posts/202510301814596.webp)

### 移动端Rikkahub（安卓）设置

如果想要在移动端也畅想自己的模型，推荐下载：

- 安卓：Rikkahub
  ![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 22](/images/posts/202510301823634.webp)

- iOS: Apollo - Powered by liquid
  ![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 截图 23](/images/posts/202510301824626.webp)

因为我只有安卓手机，所以用 Rikkahub 来做演示。点击设置->提供商，然后点击右上角“+”，在添加供应商弹窗中，参照 Cherry studio 的设置进行填写即可。

- 名称：按照自己的喜好命名即可
- API key：填写我们在 Koyeb 的环境变量的密码
- API base url：为 Koyeb 服务的公网地址。此时，记得在 url 最后面加“/v1”。

添加成功后保存，移动到模型界面，稍等一会可用模型会加载出来，按需选择即可。
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 24](/images/posts/202510301843558.webp)

![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 25](/images/posts/202510301843566.webp)

![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 26](/images/posts/202510301843565.webp)
![如何搭建不需要魔法也能使用的Gemini（保姆级教程） - 配图 27](/images/posts/202510301843564.webp)

> **版权声明**
>
> - 该教程非本人完全创作，其中大量参考老婆宝老师的教程，本教程在原教程基础上做了验证和补充、删减，并优化了UptimeRobot保活方式。
> - 本教程添加了电脑端Cherry studio配置步骤和手机端Rikkahub（安卓）的配置步骤
> - 原教程地址：docs.laopobao.online
> - 该教程项目来自Github @su-kaka 老师的 gcli2api 项目，和 gzzhongqi 老师的 geminicli2api项目
> - Github项目地址： [su-kaka/gcli2api-点击进入](https://github.com/su-kaka/gcli2api)
> - Github项目地址： [gzzhongqi/geminicli2api-点击进入](https://github.com/gzzhongqi/geminicli2api)

> **部署说明**
>
> - 本教程的CLI反代基于Koyeb署。原教程基于Render部署，因 IP 不纯净的话会提示需要绑定信用卡，故更换到Koyeb部署，步骤和Render基本一致。
> - Koyeb部署，部署过程简单方便，且可以脱离电脑使用（不需要电脑一直开着）。

> **关于Google CLI**
>
> - 简单来说，Google Gemini CLI是基于终端的AI编程工具，这个你有兴趣可以自行了解。
> - 对于个人日常使用而言，Google CLI每天1000次请求，每分钟60次，上下文100w左右。
> - 对于个人用户而言，一个账户基本足够满足使用，2.5限额情况不定，根据原教程的说明， \*\*429时可以切换到0506、0605模型，会重定向到gemini-2.5-pro
