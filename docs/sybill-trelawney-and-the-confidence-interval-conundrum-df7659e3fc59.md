# 塞比尔·特里劳妮和置信区间难题

> 原文：<https://towardsdatascience.com/sybill-trelawney-and-the-confidence-interval-conundrum-df7659e3fc59?source=collection_archive---------46----------------------->

今天我将尝试一些不同的东西，我将我喜欢谈论的两个(完全不相关的)话题结合起来，希望创造一些有趣且有教育意义的东西。

…实际上，算了吧。如果你曾经读过我在 Medium 上写的任何东西，这实际上是很棒的品牌([向迈克尔·斯科特](/explaining-linear-regression-to-michael-scott-973ed050493c)解释线性回归，有人吗？)在今天的文章中，我将解释什么是置信区间，如何计算置信区间，以及如何解释置信区间——所有这些都是通过哈利波特臭名昭著的占卜老师这个用例来实现的。

![](img/eabb49e5d9253d177a3cc9d755e6d109.png)

或者至少是对未来的一种统计上可能的猜测。GIF 由 [gyfcat](https://gfycat.com/academicglaringboilweevil) 提供

对于那些不熟悉哈利·波特和塞比尔·特里劳妮的人(我假设目前没有人在读这篇文章，因为这意味着你已经有 20 多年没有互联网了)，她是一个女巫，她可以通过 99%的有根据的猜测和 1%的真实预言“预见未来”。至少在我看来，置信区间是非常相似的:基于一小组观察对整个人口做出有根据的猜测。但是，我们的工具不是水晶球和茶叶，而是标准差和样本均值。

# 什么是置信区间，人们为什么使用它们？

特里劳妮教授在霍格沃茨任职期间有数千名学生，邓布利多正在审核她的工作，看看她*在预测未来方面到底有多准确。然而，邓布利多是一个忙碌的家伙(试图追捕魂器和管理一所学校)，无法接触到每一个上过特里劳妮课的学生。因此，他随机选择了 300 名以前的学生作为样本，并询问他们到目前为止，她的预测实现的比例是多少。*

![](img/26135b88836b560b6afc5af10825aafa.png)

特里劳妮预测精度的左偏分布。图片由作者提供。

邓布利多收集了回答，发现回答的分布是左偏的，这意味着学生们更有可能发现特里劳妮的预测不准确。事实上，样本平均值为 55.6%，这意味着特里劳妮的“预测”比随机猜测好不了多少。

这让邓布利多非常担心，因为他不想要一个在教授占卜课时本质上是猜测的老师。他想知道她的预测的真实平均准确性是多少，如果他联系了她教过的每一个学生，是否会低于样本平均值 55.6%。

幸运的是，邓布利多记得一个麻瓜概念叫做**中心极限定理(我能说什么呢，他是一个多面的家伙)**这让他有能力接近特里劳妮预测的真实平均准确度。中心极限定理假设，当你有一个数据样本，你想找到真正的人口统计(即，一个常见的例子是均值，所以我将在本文中使用它，但它也可以是其他措施)，你可以采取更小的样本组，并找到他们的均值(即，随机抽样 30 人一次，当你有 300 人的总样本和 30，000 人的总人口)。如果你有足够多的样本，并且这些样本满足一定的标准，那么样本均值将属于正态分布(不考虑数据的原始分布)，样本均值(我有时讨厌统计)的样本分布的**均值将接近真实的总体均值(如果你实际上调查了总体中的所有 30，000 人，这个均值)。**

![](img/fb77c578aaa9a684226f85f8d276b4cc.png)

中心极限定理的应用。在这幅图中，你有 4 个从总体中随机抽取的样本，它们都是非正态分布的。但是当你从每个样本(以及更多随机样本)中取平均值时，样本平均值的分布就形成了一条正态曲线。这条曲线的平均值是真实的总体平均值(如果我们对总体中的每一个人进行抽样，我们只能得到真实的总体平均值)。图片由[分析公司 Vidhya](https://www.analyticsvidhya.com/blog/2019/05/statistics-101-introduction-central-limit-theorem/) 提供

基于这个概念，邓布利多知道 55.6%的平均准确率是样本均值正态分布曲线上的*某处*，真正的准确率在这个同分布的中间。

![](img/78290c1f5e465506538a2aad6f28bac4.png)

老实说，他们应该让我上教科书信息图。奥雷利·HMU。图片由作者提供(因为还有谁会制作这个 LOL)。

然而，他仍然不知道样本均值在分布上的确切位置，以及它与实际总体均值的接近程度(表示为 **μ** )。这就是置信区间的由来。

置信区间创建以样本均值为中心的标准差区间。根据间隔的大小，您可以声明该间隔将包含 x%时间的真实总体平均值。许多研究人员和公司使用 95%的置信区间(每侧距离样本均值 2 个标准差)，但根据您的使用情况，您可以提高或降低置信度(即距离均值 3 个标准差为 99.7%的置信度)。

![](img/527ae962a145e5d8f79491e0712a6d29.png)

样本均值分布的 4 种不同均值的 95%置信区间示例。浅紫色代表包含在以每个样本平均值为中心的 95%置信区间内的值。深紫色线代表理论总体平均值的 2 个标准偏差。

基于上面的例子，您可以看到落在**总体均值**(深紫色线内)的 2 个标准偏差内的样本均值如何将总体均值(蓝色虚线)包含在其 95%置信区间内。但是，距离总体均值超过 2 个标准差的样本均值不会将总体均值包含在其置信区间内。

由于正态分布中 95%的值位于平均值的 2 个标准偏差内，我们可以确信 95%的样本平均值将位于总体平均值的 2 个标准偏差内。据此，我们也可以说**从该人群中抽取的所有随机样本的 95%将包括其 95%置信区间**中的真实总体均值。

# **如何计算置信区间**

现在我们对置信区间的用途和作用有了一个大致的了解，我们可以回到霍格沃茨，帮助邓布利多计算特里劳妮教授预测准确度的置信区间。

![](img/cdd29f4cef645f88923e169ef640c2f9.png)

置信区间计算公式。图片由[统计如何](https://www.statisticshowto.com/probability-and-statistics/confidence-interval/)提供

以上是计算置信区间的通用公式，其中 **x̅** 是样本均值，**t11】zt13】是我们希望区间跨越的均值的标准差个数，**t15【s】t16**是样本的标准差，**t19】nt21】是组中样本的个数。****

公式的后半部分(z * s / √n)计算出 ***z*** 标准差是什么的实际值( ***z*** = 2 为 95%置信区间)，你将这个值从**【x̅】**中加减，就可以求出你的置信区间的上下界。

如果邓布利多把评估值代入这个公式，他会得到:

**上限**

= 55.6 + (2 x (12.9/√300)

= 57.08%

**下界**

= 55.6 - (2 x (12.9/√300)

= 54.12%

这意味着特里劳妮教授预测的真实准确性很有可能在 **54.12% — 57.08%** 之间。然而，由于邓布利多只评估了一个样本，我们不能说这个样本平均值(55.6%)是否在总体平均值的 2 个标准差之内，以及它的置信区间是否成功地捕捉了真实的总体平均值。样本平均值有可能恰好在与平均值相差> 2 个标准差的 5%的数据中(也就是下面红色的坏 BOIS 之一)，因此完全错过了总体平均值。

![](img/6092485eaeb9d6313109e7a3cbe37767.png)

图片由[麻省理工](http://www.mit.edu/~6.s085/notes/lecture2.pdf)提供，由您真实标注。

# 特里劳妮教授的命运(又名邓布利多的下一步)

邓布利多对下一步有几个选择:

1.  他可以将调查问卷发送给另外几组，每组 300 名学生，然后开始绘制各组学生的平均值分布图。这将使他更好地了解 55.6%落在哪里(即，接近其他值，可能在总体平均值的 2 个标准偏差内，或明显远离其他值，可能大于 2 个标准偏差)。
2.  他可以重新进行同样的分析，这次从他的 300 个回答中取出更小的组，并将它们的平均值绘制成分布图(即 100 个随机组，每个组 30 名学生，替换)。这种分布的平均值将使他很好地了解实际人口的平均值，而不需要使用置信区间。样本量为 30 (n=30)是中心倾向定理的“经验法则”,所以邓布利多实际上超过了他最初的样本量 300。

邓布利多考虑了他的选择，决定暂时接受 **54.12% — 57.08%** 预测准确率的置信区间。他对结果并不十分激动，但看到区间的下限仍然大于 50%，他松了一口气，这意味着——至少——特里劳妮教授的预测比随机猜测要好！

他总结了自己发现，并将在特里劳妮教授下一次绩效评估中向她展示。也许他会建议她在未来几年的🧙教学大纲中增加置信区间🏼‍♀️🔮

![](img/32c2202f157bd50cff193fc63bc60773.png)

GIF 由 [Giphy](https://giphy.com/explore/gambon) 提供。