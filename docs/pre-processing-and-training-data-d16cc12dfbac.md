# 预处理和训练数据

> 原文：<https://towardsdatascience.com/pre-processing-and-training-data-d16cc12dfbac?source=collection_archive---------22----------------------->

## 转变数据和训练模型以获得最佳性能是一个整体过程。

![](img/4021e56f94b36411b5d15a4d00de7ac7.png)

图片由[皮克斯拜](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=3706562)的 Gerd Altmann 提供

# 预处理

那么，什么是预处理呢？常见的例子包括

*   输入缺失值
*   转换数值(线性或非线性)
*   编码分类变量

## 输入缺失值

你的数据中经常有漏洞。有人没有回答调查问题。传感器故障。数据丢失了。价值缺失及其原因多种多样。缺少的值可以用一个特殊的“值”NaN(在 Python 中，来自 NumPy)或 NA(在 R 中)来表示。但是思念并不总是由这些特殊的标记来表示。负值表示缺少数据，例如-999 表示某人的年龄。这可能取决于原始系统或软件，以及在您收到数据之前数据是如何处理的。在您的上下文中，空字符串可能被归类为“丢失”，也可能不被归类为“丢失”。

你现在应该已经解决的一个重要问题是，在丢失的数据中是否有任何模式。您在之前的 EDA 阶段确实探索过这一点，对吗？这些河流水位传感器读数丢失是因为站点被淹没吗？或者，丢失的值是随机散布在数据中的，暗示着一些更无害的原因，比如间歇性的无线电干扰？如果是前者，那么我希望您已经添加了一个新特性来捕获值丢失的事实。无论如何，大多数机器学习算法不喜欢丢失值，所以你需要采取措施，比如，坦白地说，猜测值可能是多少。这是归罪。

有许多输入缺失值的方案。您可以使用剩余值的平均值。或者中间值。或者取最后一个已知值。是的，选择最佳策略需要反复试验。

## 转变价值观

有几个原因需要转换要素的值。您可能有高度偏斜的分布，而非线性变换可以使这些分布正常化，这有助于许多算法。您可能有一组以非常不同的比例测量的要素，例如以英尺为单位的土地高程和以英亩为单位的面积。或者以磅为单位的体重和以华氏度为单位的体温，与以千克为单位的体重和以摄氏度为单位的体温。事实上，这些单位并没有太大的不同，但是这让我们有了另一个理由去转换特性值；计算点与点之间距离的算法和正则化(惩罚)它们的系数的算法可以任意产生非常不同的结果，因为这种单位上的差异。缩放要素将所有要素置于同等地位。

## 编码分类变量

像数字这样的算法。他们对字符串(文本)不太感兴趣。可以说，大部分数据科学都是寻求将数据转换成机器学习算法可以处理的适当数字表示。与其让名为“Animal”的列具有“Cat”或“Dog”的值，不如创建一个“Cat”列，用值 0 或 1 表示“not a cat”或“is a cat”，用值 0 或 1 表示“not a dog”或“is a dog”。即使这种相对简单的方案也有一些微妙之处，比如需要为包含截距的线性回归等模型删除其中一列。这是为了避免[虚拟变量陷阱](https://www.algosome.com/articles/dummy-variable-trap-regression.html)。

# 列车测试分离

如果在训练机器学习模型之前有这么多可能的决定要做，我们如何决定使用哪个？我们可以使我们的预处理和模型变得越来越复杂，以适应数据中越来越多的任意结构。我们如何知道我们的预处理决策是正确的，而不仅仅是适应数据中的噪声？这就是所谓的过度拟合。评估一个模型是否过度拟合它所知道的数据的基础是，在训练它时不要给它所有的数据，保留一些数据，然后观察它的表现。

一个巧妙的变化是将训练数据进一步分割成多个部分，除了一个部分之外，对所有部分进行训练，并对剩下的部分进行测试。通过旋转这样保留的分区，我们最终得到了对一个验证集的许多性能估计(其中验证集每次都是不同的)。这是交叉验证，在执行模型选择时特别有用。当然，我们仍然可以保留一组数据，以确保我们有一些我们的模型从未见过的数据。在对多个模型进行测试的多个交叉验证回合之后，这样的最终测试集是对预期未来性能的有用的最终检查。

# 韵律学

但是我们如何衡量绩效呢？有许多可能的度量或指标，最合适的一个取决于用例。如果我们正在执行分类，例如“猫”或“狗”，那么一个能捕捉我们得到正确答案的次数与我们得到错误答案的次数的指标是合适的。但如果我们在做回归，我们试图预测一个连续变量，如某人的工资，或房价，那么反映我们倾向于接近真实值的平均水平的度量是最好的。这里一个常见的度量是平均绝对误差，顾名思义，它是误差大小的平均值。

# 齐心协力

现在我们实际上已经有了所有需要的材料。对于我们特定类型的机器学习问题，我们可以选择一个度量标准。有了度量标准，我们就可以衡量成功(或失败)的程度。拥有一个训练测试分割给了我们一种方法，可以将这个度量应用到算法不知道的数据分区。这些共同允许我们尝试许多不同类型的模型和预处理步骤，并评估哪一个执行得最好。

嘿，很快！如果您已经尝试了各种预处理步骤和算法，并且应用了适当的度量标准，并且根据测试集评估了您的整个过程(例如，通过交叉验证)，那么您已经获得了一个训练好的模型。具体来说，您已经建立了预处理步骤和算法性质的组合。

# 关于这篇文章

这是一个链接系列的第五篇文章，旨在简单介绍如何开始数据科学过程。你可以在这里找到简介[，在这里](https://medium.com/@guymaskall/the-data-science-method-dsm-35200eb4984)找到上一篇文章[，在这里](https://medium.com/@guymaskall/exploratory-data-analysis-86eb12060eac)找到系列文章[。](https://medium.com/@guymaskall/modelling-e096495d8d70)