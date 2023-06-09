# 选择合适视觉效果的终极指南

> 原文：<https://towardsdatascience.com/ultimate-guide-to-choosing-the-right-visual-2a77aa8eec08?source=collection_archive---------46----------------------->

## 从“用数据讲故事:商业专家数据可视化指南”中吸取的经验教训

![](img/b97161918c08146ae8efb7797c633854.png)

威廉·艾文在 [Unsplash](https://unsplash.com/s/photos/data-science?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

说到有效的数据可视化，第一步也是最关键的一步是为您想要呈现的数据选择正确的图形/视图。由于有各种各样的可视化软件可以提供大量不同的图表，选择正确的软件通常是一项具有挑战性的任务，它以尽可能简单的方式解释数据和见解。我最近读了一本关于数据可视化的非常著名的书——《用数据讲故事:商业人士的数据可视化指南》，作者是 Cole Nussbaumer Knaflic。这本书是迄今为止我所见过的关于数据可视化的最佳资源，在本文中，我将解释书中的一个主题——选择有效的可视化。

大多数数据可以使用我将在本文中讨论的 12 种视觉效果中的任何一种来可视化。视觉效果可分为:

1.  简单文本
2.  表格(表格、热图)
3.  点(散点图)
4.  线(线形图、斜率图)
5.  条形图(水平、垂直、堆积、瀑布)
6.  面积

*注:*

1.  所有显示的图表都是使用 Google Sheets 制作的。 [*链接到文档*](https://docs.google.com/spreadsheets/d/1_tOqS4c861VNc0Oi1hsDVCtD1L1bO02Un_3KJsLGcCg/edit?usp=sharing) *。*
2.  *用于生成图表的数据完全是虚构的，并非取自任何来源*。

所以让我们开始探索列表中的每一个。

**简单文本**

你不必总是用图表来显示数字。如果只有一些数字和一些支持文本，直接显示数字可能是最好的方法。让我们看一个例子来更好地理解。

![](img/400fa7d87c50cde98e3097ae99129ea8.png)

作者图片

在上面的例子中，图表没有为解释提供太多的帮助，只是占据了很大的空间。所以，当你只有几个数字的时候，直接展示出来。

**表**

如果你想用多种计量单位进行交流，表格可能是最合适的选择。创建一个表格很容易，但是一定要确保设计淡出背景，数据是主要焦点。下面是一个将设计淡化到背景并专注于数据的例子:

![](img/6a28ed84a5f5aa9e986ac8ec3b8ede41.png)

作者图片

你能观察到每次迭代后的改进吗？这就是它如此重要的原因。

**热图**

热图只是一个表格的升级版本，我们在其中添加颜色来更好地解释数据或数字。在一个简单的表格中，读者必须浏览每一个元素，才能对其中的内容有所了解。通过添加颜色，我们让读者直接关注感兴趣的区域，从而更好地理解数据。

![](img/33eef6371a08762f14cc5a68050e5e4b.png)

作者图片

像 Excel 这样的绘图应用程序具有创建热图的条件格式选项。为了更好地理解，加入图例也是一种很好的做法。

**散点图**

散点图用于显示两个变量之间的关系，其中每个变量分别用 X 轴和 Y 轴编码。这在解释相关性时特别有用。

![](img/10f019e9e4f39a76b623285cb9f4b195.png)

作者图片

**线图**

折线图是绘制连续数据(如日期和时间)的最佳方式。由于所有的点都用一条线连接起来，所以很容易解释连续的数据，但同时，这对于绘制分类变量没有意义。折线图可用于显示单个系列或多个系列的数据，如图所示。

![](img/d3b8d7941a94a008119de5b54ed83d9d.png)

作者图片

**斜率图**

斜率图只是线形图的一个特例，非常适合比较两个不同点或时间段的指标变化。这对于直观地显示变化率(增加或减少率由线条的斜率表示)以及绝对值非常有用。

![](img/21b5f8d815a12c04024ee6cb102f29f4.png)

作者图片

接下来，我们将看看条形图的一些变化，这是分类变量的理想选择。条形图往往被避免，因为它们是常见的，但由于它们是常见的，与其他类型的视觉效果相比，读者很容易理解条形图。这使得条形图成为最重要的视觉形式之一。

**竖线**

这是一个普通的条形图，每一列代表一个类别。与折线图类似，条形图也可以包含多个系列。

![](img/54ed9a9887e3ebe72d397b82939a7042.png)

作者图片

**堆叠竖条**

堆积条形图可用于比较不同类别的子组件。它可以使用 100%堆积图来保存实际数字或百分比。

![](img/0f32be572f7f83592ff21787f31ef229.png)

作者图片

同样，你不能用太多的子组件来填充类别，因为这会变得难以理解和比较。

**瀑布**

瀑布图是垂直条形图的另一种特殊情况，它可以用于拉动堆积条形图的子组件，一次聚焦一个组件，或者显示起点、增加和减少以及最终的终点。

![](img/ad059639410f9ba62cf4982212dec900.png)

作者图片

**单杠**

水平栏通常是分类数据的首选项，因为它比垂直栏更容易阅读，并且还可以容纳大型类别名称。与垂直条形图类似，它也可以有单个或多个数据系列。

![](img/ee0d64840a0e13d2e03d596316a7665c.png)

作者图片

**堆叠的水平条**

这类似于堆叠垂直条形图，但由于水平条形图所讨论的原因，相对更好。

**面积图**

应尽可能避免面积图，因为人眼不太擅长比较二维空间中的值。但是，如果您非常想包含多个指标，那么面积图可能行得通。

至此，我已经介绍了可以用来可视化大部分可用数据的图表。因此，选择一个图表，可以清楚地解释你试图传达的信息。

我们已经讨论了最佳实践，现在是时候看看一些应该避免的实践了。

**要避免的视觉实践**

避免使用饼图，因为读者必须比较弧线的区域，这变得非常困难且不直观。使用一个标准的条形图会使它更容易解释。看看下面的例子可以更好的理解。

![](img/2dcef30845f11beab0d16389a7511abe.png)

作者图片

永远不要使用三维图表。3D 图表会产生不必要的干扰，使其难以解读。**所以千万不要用 3D** 。

**结论**

我希望这篇文章能让你很好地理解不同的视觉效果，以及在什么地方使用每种视觉效果。所以，一定要选择能充分传达你想要展示的信息的视觉效果。说到您可以使用的应用程序/软件，这完全取决于您。Excel，Tableau，Power BI，Google Sheets 是一些可用的应用程序，你可以使用任何你觉得舒服的东西。请记住，图形应用程序并不知道视觉对象的实际用途，而是由您根据需要定制它。我希望它有帮助。