# 脸书获得集成分类器的故事

> 原文：<https://towardsdatascience.com/the-story-of-an-ensemble-classifier-acquired-by-facebook-53eeaa5b5a97?source=collection_archive---------45----------------------->

## [人工智能笔记](https://pedram-ataee.medium.com/list/notes-on-ai-for-developers-29d1d79c4824)

## 以及设计您自己的集成分类器的一些见解

![](img/8e64dcf61d869be3d33182f014563ebb.png)

由[在](https://unsplash.com/@jenrielzany?utm_source=medium&utm_medium=referral) [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的滑稽 Jadraque

我写这篇文章是想通过我自己的故事来描述集成方法在行业中的意义。在本文中，我不解释经典方法，因为存在各种资源。尽管如此，我还是想向你们展示集合方法的力量以及你们实现它的方式。我的目标是分享一个我们几年前发明的集合方法的故事，这个方法在脸书的领导下仍然有效。集合方法无论是经典的还是你自己设计的都比你想象的要好得多。我保证。

首先，让我告诉你故事是如何开始的。我是一家初创公司的机器学习团队的负责人，致力于开发一种智能设备。该设备旨在根据肌肉信号识别手势。这个小装置在前臂上有八个传感器，记录肌肉信号。我们处于早期阶段，产品还没有准备好。我们的原型在数据记录方面的功能让我们惊讶了很多次。此外，我们不确定可能的手势应该有针对性。然而，**我们不得不在早期设计一个手势识别引擎**，因为我们到处都有演示。

## —基本分类器不必是弱分类器。

建议基于大量数据建立模型。然而，对我们来说很明显，原型记录的数据质量很差。另外，用例还没有确定。所以，我们用原型收集大量数据的努力可能会白费。

因此，我决定设计一个基本分类器，它不需要那么多数据，但性能仍然一般。我引入了一个向量分类器作为基本分类器，它使用余弦相似性来评估类成员。对我们来说，向量分类器比弱分类器好(比随机分类器稍好)，但它离可接受的分类器还很远。这是设计一个集合方法的第一步，这个方法在多年后仍归脸书所有。

## —基本分类器应基于相同的算法构建。

集成分类器是关于组合或聚集几个分类器，而不管它们的类型或算法。还建议基分类器应该相互独立。

知道我决定开发**大量简单的具有相似算法**的基分类器，而不是几个具有不同算法的基分类器。这个决定是由随机森林算法的直觉启发的，其中它的基本分类器有一个类似的算法。还可以想到聚合一系列一级决策树的 Adaboost 还是类似的算法。

拥有相似的基分类器也给了我一个机会来获得更好的洞察力，然后控制集成方法，因为基分类器的行为在这个过程中被广泛地研究。下一个问题是我们应该如何聚集基本分类器。

> 建议——你应该对基本分类器使用相同的算法。这给你一个更好的机会来控制你的集成分类器的进化。

## —必须精心设计聚合基本分类器的策略。

下面简要列出了聚合基本分类器的不同经典策略。在这个概述之后，我解释我们使用了什么策略。

*   **策略一:注意机制**。该算法使用夸张或注意机制以自适应的方式学习基本分类器。这意味着算法更加关注基本分类器失败的区域。这有助于减少预测中的偏差。这些方法通常被称为升压。
*   **策略二:数据拆分**。该算法在没有交互的情况下并行学习基本分类器。每个基本分类器是在训练数据集中随机生成的数据集上学习的。这有助于减少预测中的差异。这些方法通常被称为装袋。
*   **策略三:模型堆叠。**该算法在没有交互的情况下并行学习基分类器。每个基本分类器是在整个训练数据集上学习的。然后，它通过训练元模型来组合基本分类器的结果，该元模型采用初步结果并创建最终预测。

在这里，我想描述我们如何选择一种策略来聚合基本分类器的结果。

机器学习问题中存在**偏差-方差权衡**。我们也有。然而，我们决定以不同于教科书建议的方式来应对这一挑战。我们介绍了两个模型:人口模型和个性化模型。人口模型旨在为一大群人完美地工作，但不是每个人。该模型是使用训练数据集学习的。个性化模型旨在为一小组用户工作，而人口模型工作正常。这个模型是利用一个人在每次使用中记录的数据来学习的。

简而言之，我们希望这个小工具能够完美地为一大群人工作，而不是为所有人工作。我们决定在人口模型中减少对方差的关注来改善偏倚。因此，旨在减少方差的策略 2 不可能是一个选择。

我们还有另一个挑战。用户可以根据方位和旋转以多种形式佩戴这个小工具。因此，每次用户佩戴小工具时，都必须调整基本分类器。我们花费了大量的时间和精力来开发一种可以有效调整基本分类器的算法，这超出了本文的范围。在 boosting 算法中，基本分类器是按顺序模式设计的，这种模式会产生相互依赖性，从而增加复杂性。因此，战略 1 也不是一个选择。

> 建议——构建强分类器的一个好策略是使用模型堆叠方法聚集大量使用相同算法训练的简单基础分类器，但是使用不同的数据集和/或超参数。

正如您所猜测的，我们选择了模型堆叠策略。我们设计的**元模型**是概率分类器和投票机制的结合。我们处理长度不固定的时间序列数据。例如，一个手势可能需要一秒钟，另一个手势可能需要两秒钟。因此，您可以在此列表中添加大量的超参数调谐。具有大量灵活基分类器的模型堆叠策略很好地解决了我们的问题。

## 临终遗言

简而言之，集成方法背后的哲学是使用“**加权专家群体的智慧**”。我喜欢这句话，这句话引自帕特里克·温斯顿教授在麻省理工学院开放式课程中讲授的人工智能课。

在工业中，你经常有许多未知，但你被要求定期提供结果。这不会通过应用花费大量时间学习和调整的方法来实现。另外，您总是希望设计一个可以在未来得到增强的分类器。集合方法可能是正确的方法。

开发一种能够解决不同问题的通用方法将是非常好的。但是，你可能想不出这样的方法。然而，如果你用整体方法来解决一个行业问题，你永远不会后悔。

# 感谢阅读！

如果你喜欢这个帖子，想支持我…

*   *跟我上* [*中*](https://medium.com/@pedram-ataee) *！*
*   *在* [*亚马逊*](https://www.amazon.com/Pedram-Ataee/e/B08D6J3WNW) *上查看我的书！*
*   *成为会员上* [*中*](https://pedram-ataee.medium.com/membership) *！*
*   *连接上*[*Linkedin*](https://www.linkedin.com/in/pedrama/)*！*
*   *关注我* [*推特*](https://twitter.com/pedram_ataee) *！*

[](https://pedram-ataee.medium.com/membership) [## 通过我的推荐链接加入 Medium—Pedram Ataee 博士

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

pedram-ataee.medium.com](https://pedram-ataee.medium.com/membership)