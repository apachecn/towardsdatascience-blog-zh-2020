# 5 个专业 Python Web 开发/端点技巧

> 原文：<https://towardsdatascience.com/5-pro-python-web-development-endpointing-tips-c9375cc95a21?source=collection_archive---------56----------------------->

## 用 Python 简化端点的 5 种简单方法！

![](img/3f054eec1a02c5461a4d5d4cd7496701.png)

# 介绍

> 我们都经历过…

您有一个准备好部署的模型，但是您正在努力让模型得到部署。这可能是一个会让你的模型停滞不前的结果，让它永远见不到天日。这是一个如此复杂和庞大的问题，以至于我所在的团队已经改变了模型，并且将我们的工作逆向工程到新的模型中，仅仅是为了避免一些部署错误。

让我们面对现实吧——数据科学家不是网络开发者。尽管我们中的一些人可能比大多数人更热衷于 Unix 命令行并了解更多的 web 协议，但当您第一次成为数据科学家时，您不太可能想到部署自己的端点。在很多方面，您的端点和您的模型一样重要！如果没有端点，我们日常使用的许多机器学习模型肯定不会正常工作，这令人震惊！

那么，当你把一个不是 web 开发人员或开发运营工程师的人和一个机器学习工程师混在一起时，你会得到什么呢？

> 一个数据科学家！

不幸的是，这绝对是经常被忽视的一小部分工作。开发运营本身就是一个完整的领域，真正精通它就像精通笔记本中的数据科学一样深入。幸运的是，今天我将回顾我认为所有数据科学家都会发现对部署和终结点有用的 5 个技巧，所以请合上笔记本，让我们进入部署阶段！

# 最快的开发服务器

在 Python 中，可能有一千种独特的方式来启动服务器。我个人和职业最喜欢的可能是 Gunicorn3。然而，虽然 Gunicorn 对于服务器来说是一个很好的部署解决方案，但是对于开发来说可能不是那么完美。Gunicorn 有很多我称之为“输出屏蔽”的东西，在这里，你不会在你自己的代码中得到错误，你会收到 Gunicorn 的输出，它可能是误导性的，甚至是不清晰的。如果是这样的话，对你的代码进行修正将会非常困难。幸运的是，除了使用 Gunicorn 来运行您的服务器，还有一些替代方法。

这个服务器有什么了不起的？这个服务器包含在 Python 的标准库中，可以通过一个 Bash 命令在任何 Unix(或 Python)终端上轻松运行。或者，您甚至可以使用 Python 来创建这样一个服务器，这是非常独特的，因为通常服务器只由 Bash 启动。包含此服务器的 Python 库是“http”库。从 http，我们可以导入服务器:

```
**def** run(server_class=HTTPServer, handler_class=BaseHTTPRequestHandler):
    server_address = ('', 8000)
    httpd = server_class(server_address, handler_class)
    httpd.serve_forever()
```

然后使用以下命令运行它:

```
run()
```

也可以使用带有端口参数的解释器的-m 开关直接调用 http.server。

```
python -m http.server 8000
```

这是并且将永远是启动开发服务器的最简单的方法。当我在我的电脑或同事之间共享文件时，我一直在使用它！只要确保你有 TCP 转发到你想要的端口，你就可以让全世界都看到你的主机！不幸的是，虽然这个服务器很容易使用，但我肯定不建议在这样的服务器上部署任何东西 ***官方*** 。但是，对于调试、文件共享或。PCK —用 HTML5 或者 WebAssembly 阅读，绝对完美！

# Crontab:自动化一切！

我以前确实提到过克朗塔布，这是有充分理由的。Crontab 是一个非常简单，但功能非常丰富的工具，通常被开发-运营工程师用来根据 Unix 系统上的特定时间戳在后台自动执行脚本任务。这些时间戳存储在 CRON time 中，您需要习惯读取这些时间戳。

不管它的整体不可接近性如何，我认为 Crontab 是一个你生活中不可或缺的工具。这是一种快速有效的方法，可以非常容易地实现任何事情的自动化。我一直用它来进行大型 API 提取和后端端点更新。我还使用 Crontab 制作了自我训练模型，这些模型用脚本序列化，然后读入端点。与自动化后端部署的其他方法相比，Crontab 无疑因其易用性和可靠性而独占鳌头。如果您想了解我如何使用 Crontab、NGINX、Julia 和 Julia 在不到一个小时的时间内部署了一个自我训练模型，我写了一整篇关于如何做的文章，您可以在这里查看！：

