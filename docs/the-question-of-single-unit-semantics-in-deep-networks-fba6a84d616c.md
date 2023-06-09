# 深度网络中单个单元的语义问题

> 原文：<https://towardsdatascience.com/the-question-of-single-unit-semantics-in-deep-networks-fba6a84d616c?source=collection_archive---------68----------------------->

## 在深度神经网络的背景下，我们有理由不那么困惑于所谓的祖母细胞吗？

深度学习中一个常见的假设是，网络的单个更高层单元可能对应一个复杂的语义实体，例如一个人或一只特定类型的狗[2，9]。这被通俗地称为*祖母细胞*或*荷马辛普森细胞*。

这些名字源于神经科学。据观察，当一个人看到詹妮弗·安妮斯顿(Jennifer Aniston)照片的任何变体时，人类大脑视觉通路晚期的特定皮质细胞就会激活，正如 Quiroga 等人在研究中所做的那样[6]。然而，在研究中还发现，詹妮弗·安妮斯顿(Jennifer Aniston)的印刷体名字也能引发同样的反应，这表明这种放电是由记忆机制而非纯粹的视觉刺激及其几何变换引起的。

祖母细胞的概念已经在深度学习的实践者的广泛社区中留下了印象，既迷人又容易掌握。已经提出了这些细胞的可视化方法，包括基于网络的[2，7]和基于输入的[9]。

在深度学习论文中，展示这些类型的可视化并假设它们是网络已经学习了一些明智的东西的证据并不罕见，例如[3]。

这是不是真的是这样，这是我在这篇博文中想要探究的。为此，我将主要提及代表对此问题的三种不同观点的三份文件。它们是泽勒&费格斯【9】的*可视化和理解卷积神经网络*，马亨德兰&韦达尔迪【4】的*显著反卷积网络*，以及莫科斯&巴雷特【5】的*关于单一方向对于泛化的重要性*。

## 特征重构和活动最大化

第一篇可能是最著名的论文，试图研究卷积网络的内部工作原理。这里，去卷积(也称为转置卷积)用于将某个滤波器的特征激活投射回像素空间，以查看神经元“看到”了什么。我们可以称之为特征重建。

另一方面，还有活动最大化的方法，这个术语是 Erhan 等人创造的[2]。在活动最大化中，对输入噪声执行优化，以找到将导致一个特定单元的最大激活的输入。Erhan 等人使用这种方法来可视化深度信念网络的隐藏单元。

活动最大化和特征重构之间有着至关重要的区别。[9]的方法是以数据为中心的，即自然图像被输入到网络中。在活动最大化中，输入仅仅是噪声，以便不约束可能的响应(尽管可以在噪声之上应用正则化来加强平滑)。如果特征重构是以数据为中心的，那么活动最大化反而是以网络为中心的方法，因为它是正在研究的网络的激活空间。

[9]中介绍的特征重构方法应用于网络中给定层的特定单元。这些重构被呈现出来，好像这些神经元有语义偏好。

## 随机单元给出了相似的响应

但是我要提到的第二篇论文(Mahendran 等人[4])对这一假设提出了质疑，该论文表明，当应用将激活从随机选择的神经元投射回像素空间的相同方法时，会获得相同的重建。在这里，信息瓶颈的概念被提出来作为一种可能的解释，即为什么从随机单元的特征重构实际上与从最大激活单元的特征重构给出相同的响应。其思想是，前向传递的信息瓶颈所产生的独特信息实际上是重新创建特征时的主要响应。

此外，甚至在此之前，Szegedy 等人[8]对单个单元的语义解释提出了质疑，并声称语义也可以作为分布式代码在一个层的许多单元中找到。这通过将单个最大激活单元的特征重构与过滤器空间中随机(分布)方向的特征重构进行比较来显示:两者都显示了它们响应的清晰语义分组。Agrawal 等人的另一篇论文[1]进行了实验，表明在某个图像的最高激活单元中，为后续分类保留的单元越多，性能越好。

![](img/f5d05a438e9e50be7532fcc1bfdb7397.png)

Solen Feyissa 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片。我们应该重视分布式代码还是单一单元语义？

## 单一单位依赖和概括

最后一篇论文是 Morcos & Barrett 的论文[5]。他们的动机是调查祖母细胞的作用，或*单一单位依赖*，以进行概括。他们进一步研究针对特定语义概念激活的神经元对于这些网络的分类决策是否重要。

他们的结果之一是，有效推广的网络倾向于最大限度地减少对单一方向的依赖。这是通过网络单元的累积烧蚀发现的。非一般化网络(根据实验设计，它们已经记忆了带有随机标签的训练数据集)对这些消融不太鲁棒。此外，他们还研究了消融具有类别选择性的单位是否重要(引入了类别选择性的度量)。在 CIFAR-10 上，明显地，为了网络的性能，移除类选择单元稍微好一些。在 ImageNet 上，在非选择性和类选择性方向之间没有任何偏好。

我简要地浏览了一系列关于单一单位语义学的结果。我们已经看到，对于特定的语义概念，神经网络单元可以具有最大的激活(即，在分类内是类选择性的)。但是，这并不能告诉我们网络的一般性能，也不能告诉我们这个单元是否重要。由于这个原因，正如[5]中所总结的，把重点放在类选择单元上可能会产生误导。类似于[4]中的结果，有趣的是看到分布式单元集的活动最大化，而不是单个单元。这恰好便于可视化一个单元最大程度地激活什么，但是可能在网络的激活空间中存在非坐标对齐的方向，这些方向可能包含至少同样有趣的发现。这些其他方向只是更难放进一个引人注目的故事，更难系统地调查。

*然而，在[2]中，对于图像等复杂分布的数据，似乎缺少全局最大值。

[1] P. Agrawal、R. Girshick 和 J. Malik，分析多层神经网络用于对象识别的性能(2014 年)，ECCV，2014 年

[2] D. Erhan、Y. Bengio、a .库维尔和 P. Vincent,《深层网络的高层特征可视化》( 2009 年), ICML 2009 年学习特征层次研讨会

[3] C. Feichtenhofer，A. Pinz，R. P. Wildes 和 A. Zisserman，我们从动作识别的深层表征中学到了什么？(2018 年)，CVPR 2018 年

[4] A. Mahendran 和 A. Vedaldi,《突出的反进化网络》( 2016 年), ECCV，2016 年

[5] A. S. Morcos，D. G. T. Barrett，N. C. Rabinowitz 和 M. Botvinick，关于单一方向对一般化的重要性(2018 年)，ICLR 2018 年

[6] R. Q. Quiroga，L. Reddy，G. Kreiman，C. Koch 和 I. Fried,《人脑中单个神经元的不变视觉表示》( 2005 年),《自然》,第 435 卷

[7] K. Simonyan，A. Vedaldi 和 A. Zisserman，深入卷积网络内部:可视化图像分类模型和显著图(2014 年)，ICLR，2014 年

[8] C .塞格迪、w .扎伦巴、I .苏茨基弗、j .布鲁纳、d .埃汉、I .古德菲勒和 r .弗格斯，《神经网络的迷人特性》(2014 年)，ICLR，2014 年

[9] M. D .泽勒和 r .弗格斯，《可视化和理解卷积网络》(2014 年)，ECCV，2014 年。