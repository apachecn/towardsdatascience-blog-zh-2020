# 从头开始创建一个不和谐机器人并连接到 MongoDB

> 原文：<https://towardsdatascience.com/creating-a-discord-bot-from-scratch-and-connecting-to-mongodb-828ad1c7c22e?source=collection_archive---------3----------------------->

## 使用 python 为您的 discord 服务器创建一个功能记分员 bot，并将数据存储在 MongoDB 数据库中。

Discord 是一个对开发者非常友好的消息平台。discord 开发者的一个主要出路是生产 discord 机器人，这些机器人可以执行无限多的任务，如发送消息、播放音乐，甚至允许在聊天服务器上玩小游戏。在本教程中，我们将使用 Python 创建一个 discord bot，它将跟踪用户发送的某些消息，并使用 MongoDB 添加一个评分系统。

![](img/6cb0f3514d54d1d35a7413e3da123638.png)

[来源](https://www.google.com/imgres?imgurl=https%3A%2F%2Fdiscordapp.com%2Fassets%2Ff7a4131e47f50b48b3f85f73c47ff1dc.png&imgrefurl=https%3A%2F%2Fdiscordapp.com%2F&tbnid=llbk160_bIKyPM&vet=12ahUKEwi8hOLUvP3oAhVIGt8KHY7ZCrwQMygAegUIARCYAg..i&docid=tL3jcu20AJy75M&w=1200&h=630&q=discord&ved=2ahUKEwi8hOLUvP3oAhVIGt8KHY7ZCrwQMygAegUIARCYAg)

首先，在终端中安装 discord.py、dnspython 和 pymongo 模块。Dnspython 和 pymongo 将用于我们的 MongoDB 连接。

接下来，导入您刚刚安装的所有模块。

在这之后，我们必须在 discord web 应用程序上激活我们的机器人。首先，请前往:

[](https://discordapp.com/) [## 不和-与朋友和社区聊天的新方式

### 不和谐是通过语音、视频和文本进行交流的最简单的方式，无论你是学校俱乐部的一员，还是晚间……

discordapp.com](https://discordapp.com/) 

然后点击开发者门户。

![](img/7fad2a7364767533878f4c4012a39ab0.png)

点击开发者门户后，点击右上角的蓝色按钮“新应用”。一旦你为你的机器人输入了一个名字，你应该会看到这样一个屏幕:

![](img/8d60db363d8c8f5c724c7182d9c47367.png)

一般信息屏幕

接下来，点击屏幕右侧显示“Bot”的标签。您应该会看到这样的屏幕:

![](img/37580fd349d83831a15f07d23bfca2c2.png)

添加 bot 屏幕

当你到达这个屏幕后，点击右边的蓝色按钮“添加机器人”。您应该会看到这样的屏幕:

![](img/caba21598b4c173c304dd5462aaf1745.png)

机器人信息屏幕

在这里，您将看到您的机器人的所有信息，包括允许您访问机器人的令牌。请确保这个令牌是安全的，因为它是决定谁可以访问 bot 并更改其功能的唯一因素。接下来，我们必须将机器人添加到服务器。在本教程中，有一个为测试而创建的单独的服务器。要将 bot 添加到服务器中，请点击屏幕左侧的“OAuth2”选项卡。该工具为您的 bot 创建一个访问 URL，然后连接到 Discord“oauth 2 API”。您应该会看到这样的屏幕:

![](img/6c10ad3edfbf0c64244803d38735ff33.png)

OAuth2 屏幕

一旦你到达这个屏幕，选择写着“机器人”的盒子。单击该框后，屏幕上会显示可选的权限。对于这个机器人，您可以选择标有“管理员”的框，以允许出于测试目的的所有权限。但是，在创建要添加到公共服务器的 bot 时，您可能不想添加所有权限。

![](img/3fe387814cd24cf0e448fedc96950bf4.png)

范围类型和权限

一旦选择了所有选项，就会自动生成一个 URL。将该 URL 复制到剪贴板并粘贴到浏览器中。一旦你被发送到那个 URL，选择你想要添加机器人的服务器。恭喜你，你已经正式将你的第一个机器人添加到你的服务器上了！

![](img/fc489575386ee6b3d0858f40ae1ac634.png)

成功屏幕

现在我们已经将机器人添加到我们的服务器中，我们可以开始编程了！我们必须首先创建一个与机器人的连接。这就是令牌的用途。

在这个代码片段中，我将我的机器人的令牌保存在一个单独的文本文件中，然后将该值存储在变量“token”中。在这之后，我创建了一个客户端，它是你的机器人与 Discord 及其 API 之间的连接。在代码片段中，您可以看到客户端实现了它的“on_ready()”函数。一旦机器人准备好进一步的动作，就调用这个函数。深入研究 on_ready()函数，关键字“async”表示该函数是异步的，并且与正在运行的任何其他函数一起发生。一旦机器人实现了更多的功能，这就更有意义了。最后，我们使用保存在变量中的令牌运行客户端。如果您运行这个代码片段，您应该在屏幕上看到您的 bot 输出的名称，后面跟着剩余的 print 语句。

接下来，我们必须对机器人进行编程，以读取用户消息，并确定是否有一个关键字将被它的调平系统选中。对于这个机器人，我将使用“不和谐”、“python”、“代码”和“乐高”这些词。这些关键字不区分大小写。

这里，我们为我们的客户机创建了另一个事件，它实现了函数“on_message()”。这个函数只是在用户向通道发送消息时运行。它应该打印关于发送的消息的基本信息，比如它的通道、作者、作者的名字以及消息是什么。一旦 bot 检查到诸如“python”之类的关键字，它将向通道发送它被接受的消息。下面是发送和接收消息的完整代码片段:

既然我们已经有了发送和接收消息的基本功能，现在是时候在我们的 MongoDB 数据库中记录用户级别了！我们将简单地通过计算用户说一个关键词的次数来计算用户级别。

首先，我们必须在[mongodb.com](http://mongodb.com)创建一个 MongoDB 帐户，以便创建一个集群，也就是一组数据库。创建帐户后，屏幕会提示您:

![](img/dd56baa3a8544181bdfe20d237577585.png)

集群创建

在创建数据库时，MongoDB 将您的集群存储在它的一个物理数据库中，因此您必须选择您的地区和提供商。选择离您最近的地区，以确保最快的反馈时间。如果愿意，您也可以更改集群的名称。创建集群后(需要 1-3 分钟)，您将看到以下屏幕:

![](img/d895542fdeebb7b8f02d2dc287d334b0.png)

集群屏幕

我们现在必须连接到我们的集群。为此，请点击“连接”按钮。这将通过以下屏幕提示您:

![](img/c7629acd57e336db18004abc6ac7c2c7.png)

连接到群集

只需点击绿色按钮，上面写着“添加您当前的 IP 地址”。在那里，创建一个用户来链接到集群。请确保记住您的用户凭据，因为它将用于后续步骤。一旦你完成了，继续你的连接方式。这是将出现的屏幕:

![](img/61f636236214cfa020533898a7219e8c.png)

连接方法

在本教程中，我们将使用 MongoDB Compass，它是 MongoDB 的 GUI，允许轻松访问集群，是对数据进行分析的好方法。如果您没有 MongoDB Compass，请按照它提供的说明下载该程序。一旦您下载了 MongoDB Compass，您将会看到这样一个屏幕:

![](img/435ef741a544782a0c2fa52f296595ca.png)

MongoDB 指南针连接屏幕

回到 MongoDB online，您会看到这样一个屏幕:

![](img/654c8f9c7a0011e3ab906818d8676f15.png)

MongoDB 集群连接

您得到的 URL 是您将复制并粘贴到 MongoDB Compass 门户中的内容。在网址中，你会看到它的一部分有“<password>”。您将用您的群集用户帐户的密码替换它。一旦你把这个链接粘贴到你的 MongoDB Compass 门户，你就会看到你的集群！</password>

![](img/e8a6d0593f4742debd0679307e8c6c05.png)

完整集群

现在，让我们回到 MongoDB 的 web 门户，探索我们的集群。请点击“收藏”按钮。集合是群集中可以存储数据的子组。它将询问您是否希望加载样本数据集。让我们加载它来了解集群的结构。加载可能需要几秒钟。

![](img/9b4015ac183b149e2a817f2c6dbe21b2.png)

加载的样本数据集

我们接下来要做的是创建一个数据库来存储我们的用户数据。点击显示“+创建数据库”的按钮。您可以随意命名数据库。MongoDB 中的数据存储在一个层次结构中。它的结构是集群>数据库>集合。一旦我们创建了一个数据库，我们还需要创建一个将存储在数据库中的集合。

![](img/90b3aa32f09abe221934b4ab5ca51757.png)

空用户数据数据库

我们现在有一个空的数据库等待填充我们的用户数据！

为了检索和上传数据到我们的数据库，MongoDB API 创建了许多函数，我们不会完全涵盖所有使用的函数。如果您想进一步探索，这里是 MongoDB 文档:

 [## PyMongo 3.10.1 文档— PyMongo 3.10.1 文档

### 如果您对 PyMongo 有困难或有疑问，最好的地方是 MongoDB 用户组。一旦你得到…

pymongo.readthedocs.io](https://pymongo.readthedocs.io/en/stable/) 

首先，让我们从停止的地方开始。我们将在现有的不和谐机器人代码中添加内容。

这些是我们运行代码所需的导入。我们接下来要做的是在代码中连接到我们的集群，然后导航到我们存储数据(用户数据)的位置。

首先，我们必须连接到我们的集群。在代码中显示“CONNECTION_URL”的地方，用您用来连接 MongoDB Compass 的 URL 替换它，并用引号将它括起来。该链接在本教程中没有显示，因为它包含一个安全漏洞。之后，我们必须连接到我们的数据库，然后连接到我们的集合。我们现在在我们需要在的位置！

我们接下来要做的是为放入数据库的每个条目选择属性。每个条目将被视为一个独特的用户，其中应包括用户名，他们的分数，和他们的 ID。MongoDB 数据库中的每个条目都与一个惟一的 ID 相关联。您可以让它自动生成，也可以自己决定。出于我们的目的，最好是让条目 ID 与用户 ID 不一致。

在这个代码片段中，我们创建了一个名为“post”的变量，它包含了条目的属性。然后，我们将这些属性插入到“UserData”集合中。一旦我们运行程序并在我们的 Discord 服务器中键入“python ”,我们将看到我们的数据存储在数据库中。

![](img/ec87834b1a7d5f1ef5a2893ec5b5a7cd.png)

存储的用户数据

将向我们的数据库发送数据的代码添加到我们的机器人正在搜索的所有其他关键字中。现在，代码将如下所示:

然而，我们的计划有一个小问题。一旦我们键入另一个关键字，数据库就不能再次输入同一个用户。我们可以用一些简单的条件语句来解决这个问题。

在这里，我们创建了一个对数据库的查询，主要是询问是否有任何条目的预先存在的 ID 与当前输入的 ID 相同。如果当前输入的 ID 不同，那么新用户将登录到数据库中。接下来，如果用户已经存在于数据库中，我们必须修改它将会发生什么。

在这个代码片段中，如果用户已经在数据库中注册，我们基本上是在更新一个预先存在的条目。我们首先找到带有。find()方法，然后我们遍历用户并捕获其“score”属性。然后我们给这个值加 1。最后，我们使用。update_one()函数专门更新“score”属性。把这个函数添加到所有关键词之后，你就有了一个完整的链接到 MongoDB 的 Discord bot！以下是完整的代码:

信息和图像来源:

[](https://www.google.com/imgres?imgurl=https%3A%2F%2Fdiscordapp.com%2Fassets%2Ff7a4131e47f50b48b3f85f73c47ff1dc.png&imgrefurl=https%3A%2F%2Fdiscordapp.com%2F&tbnid=llbk160_bIKyPM&vet=12ahUKEwi7xrC5pPvoAhVDCN8KHWGZBtQQMygBegUIARCbAg..i&docid=tL3jcu20AJy75M&w=1200&h=630&q=discord&ved=2ahUKEwi7xrC5pPvoAhVDCN8KHWGZBtQQMygBegUIARCbAg) [## https://discordapp . com/assets/f7a 4131 e 47 f 50 b 48 B3 f 85 f 73 c 47 ff 1 DC . png 的 Google 图片结果

### 编辑描述

www.google.com](https://www.google.com/imgres?imgurl=https%3A%2F%2Fdiscordapp.com%2Fassets%2Ff7a4131e47f50b48b3f85f73c47ff1dc.png&imgrefurl=https%3A%2F%2Fdiscordapp.com%2F&tbnid=llbk160_bIKyPM&vet=12ahUKEwi7xrC5pPvoAhVDCN8KHWGZBtQQMygBegUIARCbAg..i&docid=tL3jcu20AJy75M&w=1200&h=630&q=discord&ved=2ahUKEwi7xrC5pPvoAhVDCN8KHWGZBtQQMygBegUIARCbAg) [](https://realpython.com/how-to-make-a-discord-bot-python/) [## 如何用 Python 制作一个不和谐机器人——真正的 Python

### 在这个循序渐进的教程中，您将学习如何用 Python 制作一个 Discord bot，并与几个 API 进行交互。你会…

realpython.com](https://realpython.com/how-to-make-a-discord-bot-python/) 

[pymongo.readthedocs.io](https://pymongo.readthedocs.io/en/stable/)