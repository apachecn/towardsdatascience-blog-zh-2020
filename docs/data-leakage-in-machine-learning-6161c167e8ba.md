# 机器学习中的数据泄漏

> 原文：<https://towardsdatascience.com/data-leakage-in-machine-learning-6161c167e8ba?source=collection_archive---------24----------------------->

## 如何检测和避免数据泄露

![](img/ab0107d678062e1e5a21eecc87261d41.png)

照片由[德鲁·比默](https://unsplash.com/@drew_beamer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/future?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

当训练过程中使用的数据包含有关模型试图预测的信息时，就会发生数据泄漏。这听起来像是“欺骗”，但我们并没有意识到这一点，所以称之为“泄漏”更好。数据泄漏是数据挖掘和机器学习中一个严重而普遍的问题，需要很好地处理以获得一个健壮和通用的预测模型。

数据泄露有不同的原因。有些非常明显，但有些乍一看就很难发现。在这篇文章中，我将解释数据泄漏的原因，它是如何误导的，以及检测和避免数据泄漏的方法。

你可能知道它们，但我只想提一下我在这篇文章中经常用到的两个术语:

*   目标变量:模型试图预测的内容
*   特征:模型用来预测目标变量的数据

# **数据泄露的例子**

**明显案例**

数据泄露最明显的原因是将目标变量作为一个特征包括进来，这完全破坏了“预测”的目的。这很可能是错误的，但是要确保目标变量与特征是不同的。

数据泄漏的另一个常见原因是在训练数据中包含测试数据。用新的、以前看不见的数据来测试模型是非常重要的。在训练过程中包括测试数据会破坏这个目的。

这两种情况不太可能发生，因为它们很容易被发现。更危险的原因是那些能够偷偷摸摸的原因。

**赠品功能**

赠品特征是暴露关于目标变量的信息的特征，并且在模型被部署之后将不可用。

*   示例:假设我们正在构建一个模型来预测某种医疗状况。指示患者是否进行了与该医疗状况相关的手术的特征会导致数据泄露，并且不应作为特征包含在训练数据中。手术指征高度预示了医疗状况，可能并不是在所有情况下都适用。如果我们已经知道一个病人做了与医疗条件相关的手术，我们甚至不需要一个预测模型来开始。
*   例如:考虑一个预测用户是否会停留在网站上的模型。包含暴露未来访问信息的功能将导致数据泄漏。我们应该只使用关于当前会话的特性，因为在部署模型之后，关于未来会话的信息通常是不可用的。

**预处理过程中的泄漏**

有许多预处理步骤来探索或清理数据。

*   查找用于规格化或重新缩放的参数
*   要素的最小/最大值
*   估计缺失值的特征变量的分布
*   移除异常值

这些步骤应该只使用训练集来完成。如果我们使用整个数据集来执行这些操作，可能会发生数据泄漏。对整个数据集应用预处理技术将使模型不仅学习训练集，而且学习测试集。我们都知道测试集应该是新的，以前从未见过的数据。

在处理时间序列数据时，我们应该更加注意数据泄漏。例如，如果我们在计算当前特征或预测时以某种方式使用来自未来的数据，很有可能以泄漏的模型结束。

# **如何检测和避免数据泄露**

作为一个将军，如果模型好得不真实，我们就应该怀疑。该模型可能以某种方式记忆特征-目标关系，而不是学习和概括。

在探索性数据分析过程中，我们可能会发现与目标变量高度相关的特征。当然，有些特性比其他特性更相关，但是惊人的高相关性需要仔细检查和处理。我们应该密切注意那些特征。

模型训练好之后，如果有权重非常高的特征，就要密切关注。它们可能是泄漏的特征。

为了最小化或避免泄漏，如果可能的话，除了训练集和测试集之外，我们应该尽量留出一个验证集。验证集可以用作最后一步，模拟真实场景。

当处理时间序列数据时，时间上的截止值可能非常有用，因为它会阻止我们获得预测时间之后的任何信息。

在训练过程中经常使用交叉验证，尤其是在数据有限的情况下。交叉验证将数据分成 k 个折叠，并在整个数据集上迭代 k 次，每次使用 k-1 个折叠训练和 1 个折叠进行测试。交叉验证的优点是它允许使用整个数据集进行训练和测试。但是，如果您怀疑数据泄漏，最好对数据进行缩放/标准化，并分别计算每个折叠的参数。

# **结论**

数据泄露是预测分析中的一个普遍问题。我们用已知数据训练模型，并期望模型对以前看不到的数据进行预测。一个模型要在这些预测中有良好的表现，它必须有良好的泛化能力。数据泄漏会阻止模型很好地泛化，从而导致对模型性能的错误假设。为了获得稳健的广义预测模型，我们应该密切注意检测和避免数据泄漏。

感谢您的阅读。如果您有任何反馈，请告诉我。