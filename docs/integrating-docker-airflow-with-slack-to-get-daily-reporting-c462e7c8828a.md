# 为每日报告整合气流和松弛度

> 原文：<https://towardsdatascience.com/integrating-docker-airflow-with-slack-to-get-daily-reporting-c462e7c8828a?source=collection_archive---------14----------------------->

## 使用 Airflow + Docker 向 Slack 发布天气预报的分步指南

![](img/205f0df376141a587535bd8ac0feb5e0.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由 [Austin Distel](https://unsplash.com/@austindistel?utm_source=medium&utm_medium=referral) 拍摄的照片

**技术栈:** Python 3.7，Airflow (1.10.10)，Docker

**GitHub 链接:**所有的代码都可以在[这里](https://github.com/happilyeverafter95/slack-airflow)找到。

# 气流+松弛

Slack 是一款越来越受欢迎的工作场所聊天应用。Apache Airflow 是一个用于编排工作流的开源平台。使用气流的最大优势之一是其**挂钩**和**操作器**的多功能性。钩子是外部平台、数据库的接口，也是操作符的基本构件。

[松紧网钩操作器](https://airflow.readthedocs.io/en/stable/_modules/airflow/contrib/operators/slack_webhook_operator.html)可用于整合气流和松紧。该操作符通常用于报告和警报目的，在满足某些触发条件时将传入消息调度到空闲通道。

我将向您展示如何利用这些工具在您的空闲工作空间中执行一些非常简单的报告:向频道发送每日天气预报。

这些基础可以扩展，以创建更复杂的气流+松弛集成。**我们开始吧！**

如果您有兴趣了解更多关于数据工程基础的知识，这里有一门课程可以帮助您入门。

[](https://click.linksynergy.com/link?id=J2RDo*Rlzkk&offerid=759505.18321546102&type=2&murl=https%3A%2F%2Fwww.coursera.org%2Fspecializations%2Fdata-engineering-foundations) [## 数据工程基础

### 为数据工程职业打下基础。开发 Python、SQL 和关系型数据库的实践经验…

click.linksynergy.com](https://click.linksynergy.com/link?id=J2RDo*Rlzkk&offerid=759505.18321546102&type=2&murl=https%3A%2F%2Fwww.coursera.org%2Fspecializations%2Fdata-engineering-foundations) 

# 设置宽松的工作空间

**注意:如果你已经熟悉在 Slack 上设置应用程序和 Slack webhook，请跳到**[**“air flow+Docker”**](https://medium.com/@mandygu/integrating-docker-airflow-with-slack-to-get-daily-reporting-c462e7c8828a#ca7e)

工作区是一个共享的渠道中心，队友和协作者可以在这里一起交流。我创建了一个名为**天气爱好者的工作空间。**

![](img/44fdcf81037324d3c68a163775512952.png)

在我们的工作区，我们需要:

*   接受这些信息的渠道
*   webhook url

让气流发布到一个名为#每日天气信息的公共频道。如果消息内容敏感，请考虑将其更改为私人频道。

![](img/e79cfe13ef408c342035716e6b953b36.png)

接下来，我们想为工作区创建一个 Airflow 应用程序。前往 https://api.slack.com/apps[的](https://api.slack.com/apps)点击`Create New App`

![](img/5a2937f752a2f2fd2a77ead9d707b012.png)

这将引导您进入一个可以设置应用程序名称的模式。Airflow 会以您选择的名称发布消息。为了简单起见，我将我的应用程序命名为`airflow`。

退出模式后会出现一个页面，你可以在其中添加“传入网页挂钩”作为应用程序功能。

![](img/24a8a46492b4e73d897ef353928c6b4f.png)

确保传入的网络钩子打开**。**

![](img/680502b0792fc91fe46f225004ddbe0b.png)

滚动到页面底部，点击“添加新的 Webhook 到工作区”。

![](img/68f197bdd98252c41b26531343f7fb0c.png)

这将生成一个 WebHook URL，可用于对 Airflow 进行身份验证。

WebHook URL 还允许您以编程方式向 Slack 发送消息。这里有一个非常简单的 POST 请求，您可以在终端中尝试。别忘了用你的网址替换我的。

```
curl -X POST -H 'Content-type: application/json' --data '{"text":"Hi, this is an automated message!"}' https://hooks.slack.com/services/XXXX
```

请检查您的频道以查看自动消息。

![](img/48000114299fba6b312015da62aa27a6.png)

如果你有兴趣学习更多关于在软件工程环境中使用 API 和 Python 的知识，这是一个非常适合初学者的 Coursera 专业。

[](https://click.linksynergy.com/fs-bin/click?id=J2RDo*Rlzkk&offerid=759505.31&type=3&subid=0) [## 面向所有人的 Python

### 由密歇根大学提供。这种专业化建立在 Python 面向所有人课程的成功基础上，并且…

click.linksynergy.com](https://click.linksynergy.com/fs-bin/click?id=J2RDo*Rlzkk&offerid=759505.31&type=3&subid=0) 

# 气流+ Docker

我将向您展示如何使用 Docker 设置气流，以适当地容器化您的应用程序。我使用了 [puckel/docker-airflow](https://github.com/puckel/docker-airflow) 的部分设置。

Airflow 附带了许多设置复杂的配置。使用 Docker 可以更容易地获得可重现的结果。

**Docker 是什么？** Docker 是一种独立于您的本地设置打包单个应用程序的方法。每个应用程序都在自己的 Docker 容器中。这里有一些关于 Docker 的有用资源，包括我写的一个关于 Docker 命令的资源。

[](https://docker-curriculum.com/) [## 面向初学者的 Docker 教程

### 学习使用 Docker 轻松构建和部署您的分布式应用程序到云中，Docker 由…

docker-curriculum.com](https://docker-curriculum.com/) [](/the-1-2-3s-of-docker-ea123d7c5f91) [## 码头工人的 1–2–3

### 我(几乎)每天使用的 6 个 docker 命令。

towardsdatascience.com](/the-1-2-3s-of-docker-ea123d7c5f91) 

对于带有 AWS 服务的更高级 Docker 应用程序:

[](https://click.linksynergy.com/link?id=J2RDo*Rlzkk&offerid=759505.16005422530&type=2&murl=https%3A%2F%2Fwww.coursera.org%2Flearn%2Fcontainerized-apps-on-aws) [## 在 AWS 上构建容器化应用程序

### 由亚马逊网络服务提供。本课程向您介绍容器技术，以及如何将它们用于…

click.linksynergy.com](https://click.linksynergy.com/link?id=J2RDo*Rlzkk&offerid=759505.16005422530&type=2&murl=https%3A%2F%2Fwww.coursera.org%2Flearn%2Fcontainerized-apps-on-aws) 

## 气流

整个 Airflow 平台可以分为四个部分:调度器、执行器、元数据数据库和 web 服务器。

*   调度程序决定运行哪些作业以及在什么时间/以什么顺序运行
*   执行者执行每个作业的指令
*   数据库存储气流状态(这项工作是成功还是失败？跑了多长时间？)
*   网络服务器是用户界面，使其更容易与气流接口；网络服务器是一个隐蔽的烧瓶应用程序

![](img/0a9ed2cfc38093e63143442aeb19f024.png)

这是 web 服务器的样子(摘自 Apache Airflow 的文档)

## 有向无环图

Dag 是气流中一个非常重要的概念。每个 DAG 都是相似任务的集合，这些任务以反映其依赖性和关系的方式进行组织。这些图不能有有向循环，换句话说，不能有相互依赖的作业。

Dag 是在 Python 脚本中定义的，它们帮助调度程序确定要运行哪些作业。在所有上游作业成功完成之前，下游作业无法运行。

![](img/b215ca6984a0860b8aba82604085a796.png)

箭头代表依赖关系；run_after_loop 仅在 runme_0、runme_1、runme_2 成功完成时运行

# 设置气流

为您的 Airflow 服务器创建存储库。我会给我的取名`slack-airflow`。我的存储库又一次被托管在[这里](https://github.com/happilyeverafter95/slack-airflow)。这些是目录中的组件:

*   requirements.txt
*   Dockerfile 文件
*   用于管理配置的气流子目录
*   docker-compose.yml
*   启动气流的外壳脚本
*   一个 DAG 文件(我们将在后面得到更多)

**requirements.txt**

这是为了安装所需的气流库(以及任何其他所需的库)。

```
apache-airflow[crypto,celery,postgres,jdbc,ssh,statsd,slack]==1.10.10
```

**air flow/config/air flow . CFG**

气流配置文件通常作为气流安装的一部分下载(使用 Docker 的额外好处是:您不需要完成安装过程)。默认配置本身很好，但是可以针对您的特定用例调整设置。

下面是一个综合列表，说明每个字段对应的内容:[https://air flow . Apache . org/docs/stable/configuration s-ref . html](https://airflow.apache.org/docs/stable/configurations-ref.html)

这是气流目录中唯一需要的文件。

**Dockerfile**

这包含了你的 Docker 镜像的说明。我们为运行`pip install`指定了一些环境变量、更多的依赖项和指令，并用我们的`entrypoint.sh` shell 脚本定义了图像入口点。最后一行还启动 web 服务器。

我还使用 Dockerfile 将秘密存储到 Slack 和 Open Weather API。理想情况下，秘密应该存储在它们自己的环境文件中，并在构建时放入 Docker 容器中。环境文件应该添加到`.gitignore`中，这样它就不会出现在代码库中。

冒着使这个设置过于复杂的风险，我们将把秘密留在 over 文件中。

请将你的秘密填入这两行。在共享您的代码时请记住，这些是敏感的凭证！`weather_api_key`用于获取每日天气预报——下一节将介绍如何获取这个令牌。现在，你可以空着它。

```
ENV weather_api_key=
ENV slack_webhook_url=
```

**docker-compose.yml**

docker-compose 是一种处理 docker 设置的有组织的方式。如果您正在处理多个相互依赖的容器，这将特别有帮助。

第一个服务`postgres`创建负责存储气流状态的 Postgres 数据库。凭证在 docker 文件中设置，可用于连接到本地网络上的数据库。

这是完整的数据库 URL。凭证组件分散在 Dockerfile 文件和启动脚本中。您可以使用此 URL 从本地网络连接并查询气流数据库。

```
postgresql+psycopg2://airflow:airflow@postgres:5432/airflow
```

要了解关于如何连接到 DBAPI 的更多信息，请查看我关于 Postgres DBs 的另一篇文章。

[](/becoming-the-full-stack-data-scientist-part-1-e0d933280b) [## 成为全栈数据科学家:设置并连接到 Postgres 数据库

### 全栈数据科学家是所有数据角色梦寐以求的海报儿童雇员。这位顶级数据科学家是…

towardsdatascience.com](/becoming-the-full-stack-data-scientist-part-1-e0d933280b) 

对于那些想要更详细地探索 Pythonic 与数据库的联系的人来说，这里有一个有用的 Coursera 课程:

[](https://click.linksynergy.com/link?id=J2RDo*Rlzkk&offerid=759505.1560524593&type=2&murl=https%3A%2F%2Fwww.coursera.org%2Flearn%2Fpython-databases) [## 通过 Python 使用数据库

### 由密歇根大学提供。本课程将向学生介绍结构化查询语言的基础…

click.linksynergy.com](https://click.linksynergy.com/link?id=J2RDo*Rlzkk&offerid=759505.1560524593&type=2&murl=https%3A%2F%2Fwww.coursera.org%2Flearn%2Fpython-databases) 

第二部分定义了 web 服务器，它将被托管在本地网络的 8080 端口上。

# 开放天气 API

![](img/aa4a8df1b8ab6a21f794018c7ad19af9.png)

照片由 [Gavin Allanwood](https://unsplash.com/@gavla?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

我们可以利用[开放天气 API](https://openweathermap.org/api) 获取每日天气预报。创建一个帐户并为您的帐户生成一个 API 令牌。

回到 token 文件，用您的令牌设置这个环境变量:

```
ENV weather_api_key=
```

# 天气日报

这是我的天气 DAG 的[链接。我把它放在一个叫做`dags`的文件夹里。](https://github.com/happilyeverafter95/slack-airflow/blob/master/dags/weather_dag.py)

## **步骤 1:** 加载依赖项

## **步骤 2:** 指定默认参数

我将自己添加为这条 DAG 的所有者。这是每个 DAG 的必需参数。如果`depends_on_past`设置为真，则后续任务将不会运行，除非之前的运行成功。从过去挑一个`start_date`。我选择了昨天的日期。`retries`设置为 0 意味着气流不会尝试重新运行失败的任务。

## **步骤 3:** 获取每日预测的简单类

我们向 Open Weather 发送 GET 请求，以获取多伦多的天气详情。有效负载被解析，描述字段用于描述预测。

API 键是从 docker 文件中实例化的环境变量中获取的。

## **步骤 4:** DAG 定义

我们在 DAG 中使用`SlackWebhookOperator`。您可以随意命名`http_conn_id`，但是**需要在 Airflow 服务器上设置相同的连接(这将在“在 Airflow 上设置您的 Slack 连接”一节中介绍)。**从环境变量中获取 webhook 令牌。

除了预定间隔和`catchup=False`(这防止气流运行回填)之外，这里还引用了默认参数。

`schedule_interval`是一个 cron 语法，它决定了运行 DAG 的节奏。参数对应于(按顺序):分钟、小时、日、月和星期几。

我通常用这个网站来破译 Cron 语法:[https://crontab.guru/](https://crontab.guru/)

# 启动 Docker 容器

在根目录下运行这两个命令。

这将构建图像并将其标记为`airflow`。重要的是不要改变标记名，因为它在启动脚本中被引用。

```
docker build . -t airflow
```

这将根据 docker-compose 中的指令启动相关的 Docker 容器。

```
docker-compose -f docker-compose.yml up -d
```

第一次运行这些步骤需要几分钟时间。完成后，web 服务器将暴露于您的本地 8080 端口。

您可以通过本地网络`localhost:8080`访问它。这是我的样子。

![](img/7b10a073107c2d48365359aa69fc7a9e.png)

# **在气流上设置松弛连接**

我们差不多完成了。

我们需要做的最后一件事是在 Airflow 中设置`slack_connection`(这个名称需要与 DAG 文件中指定的`http_conn_id`相匹配)。

## 步骤 1:进入管理>连接

转到`localhost:8080`访问网络服务器并点击管理>连接。

![](img/e03a81c7152d69fb8aa8219a050be580.png)

## 步骤 2:创建新连接

点击`Create`并相应地填写字段。对于松弛连接，您只需要`Conn id`和`Host`

*   conn _ id = slack _ 连接
*   host =您的 webhook URL

![](img/8ced24e4b3d81077848428ec10853c3f.png)

# 测试 DAG

如果您不想等待预定的时间间隔来观察结果，可通过点击`Trigger DAG`按钮手动触发 DAG 运行。

![](img/d03880ecc07bdbf377752544e292811e.png)

任务成功运行后，此消息将出现在“时差”中。今天的天气预报是*晴，*听起来差不多是☀️

![](img/b99b725af8cf4ba8a0f02fe8f3e4361e.png)

厉害！向天气网络说再见，向程序化预报问好😃

要获得每天的天气预报，让气流服务器运行。

我希望这篇文章对你有所帮助。对于额外的气流资源，查看官方文件，这是一个非常全面的指南。

[](https://airflow.readthedocs.io/) [## Apache 气流文档-气流文档

### Airflow 是一个以编程方式创作、调度和监控工作流的平台。使用 Airflow 将工作流程创作为…

airflow.readthedocs.io](https://airflow.readthedocs.io/) 

# 感谢您的阅读！

请通过 Medium 关注我的最新消息。😃

作为一个业余爱好项目，我还在[www.dscrashcourse.com](http://www.dscrashcourse.com/)建立了一套全面的**免费**数据科学课程和练习题。

再次感谢您的阅读！📕