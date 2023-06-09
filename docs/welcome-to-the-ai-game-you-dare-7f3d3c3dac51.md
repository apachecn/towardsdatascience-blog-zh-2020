# 欢迎来到人工智能游戏。你敢吗？

> 原文：<https://towardsdatascience.com/welcome-to-the-ai-game-you-dare-7f3d3c3dac51?source=collection_archive---------87----------------------->

## 在探索机器学习及其算法背后的主要概念时获得乐趣。

“只是玩玩。玩得开心。享受比赛”——迈克尔·乔丹

我们将从头开始。在机器学习中，我们将使用矩阵、数组和向量符号来指代数据。

游戏规则是这样的:

*   一行、一次观察或特定数据。
*   前一次观察的一列、一个特征(或属性)。
*   在最一般的情况下，会有我们会称之为“目标”，标签或回应，这将是我们要预测或实现的价值。

*仅此而已。我让你轻松了，对吧？*

![](img/59b3c7ad9c7d5a3da2a73f516d6261b1.png)

照片由[埃里克·麦克莱恩](https://unsplash.com/@introspectivedsgn)在 [Unsplash](https://unsplash.com) 上拍摄

*如果你想了解更多，请访问*[***oscargarciaramos.com***](https://oscargarciaramos.com)

现在，**三种不同的机器学习技术**:

## 监督学习，

“我们的第一场比赛”。这些算法采用一组已知的输入数据集及其对数据的已知响应(输出)来学习。我们知道什么“进”，什么“出”。一旦算法学习并得到适当的训练，我们就可以进行“泛化”，即模型有能力适当地适应新的、以前从未见过的数据。我们将区分两种类型的监督学习算法:回归和分类。

*—标记数据、直接反馈、预测结果/未来*

## 无监督学习

“走出下一步”。这一次，数据将被取消标记，结构将是未知的。我们的任务？找到数据的内在结构或模式。我们会发现两种类型的算法:聚类和降维。

— *没有标签，没有反馈，在数据中找到隐藏的结构*

## 强化学习

“从经验中学习”。我们最后一个。尝试最大化算法因其行为而获得的回报。使用反馈反复试验。

*—决策过程、奖励系统、学习系列行动*

我们可以开始玩了吗？

# 线性回归

你家里有原木吗？根据体重有条理地摆放。但是，你不能称它们。你必须通过观察高度和它的直径来猜测(*视觉分析*)通过组合这些“可见”的参数来组织它们。 ***那是一元线性回归*** 。

我们该怎么办？我们通过将自变量和因变量拟合到一条直线上来建立它们之间的关系，这条直线就是我们的回归线，表示为 *Y = a * X + b*

*   y-因变量
*   a-斜率
*   X —独立变量
*   b —截距

我们如何计算系数 a 和 b？最小化数据点和回归线之间距离的平方差之和。

# 逻辑回归

我们将讨论 0 和 1，我们的离散值，我们必须从一组独立变量中估计它们。

该模型将尝试用一条线来拟合这些点，**它不可能是一条直线**，而是一条 S 形曲线。它也被称为 *logit 回归*。

如果我们想改进我们的逻辑回归模型呢？包括交互项、消除特征、调整技术或使用非线性模型。

# 决策图表

当今数据科学家最喜欢的算法之一。

这是一种用于分类问题的监督学习算法。我们将从对某个项目的观察(在分支中表示)到关于该项目的目标值的结论(在树叶中表示)。它对分类变量和连续因变量的分类都很有效。

它是如何工作的？我们根据最重要的属性/独立变量将总体分成两个或更多的同类集合，然后…我们往下走！

# SVM(支持向量机)

SVM 是一种分类方法，在这种方法中，算法将原始数据绘制为 n 维空间中的点，其中 n 是您拥有的要素数量。然后，每个要素都被绑定到一个特定的坐标，这使得对数据进行分类变得很容易。

*算法的特别之处在哪里？我们将以苹果和橘子为例。它不是在群体中寻找那些最能被描述为苹果和橘子的，而是寻找苹果更像橘子的情况，这是最极端的情况。这将是我们的支持向量！一旦确定，我们将使用称为“分类器”的线来分割数据，并将它们绘制在图表上。*

# 朴素贝叶斯

朴素贝叶斯分类器。它是一种基于贝叶斯定理的分类技术，假设预测器之间是独立的。朴素贝叶斯之所以“朴素”，是因为它假设测量的特征是相互独立的。

**一种快速简单的方法来预测类**，用于二进制和多类分类问题。

# KNN(K-最近邻)

想象一下，你要去拜访一个比你的朋友或家人更好的人，对吗？

这是一样的。我想和我的朋友在一起。

我们可以将这种算法应用于分类问题和回归问题。它是如何工作的？简单，我们将所有可用的案例进行排列，并根据其 K 个邻居的多数投票对新案例进行分类。案例将被分配到具有最大共同点的类别或分类中。测量是如何进行的？用一个距离函数，一般是欧几里德距离。

*注意:KNN 计算量很大，变量应该归一化。*

# k 均值

这是一种解决聚类问题的无监督算法。橘子配橘子，苹果配苹果。数据集被分类成特定数量的簇，我们的 *k* 数，因此一个簇中的所有数据点都是同质的，同时与其他簇中的数据是异质的。很简单:

*   1.选择 k 个簇的数量。
*   2.选择一个随机的 k 点，质心。
*   3.将每个数据点分配到最近的质心(欧几里得)。
*   4.计算并放置每个簇的新质心。
*   5.将每个数据点重新分配给新的最近质心。

再次执行第 4 步…第 5 步，一遍又一遍…

# 随机森林

随机森林背后的基本思想是将许多决策树组合成一个模型。

*为什么？*作为一个委员会运作的大量相对不相关的模型(树)将胜过任何单个组成模型。

这个模型确保了 **bagging** *(允许每棵树随机地从数据集中进行替换采样，从而产生不同的树)*和**特征随机性** *(其中每棵树只能从随机的特征子集中选取，从而产生更多的变化)*。

# 降维算法

虽然看起来不合逻辑，但是“多多益善”并不总是对的。由于这种类型的算法，我们通过获得一组主要变量来减少所考虑的随机变量的数量。 ***PCA*** (主成分分析) ***缺失值比率*** 或 ***因子分析*** 就是一些例子。

# 梯度增强和 AdaBoost

我们的赢家！ *其主要目标是什么？*进行高精度的预测。

我们将组合多个“弱或平均”预测器来构建一个强预测器。它结合了几种基本估计量的预测能力，以提高模型的稳健性。

这是最优秀的算法，也是当今最受欢迎的算法。

## 那么，下一步是什么？

现在开始，开始玩吧！这就是我要说的全部…

*欢迎留言、鼓掌或分享这篇文章。以后的帖子关注* [*me*](https://medium.com/@ogarciaramos) *。*

如果你想了解更多，你可以在 oscargarciaramos.com[](https://oscargarciaramos.com)*找到我*