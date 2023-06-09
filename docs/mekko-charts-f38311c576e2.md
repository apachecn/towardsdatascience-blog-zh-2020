# Mekko 图表

> 原文：<https://towardsdatascience.com/mekko-charts-f38311c576e2?source=collection_archive---------39----------------------->

## 为什么和如何

![](img/1948a417114adf8b5431adb8f0e9f5d7.png)

图片由来自 Unsplash 的 Khara Woods 提供

有不同类型的**可变宽度条形图**，但有两种是最流行的:1)条形图；2) Marimekko 图。

它们在以下方面有所不同:T2 条形图 (BMc)像一个“标准”条形图，但它的条形是可变宽度的，而 T4 条形图 (Mc)像一个 100%堆积条形图，但它的条形是可变宽度的。

**为什么**:它们用于显示数据集中每个类别的两个数值变量；目标是在类别之间进行**比较**，而不是在数字变量之间。它们广泛用于仪表板或营销和销售演示中，其中的类别通常是产品、区域、部门、细分市场等。数字变量通常是销售额、利润、成本、利润、增长率等。它们不适合用于分布、关系或长期趋势分析。

**如何**:是一个类似于标准条形图的二维图形，矩形条通常以垂直方向排列。纵轴有一个数字刻度(在 Marimekko 图上为 100%)，代表一个定量变量。横轴可以是数字，也可以是类别。如果是数字，每个矩形的宽度与第二个定量变量的值成比例，有不同的颜色和标识它的图例。如果是分类的，每个条形的宽度也表示第二个定量变量的值。

每个类别的矩形宽度通常不同。用数字或百分数表示横轴上的数值变量总是很方便的。这些值通常显示在上基线上。