[](https://medium.com/chifi-media/build-a-beautiful-model-that-trains-itself-the-easy-way-a0d31b611cee) [## 建立一个自我训练的美丽模型！(简单的方法)

### 结合开发运营和数据科学的元素，在 Ubuntu 上部署可扩展的自我训练模型。

medium.com](https://medium.com/chifi-media/build-a-beautiful-model-that-trains-itself-the-easy-way-a0d31b611cee) 

# 监督者

Supervisor 或 supervisord 是另一个在开发-运营领域非常受人尊敬和广泛使用的工具。Supervisor 允许 Unix 系统以任何用户的身份执行 Bash 命令，而无需真实用户在场。换句话说，你可以在终端中创建一个你自己的人工版本来“监督”你不想自己管理的应用程序。

Supervisor 是一个特别有用的工具，用于部署您仍然希望监控但不希望有一个无头单元一直运行的服务器。使用 supervisor，您可以通过允许服务器以不同的权限同时处理一系列应用程序来轻松扩展服务器的覆盖范围。所以公认 Supervisor 是一个很棒的工具，但是怎么用呢？

与大多数 Unix 应用程序一样，尤其是那些用于服务器的应用程序，supervisor 可以通过存储在/etc/conf.d 中的配置文件轻松配置。当然，首先您需要实际安装 Supervisor:

```
# (Ubuntu)
sudo apt-get install supervisor
```

接下来，您可以使用您选择的文本编辑器编辑 supervisor 配置。我个人喜欢用 GNU Nano。

```
[program:app]
directory=/var/
command=gunicorn3 -workers=3 flask_app:app
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
stderr_logfile=/var/log/appname/lognameerr.log
stdout_logfile=/var/log/appname/lognamestdout.log
```

上面我们看到了一个相当基本的管理员配置文件。这个配置的目录部分将决定我们需要在哪个目录中运行我们的命令。接下来，该命令是 Bash 命令，通常用于运行脚本或启动服务器，在本例中是美妙的 Gunicorn3。接下来，我们有 autostart 和 autorestart，它们都是布尔值，将决定每当装入管理程序服务时是否启动管理程序。当 supervisor 实例启动、重新加载或服务器因任何原因重新启动时，将加载 supervisor 服务。接下来，stopasgroup 和 killasgroup 将确定每当重新加载该服务时，该配置文件中的其他应用程序配置是否也会被终止。最后，但同样重要的是，我们能够为输入和输出添加日志文件，这对调试很有用。

Supervisor 是每个数据科学家都应该熟悉的行业标准工具。它不仅对于部署端点几乎是必不可少的，而且当以 Unix 方式完成时，它还可以作为许多事情的基础。这是一个高度通用的工具，我真的发现拥有有用的知识。如果你想看用 NGINX 和 Supervisor 部署 Flask 应用程序的完整教程，幸运的是我正好有这篇文章:

[](/deploying-flask-with-gunicorn-3-9eaacd0f6eea) [## 用 Gunicorn 3 展开烧瓶

### 应用程序部署通常会带来意想不到的后果和错误。部署可以是制定或…

towardsdatascience.com](/deploying-flask-with-gunicorn-3-9eaacd0f6eea) 

# 使用正确的工具

如果你听过这句话

> "使用适合这项工作的工具。"

这个概念直接适用于使用不同的 Python Web 框架。例如，像 Django 这样的框架打包了像 0auth authentication 这样的预制工具和大量其他工具。如果是端点控制，那么创建一个完整的 Django 应用程序，而不是从 Flask 创建，是没有意义的。如果你想了解更多关于 web 框架和它们的设计目的，我写了一篇文章，包含了 5 个我最喜欢的 web 框架，有低级的也有高级的。

[](/5-smooth-python-web-frameworks-for-the-modern-developer-47db692dfd52) [## 面向现代开发人员的 5 个平滑 Python Web 框架

### 5 个更棒的 Python Web 框架供你欣赏！

towardsdatascience.com](/5-smooth-python-web-frameworks-for-the-modern-developer-47db692dfd52) 

每当您创建一个端点时，仔细考虑速度和体积是非常重要的。有许多 web 框架都有几十种不同的特性，在创建端点或全栈应用程序时，需要考虑的东西多得惊人。您肯定不希望使用 Django 这样的东西作为简单的端点。虽然 Flask 当然可以用于全栈开发，但是有很多更好的选择。

# 成为一个万事通

仅仅因为您的工作主要涉及部署返回 JSON 数据的简单端点，并不意味着学习如何使用 Python 进行身份验证和 fullstack 对您没有好处。你可能会遇到成百上千的问题，所有的问题都有成百上千个完全不同的解决方案。在某些方面，虽然您可能想避免“将胡萝卜放在不同的篮子里”，但您肯定不想避免使用部署技能。

如果您知道如何简单地在 Heroku 或类似的服务上部署模型，为什么不自己尝试在 Unix 服务器上部署呢？这些不同的技能肯定会让你在就业和个人发展方面受益。所有的数据科学家都应该了解终端，即使你不能用 NGINX 和 Supervisor 部署自己的端点，只要熟悉 Bash，你仍然可以成为一名更好的程序员。

# 结论

使用 Python 的一个好处是你可以有很多选择来解决一个特定的问题。拥有几个 web 框架当然是有益的，并且可以使您的部署和开发工作容易得多。学习如何使用诸如 Crontab 之类的东西，以及诸如 Tornado 和 Pyramid 之类的不同网络框架，肯定会对您的数据科学职业生涯带来难以置信的好处。