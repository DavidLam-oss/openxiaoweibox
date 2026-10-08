---
title: （保姆级教程）Gemini 免魔法方案二：部署到 Zeabur
date: "2025-11-04"
excerpt: 保姆级教程：手把手教你利用 Zeabur 平台部署 Gemini API 代理，解决 Koyeb 部署受限问题，实现免魔法访问 Gemini。
tags:
  - AI模型
  - 编程开发
  - 效率工具
---

Hi，朋友们～

之前的[如何搭建不需要魔法也能使用的Gemini（保姆级教程）](/blog/%E5%A6%82%E4%BD%95%E6%90%AD%E5%BB%BA%E4%B8%8D%E9%9C%80%E8%A6%81%E9%AD%94%E6%B3%95%E4%B9%9F%E8%83%BD%E4%BD%BF%E7%94%A8%E7%9A%84Gemini%EF%BC%88%E4%BF%9D%E5%A7%86%E7%BA%A7%E6%95%99%E7%A8%8B%EF%BC%89)教你在 Koyeb 平台上搭建项目对 Gemini CLI 的 API，最终实现**不需要魔法也能访问 Gemini。**

- 之前为什么不用Render 而选择 Koyeb 是因为 Render 有时候会要求绑定信用卡。

- 为什么今天再出这一期教程，是因为有朋友按照教程在 Koyeb 部署到最后面的时候收到了下面这个提醒：“We cannot offer you access to Koyeb
  ![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 1](/images/posts/202511041859347.webp)

所以，今天再出一期教程，是在另外一个平台 - **Zeabur**。闲言少叙，让我们进入正题。

### 获取Google认证OAuth文件

> 如果你已经获得了 Google oAuth 文件，那么忽略这一步，直接跳到下一个步骤即可。

#### 1. 确认你的Google账号中存在至少一个项目

打开链接： https://console.cloud.google.com/ 使用 Google 账号登录。最好你的Google 账号开启了两步验证，这样可以确保你的谷歌账号绝对安全。

> 关于如何开启 Google 账号 两步验证，可参考以下公众号的文章：（此处插入文章）

部分人的Google账号中没有项目，所以可以先检查一下或者创建一个项目。若没有项目，选择我左上角的项目选择器即可，点开，新建一个项目。
![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 2](/images/posts/202510301531049.webp)

**如果你之前的Google账号已经提取过API key，或者自己创建过项目，这里就直接忽略下方的创建项目内容，跳转到下一步 `获取认证链接`**

#### 2. 访问认证网站

我们通过sukaka老师搭建的认证网站来获取凭证。通过这个方法获取凭证，整个的操作步骤几乎被简化到极致。

