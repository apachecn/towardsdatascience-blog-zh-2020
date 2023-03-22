# 三维打印的人工智能(三):异常熔池分类的非纠缠变分自动编码器

> 原文：<https://towardsdatascience.com/ai-for-3-d-printing-part-3-disentangled-variational-autoencoder-for-anomalous-melt-pools-aaed53b80140?source=collection_archive---------49----------------------->

*本文是 3d 打印人工智能系列的第 3 部分。阅读* [*第一部分*](https://medium.com/@boonyang961005/ai-for-3-d-printing-anomalous-melt-pools-detection-and-classification-part-1-e84ed6f5a137) *和* [*第二部分*](https://medium.com/@boonyang961005/ai-for-3-d-printing-anomalous-melt-pools-detection-and-classification-part-2-895704203c5a) *。*

自动编码器的使用提供了一种用较少的参数描述熔池图像的方法。本质上，这是一种数据压缩形式。然而，如[第 2 部分](https://medium.com/@boonyang961005/ai-for-3-d-printing-anomalous-melt-pools-detection-and-classification-part-2-895704203c5a)所示，自动编码器编码的潜在向量高度密集，并以簇的形式出现。因此，潜在空间不是平滑和连续的。在潜在空间中可能有严重的过拟合，其中当重建时，彼此接近的两个潜在向量看起来非常不同。这是因为缺少正则化项来控制在损失函数中应该如何压缩数据。

> 嗯，你可以说自动编码器为了压缩而压缩数据，因此它不一定在潜在空间中保持数据的结构。

如果我们想两者兼得，这是一个问题:

1.  较小的参数(可通过自动编码器实现)和
2.  高质量数据压缩(自动编码器不是为此目的而优化的)

来描述熔池的几何形状。

使用 autoencoder 的变体可以解决这个问题。本文介绍了一种自动特征提取方法，用于异常熔池检测和分类任务，其核心是使用一种无纠缠的变分自动编码器。具体地说，变分自动编码器的质量数据压缩特性将用于提取不同的熔池表示。

# 介绍

变分自动编码器(VAE)具有与自动编码器相似的结构，除了它是后者的概率变型。VAE 的使用假设有几个未观察到的数据生成因素(也称为表示)，每个因素控制输入的不同方面。接下来，这里的目标是训练 VAE 来近似表示的分布，以便编码器可以有效地用作特征提取器。

![](img/e482dba3eef693b393d7275bd61dbfc9.png)

VAE 的一般架构

VAE 的一般架构如上所示。注意，不同于普通的编码器和解码器，VAE 由两个概率组件组成。概率编码器将输入数据 ***X*** 映射到潜在向量 ***z*** 。另一方面，解码器将来自潜在空间的任何采样向量映射回原始维度***【X’***。

![](img/b74bf5f35f5ff145b18b9a57821b33dd.png)

VAE 的损失函数

这个损失函数有两项。**重建损失**确保重建数据与输入相似。第二项，也称为**KL-散度项**，是数据的潜在分布和潜在编码的先前分布之间的差异的度量。当网络将输入编码到一个高度密集的区域时，它会对网络施加一个惩罚，从而促使编码获得一个类似于先前分布的分布，该分布假定为~N(0，I)。

约瑟在他的媒介文章中对 VAE 做了非常直观和清晰的解释。参见下面的文章:

[](/understanding-variational-autoencoders-vaes-f70510919f73) [## 了解变分自动编码器(VAEs)

### 逐步建立导致 VAEs 的推理。

towardsdatascience.com](/understanding-variational-autoencoders-vaes-f70510919f73) 

为了获得β-VAE 的损失函数，VAE 的损失函数通过将β的因子乘以 KL 散度正则化项来修正。

![](img/2cd445de055bc98092e775cbcc4f4b5d.png)

β-VAE 的损失函数是由 VAE 的损失函数修改而来的。KL 散度项被赋予一个相对权重β。

本质上，这种修改允许我们控制编码的潜在成分之间的解缠结的量。当每个组件对表征的某一方面的变化相对敏感而对其他方面不敏感时，一组潜在组件被称为**解纠缠**。在熔池几何形状的背景下，当潜在编码被完全解开时，改变一个潜在成分将仅仅改变熔池几何形状的一个方面。而对于正常的 VAE，很难理解每个单独的潜在成分捕捉到熔池几何形状的哪个方面，因为改变一个潜在成分会导致多个变化的熔池表示。

在这个项目中，β被选择为 4，因为这个β值根据经验给出了最好的解缠结效果。

# 数据预处理

为了更精确地描述熔池的几何形状，熔池图像从 128x128 的尺寸裁剪为 32x32。这是因为熔池的周围不包含太多关于其几何形状的信息。我们还确保熔池的质心与图像的中心对齐。

![](img/edfb115835bc0d3dba81920bc3fb0083.png)

熔池框架的 ROI。

对所有裁剪的视频帧执行最小最大归一化。与一类学习框架不同，该框架不依赖于正常熔池的任何分析。因此，数据不需要预先筛选。

# 特征提取

通过在熔池视频帧上训练β-VAE，编码器学习熔池潜在表示的概率分布。为了探索编码，可以从潜在维度的特定范围采样，并解码采样的潜在向量以便可视化。

![](img/ec66404a561df4a4cde89a3e412939f7.png)

具有固定的第三潜在成分的生成的熔池图像的网格。(图片由作者提供)

![](img/1744eb62e45dcca53d2b5bdf58f89442.png)

具有固定的第二潜在成分的生成的熔池图像的网格。(图片由作者提供)

根据生成图像的网格图，我们观察到:

*   第一个潜在分量捕捉熔池的尺寸
*   第二个潜在分量捕捉熔池的圆度。熔池图像被垂直或水平挤压。
*   第三个潜在分量捕捉熔池的尾部长度。第三潜在成分的符号也捕捉了熔池的移动方向。

此外，我们可以验证压缩是高质量的，因为熔池图像在潜在空间中平滑地从一种形式“变形”为另一种形式。此外，当我们改变单个潜在成分时，我们几乎可以完美地隔离熔池几何形状的变化。例如，增加第一个潜在成分会改变大小，但对其他两个方面几乎没有影响。这就是我先前所说的解开表象的意思。

从 Arxiv Insights 了解更多关于解开变分自动编码器的信息:

Arxiv Insights 的变分自动编码器简介。

如果我们检查训练数据的潜在成分的分布:

![](img/22e434792007dae91f07d73004f7fad8.png)

(a) Z1，(b) Z2 和(c) Z3 的分布

第一和第二潜在分量类似于高斯分布，而第三潜在分量类似于双峰分布(两个高斯分布的叠加)。第三潜在组分的双峰分布归因于所采用的曲折扫描策略，该策略导致熔池以之字形行进。由于β-VAE 损失函数中 KL 散度项施加的正则化力，所有分布都以 0 为中心，并具有接近 1 的标准偏差。

# **异常检测和分类**

接下来，编码的熔池以散点图的形式呈现。

![](img/b40b6f8a7ebdbc99e26691f5100e88f4.png)

Z2 与 Z1 的散点图，带有锚定熔池图像。(图片由作者提供)

![](img/182c4f875b01f3c953f76d3f38c5034d.png)

Z3 与 Z1 的散点图，带有锚定熔池图像。(图片由作者提供)

根据散点图，编码似乎与潜在的表征定性一致。此外，几个异常清楚地编码远离密集区的潜在空间。这表明使用从一些参考点的欧几里德距离度量作为异常测量。基于可视化，将数据点分类成簇也是明智的。接下来，可以计算熔化池离它们的群集质心的距离，并将其用作异常度量。

> 从概念上讲，这意味着一组给定的熔池特征偏离它们的平均值越多，熔池就越不规则。

![](img/c1f99efdd3cabcd842b557b7de0bf4d5.png)

(a)所有数据点，(b)由 DBSCAN 识别的异常值(橙色)和正常数据点(蓝色)，(c)拟合正常数据点的 K 均值聚类，以及(d)所有数据点和两个识别的聚类的散点图。(图片由作者提供)

使用基于密度的聚类算法 DBSCAN 来清理数据，然后在清理的数据集上拟合 k=2 的 K 均值聚类。这些聚类的质心将被存储用于测试期间的欧几里德距离计算。距离度量将被用作熔池异常程度的量度。

三种不同的监督分类器，支持向量机(SVM)、K 近邻(KNN)和随机森林(RF)用于熔池异常分类任务。这次，我们明确地将熔池的类型分为几类——具有不稳定尾部的熔池、羽状熔池和大型熔池。

分类器的最优超参数通过五重网格搜索交叉验证获得。最后，使用测试数据集来量化分类器的性能。分类结果总结如下:

![](img/9d0b28873db0ea350eedda8f34206c94.png)

(a) SVM，(b) KNN 和(c) RF 的混淆矩阵

一些正确的分类如下所示:

![](img/55fbc51c3b6cd58aa77fb961a981a650.png)

正确的分类:( a)不稳定尾翼,( b)羽流,( c)大型熔池。

我们的 VAE 框架现在可以分配异常度量，此外，它还具有根据熔池的几何形状对其进行分类的能力。

这种一体化异常分类和检测框架在三条扫描线上的使用示例:

![](img/c9838d1ad4dcd8fad5779fc0ec95f47a.png)

每个框架顶部的熔池和异常度量的预测类别。

# 一些想法

β-VAE 框架比端到端的监督深度学习方法(端到端的深度学习方法是，在没有任何特征提取的情况下，在标记的数据上训练监督的神经网络)具有一些优势:

1.  对于异常分类问题，没有监督模型是很难进行的。β-VAE 框架通过首先提取熔化池表示来工作。这为后续的聚类和经典的监督模型提供了适当的特征空间来操作。意思是，框架的前半部分是完全无人监管的。与在没有足够数量的训练数据的情况下容易过拟合的端到端监督深度学习方法相比，β-VAE 框架的后半部分将需要较少的标记数据来进行训练。
2.  就可解释性而言，β-VAE 将熔池图像分解成三个明显的清晰表示。我们已经看到并验证了表示分布与生成的熔池图像的网格图一致。至于端到端深度学习，更难解释为什么某些融化池会被归类到某些类别中。

# 未来的工作

未来的工作可能涉及用更精确的训练数据集来训练β-VAE。在已知限制的情况下(在一组指定的打印参数内工作)，该框架可以被合并到现有的 LPBF 监控系统中。用序列模型解决这个问题是另一个有待实验的有趣方法。本质上，我们可以将熔池动力学建模为一个时间序列问题。这是有意义的，因为像羽流这样的异常情况的特征是它们在多个帧中快速变化的形状。也许用这种新的视角来看待这个问题将是建立一个更准确的框架的关键。

# 结束语

在这篇文章中，我们探讨了更多的数据压缩能力的一个解开变分自动编码器。通过各种可视化，我们验证了所产生的潜在空间是平滑和连续的，在某种意义上，熔池图像是相似的，彼此编码紧密。此外，利用这个框架，我们还可以提取有用的和可解释的熔体池表示，用于异常检测和分类。通过对潜在表示训练一些监督分类器，我们还表明该框架可以用于分类异常并同时量化其异常程度。

感谢阅读:)