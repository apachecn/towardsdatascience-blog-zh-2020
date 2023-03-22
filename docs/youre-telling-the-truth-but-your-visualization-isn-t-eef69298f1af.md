# 你说的是实话，但你的想象不是

> 原文：<https://towardsdatascience.com/youre-telling-the-truth-but-your-visualization-isn-t-eef69298f1af?source=collection_archive---------35----------------------->

## 关于视觉完整性的一课

![](img/11312659a417657ba73a449ba4774921.png)

马库斯·温克勒在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

为什么要创造一个歪曲事实的形象呢？问得好。

虚假陈述可能有多种原因，但最主要的一个原因是:为了迫使观众做出某个特定的行为，在观众内部制造一种情绪反应。换句话说，可视化创建者对发布他们的议程比对精确描述数据更感兴趣。

现在，不要误解我，有很多时候事实数据支持一个人的潜在意图，但当它不支持时，一个人不应该在视觉上夸大它，使它确实如此。

综上所述，我们知道数字不会说谎，但是数字的呈现方式会极大地影响得出的结论。

在讲述一个当今的例子之前，我想先给你们介绍一下耶鲁大学的教授爱德华·塔夫特。早在 1983 年，他写了一本名为[的书，定量信息的可视化显示](https://www.edwardtufte.com/tufte/books_vdqi)，这本书对当今的统计界产生了深远的影响。《美国统计组织杂志》甚至称之为“迄今为止对图形研究的最重要贡献”

在这本书里，塔夫特介绍了一个**寿命因子**的概念。简而言之，这个因素的目的是计算可视化在表示其底层数据时的诚实程度。理想情况下，lie 因子应该是 1.0，因此任何其他值(除了较小的方差之外)都意味着可视化在表现底层数据方面存在一些不匹配。

寿命因数定义为:

![](img/a90b3daaa268b87b13f478e72497e052.png)

接下来，数据中效应的大小定义为:

![](img/175a00d905c56464f49886bfefbe0335.png)

这还有点模糊吗？我的猜测是肯定的，因此当前的示例应该有助于您轻松理解这一重要指标。

在《华尔街日报》最近发表的一篇文章[中，展示了一张图表，旨在说明 2020 年和之前年份之间各种原因导致的死亡的增加。在详细讨论图表之前，您认为其创建者的潜在意图是什么？](https://www.wsj.com/articles/covid-19s-exact-toll-is-murky-though-u-s-deaths-are-up-sharply-11589555652)

![](img/67ac4ff00dd5756aa3266479f99075f8.png)

资料来源:*国家卫生统计中心*

我认为他们想让你认为 2020 年 4 月死亡人数会大幅增加。不仅仅是增加，而是显著的增加。此外，这张图出现在一篇关于新冠肺炎的文章中，这也可能是他们想让你认为这种病毒本身非常致命，尽管它实际上的[死亡率在 0.2%到 0.4%之间](https://www.medrxiv.org/content/10.1101/2020.05.13.20101253v1)。

现在，让我们通过计算它的谎言因子来研究这个图表，看看它在视觉上如何准确地表示基础数据。

为了计算图形中效果的大小，我们首先测量从 X 轴到蓝色和褐色线的像素距离。蓝色线条的高度为 352 像素，而棕色线条的高度为 92 像素。

![](img/d28d15d9dd194ad3240879c437b010de.png)

图形中显示的效果大小

接下来，我们计算数据中影响的大小。在这里，我们观察到，在 4 月 11 日这一周，2020 年记录了 71，784 例全因死亡，而同一周 2017-2019 年的平均值为 55，647 例死亡。

![](img/ff5e21961a2b4db1eeb79e59dfc341af.png)

数据中显示的效果大小

最后，我们计算谎言因子为:

![](img/6f55efaaaafc2344efbd042a16f337c2.png)

呀！看来我们关于图表歪曲数据的预感是正确的。可悲的是，这种事情发生得太频繁了。在这种情况下，用来误导观众的技巧是从 50，000 而不是 0 开始绘制图形。

将来，当你看到各种各样的视觉化图像时，请记住谎言这个因素。此外，问自己这些问题:

*   轴线从哪里开始？它们是从 0 还是其他数字开始？
*   这个图表是三维的吗？(我们的大脑很难理解这些)
*   有不同大小的物体被比较吗？

这些问题，以及达雷尔·赫夫写的本书中概述的[中的许多问题，在消化和创作图形时问自己是很重要的。](https://www.amazon.com/How-Lie-Statistics-Darrell-Huff/dp/0393310728)

请记住，数字不会说谎——人会说谎，而且人们有各种各样的理由这样做。做一个能够正确描述你的数据的可视化的人，同时也要意识到其他人可能会试图用他们的数据误导你。