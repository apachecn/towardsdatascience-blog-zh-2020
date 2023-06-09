# 何时不使用数据科学

> 原文：<https://towardsdatascience.com/when-not-to-use-data-science-f2e42a3a77d3?source=collection_archive---------54----------------------->

## 意见

## 数据科学不占优势的例子。

![](img/f267b70dd3e13f3c935aefb2c01a43fd.png)

安德里亚斯·克拉森在[Unsplash](https://unsplash.com/s/photos/success?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)【1】上拍摄的照片。

# 目录

1.  介绍
2.  例子
3.  何时应该使用数据科学
4.  摘要
5.  参考

# 介绍

数据科学和机器学习都是有用的领域，它们应用多种工具来预测、建议、分类并最终解决常见的业务问题。您可以创建高度精确的模型，将以前的手动任务自动化。数据科学非常强大，可以为公司节省资金和时间。然而，你会发现你不一定需要数据科学来解决你遇到的每一个问题。在某些情况下，人工干预更重要，或者情况不允许通用模型。

我将描述何时不使用数据科学的四个例子。作为一名数据科学家，我发现随着时间的推移，我已经慢慢了解或体验到数据科学和机器学习不是必需的。我希望我能为你和你未来的处境提供一些启示和直觉。

# 例子

关于何时使用数据科学，何时不使用数据科学，有几个例子。以下是我想到的一些不需要数据科学模型的情况，这些情况可能会使情况变得更糟:

> 如果这个模型预测不正确，会有什么后果？

然而，数据科学、机器学习和人工智能正在不断发展，你可以期待很快看到新兴技术和模型准确性的改进。

*   **当你没有足够的数据时**

这个例子比较常见。当您生成模型时，您希望确保您有足够的数据。可能会出现坏数据输入和坏模型输出，同样，如果没有足够的数据，也会产生坏模型。该模型甚至可能表现良好，但它不会很好地推广到新的情况。您可能会过度适应，或者只是没有将环境暴露给足够多的可能的训练数据实例。在你建立一个模型以及在开发和资源上花费时间之前，先检查你是否有足够的数据。

*   **一次性任务时**

这个例子更依赖于具体的情况。您可能会被公司中的非技术利益相关者或领导者要求执行数据科学模型，也许您应该问问自己数据科学是否有必要。

*—如果您不是每天、每周甚至每月都输出结果，您可能不想花费时间或创建一个复杂的模型来整合接收新数据的计划。*

您可以应用类似的技巧来回答这个业务问题，并向利益相关者建议，例如，因为您只需要一个输出的 CSV 文件，所以您可以用一个简单的 Python 函数来回答这个问题(*您可能不需要与您的利益相关者深入探讨为什么您不打算使用数据科学模型，因为一些利益相关者只是想要一个输出的结果，并不关心您是如何得到它的*)。您可能只需要一个手动模仿数据科学模型主题的小函数。如果您非常了解这种情况，您可以自己创建容器或权重，并将其应用于特征或列，得出您自己的分数。以下是我描述的一个例子:

```
***Example:******.50*(feature_1) + .20*(feature_2) + .30(feature_3) = score (scaled)***
```

虽然这可能不是最准确的*，但是如果你需要一种快速的方法来组织数据，像这样的函数或者类似的函数就足够了。*

*   ***没有标记数据时***

*有时，您可能会遇到这样的情况:您想要对成千上万的观察值进行分类，但是您的数据集中有太多未标记的数据。有办法解决这个问题，如标签软件或无监督技术来创建新的标签。但是，如果您发现使用人工或其他软件服务来标记花费了太多的时间和金钱，那么您可能需要重新评估这种情况。也许在实现数据科学模型之前，您需要执行更多的数据工程技术，比如访问 API。*

*   ***预算紧张时***

*根据您接收和预测的数据量，训练模型可能会很昂贵。您的公司可能还没有足够的资源，昂贵的数据科学模型也不可行。*

*当你没有足够的时间时，这一点也与*一致。您可能有一个即将到来的截止日期，除了数据科学之外，还有一些方法是有益的，比如 Python 函数和规则。**

# *何时应该使用数据科学*

*有无数的情况下，你应该使用数据科学和机器学习。本质上，你可以翻转上面的例子，或者看看当你应该使用数据科学时，你是否有一个无监督的，监督的，时间序列等情况。*

*您也可以应用上面的示例，但是也可以结合数据科学技术和手动流程。*人在回路*作为这两种实践之间的桥梁变得越来越普遍。*

*何时使用数据科学的一些具体示例包括但不限于:*

*   **向用户推荐电影**
*   **预测一家公司的销售额**
*   **分析评论的情感**
*   **预测给定月份的温度**
*   **等。**

*“*何时不使用数据科学*的例子并不是阻止你使用数据科学，而是强调“*的重要性，因为你可以，并不意味着你应该*。最终，这取决于您的具体情况以及输出会影响什么。因此，在给定的特定环境下，每个示例都可以被反驳为数据科学的用例。*

# *摘要*

*所有这些例子都有注意事项，在这些情况下，您可能最终会使用数据科学。数据科学正在发展，新的方面正在出现。请记住，本文是以观点为导向的，这些观点或例子可能会很快改变。当您认为在特定情况下应该或不应该使用数据科学时，请随时在下面发表评论。总而言之，这里有四个不应该使用数据科学的例子。*

```
*When you don’t have enough dataWhen it’s a one-off taskWhen you don’t have labeled dataWhen your budget is tight*
```

*我希望你喜欢我的文章。感谢您的阅读！*

# *参考*

*[1]图片由 [Andreas Klassen](https://unsplash.com/@schmaendels?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/success?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄，(2017)*