访问认证网站： [http://gcli-auth.sukaka.top:7861/](http://gcli-auth.sukaka.top:7861/)

输入访问密码： `pwd`

即可进入Google OAuth认证页面。

![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 3](/images/posts/202510301535042.webp)

#### 3. 获取认证链接

在页面中，你可以直接点击 `获取认证链接` 按钮，来获取认证链接

也可以点击 `高级选项` 部分输入你的项目ID，如果你不知道这个是什么，就不要输入，让系统自己检测。

点击了获取认证链接后，会出现一个很长的链接，点击打开。如图：
![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 截图 4](/images/posts/202510301540799.webp)

#### 4. Google账号认证

点击上一步获取到的那条很长的链接。点击后，会让你登录你的Google账号，请根据提示自行登录。

登录完成后会出现一个 `错误页面` 。
![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 截图 5](/images/posts/202510301542054.webp)

我们需要更改一下地址栏（浏览器中输入网址的地方）的链接。

将地址中的 `localhost` 更改为 `gcli-auth.sukaka.top` （直接复制下面的地址也行）

```ts
gcli - auth.sukaka.top;
```

![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 截图 6](/images/posts/202510301546952.webp)

> **注意：localhost 后方的冒号也需要保留，只需替换 localhost 即可。其他的任何地方都不要改**

更改完成后，按回车访问这个地址。

会出现 `OAuth authentication successful!` （如果没出现的话，确定网址你没有改错，然后可以刷新几次试试）。如图：

![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 7](/images/posts/202510301547159.webp)

#### 5. 获取认证文件

返回到上一个标签页，点击页面中的`获取认证文件`，稍等片刻，会显示`步骤二：认证成功`

我们先点击 `下载认证文件`，将认证文件下载下来。

![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 8](/images/posts/202510301552037.webp)

这个页面不用关闭，等下直接复制那一串认证的内容也可以的。

至此Google认证已经完成。

### 注册Zeabur

通过链接注册：https://zeabur.com/login。推荐使用 Google 登录，简便快捷。这个平台是有中文支持的，你可以选择中文进入，之后的界面都会显示为中文的语言了。

![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 9](/images/posts/202511041851721.webp)

进入之后最终会进入下面这个界面。因为我之前部署过项目，所以我的界面是下图的样子。可能你是第一次进入的话，中间会有一些要你的问题或者步骤，自行判断完成即可。
![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 10](/images/posts/202511041555092.webp)

### 创建和部署项目

此时，点击右上角的 `new project` 旁边的下拉箭头，免费用户只能看到两个区域可供选择：印尼雅加达和美国硅谷。建议选择美国硅谷。
![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 11](/images/posts/202511041556312.webp)

选择完地区之后，会进入下面这个界面去 Add service。选择`Docker Image`。
![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 12](/images/posts/202511041556585.webp)

接着会进入下面这一步，填入相关的信息：

- Image：填入`ghcr.io/gzzhongqi/geminicli2api:latest`
- Environment Variables(环境变量)，这个地方需要点击`Add Environment Variables`去添加到 3 个框 - GEMINI_CREDENTIALS：复制你刚刚在第一步获取的Google OAuth认证文件中的内容（花括号也要）。- PORT：填”8888“ - GEMINI_AUTH_PASSWORD：请自行填写一个密码，这将是你调用API的密钥。
  ![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 13](/images/posts/202511041558840.webp)

接着往下拉，下方会有一个`Ports`，将 Port 填写为“8888”；Port Type不变。
![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 截图 14](/images/posts/202511041600891.webp)
确认以上信息都填写无误后，点击 Deploy。

### 获取公网访问地址

上面点击 Deploy 之后，会到如下这个界面。状态会显示“Queued”表示这个部署正在排队中，此时等待即可，有时候会很快就部署好，有时候可能需要等待几分钟。

![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 15](/images/posts/202511041602954.webp)

部署成功后，`Queued`会变成`Running`。
![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 截图 16](/images/posts/202511041628420.webp)

与 Render 和 Koyeb 在部署完成后会自动分配公网地址不一样，Zeabur需要自己去生成公网地址。

点击去到`Networking`，点击 Domain 下方的“Generate Domain”，会弹出一个弹窗。在弹窗内，可以自己输入一个想要的前缀，系统会提示是否可用。显示 available 之后，就可以点击确认了。

![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 截图 17](/images/posts/202511041643387.webp)

刚刚确认的时候，状态会变成“Provisioning”，此时等待即可。完成后会变成绿色的“Provisioned“。

最后面补充一点：在Zeabur 部署的服务不会陷入休眠，所以不需要像 Render 和 Koyeb 要进行保活操作。Zeabur每个月会赠送 5 美金的额度，如果在这个额度内就不会有什么问题，个人用户一个月 5 美金基本上够用了

### Cherry studio配置

此处通过 Cherry studio 来演示在各种客户端中怎么添加模型。

打开 Cherry studio，点击设置->模型服务->添加。在下方的弹窗中

- 提供商名称自己命名即可。
- 提供商类型，选择 OpenAI
  ![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 18](/images/posts/202511041719667.webp)

接着在界面上，填入你在Zeabur 设置的参数和地址

- API 密钥：填写你在 Zeabur 设置的环境变量中的GEMINI_AUTH_PASSWORD的值。
- API 地址：填写你在 Zeabur 最后得到的公网地址。记得最后面不要有`/`. 注意：Cherry Studio 只需要填根地址，但别的客户端，比如 Rikkahub，可能需要你填入完整的 /v1 路径，请你根据你所用客户端的指引来操作。
  ![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 截图 19](/images/posts/202511042042013.webp)

测试，最终成功对话。
![（保姆级教程）Gemini 免魔法方案二：部署到 Zeabur - 配图 20](/images/posts/202511041722904.webp)

---

Enjoy～

如果你在这个过程中有任何问题，可以加我微信“linauwawa”备注"Zeabur”进行交流，希望你一切顺利！
