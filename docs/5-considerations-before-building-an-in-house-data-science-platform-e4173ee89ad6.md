# 构建内部数据科学平台之前的 5 个考虑事项

> 原文：<https://towardsdatascience.com/5-considerations-before-building-an-in-house-data-science-platform-e4173ee89ad6?source=collection_archive---------28----------------------->

构建还是购买:来自多年构建机器学习平台的见解

![](img/0f22d5aee03652e22d4656deb232905f.png)

我和我的商业伙伴作为数据科学顾问已经工作了多年，帮助企业将人工智能融入他们的商业模式。我们合作过的每个数据科学家都有自己的工具偏好，使用自己的语言，利用自己的开源工具。对于某些项目，我们也非常重视我们的流程。当我在所有工作中使用 Python 时，我的同事使用 r。当我对我的深度学习框架深信不疑时，我的同事更喜欢 Keras 的易用性。问题是，我们理解对工具灵活性和定制化的需求。当一个组织构建自己的内部平台时，他们可以根据团队的需求来构建。而且，很好玩！你可以找到创造性的方法来解决问题，这是数据科学家最喜欢的。唯一的困境是，大多数时候你不是被雇佣来构建和管理数据科学平台的。你可能被雇佣来构建和部署高影响力的机器学习模型。

尽管如此，您可能仍然喜欢从头开始构建自己的数据科学平台。在多年开发、迭代和测试数据科学平台之后，我想分享一些见解，供开始这一旅程之前考虑。

# **建筑融入了我们的血液**

作为数据科学家，我们天生就是建设者和问题解决者。如果我们想解决一个问题，我们只需建立自己的解决方案。在大多数情况下，我们拥有这样做的技能、工具和知识。我们合作的许多客户都有内部数据科学系统，或者正在创建一个。随着他们对平台的需求变得越来越复杂，他们决定寻求替代解决方案。他们决定投入更多时间来建立模型和解决复杂问题，而不是建立一个全栈数据科学平台。

因此，当您考虑构建自己的内部数据科学解决方案时，需要考虑以下几点:

# 1.无限的工具灵活性

毫无疑问，有太多的开源工具供我们使用。但是管理所有不同的工具以便能够利用它们是一个挑战。

![](img/00f78b34908fefc75e4ff6df6fa7fa98.png)

无论是 R、Python、SQL、Scikit-learn、Hadoop、spark、Tensorflow、Keras、Jupyter——这个列表还在继续——您都需要一个中心位置来将数据科学难题的所有部分集中在一起。

光是想到下载 Tensorflow 就带来巨大的痛苦。也许这看起来很熟悉:

![](img/06422ec6403fe45002f605832a7ed0fa.png)

安装张量流时出错

![](img/658a1d4a067794bae8f5024671a54a8a.png)

堆栈溢出常见问题

创建一个系统，可以轻松集成团队所需的所有工具。此外，工具也在不断地适应和发展。一定要通过构建能够集成新工具的开放基础设施来规划未来。

# 2.再现性

有许多手动系统，公司可以在其中支持可再现的数据科学。公司已经使用 Excel 文件、笔记本、Docker、Git 等。不幸的是，人类是不完美的，有时会在记录工作时错过一些关键元素。让所有数据科学活动集中在一个位置有助于解决跟踪问题。通过自动记录和存储每个过程，数据科学家能够回溯和重现项目，并审查研究的有效性。

# 3.小组管理

人们常说，数据科学家在孤岛中工作。团队面临的一个挑战是统一和同步他们的工作。任务管理、职责转换、报告和进度跟踪等简单的团队组织如果集中化，都可以加快数据科学进程。考虑交流的方法，并创建简单的用户界面来实现无缝转换将节省时间。不仅如此，它还会避免团队成员的挫败感。根据您的团队，项目可能涉及研究人员、数据工程师或机器学习工程师，甚至开发人员或 IT 人员。任务之间的平稳过渡会带来沟通障碍和技术低效。这意味着构建可以与团队共享的组件，以节省编码时间并支持可重用的机器学习。这样，团队成员，无论他们是否是数据科学家，都可以快速构建新模型。重要的是要考虑平台元素，这些元素可以无障碍地执行整个工作流程。并且，建议在这个任务中使用产品经理来咨询，以便正确地完成它。尽可能集成 mlop，以减少机器学习管道中的摩擦。

# 4.资源管理和可扩展性

无论您是在构建机器学习模型还是在生产中运行模型，计算能力都是不可避免的。一个有组织的计算资源管理系统将会改变游戏规则。添加到内部平台的一个重要组件是在团队成员之间共享计算资源的方法。不仅如此，管理计算预算和监督计算使用的方法可以节省大量资金。

其次，做好最好(或最坏)的准备。对于您的平台来说，能够连接到现有计算并立即自动扩展到云而无需配置是至关重要的。准备资源，让您的数据科学家能够一次运行数百个实验。更重要的是，对于任何成功的生产模型，都要做好模型流量意外激增的准备。它可以将你的生产模型从完全崩溃中拯救出来。无法扩展计算会扼杀促销的动力和业务的成功。

# 5.可用性和设计

对于数据科学平台，功能是第一位的。但是，必须考虑用户体验。无论是简单的功能，如搜索和标记实验，还是复杂的直观用户界面。内部平台可以根据团队的需要慢慢构建。唯一的问题是，它几乎永远不会是故意的。设计超越功能的工作流并真正最大化效率需要计划、时间和努力。有时候你会发现，商业产品比你先知道你可能需要什么。以苹果公司为例。在苹果之前，大多数手机只需要打电话、发短信和偶尔拍摄像素化照片的功能。今天，你能想象你的手机没有全球定位系统，互联网搜索，Siri 或你最喜欢的播客随时可用吗？走在路边，预测机器学习工作流。

# **建造智能机器**

制造智能机器是我们——数据科学家——最擅长的事情。当决定是否建立一个内部数据科学平台时，考虑一下你受雇做什么。作为一名数据科学家，为了给公司带来价值，你需要拿出成果。数据科学平台的目标是帮助数据科学家专注于魔法——算法。下一步是考虑你的备选方案。自从我和我的商业伙伴开始以来，数据科学平台已经有了巨大的发展，并且具有广泛的功能。在分析商业机器学习平台或开源工具时，也可以使用这 5 个考虑因素。确保你考虑了所有的方面，你将会在机器学习的道路上取得突破。