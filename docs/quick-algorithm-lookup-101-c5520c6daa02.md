# 快速算法查找 101

> 原文：<https://towardsdatascience.com/quick-algorithm-lookup-101-c5520c6daa02?source=collection_archive---------48----------------------->

## 看看其他一些常见的数据科学算法。

如果你想到数据科学，你的思维往往会转向神经网络，但实际上，数据科学家会想到大量其他算法，它们有自己的优势或劣势。

当然，这些提供了一些更常用的版本，在许多情况下，还有更复杂的版本来解决问题或增加功能。然而，为了保持这篇文章简短，我只包括了更基本的版本。

我不会涵盖神经网络，因为有数百篇关于它们的文章，但是如果你想要一个快速介绍，我可以推荐我的快速介绍文章。

![](img/407309785af6688aa40e3b4afe43372a.png)

由[格伦·卡斯滕斯-彼得斯](https://unsplash.com/@glenncarstenspeters?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

在我们开始之前，我最好先看一下我将在括号中使用的几个术语的标题，以及我使用它们时的含义:

*   监督学习—数据被标记
*   无监督学习-数据未标记
*   白盒方法——可以询问算法以帮助解释其决策过程的结果
*   黑盒方法——该算法采用输入变量并提供输出(或决策),但不容易解释它是如何做到这一点的
*   回归方法——使用输入提供一个[连续的](https://www.dictionary.com/browse/continuous)输出(例如 0.0 到 2.5)
*   分类方法——使用输入提供一个[离散](https://www.dictionary.com/browse/discrete?s=t)输出(例如“红色”、“黄色”、“蓝色”)

**注意**当谈论带标签的数据时，这意味着我们知道结果(即，一张照片是“狗”或“猫”)，并且是我们试图让机器学习算法复制的结果。对于无监督的，相当于它在数据中寻找分组和区别，但它不知道答案(即，它将所有图片分组为不同的动物类型，但它不知道一个组是“猫”，另一个是“蛇”)。

![](img/c3076245dd1b0e96d8a1295c0c32fe32.png)

照片由 [Isaac Smith](https://unsplash.com/@isaacmsmith?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 1.线性回归

(监督学习、白盒方法、回归方法)

用于估计基于连续变量的真实值。它通过拟合数据点的最佳拟合线来建立自变量和因变量之间的关系。这条“最佳拟合”线被称为回归线，并表示为(对于一个自变量而言):

![](img/cbaf389a3bff0ba52854c05b83d29f0e.png)

其中:

*   y-因变量
*   x —独立变量
*   a-回归线斜率的系数
*   b —回归线截距的系数

如果要使用多个独立变量，那么就要使用多元线性回归。也可以拟合多项式和曲线。

为了拟合回归线，可以使用不同的策略，但最常见的是:

*   最小平方-这是误差平方和最小的地方
*   最大似然-这是一种概率方法，对于给定的系数(相对于其他选择)，看到观察结果的可能性最大

**作者注:**如果工具有限，在 Excel 中单一和多重线性回归都是可能的

# 2.逻辑回归

(监督学习、白盒方法、分类方法)

线性回归的分类版本。这采用离散变量(如“是”或“否”)，而不是连续变量(如 0.0 到 1.0)。它通过将逻辑函数(也称为 Logit 函数)拟合到独立变量来对其是否属于某一类进行概率评估。因此，输出将在 0.0 和 1.0 之间，这可以解释为概率。

为了快速说明其工作原理，我们将使用两个分类问题(“事件发生”和“事件未发生”)和一个独立变量 x，则 Logit 函数σ看起来像:

![](img/c397741f99f827ae1ce5e484761e6966.png)

其中:

*   Logit 函数
*   y —任何实际输入

如果我们假设 y 来自独立变量的线性组合，那么在这种情况下，它看起来像:

![](img/cbaf389a3bff0ba52854c05b83d29f0e.png)

因此，Logit 函数将变为:

![](img/68070fa9c73c53d343f54f0716133fea.png)

F(x)可以解释为这种情况下事件发生的概率。通常，然后利用临界值来确定事件被归类为“已经发生”的概率水平，一种方法是使用 ROC 曲线和混淆矩阵进行优化。

此示例是二元逻辑回归的一个示例，其中只有两个分类可用，但是，还有许多其他形式可以执行更多分类(多项式逻辑回归)，并且也能够接受更多输入变量。也存在关心分类是否有序的形式。

**作者注:**可以在 Excel 中执行二元逻辑回归(有一个或多个自变量)。然而，预计这将是一项艰巨的调试工作！

![](img/1237c8cafb2c72fa6d596c06a6a43e59.png)

一个决策树的例子，如果它的分裂规则被画出

# 3.决策图表

(监督学习、白盒方法、分类方法、回归方法)

该算法的工作方式是选择最能拆分数据的输入变量(与其他输入变量相比，错误选择最少)，然后根据规则(例如“如果时间大于 5 小时”)拆分数据。然后，它依次获取每组拆分的数据，然后找到下一个变量(或再次使用同一个变量)来再次拆分数据。它会一直这样做，直到形成一个决策“树”,从而产生具有相同标签的同类数据集的输出。数据科学家能够制作和研究决策流程图。这使得它不仅有助于解释结果，而且有助于嵌入到不能容纳机器学习算法的设备中。

总的来说，该算法根据最重要的输入变量不断地将数据分割成 2 个或更多的同类数据集，以尽可能多地形成不同的组。这种分割可以通过各种方法来完成，例如:

*   基尼
*   信息增益
*   卡方检验
*   熵
*   更多

但是，你会问，使用这些方法之一，如何决定拆分是好的呢？通常，分割是通过度量的变化来衡量的。通常这可能是由于杂质，其中合并的分离样品的纯度比未分离的数据小得多，并且选择降低纯度最多的分离。如果你有兴趣的话，我这里有一篇关于它的更深入的文章。

该算法能够执行回归和分类分析。

**作者注:**由于其灵活性和研究决策如何达成的能力，这种算法(以及决策森林)往往是数据科学家最常用的算法之一。它经常给出令人惊讶的好结果，可以作为以后算法的基准。

![](img/700a7c3c78bc6c699f51507bee0c0c71.png)

照片由[塞巴斯蒂安·恩劳](https://unsplash.com/@sebastian_unrau?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 4.随机森林

(监督学习、黑盒方法、分类方法、回归方法)

在决策树之后，值得一提的是随机森林。最简单地说，随机森林就是决策树的集合，其中每棵树根据给定的数据做出自己的决定，然后进行集体投票。获胜的决策将作为输出给出。就像决策树一样，它能够进行回归和分类。

“种植”和“培育”一片森林的基本方法是“装树袋”:

1.  如果训练案例的数量为 N，则通过替换抽样获得大小为 N 的样本。每次为种植的每棵树构建该样本。
2.  如果有 M 个输入变量，那么这些变量中的一个随机子集(m <
3.  This set of m input variables and the samples data points are used to grow each tree to its fullest extent without pruning (this is where weak decisions are removed or decisions that result in a low number of resulting samples in one group are deleted from the trees decision flowchart).

The results of this method is that not every tree will see the same input data and input variables which results in a reduction in the chances of over-fitting, but also improved model performance. The disadvantages is that many trees (100s to 1000s or more) are often required and takes a large computation time as a result. One advantage is that the optimal number of trees can be found by looking at the “out-of-bag-error”. This is where for each tree is it is given the input data that was not part of the original random sample that was used to create it. The result performance of each tree is then aggregated and by looking at the error against the number of trees “planted” there will often be a plateau where no further model improvement is gained by adding more trees.

**作者注:**在过去几年中，已经开展了一些工作来提高随机森林的可解释性。其中包括功能重要性和决策路径(查看每个功能的平均响应)。

# 5.支持向量机(SVM)

(监督学习、黑盒方法、分类方法、回归方法)

这种算法传统上用于分类问题，但也能够回归(在这些领域中使用越来越多)。该算法的目的是插入一个平坦的边界，将类分成各自的组。在最基本的层次上，如果在一个图形上，一个类的点在左下方，而另一个类的点在右上方，该算法将插入一条从左上到右下方的线。这条线是“决策边界”,新点的分类是根据这些点落在线的哪一侧进行的。对于不容易分离的数据，SVM 会增加数据的维数(每个要素都绘制为一个坐标),直到它可以插入一个平坦的超平面边界来分隔各个类。

通常会插入边界，以便最大化每类离线最近的点之间的距离(等距),并且所涉及的数学往往会给给出可解释的结果带来很大困难。将数据(这是核函数本质上所做的)映射到更高维度使用了“核技巧”，这是一种可以拟合边界的方法，而不必经历将所有数据转换成高阶维度中的坐标的全部昂贵的计算成本。此外，因为只有靠近决策边界的数据点(这些点被称为支持向量)被用于决定在哪里放置边界，所以不需要其他点。这可以使 SVM 在能够紧凑地存储和训练模型方面具有优势。

SVM 可以是一个非常强大的工具，已经在几个不同的领域使用。比如:

*   文本分类——在识别语言的同时，也根据主题对内容进行分类
*   基因研究——基因表达的分类
*   事件检测—检测罕见事件，如安全漏洞、引擎故障等。

**作者注意到:**可以执行无监督学习的 SVM 版本是可用的，并被称为“支持向量聚类”

**作者注 2:** 迄今为止，机器学习的一些最强大的成果来自 SVM 和神经网络(有时在类似的挑战中竞争)

![](img/9ef24dd1adca4051efa59bb4996dee59.png)

照片由 [Riho Kroll](https://unsplash.com/@rihok?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 6.朴素贝叶斯

(监督学习、白盒方法、分类方法)

该模型使用输入变量之间的独立性假设，并利用贝叶斯定理产生一种数据分类方法。

贝叶斯定理的基本方程是:

![](img/568d35f815a7b2e18fd7f087b8a11ef5.png)

其中:

*   P(A) —独立于事件 B 观察到事件 A 的概率
*   P(B) —独立于事件 A 观察到事件 B 的概率
*   P(A|B) —观察到事件 A 的概率给定事件 B 已经发生
*   P(B|A) —假设事件 A 已经发生，观察到事件 B 的概率

注意:P(B) > 0 和 A & B 是事件

它具有强大的优势，因为它是可解释的，易于构建，快速训练，并且可以非常快速地做出决策。这对于非常大的数据集和某些行业(如试图量化风险的行业)非常有用。众所周知，它甚至优于复杂得多的模型和方法。

**作者注:**因为该算法假设输入变量是独立的，如果它们不是独立的，那么这会强烈影响最终的模型。

![](img/c363e5611742ba9bd8fc919d1911d89c.png)

照片由[捕捉人心。](https://unsplash.com/@dead____artist?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 7.k-最近邻(KNN)

(监督学习、黑盒方法、分类方法、回归方法)

这被广泛用于执行分类，但是回归问题也是可能的。

使用的方法是分组的方法之一。通过在特征空间中绘制点，并且添加新的数据点，在空间上为其找到最近的 K 个邻居。这种分类在最近的邻居中是最常见的。

距离度量不必是纯欧几里得的(也使用了 Manhattan 和 Minkowski)，但是为 K 选择正确的值可能是该模型的挑战之一。幸运的是，模型训练非常快，但是因为它们存储所有的数据，所以它们可能很大，并且为了获得结果，计算上可能非常昂贵，因为每次都必须找到 K 个最近的邻居。

**作者指出:**在使用该模型时，所有输入变量都要标准化，这一点很重要，否则该模型会受到某些变量的更大影响，而其他变量只受其值域的影响。

# 8.k 均值聚类

(无监督学习、盒子方法、分类方法)

这是一个无监督机器学习算法的例子。基本方法是:

1.  所有数据点都绘制在特征空间中(类似于 KNN)
2.  在特征空间内植入 k 个点(随机或由数据科学家选择)
3.  然后，数据点围绕这些点形成聚类。他们成为最接近他们的点的成员
4.  对于每个聚类，计算中心点
5.  基于它们与这些聚类中心点的距离来重新确定数据点成员资格
6.  步骤 4 和 5 被重新计算，直到中心点的移动低于设定的阈值。即收敛已经发生

从表面上看，这似乎与 KNN 相似，但它以不同的方式运作。它确实存在确定要放置的初始 K 点的数量的问题，但是可以对这些进行估计。

帮助优化 K 值的方法是对每个聚类将每个聚类数据点到聚类质心的平方差相加。当这些值相加后，我们就有了每个模型的集群解决方案。通过改变 K 的值并重新计算集群解决方案，我们可以看到该值应该随着 K 值的增加而减小，但是将会有一个点，在该点处增加 K 的增益减小。这为 k 的最佳值提供了指导。

**作者注:**混合良好的数据可能很难分开。考虑两个相连的螺旋，一个标准的 K-均值将不能分开这两个。然而，有不同的方法可以解决这个问题。

![](img/4d4f970a413adea80899d52eda9d0dcf.png)

照片由[格雷格·希尔](https://unsplash.com/@achiever_studios?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 结束了…或者是？

我希望这个列表已经提供了关于一些常见的数据科学算法是如何工作的(至少在高层次上)以及它们的优缺点的信息。

当然，该领域一直在不断学习和发展，这不可能是一个详尽的列表，但了解这些将有助于你了解他人。

# 参考源材料:

1.  [机器学习算法基础](https://www.analyticsvidhya.com/blog/2017/09/common-machine-learning-algorithms/)
2.  [线性回归](https://en.wikipedia.org/wiki/Linear_regression)
3.  [逻辑回归](https://en.wikipedia.org/wiki/Logistic_regression)
4.  [决策树](https://en.wikipedia.org/wiki/Decision_tree)
5.  [随机森林](https://en.wikipedia.org/wiki/Random_forest)
6.  [支持向量机](https://en.wikipedia.org/wiki/Support_vector_machine)
7.  [黑盒方法—神经网络和支持向量机](http://www.johnverostek.com/wp-content/uploads/2014/06/Chapter-7.pdf)
8.  天真的贝叶斯
9.  [KNN](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)
10.  [K-均值聚类](https://en.wikipedia.org/wiki/K-means_clustering)