# 统计上无关紧要的烟雾

> 原文：<https://towardsdatascience.com/statistically-insignificant-smoke-f86ede4a8289?source=collection_archive---------29----------------------->

夸大统计签名卡

![](img/631bb9f71549d18a43cebe7ec3eabe86.png)

资料来源:https://unsplash.com

假设你正在开会，看着某人展示一个图表。该图显示了一个重要的小客户群的关键绩效指标的趋势。我们都经历过。

演讲者指着图表中的一个尖峰，告诉人们忽略它，因为它的“样本量”很小，缺乏“统计意义”。人们点头，演示继续进行。

坚持住。结论可能是对的，但推理是错的。

首先，图表不是基于一个*样本*。该图基于*整个*段。只是刚好是一小段。

这意味着采样没有方差或偏差，这反过来意味着尖峰确实发生了。然而，油价飙升是否重要，是否值得采取后续行动，则是另一回事了。

这是怎么回事？小*人口*规模正与小*样本*规模*混为一谈。但是这种区别实际上关系到我们如何解释数据。*

让我们通过浏览这两个场景来深入了解一下。

**关于小群体:**

假设我们有两个小村庄——村庄 A 和村庄 B——每个村庄有 5 个居民。我们想比较这些村庄的平均收入水平。这些村庄所有 10 个人都有干净的收入数据。

我们的计算显示，A 村的平均年收入为 50k 美元，b 村为 60k 美元。这种差异是 100%真实的，因为我们查看了这两个村的所有数据。还有，感觉是实质性的区别；B 村的人平均多赚 20%的钱。

现在，事实证明 B 村的平均收入更高，因为有一个人每年挣 10 万美元。这个人决定搬到另一个村庄，现在 B 村的平均收入下降到 51k 美元。1000 美元的差异仍然是 100%真实的，因为我们仍然在看所有公民的数据，但这感觉不再是实质性的。只需要一个人动一动！

这个故事的寓意是什么？在处理小群体(例如，小部分客户)时，我们在解释指标峰值时一定要小心，因为单个异常值或几个新数据点的添加都会改变事情。波动性更大。但这与统计显著性或抽样无关。

**关于小样本量:**

这就是统计学意义发挥作用的地方。

想象两个大城市，每个都有数百万居民。我们想知道这些城市的平均家庭收入水平是否不同，但是我们没有这些城市的任何收入数据。

所以我们使用假设检验和抽样:

1.  创建一个无效假设和一个替代假设。无效假设是平均收入水平相同。另一个假设是平均值不同。
2.  从每个城市随机抽取样本。
3.  拒绝或接受零假设。通常，您会根据测试统计来计算*p*-值(除非您是反频率主义者)。我们可以不严格地**将*p*-值视为当其为真时拒绝零假设的机会(犯类型 1 错误)。在大多数情况下，当*p*-值小于 0.05 时，人们会舒服地拒绝零假设并声称有统计学意义。

我们的样本越小，我们就越有可能犯第二类错误——也就是说，当*和*确实存在差异时，我们无法拒绝零假设。

**那么有哪些外卖？**

→我们不应该如我的题目所暗示的那样忽视统计学意义。这是一个完全合法的框架，经常应用于许多不同类型的应用程序，从药物测试到市场营销。但它不适用于小群体的尖峰图。

→如果我们处理的是小规模*人群*，我们不能说指标中的所有峰值和谷值在统计上无关紧要，就自动放弃它们。这只是在吹统计烟雾时应用了错误的框架。

→为什么这很重要？这不仅仅是关于使用正确的统计学术语(尽管那样会很好)。真正的问题是:如果我们总是对每一个小群体异常做出相同的(错误的)全面诊断，我们将不可避免地错过一些重要的东西。在某些时候，所有大客户群都是小群体。

**从技术上讲，*p*-值是在假设零假设为真的情况下，获得至少与观察结果一样极端的结果的概率。当零假设为真时，它实际上不是拒绝零假设的概率，因为*p*-值是基于频率主义推理(与贝叶斯推理相反)，因此不提供关于假设的任何概率度量。见[此处](https://multithreaded.stitchfix.com/blog/2015/05/26/significant-sample/)。