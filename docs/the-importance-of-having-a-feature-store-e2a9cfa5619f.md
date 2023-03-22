# 拥有功能库的重要性

> 原文：<https://towardsdatascience.com/the-importance-of-having-a-feature-store-e2a9cfa5619f?source=collection_archive---------43----------------------->

## 我已经看到了构建和维护一个集中的特性库所带来的巨大价值。特征库是一个包含许多功能的集中式软件库，其中每个功能根据标准化输入(数据)创建一个特征。这些特征可以在以后输入到旨在解决不同问题的机器学习算法中。

![](img/d1c2f4b45e06f857114e9140ddebc9b0.png)

约书亚·阿拉贡在 [Unsplash](https://unsplash.com/s/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

尽管特征存储在数据策略中起着至关重要的作用，但仍然很难在网上找到关于它们的信息。但是，了解什么是功能存储以及它们为什么重要是至关重要的，特别是在当今世界，数据治理越来越多，商业问题越来越多地由机器学习模型解决。事实上，功能商店应该是你公司整个机器学习运营的基础部分。

在它们提供的其他好处中，特性存储的三个具体优势使它们变得非常有价值:它们支持在整个公司范围内简单地重用特性；它们使得标准化特性定义和命名约定变得简单；它们使企业能够在数据科学家离线开发的模型和在线部署的模型之间实现一致性。

**什么是特色店？**

因为“存储”可能有多种含义，所以有必要澄清在术语“功能存储”中，这个词与“存储”相关商店实际上是一个包含许多功能的集中式软件库，其中每个功能根据标准化输入(数据)创建一个单一特征。这些特征可以在以后输入到旨在解决不同问题的机器学习算法中。

当大规模操作机器学习系统时，数据专业人员通常需要设计大量功能，以便训练他们的模型。如果模型成功地解决了创建它所针对的问题，并部署到生产环境中，那么以后应该在生产环境中创建完全相同的特性，以提供给在生产环境中运行的模型。在此过程中，要素存储成为数据科学家的宝贵资源。

要素存储还允许数据科学家简化维护要素的方式，为更高效的流程铺平道路，同时确保要素得到正确存储、记录和测试。整个公司的许多项目和研究任务都使用相同的功能。通过要素存储，数据科学家可以快速访问他们需要的要素，并避免重复工作。功能商店还提供了一种经过测试和质量保证的方法来创建功能，并知道它是可靠的。

为什么我们需要特色商店？

使用要素存储有助于缓解数据科学家面临的一些特定于要素的挑战。其中包括:

*   不会重复使用特征。数据科学家面临的一个常见障碍是花费时间重新开发功能，而使用以前开发的功能或其他团队开发的功能就足够了。要素存储允许数据科学家避免重复工作。
*   功能定义各不相同。任何一家公司的不同团队可能会以不同的方式定义和命名特性。此外，访问某个特定特性的文档(如果存在的话)通常是一个挑战。特征存储通过保持特征及其定义的组织性和一致性来解决这个问题。功能库的文档可以帮助您围绕公司的所有功能创建一种标准化的语言。您确切地知道每个特征是如何计算的，以及它代表什么信息。
*   培训和生产功能不一致。生产和研究环境通常使用不同的技术和编程语言。流入生产系统的数据流需要实时处理为特征，并输入到机器学习模型中。为了使建模工作有效，在研究中离线开发的模型需要提供与在线部署的模型完全相同的预测，给定相同的数据作为输入。拥有一个与环境无关的特征库(在线和离线)意味着给定相同的数据，模型将被提供完全相同的特征。‍

**特色店福利**

当一家公司采用功能存储时，它允许团队中的数据专业人员针对任何机器学习用例遵循相同的通用工作流，而不管他们当前正在解决的挑战(例如分类和回归、时间序列预测等)。).这种工作流通常是与实现无关的，这意味着它可以很容易地用于新的算法类型和框架，例如经典的 ML 算法以及较新的深度学习框架。

使用功能库的另一个主要好处是节省时间。在任何建模工作中，创建特征的阶段往往是最耗时的；这一敏感过程要求正确计算要素，一次要创建数千个要素，并在生产环境中以与研究期间离线计算完全相同的方式进行计算。使用特征库使得创建特征的过程更加简化和高效。

**我的建议:集中式功能商店**

我的团队从构建和维护集中式特征存储中获得了很大的价值，在该存储中，公司内不同的数据专业人员都可以创建和管理供团队其他成员使用的规范特征。这使得数据科学家可以轻松地将他们构建的要素添加到共享要素存储中。一旦有了特性，就很容易在线(在生产中)和离线(在研究中)使用它们，只需引用一个特性的简单规范名称。

今天，我们的功能库中有数千个功能，用于公司和所有领域的各种机器学习项目。我们的数据科学家一直在添加新功能，新功能会自动计算并每天更新。这使得我们的团队成员能够避免重复工作，并轻松访问建模和研究所需的大量数据。

更多信息和有用的信息请访问 [Bigabid 技术博客！](https://www.bigabid.com/blog/)