与标准条形图不同，**条形之间没有空间**(注意不要将 Mekko 图与直方图混淆[https://towards data science . com/Histograms-why-how-431 a5 cfbfcd 5])。在 BMc 和 Mc 中，**水平轴的整个宽度被占据**。

**Mekko 条形图**是传统条形图的替代产品，可让您减少商业演示中图表的数量。为了实现这一点，图表通过条形的高度对一个数字变量进行编码，通过条形的宽度对另一个数量变量进行编码。下图显示了 Mekko 条形图的示意图:数字垂直轴；带有可变宽度条形的水平轴，每个条形代表一个不同的类别。产品线、部门或区域是横轴上显示的类别示例。销售额、成本或利润可以是用矩形宽度表示的数字变量。

![](img/28340fb8bc9dd38dec36690a372fad3e.png)

图 1:条形图的示意图。用 Vizzlo 创建，有权限(#1)。

Marimekko 图表是分组条形图的一种替代方法，可以减少商业演示中的数量:它们显示与主要类别中的子组或子类别相关的数字信息。因此，这种类型的可视化允许我们为每个类别和每个子类别显示两个数值。

它们通过将整个矩形区域分成更小的矩形来占据它。每个类别又分为由堆叠矩形表示的子类别。这些矩形中的每一个都对数据集的每个子类别的数值进行编码。它们在视觉上相当于堆叠条形图，除了具有不同高度的矩形段之外，我们现在还具有可变的条形宽度。

图表的垂直轴显示百分比刻度，而水平轴被标准化为占据图表的整个宽度，在条形之间不留任何空白。

![](img/5bdf85bd97e285ce631d433add0dda7b.png)

图 2:marime kko 图。用 Vizzlo 创建，有权限(#1)。

图 2 在一张图中描述了一家公司的年收入，分为不同的品牌，以及对应于不同地区的百分比。可以看到 Marimekko 图的特征要素:一个矩形区域被分成宽度不同的较小矩形；垂直堆叠的矩形；占据图表整个宽度的水平轴；带有百分比刻度的垂直轴；最高基线上每个品牌的总收入；不同的条形宽度允许计算每个品牌对总收入的相对贡献。

单词来源:Marimekko 是一个芬兰纺织品牌，拥有大量多样的形状图案，以及简单明亮的颜色和风格(#2)。

**警告:**

条形图和 Marimekko 图都**难以阅读和解释**，因为它们基于受众通过比较区域来解码数字信息的能力。重要的是要记住，人类擅长评估距离，而不擅长计算面积。此外，随着矩形数量的增加，我们对不同区域进行适当比较的能力下降。

Marimekko 图和堆积条形图有同样的缺点:a)子类别的数量有一个实际的限制，超过这个限制可视化就变得困难了；b)最好的比较是在较低和较高基线附近的子类别之间进行。随着我们远离它们，子类别之间的差异变得很难评估。

小心重复使用 Mekko 图:记住矩形棒线非常“沉重”,是主要的视觉标记。

请注意，观众通常非常熟悉传统的条形图，但不熟悉可变宽度的条形图。如果您的演示中有 Mcs 或 BMC，请花些时间向观众解释它们的具体特点，以免影响故事的讲述。

Marimekko 图表不能显示负值，也不能将绝对值和相对值结合起来。

一些可视化工具允许您在垂直和水平布局之间切换。然而，在通常的实践中，使用垂直布局，因为水平布局会不必要地使故事讲述复杂化。

**不要混淆 Mcs 和 spineplots** 。从最严格的定义来看， **spineplot** 是一个一维的水平堆叠条形图，用于显示列联表(#3)中两个交叉分类的分类变量的频率、比例或百分比。出现这种混乱是因为一些 spineplots 可视化工具允许垂直方向，他们称之为**马赛克图**。该术语也被错误地归因于 Marimekko 图表，但应该保留给那些允许通过可变宽度矩形检查两个或更多分类变量之间关系的图表。

我没有在 Python 中找到允许直接绘制 Mcs 或 BMC 的绘图函数。一个*堆栈溢出*用户编写了一个策略，使用 Matplotlib 使用条形图绘制条形 Mekko 图，每个条形的宽度使用*宽度*参数(#4)单独修改。我对他的代码做了一些小的修改，得到了下图，一个非常接近条形图的图。

![](img/4a79152f05574bcfdb12247bbb9a08f7.png)

另一方面， *statsmodels* 的 12.0 版本允许从列联表(*stats models . graphics . mosaic plot . mosaic*)创建镶嵌图形。下图和绘制该图的代码可在 *statsmodels* 组织的以下页面中找到:

> https://www . stats models . org/stable/generated/stats models . graphics . mosaic plot . mosaic . html

如下图所示，镶嵌图在水平轴和垂直轴上都显示了分类变量(#5):

![](img/feda590a06a976956c42d56018daea1f.png)

总结:与 Mekko 图表相关的最重要的概念在于它们能够恰当地**加权** **一个数值变量**的大小。传统条形图的所有变体(标准、分组、堆叠、重叠等。)对所有类别使用相同的条形宽度，因此只能通过单个数值变量的长度或高度进行比较。Mekko 图表中的变量宽度允许我们在一个图表中显示第二个数值变量的相对值。相比之下，它们的视觉效果**较低**:到达受众的编码信息的准确性和清晰度相对较低。

如果你对这篇文章感兴趣，请阅读我以前的:

**"直方图，为什么&如何，讲故事，提示&扩展"**

[](/histograms-why-how-431a5cfbfcd5) [## 直方图，为什么和如何

### 讲故事、技巧和扩展

towardsdatascience.com](/histograms-why-how-431a5cfbfcd5) 

**“关于条形图你需要知道的一切”**

[](https://medium.com/nightingale/bar-graphs-why-how-8c031c224c9f) [## 条形图，为什么和如何

### 对于这种无处不在的图表类型，需要避免的基础知识、技巧和陷阱

medium.com](https://medium.com/nightingale/bar-graphs-why-how-8c031c224c9f) 

**参考文献**

第一名:[https://vizzlo.com/](https://vizzlo.com/)

# 2:[https://en.wikipedia.org/wiki/Marimekko](https://en.wikipedia.org/wiki/Marimekko)

#3:福克斯，n .，“说 Stata: Spineplots 和他们的亲属”，Stata 杂志(2008)，8，1 号，第 105-121 页

# 4:https://stack overflow . com/questions/57164333/matplotlib-bar-me kko-chart 中不同宽度和颜色的条形图

# 5:[https://www . stats models . org/stable/generated/stats models . graphics . mosaic plot . mosaic . html](https://www.statsmodels.org/stable/generated/statsmodels.graphics.mosaicplot.mosaic.html)