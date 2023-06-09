# 分析拼车数据

> 原文：<https://towardsdatascience.com/analyzing-rideshare-data-a7c83f95cd65?source=collection_archive---------22----------------------->

## 构建应用程序定量主干的过程

![](img/1aac8ef6d4eecda2e3fc619295f02165.png)

**原 app 描述**

在过去的十年里，优步、Lyft、Gett、Juno 和 Via 等叫车服务已经彻底改变了运输领域。然而，司机的盈利能力在所有这些平台上以复杂的方式变化。司机被迫根据一天中的时间、激增率、搭载乘客的等待时间等进行心算。并且基于这些因素的优化选择在任何点上为给定的服务乘车。由于这个困难的优化问题——考虑到潜在因素的数量以及许多未知因素——司机无法确定他们选择了最有利可图的服务。 *Ride King* 通过根据驾驶员的位置以及驾驶员打算驾驶的时间，汇集每项驾驶服务的历史和最新数据，消除了这种不确定性。*骑王*的最终目标是最终将这种优化服务扩展到骑手，这样他们就可以在任何给定的时间点选择最便宜的乘车公司。针对乘客和司机的各自优化的融合将有望从每个拼车服务中转移足够的注意力，以产生更好的透明度和/或对司机的更大回报。

*骑王:智能骑*

**一看原始数据**

这个应用想法的数据收集绝不简单。为了避免他们的信息被用于竞争目的，大多数拼车公司都会竭尽全力保护他们的数据。然而，经过一番深思熟虑，我们实际上可以发现一些访问这些数据的后门方法。纽约市的所有拼车应用都在出租车和豪华轿车委员会(TLC)的监管之下，法律要求它们提交每次乘车的数据。通过一些调查，敏锐的观察者会发现 TLC 是纽约市开放数据倡议的一部分，该倡议旨在增加州和城市事务的透明度。虽然这些拼车公司提供的数据非常肤浅(每次拼车的信息非常少)，但我们仍然可以从中获得相当多的信息。然而，首先，我使用的是 2014 年 4 月的优步数据(由该公司慷慨提供， [fivethirtyeight](https://github.com/fivethirtyeight/uber-tlc-foil-response) ),其格式与 TLC 数据集略有不同。

![](img/0cb3d8a35fc3f9453cf3de17991894e9.png)

来自 2014 年 4 月纽约市优步区 fivethirtyeight 数据集的示例行

快速浏览一下，我们可以看到该集合中的每一行都提供了日期、时间、取货地点(在地理坐标中)和“基地”。我们将稍后讨论最后一篇专栏文章——现在，让我们只看一下原始数据。请注意，虽然我们可以只绘制原始地理坐标，但我实际上已经覆盖了 Zillow 慷慨公开的纽约市社区边界数据。这为我们的数据增加了另一个维度！

![](img/a6ae621d154cf2f3eb37be093d6d2ad5.png)

曼哈顿中/下城 2014 年 4 月的所有优步皮卡

好吧，酷。因此，我们现在可以看到 2014 年 4 月在曼哈顿的所有优步皮卡(为了可读性，进行了缩放)，包括街区边界等！由于这个项目的目标是试图根据一天中的时间和位置来预测拼车服务的盈利能力，到目前为止我们只是触及了表面，但是我们已经可以看到拼车绝对是*而不是*均匀分布的！

![](img/5ed6d5feb4c7ad23fdcbdd72db0a0110.png)

最受欢迎的社区

**深入**

现在让我们看看这些 rideshare 服务上传到 TLC 的实际数据。

![](img/b44694e839fff2620690438f09b2f768.png)

2018 年所有纽约市拼车服务的 TLC 开放数据集

让我们从回顾最后一列开始(第一个数据集中的“base”，现在是“Dispatching_base_number”)。这些数据的最后一列是与每个驾驶员报告的基数相对应的代码。这些基地中的每一个都属于一个特定的 rideshare 应用程序，但当前的格式使分析变得复杂，因为我们不确定哪个基地对应于哪个公司。在花了一些时间在政府文件中搜索每个基本代码的所有权后，我们能够创建一个字典，轻松地将混淆的基本代码与我们熟悉的名称(例如，优步、Lyft、Gett、Via、Juno、Ola、Didi 等)进行转换。).一旦我们将接送 id 映射到实际的社区，我们就可以开始做一些有趣的事情了…

![](img/5f4d98e7d63fd4b2d5a257f6fd35a38d.png)

平均值。诺曼曼哈顿 Lyft 和优步 2018 年一天的皮卡数量。达到各自的最大值

作为我对这个应用程序想法的分析的一部分，我实际上花了几个月时间询问拼车司机这个问题，绝大多数人告诉我，最大化他们利润的最佳方式是最小化每次乘坐的持续时间。我做了一些补充分析来进一步探索这个问题，根据每个拼车应用程序的定价模型，最小化乘车时间实际上似乎是最大化利润的最佳方式。让我们继续分析，再次记住我们现在的目标是通过基于位置和时间寻找最短持续时间的乘坐来预测盈利能力。

使用 TLC 数据集中的接送时间，我们可以很容易地计算出数据中每一行的乘坐时间。通过聚集邻近地区的数据，我们可以分析一天中每个小时和每个拼车服务的平均乘车时长。我们在这里希望看到一个服务的持续时间相对于其他服务有显著的下降。

![](img/e84420c63f177672c44bb242edf40c3a.png)

纽约市 Meatpacking/W. Village W .街区的 Via、优步、Lyft 2018 年全年骑行时长比较(平均值，SD)

仅仅看一下轨迹，每个服务的乘车时长之间的间隔很小，而且有如此高的方差，我们会*疯狂*地认为我们可以从附近或一天中的时间可靠地预测持续时间。

让我们再看一些:

![](img/d29fa788e7bfb62cf2b771d5591a19aa.png)![](img/edfb32ad90656b9c2bff6176b1859772.png)

啊！还是同样的问题…这就是我的应用程序想法的问题所在:位置和一天中的时间不足以预测乘车时间。这完全有道理——你会放心用 100 美元赌你朋友在街上看到的某个随机优步的旅行时长吗？很遗憾数据显示了如此大的差异，因为这是一个非常令人兴奋的概念。我肯定有办法创造性地向数据中添加功能，以实现更好的预测，但就目前情况而言，我并不完全相信历史数据足以预测拼车服务的未来。

虽然我最终没有进一步追求这个应用程序(数据第一，总是！)，这是一次非常有趣的经历，也是我第一次对数百万行数据进行大规模分析，在这种情况下，代码效率成为一个重要因素。

非常感谢你的阅读！

**奖金调查结果**

![](img/9c2ac5a4c9073c49eca54b293b817807.png)

不足为奇的是，降雨会影响到优步游乐设施的数量。这里的每个点代表 2014 年的一天，我将 rideshare 数据与历史[天气报告数据](https://www.weather.gov/okx/CentralParkHistorical)结合起来，以确定当天的最大降雨量(****，皮尔森的 R 临界值)

![](img/04dc31428a1c2d959ea2c998c0ab6dc9.png)

Lyft(粉色)对优步(黑色)的平均得分。随机选择的社区在 2018 年的骑行时长