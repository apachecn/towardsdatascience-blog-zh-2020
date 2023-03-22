# 利用人工智能实现精确的火灾预测

> 原文：<https://towardsdatascience.com/towards-more-accurate-fire-predictions-using-ai-ee6d5c26955c?source=collection_archive---------44----------------------->

## 卫星+人工智能=前所未见的信息

![](img/e12b025e05fb1cb7aec3d938c594087a.png)

地图显示了美国西部植物相对于干生物量的水量。数字越低，植被越干燥，发生野火的风险越大，反之亦然。*作者图片。*

[美国西部森林野火的风险正在增加。在过去的五十年里，大规模野火发生的频率和破坏的面积分别增加了四倍和六倍。野火带来的风险增加，促使科学家试图评估野火的风险，以帮助通知是否在灾难性的野火发生之前将人们转移到安全的地方。](https://royalsocietypublishing.org/doi/10.1098/rstb.2015.0178)

为了克服这一挑战，我使用大量数据和深度学习来制作美国西部的动态森林干旱地图，这是有史以来第一次。这些地图可能最终导致野火风险评估的改进。

# 野火风险和森林干燥的作用

在野火风险评估中，森林干燥度——野火点燃和蔓延的重要预测指标——是使用气象指标(如先前的降水和温度)来估计的。研究人员将森林干燥度称为活燃料水分含量(LFMC ),因为它表明了树木和灌木等燃料相对于其干生物量的含水量。新鲜燃料的含水量越低，燃料越干燥，野火的风险就越大，反之亦然。

然而，气象指标并不总是代表真正的森林干旱。就像你阳台上的植物一样，不同的植物有独特的策略来应对干旱。一些可能能够通过关闭气孔(叶子上的孔)来保存水分，而另一些可能不能。一些植物可以通过长更深的根来获得更多的水分，而另一些则不能。然而，绘制什么物种生长在哪里以及它们如何对水分胁迫做出反应是很困难的。因此，火灾模型经常忽略这些影响。这可能会导致对森林干燥度的错误估计，最终在我们的野火风险评估中引入错误。我们怎样才能做得更好？

![](img/292635e0ce61f0b4f2b9d9b02f7144ed.png)

*美国林务局在 2016-2019 年间进行的森林干燥度测量。图片作者。*

当我看到美国林务局在美国西部收集数千份森林干燥度测量数据时，我看到了一个机会。利用这些测量数据，我用神经网络直接估算了森林的干燥度。

# 从太空感知的森林干旱

虽然观察森林变褐和变绿很常见，但观察森林干燥(和潮湿)很有挑战性，因为我们看不到树里面的水。虽然存在一些模型来估计森林的干燥度，但它们无法缩放，因为它们需要知道植被的几何形状。因此，科学家们只能估计 5-17 种植物的森林干燥度。通过让神经网络使用各种遥感输入来计算树冠几何形状的影响，我能够通过验证 56 种不同的物种来绘制整个美国西部的森林干旱地图。

在交叉验证时，我发现我的景观尺度森林干燥度制图工作与其他较小尺度的分析一样准确。可用于模型训练的大量地面数据，结合基于领域知识对神经网络进行的修改，产生了这个结果(如下所述)。

# 物理辅助神经网络

![](img/37ee37033446e60986b3babbc5a9e964.png)

将森林干燥度(表示为“LFMC”)与输入变量联系起来的概念模型。图片作者。

由于森林干燥度是一个随时间变化的变量，它依赖于整个前一个季节(在这种情况下是 3 个月)的时间观察，我使用了一个基于长短期记忆(LSTM)模型的递归神经网络。这一决定是在初步结果表明仅从卫星观测的快照(及时)预测森林干旱导致非常差的时间可预测性之后做出的。

利用 Sentinel-1 卫星的微波后向散射和 Landsat-8 卫星的光学反射来训练 LSTM 模型。

我根据我们对将输入与森林干燥联系起来的物理过程的概念性理解，通过使用精心设计的输入，使模型成为物理辅助的。这是通过两种方式实现的:

1.  通过使用微波和光学比率，这些比率是根据与卫星有关的机械模型的形式选择的。由于微波后向散射对植被水和光学反射对干生物量具有更高的敏感性，微波后向散射和光学反射的比率模拟了森林干燥的定义的结构。因此，我包括了偏振和光学反射率和指数的微波反向散射的比率。
2.  通过选择辅助静态输入，提供关于土壤类型、植被结构和地形对遥感观测的影响的信息。

用于实现物理辅助递归神经网络的完整代码库可以在这里[找到](https://github.com/kkraoj/lfmc_from_sar)并且该算法的进一步细节包括在[杂志*环境遥感*中的这个【开放存取出版物】中。](https://www.sciencedirect.com/science/article/pii/S003442572030167X)

# 结论

现在有了动态的、完整的森林干燥度地图，我计划测试野火发生和规模对森林干燥度的敏感性。在这个过程中，我将量化这些森林干旱地图对野火风险预测的价值。

![](img/cc6aa106aeb00ebbc69fb698fc0ed69f.png)

使用我的 LSTM 模型绘制的森林干燥度图。森林干燥度显示为树木含水量相对于其干生物量的百分比。从地图上看，与 2019 年相比，2020 年似乎会因为更干燥的燃料而导致火灾活动增加。图片作者。

**使用我的** [**网络应用**](https://kkraoj.users.earthengine.app/view/live-fuel-moisture) **探索你在美国西部当地社区的森林干旱动态。**

这篇文章的修改版本最初出现在 AWS 公共部门博客中。