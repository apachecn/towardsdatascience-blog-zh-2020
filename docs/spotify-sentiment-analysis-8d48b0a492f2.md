# Spotify 情感分析

> 原文：<https://towardsdatascience.com/spotify-sentiment-analysis-8d48b0a492f2?source=collection_archive---------12----------------------->

## 对 Spotify 播放列表中的歌词进行情感分析

# 介绍

你有没有想过你听的音乐周围都是什么样的数据？这么多不同的音乐应用程序正在将复杂的数据科学和机器学习技术应用于我们的音乐数据，并获得了非常酷的输出。例如，Spotify 是最受欢迎的应用之一，由我们听的音乐、我们喜欢的歌曲以及我们创建和遵循的播放列表驱动，为其用户和社区提供个性化产品。

当我查看 Spotify 收集的[数据](https://developer.spotify.com/documentation/web-api/reference/tracks/get-audio-analysis/)时，我注意到他们从音乐本身收集音频特征。所以声音、舞蹈、能量、节奏等的水平。但是最突出的特征是*音频价*。

> 音频效价:从 0.0 到 1.0 的一个量度，描述一个音轨所传达的音乐积极性。高价曲目听起来更积极(例如，快乐、愉快、欣快)，而低价曲目听起来更消极(例如，悲伤、沮丧、愤怒)。

所以，从这个属性出发，Spotify 可以为我们生成播放列表，播放更乐观积极的歌曲，或者更圆润消极的歌曲。虽然这很聪明，但我最近遇到了一些不准确的结果 Spotify 为我生成的正面播放列表中有悲伤的歌曲。我想知道是什么决定把它放在那里。

如果我们看看 80 年代普林斯的经典歌曲《当鸽子哭泣时》的音频特征，Spotify 的结果显示这是一首活泼的歌曲——这是真的，它有相当时髦的节奏！🕺🏻🕊️

`{"danceability": 0.729, "energy": 0.989, "loudness": -4.613, "speechiness": 0.049, "acousticness": 0.0102, "instrumentalness": 0.0000445, "liveness": 0.443, "valence": 0.84, "tempo": 126.47, "duration_ms": 352906}`

但是在与之相关的化合价分数(0.84 表示正化合价)和[歌词](https://www.musixmatch.com/lyrics/Prince/When-Doves-Cry)所表达的内容方面存在矛盾。虽然听众可以对歌词的含义有自己的解释，但这首歌使用了鸽子和紫色紫罗兰这两个众所周知的爱情象征，来表达一对相爱的夫妇之间不断争吵之前的事情。下面的歌词只是一些表达心碎和悲伤的例子:

你怎么能让我一个人站着？
一个人在这么冷的世界里？
…
我们为什么要对着对方尖叫？
这是鸽子哭泣时的声音

鉴于这一发现，我很快对这个想法产生了兴趣，即我们是否可以通过更深入地研究音乐本身并对我们播放列表中的歌曲歌词进行情感分析，来获得对我们正在听的音乐的价值的更多了解。

> 情感分析:自动识别文本中表达的观点或情感，以确定作者的态度是积极、消极还是中立。

在这种情况下，我开发了一个 **Spotify 情感分析**应用程序，Spotify 用户可以从中了解更多关于他们歌曲的情感。

这个帖子讲的是 app 的开发。我试图让文本尽可能简单明了，同时仍然提供技术细节。不管怎样，事情可能会变得有点古怪。所以坚持住，如果你坚持到最后，一定要点击“喜欢”按钮。但是如果你想跳过技术对话，直接使用这个应用，那就去主持的[吧。](https://spotify-sentiment-analysis.herokuapp.com/)

# 通用烧瓶应用说明

对于那些不熟悉框架的人来说，Flask 允许你用 Python 创建 web 应用。如果我想实现一些看起来不错的东西，我会转向 Flask，使用一个免费的 Bootstrap 主题作为界面的基础。这就是 Flask 的真正用途——它旨在快速轻松地开始使用，并能够扩展到更复杂的应用程序。

在这篇文章的这一部分，我决定给出一个关于我如何设置和构建我的 Flask 应用程序的快速分解。我已经使用 Flask 好几次了，但是当我第一次使用它时，我注意到文档有点混乱，很难快速掌握。所以，这里有一个我如何做的快速和一般的解释。

**虚拟环境**

Python 使用虚拟环境为不同的应用程序维护不同版本的包。您可以为每个应用程序设置不同的虚拟环境，并控制这些应用程序使用的软件包版本。

前往你的终端，使用`cd name_of_directory`导航到你希望你的 Flask 应用程序的目录所在的任何地方。这里，我们将创建一个名为*Spotify _ 情操 _ 分析*的目录，然后我们将使用`cd`导航到该目录。

虚拟环境包含在 Python 3 中，因此我们将创建一个虚拟环境，而无需安装任何东西。命令中的第一个`venv`是 Python 虚拟环境包的名称，第二个是我将用于这个特定环境的虚拟环境名称。

我们现在应该已经创建了一个虚拟环境。为了能够使用它，我们需要激活它，然后使用 pip 在其中安装 Flask。为了确认虚拟环境成功安装了 Flask，我们可以启动 Python 解释器和`import` Flask。

没有输出是一个好的输出，意味着 Flask 安装正确，可以使用了！💡

**应用包**

这个应用程序将存在于一个*包*中。这意味着，在 Python 中，包含一个`__init__.py`文件的子目录被视为一个包，可以被导入。我们将创建一个名为 *app* 的包——它将托管应用程序。要做到这一点，请确保你在正确的目录中(在本例中，是*Spotify _ 情操 _ 分析*)，并创建一个名为 *app* 的新目录。当我们在终端时，我们可以创建空文件`__init__.py`。

然后,`__init__.py`文件将包含一个脚本，该脚本创建 application 对象作为 Flask 从其包中导入的类的实例。传递给 Flask 类的`__name__`变量是一个预定义的 Python 变量，它被设置为使用它的模块的名称。然后我们导入`routes`模块，它还不存在，但是在我们声明了`app`变量之后被导入。这是因为`routes`模块导入了`app`变量。

**路线**

那么，`routes`模块中有什么呢？路由是 Flask 应用程序实现的所有不同的 URL。在 Flask 中，应用程序路由被写成称为*视图函数*的 Python 函数，这些函数被映射到一个或多个路由 URL。让我们在我们的 *app* 目录下创建 route 模块`routes.py`并创建一个*视图函数*。

这里，我们已经创建了一个*视图函数*。函数上方的`@app.route`被称为*装饰器*，它在作为参数给出的 URL 和函数之间创建一个关联。在这个例子中，*装饰器*与`/index` URL 相关联。这意味着当 web 浏览器请求这个 URL 时，Flask 将能够包含这个函数，并将它的返回值作为响应传递回浏览器。我们将在以后的实践中看到这一点。

为了完成应用程序，我们需要在定义 Flask 应用程序实例的目录的顶层有一个脚本。我将把它命名为*Spotify _ opinion _ analysis . py*，并包含下面一行导入应用程序实例的代码。

为了确保我们有正确的项目结构，这里是我们虚拟环境中的当前目录。

**运行烧瓶应用**

当运行应用程序时，需要通过设置`FLASK_APP`环境变量来告诉 Flask 如何导入它。然后我们可以使用`flask run`运行应用程序。

来自`flask run`的输出表明服务器运行在 IP 地址 127.0.0.1:5000 上，这总是您的计算机的本地地址，或者称为您的本地主机。在 web 浏览器中，导航到该 URL。您会注意到，当 URL 以`/index`结尾时，我们会看到在我们的*视图函数*中声明的简单消息。把网址改成别的，比如`/home`，你会发现这个网址没有找到，因为我们没有创建它。

**模板**

*模板*有助于将 web 应用程序的表示和设计与 Python 逻辑分开。在 Flask 中，*模板*被写在单独的文件中，通常是 HTML 文件，它们存储在应用程序包内的*模板*目录中。让我们创建*模板*目录，确保**不以大写字母“t”命名它，否则它将无法被识别。该目录现在应该看起来像下面的结构。**

在我们的 *templates* 目录中，我们可以创建 HTML 文件，这些文件不仅可以呈现我们漂亮的 web 界面，而且我们还可以将 Python 中的变量和结果解析到我们的前端。让我们创建一个名为*index.html*的 HTML 文件，并将其保存在我们的*模板*目录中。

如果你熟悉 HTML，你会发现第 4 行看起来有点奇怪！这里，我们实际上正在解析变量`user`，我们将用 Python 创建这个变量，并显示在前端。`{{ ... }}`本质上是 Python 变量的占位符。

如果我们跳回 *routes.py* ，我们需要声明变量`user`。然后我们使用 Flask 的`render_template()`函数将模板转换成一个完整的 HTML 页面。这个函数需要导入。它接受模板文件名和声明的 Python 变量，并返回相同的模板，但是其中的所有占位符都被这些变量替换了。

我们还可以在模板中呈现条件语句和 for 循环，但我不会在这里讨论这些。

假设我们已经设置了几个*视图功能*，我们希望能够从一个页面导航到另一个页面。轻松点。我们可以使用 HTML 的`href`标签导航并指向页面。但是，我们可以只使用我们在*装饰器*中声明的 URL，例如`/index`，而不是指向应用程序的整个 URL。

**造型**

在设置 Flask 应用程序的环境时，我想快速介绍的最后一件事是在哪里放置页面样式。我的意思是，让我们的应用程序看起来很棒的文件应该放在哪里？为了做到这一点，我们必须在我们的 *app* 目录中创建最后一个目录，名为 *static* 。在这个目录中，你可以找到你的应用程序需要的所有 CSS 和图像文件。要将样式或图像文件连接到 HTML，只需将样式表导航到`static/...`。

# SPOTIFY 情感分析烧瓶应用程序

如果你还和我在一起，太好了！

根据前面对如何设置和开始构建 Flask 应用程序的解释，我继续创建了两个*视图函数*，一个用于我的登录页面，另一个用于我的主页。登录页面是我希望用户看到我的应用程序的地方，当他们点击按钮时，他们将使用他们的凭据验证自己是 Spotify 用户，并访问他们自己的音乐。

![](img/76c325bf353facd20aeccb979dcb7915.png)

Spotify 情感分析登录页面

主页是显示情感分析结果的地方。现在，我厚颜无耻地来到 Spotify 的网站，在你登录后保存了他们主页的 HTML 样式。但我只想声明，他们的代码和设计的版权是他们自己的，这个项目的目的只是为了好玩。

您可能会注意到，图片并没有显示在 Spotify 个人资料图片通常显示的位置。这是因为该个人资料图片由 Spotify 存储，并在您登录后呈现在页面上。同样的方法也适用于这里——我们还没有提取任何数据，但一旦我们提取了数据，我们会将登录用户的个人资料图片放在那里，使其更加个性化。

![](img/bc4da0e7bc8fdebf539a7464146a93c0.png)

Spotify 情感分析主页

# SPOTIFY API 键

感谢 Spotify 的 API，我能够提取和探索我喜欢听的歌曲——那些让我点击喜欢按钮的歌曲。要使用 API 访问您的 Spotify 数据，您首先需要使用以下步骤进行初始设置:

使用您的 Spotify 凭据登录 [Spotify for Developers](https://developer.spotify.com/dashboard/) 网站。

您将看到您的仪表板，您可以'*创建一个新的应用程序*。

从应用仪表板页面，选择“*编辑设置*”。

为您的应用程序提供名称和描述。

然后，将重定向 URI 设置为 API
验证访问后您希望用户被定向到的位置。由于我使用的是 Flask，我将把它设置为我的
localhost:[http://127 . 0 . 0 . 1:5000/Spotify _ opinion _ analysis 上的主 HTML 页面。](http://127.0.0.1:5000/spotify_sentiment_analysis.)

点击保存，记下您的**客户端 ID** 和**客户端密码**密钥。下一步我们需要这些。

# 证明

现在我们已经有了 Flask 环境设置、设计的开始和 Spotify API 密钥，我们可以开始访问我们的音乐数据了。要让最终用户批准你的应用程序访问他们的 Spotify 数据和功能，或者让你的应用程序从 Spotify 获取数据，你需要授权你的应用程序。Spotify 的[授权指南](https://developer.spotify.com/documentation/general/guides/authorization-guide/)描述了如何通过两种方式获得授权:

**应用授权** : Spotify 授权你的应用访问 Spotify 平台(API、SDK 和 Widgets)。

**用户授权** : Spotify 以及用户授予你的应用程序访问和/或修改用户数据的权限。调用 Spotify Web API 需要您的用户授权。为了获得授权，您的应用程序生成一个对授权端点的调用，传递一个请求访问权限的作用域列表。

在这里，我们将让用户授权我们访问他们的音乐数据。我们希望它对我和其他想要使用它的人来说是个性化的，所以我们访问个人用户数据是有意义的。

提出授权请求涉及三方:Spotify 服务器、您的应用程序以及最终用户数据和控制:

![](img/e9c4a1165e1b68a51217f6837e319bfa.png)

Spotify API 认证

还记得你在 Spotify 仪表盘上记下的那些键吗？这里是你需要它们的地方。🔑

首先，让我们声明变量 *CLIENT_ID* 和 *CLIENT_SECRET* 作为我们的键。这些将是`string`型。然后，我们将设置一些必需的 Spotify URLs 和服务器端参数。特别注意*重定向 _URI* 。这是您在上一节设置键时声明的重定向 URI。请记住，这是您希望用户通过身份验证后被重定向到的 URL。最后，我们希望通过 Spotify 解析所有上述信息来检索数据。

我们需要设置另一个*视点*。这一次，*视点*不会返回模板。它将解析 API 信息，并将我们重定向到我们的*重定向 _URI* 。另外，注意我们需要从 Flask 库中导入*重定向*，以及从 *urllib.parse* 中导入 *urllib* 和 *quote* 。最后一件事——我们需要将登录 HTML 页面上的按钮连接到授权功能。转到那个文件，在你的`href`标签中包含`/spotify_authentication`来引用相应的*视点*。

总之，我们的`routes.py`现在应该看起来像这样:

现在身份验证已经设置好了，我们期望看到什么呢？嗯，如果你运行你的 Flask 应用，点击欢迎页面上的登录按钮，你应该会被重定向到 Spotify 的认证页面！🎉

身份验证页面应该如下所示。填写完 Spotify 详细信息后，您应该会被重定向到您的重定向 URI，并看到您的主页。

![](img/879de8eb22c446fec62e2119ecb8d8e4.png)

Spotify 认证页面

# SPOTIFY 数据

现在是有趣的部分。用户已经通过认证访问了他们的 Spotify 数据——但是我们如何检索它呢？

收到授权码后，您需要通过向 Spotify 帐户服务发出`POST`请求，用访问令牌交换授权码，这次是向其/API/令牌端点:POST https://accounts.spotify.com/api/token.发出请求

这个请求的主体需要包含一些参数，这些参数将作为 base64 编码包含在头中。在这种情况下，我们将从 Flask 的库中导入*请求*以及以下库: *base64，requests，*和 *json* 。

一旦您运行 Flask 应用程序并且认证令牌成功，来自 Spotify 帐户服务的响应具有状态代码 200 和以下 JSON 数据:

`{'country': 'GB', 'display_name': 'Lowri Williams', 'external_urls': {'spotify': 'https://open.spotify.com/user/1149952632'}, 'followers': {'href': None, 'total': 12}, 'href': 'https://api.spotify.com/v1/users/1149952632', 'id': '1149952632', 'images': [{'height': None, 'url': 'https://scontent.xx.fbcdn.net/v/t1.0-1/p320x320/37337856_10155307217510946_6222490498947350528_o.jpg?_nc_cat=102&_nc_sid=0c64ff&_nc_ohc=KD5MjymlBtcAX8vHlVP&_nc_ht=scontent.xx&_nc_tp=6&oh=eac7ae2f14c7f373371fbcdce8439241&oe=5E993E5B', 'width': None}], 'product': 'premium', 'type': 'user', 'uri': 'spotify:user:1149952632'}`

酷！我可以看到我的用户名、我有多少关注者、我的个人资料的 URL、我的个人资料图片以及我拥有的帐户类型。因为这是一个 JSON 对象，所以我可以将相关信息赋给变量。

还记得主页模板中个人资料图片的占位符吗？好了，我们可以解析 *profile_url* 变量，方法是将`{{ profile_url }}`作为主页 HTML 中个人资料图片元素的`href`，并呈现模板。我还可以显示播放列表中最近的 6 首歌曲。

![](img/4d79aeed86e17b58a8ddeebc3fc23a09.png)

将图像解析到前端

好了，现在来访问音乐数据。我们可以通过将我们的认证令牌指向用户简档端点来检索我们喜欢的歌曲。音乐数据包含各种信息。我们感兴趣的是何时将歌曲添加到播放列表中、歌曲名称、艺术家姓名、专辑封面、歌曲的 URL 以及曲目的 ID。

同样，由于这是一个 JSON 对象，我可以访问相关信息。由于我们要处理几首歌曲，我将创建一个数据帧来组织数据。

# 音乐比赛

一旦我们可以访问 Spotify 播放列表中的歌曲，我们就需要它们的歌词。Spotify 没有这个功能——这很遗憾。然而，我们可以使用其他一些资源来匹配歌词和歌曲。

[Musixmatch](https://www.musixmatch.com/) 是一个歌词平台，who 的社区由全球数百万音乐粉丝组成，建立了最佳的歌词知识，包括翻译的歌词。与其他歌词网站相比，Musixmatch 似乎在歌词的正确性和涵盖的歌曲数量方面取得了最好的结果。但是这个网站最好的一点是它有一个 API。

注册 API 密钥既快速又简单。去他们开发者的[页面](https://developer.musixmatch.com/)注册一个账户。他们的免费计划让你每天进行 2k 次 API 调用，只检索每首歌 30%的歌词。

要获得歌词，您首先需要使用以下步骤进行初始设置:

注册一个 Musixmatch 开发者账户并登录。

您将看到您的仪表板，您可以'*注册一个 API 密钥*。

为您的应用程序提供名称和描述。

点击保存，记下您的 API 密钥。

# 情感分析

已经开发了各种技术和方法来解决自动识别文本中表达的情感。在这篇文章中，我将使用 Python 情感分析库 VADER 来分类我的播放列表中的歌词是积极的、消极的还是中性的。

一种非常简单的情感分析方法是使用一个单词列表，这些单词已经根据它们的语义取向进行了标记。例如，我们可以假设单词“好”有一个正价，而单词“坏”有一个负价。VADER 使用这种技术，并提供了一个百分比分数，它代表了属于每个情感类别的歌词的比例。它还提供了一个复合得分，计算方法是将每个单词的效价得分相加，然后将得分归一化到-1(最大负值)和+1(最大正值)之间。

VADER 的好处在于我们不需要以任何方式对文本进行预处理！我们可以将歌词输入 VADER 的情感函数，并检索每首歌的复合得分。记住，如果你使用免费的 API，Musixmatch 只允许访问每首歌的前 30%的歌词。所以，当然，结果可能不像我们希望的那样准确。

首先，我们将从 musixmatch 的 Python 库中导入 Musixmatch，从 VADER 的 Python 库中导入`SentimentIntensityAnalyzer`函数。我将声明我的 Musixmatch API 键，初始化来自 VADER 的情感分析器，然后迭代来自数据帧的歌曲名称和艺术家，通过 Musixmatch 的歌词匹配器解析它们。然后，我将计算复合情绪得分是高于还是低于阈值，这样我们就可以给它们贴上积极、消极或中性的标签。

# 数据可视化

一旦我获得了播放列表中每首歌曲的复合分数，我就可以开始考虑如何可视化结果了。最近我最喜欢使用的图表之一是雷达图，或者网络图或蜘蛛图。对于那些不知道的人来说，雷达图是一种二维图表类型，旨在绘制多个变量的一个或多个系列的值。每个变量都有自己的轴，所有的轴都连接在图的中心。

假设我们想要绘制正面、负面和中性歌曲的月平均复合得分。我可以通过按*日期*列对我的数据帧进行分组，并对复合得分进行平均，来计算月平均情绪得分。然后我可以使用 ChartJS 生成下面的雷达图。

![](img/0c10f38cf1bacd61eafe2869353157ac.png)

雷达图

酷！在我的播放列表中的 320 首歌曲中，我们可以看到我听的是积极和消极的混合歌曲。有意思的是，2019 年 12 月，我喜欢上了更多积极向上的音乐。这也许可以用我一定听过的圣诞歌曲来解释。我似乎很少听可以归类为表达中性情绪的音乐。当我写这篇文章时(2020 年 4 月底)，我似乎一直在听更积极的音乐。

我们还能做什么？

我们可以提取总体得分最高的积极和消极的曲调，并把它们放在一个漂亮的记分卡上。歌曲的封面图像也可以从 Spotify 收集的数据中提取。

![](img/180e2de724b2e6373a0f7d79ad2dbb60.png)

热门音乐

我们还可以将情感分析结果与 Spotify 的音频效价分数进行对比。我们可以从我的播放列表中解析每个曲目的 id，并通过音频功能端点解析它们。如果我们将所有被分类为正面、负面或中性的歌曲的分数进行平均，我们可以使用一个简单的条形图来比较这两种方法。有希望的是，尽管我们对一首歌的 30%的歌词进行了情感分析，但结果似乎与 Spotify 的音频效价得分相对相似。

![](img/40b6a5cc483fa1318128cc4d523e6a37.png)

Spotify 音频价格与情感分析

# 结论

那么，我从这个分析中学到了什么？

深入了解我所听的音乐以及对歌词进行情感分析真的很有趣——我的音乐品味似乎比我想象的更积极！我可能会在未来的帖子中关注如何从歌词中提取关键词。这打开了其他自然语言处理项目的大门，在那里我可以研究使用机器学习来根据歌曲的内容对它们进行分类。

这个项目是我非常喜欢做的事情。因此，我进一步扩展了 Flask 应用程序，增加了一些其他功能。如果你想更多地了解你的歌曲的情感，去主办的[吧。](https://spotify-sentiment-analysis.herokuapp.com/)

如果你喜欢关注这篇文章，别忘了通过[给我买杯咖啡](https://ko-fi.com/lowri_williams)来分享或展示你的荣誉！☕