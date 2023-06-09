# 为什么每个 python 项目都应该使用虚拟环境！

> 原文：<https://towardsdatascience.com/why-you-should-use-a-virtual-environment-for-every-python-project-c17dab3b0fd0?source=collection_archive---------8----------------------->

## 虚拟环境如何加速和清理您的整体 python 工作流

![](img/8b87c9a7202a4b78a65bd641f50c1209.png)

帕特里克·托马索在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

想象一下，你想要一本特定的书，然后走进图书馆寻找。然而，令你震惊的是，整栋建筑内完全没有组织——没有办法区分小说和非小说；没办法知道哪个作者写了什么；根本没办法找到你的书。你去找图书管理员，问她具体的书在哪里，但她只告诉你“搜索一下。”要找到你非常想要的那本书，你唯一的选择就是搜索每一个。单身。书。英寸的。建筑。

这个库是您的计算机，更确切地说是您的 python 包 bin。所有这些杂乱无章的书籍都是你多年来为每个随机项目安装的无尽的软件包。现在，下一次你安装一些东西或者开始一个项目时，你将完全不知道这个包是否是最新的，它是否与另一个包或者 python 版本冲突，或者它是否存在。这样的混乱会导致痛苦和无聊的挫折，不仅会占用你的项目，还会占用你本来可以做更有成效的事情的时间。

你问的解决方案是什么？**虚拟环境**。

# 什么是虚拟环境？

![](img/96d18ba57364b9107082df05f544753c.png)

照片由 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的[伊尼基·德尔·奥尔莫](https://unsplash.com/@inakihxz?utm_source=medium&utm_medium=referral)拍摄

我喜欢把虚拟环境想象成我每个项目的包装书架。如果我正在做一个烹饪项目，我没有必要有一本关于冲浪的书。类似地，如果我正在进行一个机器学习项目，我就没有必要拥有一个前端库。在我的“书架”上只有我需要的**包，这消除了我可能遇到严重的全局安装和包冲突错误的所有机会，并允许我专注于真正重要的东西——我的代码。

就像包一样，我也可以为我的项目指定我想要的 python 的什么**具体版本**。如果你想要一个 python3 项目，就启动一个 python3 环境——如果你想要一个 python2.7 项目，就启动一个 python 2.7 环境——如果你想要一个 python 3.5.3 环境，猜猜看，今天是你的幸运日！**

![](img/e639bce9c82a7d38d30cae252bfaec6d.png)

汤姆·温克尔斯在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

虚拟环境通过创建特殊的隔离环境来帮助解决这些问题，在隔离环境中，您安装的所有软件包和版本都只适用于该特定环境。这就像一个私人岛屿！—但对于代码来说。岛上发生的任何事都不影响你的大陆，你的大陆发生的任何事都不影响你的岛。

一旦你完成了这个项目，就跳出这个岛回到大陆。

如果你仍然不相信，让我们花一点时间来看看利弊:

# **优点:**

*   你可以在特定环境下使用任何版本的 python，而不必担心冲突(对我的 python 2.7 mac 用户大喊！)
*   您可以更好地组织您的包，并且确切地知道您需要哪些包来运行您的代码，以防其他人需要在他们的机器上运行它
*   您的主 python 包目录不会被不必要的 python 包淹没

# **CONS:**

*   嗯……也许是太空？最多几百兆？这算不算骗局？

# 结论:

总的来说，虚拟环境在处理不同的项目时变得非常方便。当然，如果您的项目不依赖于包，那么就不需要版本和包的私人孤岛；但是，如果您的项目确实需要几个包，那么虚拟环境除了提供帮助之外，绝对无能为力。首先，看看 **venv** 、 **virtualenv** 或**pipenv**——我很快会有一篇[文章](/venvs-pyenvs-pipenvs-oh-my-2411149e2f43)描述它们各自带来的优势以及如何开始使用它们！

编辑:后续文章现已出，点此查看！