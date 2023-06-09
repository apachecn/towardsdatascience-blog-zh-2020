# Julia For Data Science:正则化逻辑回归

> 原文：<https://towardsdatascience.com/julia-for-data-science-regularized-logistic-regression-667857a7f0ce?source=collection_archive---------21----------------------->

## 如何在 Julia 中从头构建正则化(L2)逻辑回归

![](img/2afba030973cef7418c3eda606f983f9.png)

图片来源:[https://dzone.com/](https://dzone.com/)

用于机器学习任务的惊人的库(如 scikit-learn)使得这些天来生成机器学习模型变得非常容易。必须从头开始编写每个模型的日子已经一去不复返了。这是一件好事，我们已经走过了那些时间，因为大多数问题最终都是优化问题。另一方面，这种“*符合和预测*”文化会对整个领域的学习文化产生严重的长期影响。一些拾荒者正在利用那些半生不熟的"*在 30 天内学会数据科学*"计划来喂养"*人工智能炒作*，这些计划经常导致毫无准备的学生在他们的"*拟合和预测*"模板背后没有真正的直觉。这是我最近关注的这些“*从头创建*”帖子的主要动机。

这篇文章建立在 [***第一篇文章的基础上，在第一篇文章中，我们使用我们新发现的爱，Julia，从零开始建立了多元线性回归。因此，我们将尝试在 Julia 中从头构建最著名的分类算法——逻辑回归(带正则化)!在这个实验的最后，结果将与用 Python 实现的 scikit-learn 进行比较。***](/julia-for-data-science-how-to-build-linear-regression-from-scratch-with-julia-6d1521a00611)

## 逻辑回归和正则化背后的直觉

对于不熟悉正则化和逻辑回归内部工作原理的读者，我强烈鼓励这些读者通过观看加州大学伯克利分校的讲座，对正则化逻辑回归如何工作有一个很好的认识。这个讲座解释了内部工作逻辑回归以及正规化的需要。

对于已经熟悉这个主题的读者，让我们直接进入实现代码。

## 数据

这个实验的数据集是来自 UCI 机器学习库中的 [**HTRU2 数据集**](https://archive.ics.uci.edu/ml/datasets/HTRU2) 。本实验的目的是生成一个二元分类器，它可以根据 8 个连续特征预测一颗恒星是否是脉冲星:

1.  *综合轮廓的平均值。*
2.  *综合轮廓的标准偏差。*
3.  *积分轮廓的过度峰度。*
4.  *综合剖面的偏斜度。*
5.  *DM-SNR 曲线的平均值。*
6.  *DM-SNR 曲线的标准偏差。*
7.  *DM-SNR 曲线的过度峰度。*
8.  *DM-SNR 曲线的偏斜度。*

二进制类显示了负类和正类之间的巨大不平衡，具有**16259**个负样本和**1639**个正样本，这在大多数分类项目中非常常见。考虑到与该数据集的不平衡，任何模型都必须超过基本精度分数**91%**(***16259/17898***)才能被认为是一个像样的模型。这是一个经典的例子，说明了为什么准确性作为一种衡量标准对于存在巨大阶级不平衡的问题毫无意义。

## 建模工作流

我真的回到了董事会，为一个正则化的逻辑回归构建各种组件。这个练习非常有助于确定以矢量化为重点的优化实施方案。

![](img/57c4d5fa71bf99509d1837527ac3409c.png)

梯度下降正则化逻辑回归的矢量化实现

在理论实现的涂鸦之后，是通过 Julia 翻译成代码的时候了。

这个实验的攻击计划就像一个典型的建模工作流，其中数据将是:

*   **为算法进行预处理:**为了简洁以及关注实现的需要，训练和测试示例(以及标签)被分开保存，以便我们可以专注于建模。对于感兴趣的读者，代码将在 Jupyter 笔记本的结论链接中提供。通过下面的代码片段，将数据加载到内存非常简单:

加载了各种分区之后，让我们将注意力转向实现阶段。

*   **模型拟合&评估**:鉴于所有特征都是连续变量，预处理阶段也将相当简单。因此，训练和验证分区都将通过标准化进行规范化，如下所示:

随着特征现在被归一化，让我们为我们的正则化逻辑回归定义"*假设"*和"*成本函数"*:

这里的目标是找到权重(θ),该权重使上面使用方向梯度定义的正则化成本函数最小化。这个目标是通过这个函数实现的:

如果梯度下降在这个最小化目标上是成功的，那么成本应该在随后的迭代中开始下降。让我们看看这个实验是不是这样:

![](img/7e01354cd39c224d3f076a700c171662.png)

每次迭代的成本

该图显示了随着迭代次数的增加，成本值的减少，这是实现正在工作的积极迹象！

图片来源:[https://giphy.com/](https://giphy.com/)

让我们做一些预测，并测试生成的正则化模型的准确性。

> **注意:**对于分类项目，在面临类别不平衡的情况下，准确性可能不是模型评估的稳健指标。准确性作为一个度量标准就足够了，因为重点更多的是在实现上。

```
**Training score**: 0.9769
**Testing score**: 0.9788
```

训练和验证准确度分数几乎相同，这有助于减轻对过度拟合/欠拟合的任何担忧。为了更好地理解这个实现的成功或失败，我们将把这些结果与 Python 中令人惊叹的 scikit-learn 的结果进行比较。

*   **与 scikit-learn 实施方案的比较**:使用 scikit-learn 的带梯度下降的正则化逻辑回归构建等效管道相当简单，如下所示:

```
**Train score for SGDClassifier**:  0.9791 
**Test score for SGDClassifier**:  0.9807
```

有趣的是，结果非常接近，但毫不奇怪，sklearn 的实现在准确性分数方面超过了它。这是一个更加优化的实现，非常聪明的调整！在这篇文章中，我们在 Julia 中使用梯度下降从零开始成功地实现了正则化逻辑回归。

## 最后的想法

唷！对于少数几个被选中的人来说，我希望你们喜欢这次旅程。我和 Julia 的旅程仍处于起步阶段，这个实验比之前的线性回归实验耗时更长，难度更大。我开始明白茱莉亚是多么喜欢处理矩阵、标量和向量运算( ***那些)符号*** )。我计划在以后的文章中用这种有趣的编程语言做更多的实验来解包经典和当代的算法。它可能是最终解决了埃隆·马斯克今天所阐述的“*双语*”问题的语言！

一如既往的期待反馈(好的坏的！).这篇文章的 Jupyter 笔记本可以在这个博客的 GitHub 知识库中找到。最后，你可以在我的个人博客上查看其他帖子。直到下一个帖子，祝你在茱莉亚编码愉快！