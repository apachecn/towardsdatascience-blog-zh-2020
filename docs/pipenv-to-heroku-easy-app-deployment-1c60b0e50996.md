# Pipenv 到 Heroku:轻松部署应用程序

> 原文：<https://towardsdatascience.com/pipenv-to-heroku-easy-app-deployment-1c60b0e50996?source=collection_archive---------32----------------------->

## 使用 Pipenv 将应用程序从 GitHub 部署到 Heroku 的指南

作者: [Edward Krueger](https://www.linkedin.com/in/edkrueger/) 数据科学家兼讲师和 [Douglas Franklin](https://www.linkedin.com/in/douglas-franklin-1a3a2aa3/) 助教兼技术作家。

*在本文中，我们将介绍如何使用 Github 资源库中的 Pipfile 部署应用程序，从而简化应用程序部署！*

![](img/c76773f4ac2cc8d2b65eefc496002110.png)

照片由 [Jesus Kiteque](https://unsplash.com/@jesuskiteque?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/development?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

## 有关虚拟环境或 Pipenv 入门的更多信息，请查看本文！

# 数据科学和部署问题

数据科学家通常是跨学科的，并没有被教导如何与其他人合作并将项目推向生产。因此，通常缺乏部署、适当的环境和包管理技能。这给复制、部署和共享项目带来了困难。可再现的数据科学项目是那些允许其他人在您的分析基础上重新创建和构建，并重用和修改您的代码的项目。

由于缺乏对虚拟环境的了解或经验，新开发人员通常在系统级安装所有东西。用 pip 安装的软件包被放置在系统级。对每个项目都这样做的结果是一个臃肿且难以管理的单一 Python 环境。在这种环境下开发应用程序的人如何知道在 requrements.txt 中包含哪些依赖项？

数据科学家需要能够将他们的模型投入生产。在模型开发过程中使用良好的实践大大简化了部署过程。即使是拥有独立部署或开发团队的数据科学家也可以从学习部署过程中受益。了解从开发到部署的完整工作流程的数据科学家可以交付一个更易于部署的产品。这种意识可以减轻开发人员和 DevOps 团队的压力。

有效的环境管理可以节省时间，并允许开发人员和数据科学家创建易于部署的独立软件产品。

## Pipenv 和 Heroku

Pipenv 将软件包管理和虚拟环境控制结合到一个工具中，用于安装、删除、跟踪和记录您的依赖关系；以及创建、使用和管理您的虚拟环境。Pipenv 本质上是将 pip 和 virtualenv 包装在一个产品中。

Heroku 提供许多软件服务产品。我们需要 Heroku 云平台服务来托管应用程序。不用担心；创建帐户和托管应用程序是免费的。云平台支持多种编程语言的应用，包括 Python、Node.js、Scala、Ruby、Clojure、Java、PHP 和 Go。

## 应用部署

一旦我们将一个带有 Pipfile 的应用程序推送到 Github，Heroku 允许我们快速地将一个应用程序从 GitHub 部署到 Heroku。确保您的 Pipfile 在项目的根目录下。我们的应用程序使用 SQLite 数据库进行部署。

我们需要对我们的应用程序项目文件进行一些修改，以便应用程序可以在 Heroku 上运行。

## 安装 gunicorn

Gunicorn 是一个 Python WSGI HTTP 服务器，它将为 Heroku 上的 Flask 应用程序提供服务。通过运行下面的代码行，您将 gunicorn 添加到您的 Pipfile 中，这是在 Heroku 的容器中运行您的应用程序所需要的。

```
pipenv install gunicorn
```

## 添加 Procfile

在项目根文件夹中创建一个`Procfile`,并添加下面一行:

```
web: gunicorn app:app
```

第一个`app`代表运行您的应用程序的 python 文件的名称或者应用程序所在的模块的名称。第二个`app`代表你的应用名称，即 app.py，这个 Procfile 配合 gunicorn 和 Heroku 的 Dynos，远程为你的应用服务。

## 部署

一旦我们有我们的应用程序测试和工作在本地，我们把所有的代码推到主分支。然后在 Heroku 上，去部署一个新的 app 看看下面的页面。

![](img/5e091f3bf30f3de32e6730e5f04ed0ee.png)

选择 Github 并搜索您的存储库

接下来在 Heroku 上，选择 GitHub 并输入存储库的名称，然后点击 search。一旦您的用户名/存储库出现，单击连接。选择所需的分支，然后单击部署。

![](img/42ed924ce1c0e5796cddbfa02358509e.png)

选择主服务器并部署分支

构建日志将开始填充页面上的控制台。注意，Heroku 首先查找 requirements.txt 文件，然后从 Pipenv 的 Pipfile.lock 安装依赖项。

![](img/762eed8b5810e67e33f0a75af4bc5769.png)

一旦从 Pipfile.lock 构建了您的环境，并且构建成功，您将会看到下面的消息。

![](img/b9cc5bb65fd66512d59eadbab4d5cf2d.png)

成功的应用部署

该应用程序已成功部署！点击查看按钮，查看 Heroku 上部署的应用程序。

## 自动部署

我们可以启用自动部署，让 Github master 的更改在推送时显示在 Heroku 上。如果您使用这种方法，您将希望确保始终有一个工作的主分支。

![](img/ac991872711bc597265ecaa63c5d73ee.png)

启用自动部署

## 结论

对于希望在生产中部署、构建或使用代码的数据科学家和开发人员来说，实践良好的环境和包管理至关重要。当数据科学家和开发人员在其工作流程的上游使用这些开发技能时，可以帮助团队。

有了一个管理良好的 Pipenv 和 Pipfile，Heroku 的服务器可以用最少的故障排除来重建我们的应用程序。这使得我们可以在几分钟内将 GitHub 中的应用程序项目目录转移到一个已发布的应用程序中。

使用 Pipenv 这样的环境和包管理器可以使包括部署在内的许多过程变得更加舒适和高效！有关虚拟环境或 Pipenv 入门的更多信息，请查看本文[。我们希望本指南有所帮助。谢谢大家！](https://medium.com/@edkrueger_16881/virtual-environments-for-data-science-running-python-and-jupyter-with-pipenv-c6cb6c44a405#f91f-d040f09f69cf)