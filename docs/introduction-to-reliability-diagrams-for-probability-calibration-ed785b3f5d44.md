# 不确定度校准和可靠性图表简介

> 原文：<https://towardsdatascience.com/introduction-to-reliability-diagrams-for-probability-calibration-ed785b3f5d44?source=collection_archive---------10----------------------->

## 挑战不确定度校准的常见误解

![](img/ffc347f4673d27c2db8cacd0e2f6b1f3.png)

不确定性校准是机器学习中最容易被误解的概念之一。这可以归结为一个简单的问题:“考虑到上述下雨的可能性，你带雨伞了吗？”

我们在日常生活中使用主观概率和不确定度校准的概念，却没有意识到它们。对于一个校准良好的不确定性天气预报模型来说，如果下雨的概率只有 5%，那么带伞大概是不划算的。从频率主义者的角度来看，如果可以在大量随机试验中反复观察到上图中早上 7 点的天气状况，那么只有 5%的天气会下雨。然而，另一方面，如果不确定性校准不当，很可能早上 7 点的随机试验中有 40%会以下雨告终——这是一个大惊喜。

# 什么是不确定度校准？

DeGroot 等人[1]以*预测降雨*为例来说明校准的概念。

> 校准的概念与预报员的**预测**和实际 ***观测到的降雨相对频率*** 之间的**一致**有关。笼统地说，如果一个预测者的预测是 x，那么他的长期相对频率也是 x，那么这个预测者就被称为**校准良好的**。

换句话说，对于一个校准良好的模型，如果它预测一组图像有 40%的概率是猫，那么该组中包含的猫的频率应该等于 40%。“相对频率”有时被称为“条件概率”，可以理解为 cat 的概率，即，以预测概率为 40%为条件的阳性结果。

Dawid [1]提出了类似的程序，如下所示。

> 将预测与现实进行比较的一种方法是挑选一些相当任意的测试日，并在其中比较(a)相关事件实际发生的日的比例 p 与(b)这些日的平均预测概率π。

如果我们遵循一些划分方案来选择测试集，并在其中比较(a)和(b ),我们就得到可靠性图。

# 可靠性图表

在一个二元分类问题中，我们训练一个模型来估计一个例子被分类为正类的概率，即 f(x_i)=p(y_i=1|x_i)，如下图 1 所示。

![](img/f7b7f6a9d94ad2e608d7ee6ad7c6741a.png)

图一。估计一组例子的概率

一旦我们获得了一个测试集的概率，我们将概率划分为 K 个子集，其中每个子集代表 0 和 1 之间的一个不相交的概率区间。这如图 2 所示。

![](img/a731a88e34905574487522313dfb024d.png)

图二。这些示例基于区间[0，0.33]、[0.33，0.66]和[0.66，1]被分成三组。

对于不同颜色的每个子集，我们计算两个估计值:(a)平均预测概率，(b)正例的相对频率。

我们首先计算(a)每个子集的平均预测概率，如图 3 所示。

![](img/291490c68bd4dfdc56083ecdd0af0f31.png)

图 3。每个子集的平均预测概率。

我们接下来计算(b)正例的相对频率，这需要基础事实标签的知识。在图 4 中，我们用灰色圆圈表示负类，其余的颜色表示正类。作为例子，在集合 1 中，只有一个例子是正的；所以正例的相对频率是 1/3。

![](img/b64ac5f63cd12dd98ae0dfd8a0fabdcc.png)

图 4。正面例子的相对频率

可靠性图是绘制(b)与(a)的关系，如图 5 所示。

![](img/27568dff3d66614ce2e1679afc9b426f.png)

图 5。可靠性图表

直观地，校准图表明:(I)当平均预测概率为 0.17 时，大约 33%的预测是肯定的；(II)当平均预测概率为 0.45 时，约 50%的预测是肯定的；(III)当平均预测概率为 0.82 时，约 80%的预测是肯定的。这个人为的模型虽然不完美，但相对来说还是比较精确的。

# 误解:相对频率与准确度

关于可靠性图表的一个普遍误解是用“准确性”代替“相对频率”有时从业者——包括我非常尊敬的杰出研究人员——用“每个子集的准确度”来表示相对频率，这并不是校准的目的。我们需要从相对频率的角度来理解校准，其中阳性类别的预测置信度应该反映所有预测中阳性样本的频率(有时称为子集的流行度)，而不是准确性。

我将使用来自 [scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.calibration.calibration_curve.html) [3]的一个例子来展示它们之间的区别。图 6 显示了一个逻辑回归模型的可靠性图，这是一个相对校准良好的模型。

![](img/e249a4b57f3bc134b3345787b43d4869.png)

图 6。可靠性图表

然而，如果我使用精度来绘制 y 轴，它看起来像一条 V 形曲线，如图 7 所示。

![](img/1b4b15cbfd3289bf362771dec3dbe8e9.png)

图 7。准确度-平均预测值图

这是因为当正面预测概率较低而负面概率较高时，会提升图的左半部分。这可以通过平均预测值的直方图来验证。大量实例的平均预测值在 0 和 0.1 之间，因为它们是负类，并且它们中的大多数被模型正确分类。

![](img/922cc4f8f51f9360493cd7e58fd6eb18.png)

# 结论

我希望你永远不要担心天气预报的不确定性校准。如果当下雨的概率低于 20%时，你总是淋湿，你就知道预测模型没有校准好。

从机器学习从业者的角度来看，不确定性校准与模型的概率结果的解释高度相关，特别是在安全关键应用中，如医疗领域。

# 参考

[1] DeGroot、Morris H .和 Stephen E. Fienberg。"预测者的比较和评估."皇家统计学会杂志:D 辑(统计学家)32.1–2(1983):12–22。美国心理学协会(American Psychological Association)

[2]达维德，菲利普。"精确的贝叶斯理论。"*美国统计协会杂志*77.379(1982):605–610。美国心理学协会(American Psychological Association)

[3][https://sci kit-learn . org/stable/modules/generated/sk learn . calibration . calibration _ curve . html](https://scikit-learn.org/stable/modules/generated/sklearn.calibration.calibration_curve.html)