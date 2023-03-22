# 无 Dockerless 笔记本:期待已久的数据科学未来

> 原文：<https://towardsdatascience.com/dockerless-notebook-the-long-awaited-future-of-data-science-7cde7707f7ff?source=collection_archive---------16----------------------->

## 无坞站笔记本是未来

数据科学很难。数据科学家花费数小时想出如何在他们的笔记本电脑上安装 Python 包。数据科学家阅读了许多页的谷歌搜索结果，以连接到那个数据库。数据科学家为工程师编写详细的文档，以便将机器学习模型部署到生产中。数据科学家准备了精美的幻灯片来说服业务人员如何提高留存率。数据科学家担心他们的数据管道中断会导致数据质量问题。

数据科学的挑战是真实的。他们不熟悉的新语言有陡峭的学习曲线。没有人知道如何在有限的时间内满足业务影响需求。有最佳的工程实践可以遵循，以确保他们的交付物的质量。对数据科学团队的工程支持有限。

## docker 容器解决了哪些问题？

对于个体数据科学家和其他数据团队成员来说:建立开发环境和维护一致的操作环境是一种令人沮丧的经历。安装说明通常不会涵盖所有必需的依赖项。一些基于 GPU 的人工智能库要求数据科学家熟悉硬件的底层细节。错误信息的信息量不足以解释错误的原因。库之间的依赖冲突使得很难为多个项目维护一个工作的开发环境。数据科学家和工程师之间的合作需要双方进行额外的和不必要的工作。

![](img/1944bd7c3fa79cc64aeef7268e620229.png)

照片由[史蒂夫·哈拉马](https://unsplash.com/@steve3p_0?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/dolphin-tail?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄

## Python 虚拟环境怎么样？

不可否认，Python 虚拟环境对一些数据科学家来说工作得很好。但是，它不能满足数据科学任务的多样化要求:

1.  数据科学家每天使用 Spark、R 和 SQL 变得越来越普遍。Python 虚拟环境如何适用于 Python 之外的不同语言和框架？
2.  一些数据科学家主要与他们的工程队友合作，将机器学习模型部署到生产中。如果存在对操作系统而不是 python 库的依赖，Python 虚拟环境如何？

`conda`的诞生缓解了这两个问题，事实上 conda 在数据科学界非常受欢迎。conda 本身的安装并不困难，它为环境提供了许多常见的数据科学包。

然而，并非所有在`pip`可用的包都在`conda`可用。如果在`conda`上找不到一个包，那么数据科学家可能不得不与`conda`一起使用 pip，这是混乱和意外问题的主要来源。例如，在这个[未解决的 Github 问题](https://github.com/ContinuumIO/anaconda-issues/issues/1429)中，有许多关于`pip`如何与`conda`一起工作的争论。

具有讽刺意味的是，Anaconda 的副总裁曾经做过一个题为[“Conda、Docker 和 Kubernetes:数据科学的云原生未来”](https://conferences.oreilly.com/strata/strata-ny-2018/public/schedule/detail/71478.html)的演讲。如果 99%的环境相关问题都解决了，那就没用了。剩下的 1%的问题让开发者的体验无法接受。

## docker 容器有什么帮助？

不严格地说，docker 容器是一个“轻量级虚拟机”，它将运行应用程序所需的一切打包到一个 docker 映像中。Docker 映像旨在在服务器之间移动，并保证环境的一致性。

因此，当将机器学习模型部署到生产中时，数据科学家将不再担心依赖性的破坏。上周入职的新毕业生可以在 docker 容器运行后立即开始为团队做出贡献，而不是偷偷在拥有更好基础设施的公司寻找新职位，成立数据科学团队。

**为什么 docker 容器在数据科学社区中不受欢迎？**

Docker 根本不是什么新技术，为什么大多数数据科学家都没有采用？主要有两个原因:

1.  学习曲线很陡。
2.  开发者体验不好。

要开始使用 docker 容器，至少要学习如何

1.  启动/停止集装箱
2.  将外壳连接到正在运行的容器
3.  将本地卷装入容器

在现实中，这些还不够:如何在一个不知道密码的容器里？为什么我的 docker 容器在停止后会丢失所有数据？我如何设置一个私有的 docker 注册中心，以便从我的远程集群中提取 docker 映像？如何终止正在使用端口 8808 的进程？

当谈到编写`Dockerfile`时，人们必须熟悉 Linux Shell 命令和`Dockerfile`语法。如果一个项目要使用一个 docker 映像，那么一个软件工程师可能要管理太多的 docker 映像。

因此，数据科学家要么很难解决与环境相关的问题，放弃可再现性并遭受糟糕的工程实践，要么花太多时间学习和操作 docker。

**保护环境不是数据科学家的工作**

数据科学家应该**而不是**在环境上花费时间，以便他们可以专注于他们擅长的事情:构建仪表盘、开发机器学习模型、向业务团队成员提供可操作的见解。

## 无坞站笔记本是未来

想象一下，有一个聪明能干的 docker 助手为你做所有的事情:当你启动笔记本时，它可以自动启动容器并将其附加到笔记本上。当您想要将笔记本移动到远程集群上运行时，它可以提交您的本地 docker 容器，将其发送到远程本地集群，并自动管理它。

“ **Dockerless notebook** 的想法是，它允许你不用考虑 docker 容器就能开发和操作笔记本**。它与科学家日常使用的笔记本数据紧密集成。它消除了学习 docker 容器和操作任务，例如启动/停止容器、将外壳附加到容器以及将卷安装到容器。你甚至不会注意到 docker 正在你的笔记本上运行，就像你不会注意到 Jupyter 笔记本如何在浏览器和内存之间交换数据一样。**

“**无 Dockerless notebook** ”将帮助数据科学社区向“可再现的数据科学”和“无摩擦的数据科学”迈进，而不会产生不可接受的成本。