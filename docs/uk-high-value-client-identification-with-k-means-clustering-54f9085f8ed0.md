# 英国高价值客户识别与 K-均值聚类。

> 原文：<https://towardsdatascience.com/uk-high-value-client-identification-with-k-means-clustering-54f9085f8ed0?source=collection_archive---------38----------------------->

![](img/a73612f6e13fb995250a4ba9afd5b284.png)

[Cytonn 摄影](https://unsplash.com/@cytonn_photography?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍照

# 引言。

一家总部位于英国的在线零售店捕捉了一年期间(2016 年 11 月至 2017 年 12 月)不同产品的销售数据。该组织主要通过在线平台销售礼品。购物的顾客直接为自己消费。有些小企业批量购买，然后通过零售渠道销售给其他客户。

作为项目目标？我们努力为企业寻找大量购买其喜爱产品的重要客户。该组织希望在确定细分市场后向高价值客户推出忠诚度计划。我们将使用聚类方法将客户分成不同的组。

# 数据争论

在我的分析中，我转向了提供的数据集，我们将首先检查它，看是否需要任何争论和清理。

因为数据集中有太多的行，所以查看结构并查看是否有任何值丢失是有意义的。如果数据集中有丢失的值，最好看看哪些列受到了影响，这对我们的分析是否是个问题

我们过滤该表，以查看 NaN 值的主要位置及其对输出的影响。在 SQL 的帮助下，我们过滤数据，找出每个客户购买了多少东西，以及他们为公司创造的总收入。如果我们的主要目标是找到最大的消费群体，那么最好的办法就是比较他们的大宗订单，以确定高消费群体

在制作好表格并将所有 NaN 值分组后，我们将删除它们以避免分类列直方图中的偏差。通过这种方式，所有客户的代表性更加均匀，我们将不会出现异常值，这些异常值归因于缺少信息的客户。

之后，我们创建一个散点图，看看我们的客户购买的商品产生了多少收入。该图显示了占据图中 0 点附近空间的大部分销售，除了少数例外，这些销售似乎购买了大量的商品，但产生的收入很少，或者购买了少量的商品，但收入巨大。为了确保我们的分类以最公平的方式表示数据，我们将对最高收入和数量设置约束。

# 探索性分析

为了找到聚类，我们将使用 K-means 算法。

K-means 算法是一种迭代算法，它试图将数据集划分为 K 个预定义的不同非重叠子组(聚类)，其中每个数据点仅属于一个组。它试图使簇内数据点尽可能相似，同时保持簇尽可能不同(远)。它将数据点分配给一个聚类，使得数据点和聚类质心(属于该聚类的所有数据点的算术平均值)之间的平方距离之和最小。聚类中的差异越小，同一聚类中的数据点就越相似。

kmeans 算法的工作方式如下:

*   指定聚类数 k。
*   初始化质心，首先洗牌的数据集，然后随机选择 K 个数据点的质心没有替换。
*   继续迭代，直到质心没有变化。也就是说，数据点到聚类的分配没有改变。
*   计算数据点和所有质心之间距离的平方和。
*   将每个数据点分配给最近的聚类(质心)。
*   通过取属于每个聚类的所有数据点的平均值来计算聚类的质心。

因此，为了找到最佳的聚类数 K，我们将使用“肘方法”。该方法包括将[解释的变化](https://en.wikipedia.org/wiki/Explained_variation)绘制为集群数量的函数，并选取曲线的[弯头作为要使用的集群数量。同样的方法也可以用来选择其他数据驱动模型中的参数个数，比如描述一个数据集的](https://en.wikipedia.org/wiki/Elbow_of_the_curve)[主成分](https://en.wikipedia.org/wiki/Principal_component)的个数。

接下来，我们从数据集的列中创建一个 numpy 数组，并根据找到的最佳 K 值绘制聚类图。完成后，我们根据我们选择的集群数量和我们计算的中心绘制数据框架。为了突出结果，我们使用明亮的颜色来清楚地看到每个聚类的边缘。

为了准确起见，我们还将制作一个树状图。*树状图*是显示对象之间层次关系的图表。它通常是作为[层次聚类](https://www.displayr.com/what-is-hierarchical-clustering/) *的输出而创建的。*树状图的主要用途是找出将对象分配到集群的最佳方式。关于我们如何以及为什么使用树状图的更深入的描述，包括它们背后的数学，请随意使用超链接获取更多信息。

# **结果**

一旦找到聚类，我们使用指定的数字与每个客户相关联，显示哪些属于收入最高的客户。在筛选出特定集群编号的记录后，我们可以创建一个需要关注的顶级客户列表。使用它来查看未来几年是否会有新客户占据相关集群也很有用，现有客户的动态可能有助于调整未来几年的优秀客户名单。

# 结论

感谢您花时间阅读上面的分析，我希望它是有趣的，并为集群和探索性分析提供了一些见解。该项目的所有代码都可以在我的 [GitHub](https://github.com/NiqDS/UK-High-Value-Clients-Identifiction) 上找到，请检查一下，如果你有任何意见或建议，请随时发表评论。毕竟，我们无法学习我们认为已经知道的东西。