# 每个数据科学家都应该知道的 5 项常见技能

> 原文：<https://towardsdatascience.com/5-common-skills-data-scientists-should-know-3247b2b12318?source=collection_archive---------36----------------------->

## 意见

## 仔细看看我作为数据科学家所使用的流行技能。

![](img/091a99776cfad5c90cec5512c7726290.png)

[托马里克](https://unsplash.com/@malcoo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在[Unsplash](https://unsplash.com/s/photos/python?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)【1】上的照片。

# 目录

1.  介绍
2.  结构化查询语言
3.  Python 还是 R
4.  Jupyter 笔记本
5.  形象化
6.  沟通
7.  摘要
8.  参考

# 介绍

数据科学和机器学习经常需要大量的技能。然而，作为一名数据科学家，我在几家公司工作了几年，我想强调数据科学家应该知道的五项常见技能。作为一名数据科学家，你可能会在职业生涯中用到这些技能。我将概述 SQL、Python/R、Jupyter Notebook、可视化和通信。

当然，在工作过程中，您会遇到更多必需的技能和有益的技能，但我希望这些能作为一个良好的开端，或增强您目前作为数据科学家的旅程。

# 结构化查询语言

作为一名正在学习的数据科学家，甚至是一名专业的数据科学家，您可能会惊讶地看到这第一项技能。它通常与数据分析师相关联，而数据科学家则专注于编程语言和机器学习算法。然而，为了开始使用 Python、R 或您的机器学习算法，您需要收集数据。作为一名数据科学家(*以及我认识的其他数据科学家*)，这些年来我能想到或亲身经历的最流行的技能是 SQL。大多数公司都有一个数据库，里面有你可以查询的表格。查询结果可能是您用于数据科学模型的数据集。虽然通常情况下，成为一名成功的数据科学家并不需要成为 SQL 专家，但是您应该熟悉一些关键的 SQL 概念和命令。

*我遇到的最流行的 SQL 概念是:*

```
SelectInner JoinsLeft JoinsWhereGroup ByOrder ByAliasCase WhenSubqueries Common Table Expression
```

**例子**

***下面是一个简化的查询示例，我将运行该查询来获取我的数据科学数据集。***

```
*select t1.column_1, t1.column_2, t2.column_3**from table_1 t1**inner join table_2 t2 on t2.shared_id = t1.shared_id**where date > ‘2020–08–01”**group by t1.column_1**order by t1.column_1*
```

# Python 还是 R

我在学校学过 R，并在一些项目中使用它，但我主要使用 Python，所以我将讨论 R 之上的语言。数据科学家可能使用的另一个工具是 SAS。然而，Python 是有益的，因为大量的库或包已经包含了常见的数据科学和机器学习算法。您可以使用准备好的库，这些库涵盖了广泛的模型，如**随机森林、逻辑回归、决策树**等。除了访问大量重要信息并使您的数据科学更加高效之外，您还可以在 Python 中使用面向对象的格式(*类、方法或函数、模块等)。*)。这种格式有助于使您的模型更有效地运行，同时还创建了一个可伸缩的部署框架。此外，当处于 *OOP* 格式时，它帮助您的模型变得更容易部署，因为您可以自己完成或者与软件工程师、数据工程师或机器工程师就您的部署进行交流。

***Python 中一些有用的库包括，但不限于:***

```
NumPySciPyPandasKerasTensorFlowSciKit-LearnPyTorch
```

> 我可能在探索性数据分析期间使用 NumPy 和 Pandas 最多，在数据科学的模型建立期间使用 SciKit-Learn，在更多的机器学习和深度学习练习中使用 Keras 和 TensorFlow。我自己没有用过 PyTorch，但听说它很受欢迎。

# Jupyter 笔记本

![](img/d6eb2b54eb693504e8a3007d3382753c.png)

照片由[JESHOOTS.COM](https://unsplash.com/@jeshoots?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在[Unsplash](https://unsplash.com/s/photos/notebook?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)【2】上拍摄。

使用 Python 时，还可以使用流行的 Jupyter Notebook 工具来组织和研究数据集，并执行主要的代码集。在导入数据集、应用探索性数据分析、特征工程和模型构建时，我通常首先使用 Jupyter 笔记本。我认为它是一个地方，在将我的代码最终确定为最终将被集成和部署的 *OOP* 格式之前，有我的草稿。在单元格中添加注释以及创建标题和项目符号很好，这样您就可以轻松地与其他数据科学家合作，或者如果您希望在将来回到您的模型并找到记录良好的单元格，也很好。

***下面是***[***Jupyter 笔记本***](https://jupyter.org/)***【3】:***

[](https://jupyter.org/) [## Jupyter 项目

### Jupyter 笔记本是一个基于网络的交互式计算平台。该笔记本结合了现场代码，方程式…

jupyter.org](https://jupyter.org/) 

# 形象化

能够可视化数据科学过程的几个部分非常重要。您可能希望可视化业务问题、数据集以及可视化模型本身。也许数据科学中最流行的可视化时间是在模型建立之后。当你向利益相关者解释你的结果时，你将描述复杂的想法和输出，这些可以更好地用视觉来解释。它还可以帮助您自己和团队中的其他人更好地了解模型正在执行什么，以及当您添加可视化时它是如何工作的。

***您可以用于数据科学流程的一些可视化工具包括但不限于:***

```
TableauLookerPowerBIPython Libraries (Matplotlib, Plotly, Seaborn)
```

> 我个人倾向于使用 Tableau 和 Seaborn，但它们都是用于数据科学的非常有用的工具。

# 沟通

除了视觉化，你还可以期待交流。

> 沟通是一项技能，在数据科学教育或训练营中没有教授多少，但作为一名数据科学家，这是一项至关重要的技能。

在开始编码的数据科学过程之前，您必须与几个不同的利益相关者和主题专家交谈。您可能需要说服他们，对于特定的情况，数据科学首先是必要的。一旦您成功完成了流程的这一部分，您将会看到模型本身的优势、关键点和更新，以及最终模型的结果和影响。

***在数据科学过程的这些部分，你可以期望使用沟通:***

```
Business problem with stakeholdersProof of concept with subject-matter expertsUpdates on modelResults and impact of the model
```

# 摘要

![](img/6729091392d8b13f995a4c32931caf14.png)

照片由[克里斯蒂娜@ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在[Unsplash](https://unsplash.com/s/photos/success-female?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)【4】上拍摄。

如您所见，数据科学家应该知道几项关键技能。你可以花几个小时来描述技能，但最好是一天一天地开始学习，不要不知所措。您应该知道的五项常见数据科学技能是:

1.  *SQL*
2.  *Python 或者 R*
3.  *Jupyter 笔记本*
4.  *可视化*
5.  *交流*

如果您能想到您使用的任何通用技能，以便其他数据科学家可以在进入就业市场时进行预测，或者作为当前的数据科学家提升自己，请在下面发表评论。

*感谢您的阅读！*

# 参考

[1]由[托马里克](https://unsplash.com/@malcoo?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/python?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片，(2018)

[2]JESHOOTS.COM 在 [Unsplash](https://unsplash.com/s/photos/notebook?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上[拍摄的照片，(2017)](https://unsplash.com/@jeshoots?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

[3]朱庇特项目，[朱庇特项目|首页](https://jupyter.org/)，(2020)

[4]照片由[克里斯蒂娜@ wocintechchat.com](https://unsplash.com/@wocintechchat?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在[Unsplash](https://unsplash.com/s/photos/success-female?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)(2019)上拍摄