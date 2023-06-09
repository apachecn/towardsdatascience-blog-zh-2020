# 如何选择预处理技术来减轻人工智能偏差

> 原文：<https://towardsdatascience.com/how-to-choose-a-pre-processing-technique-to-mitigate-ai-bias-11ed9fc0f881?source=collection_archive---------49----------------------->

## 不同预处理技术的高级概述

![](img/effda7aa38299187f90385b9cf770480.png)

拉奎尔·马丁内斯在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

早些时候，在我的[博客](/reweighing-the-adult-dataset-to-make-it-discrimination-free-44668c9379e8?source=email-9bfcef3ebec4-1586898230635-layerCake.autoLayerCakeWriterNotification-------------------------69938872_94b8_4c59_bda0_ec47396b9398&sk=1a42df4fda2bf8dceaee361ef306c6db)关于[如何处理人工智能偏差](/how-to-tackle-ai-bias-ec39313ccacf)的系列文章中，我们探索了深度重新加权【1】，这是一种减少偏差的预处理技术。然而，这只是一种技术。预处理缓解措施的类型从简单的数据准备方法，如取样、按摩、重新称重[1]到更复杂的方法，如优化数据转换，以减少偏差和受保护或敏感属性的可预测性[2–3]。

在这篇文章中，我不想深入讨论任何一种技术，而是想讨论一个数据科学家在预处理阶段试图解决偏差时可能有的选择。也就是说，这些技术之间的区别是什么，以及它们中的每一种如何对数据科学家和 ML 实践者有益？在我开始讨论它们之前，理解 AI 偏见的来源是很重要的。

正如我在人工智能偏差系列的第一篇[帖子](https://medium.com/p/how-to-tackle-ai-bias-ec39313ccacf?source=email-9bfcef3ebec4--writer.postDistributed&sk=0cd7318ea075d7dea801f776fd622cfe)中提到的，偏差可能会悄悄进入 ML 管道，并被各种来源的模型预测放大。数据不足、数据收集不一致以及数据中存在的不良做法会通过各种机制导致模型决策中的偏差。例如，模型可能无法为代表性不足的群体提供高度确定性的预测。或者，它可能从历史数据中的现有偏差中了解到歧视性行为，并因此延续甚至增加其预测中的偏差水平。

下面是两个数据缺陷的例子，这些数据缺陷会导致模型偏向某些群体:

*   一个图像数据集被放在一起用于面部识别。模型未能正确识别某些群体的原因可能是数据集中这些群体的图像数量不足。
*   数据集是根据一家公司的历史雇佣情况创建的。该模型不愿意给某些群体的候选人打高分，这可能不仅是因为数据不平衡，也是因为数据中隐含的历史性歧视性招聘做法。

当呈现偏斜的、不平衡的数据或缺乏多样性的数据时，例如上述面部识别数据集，模型对代表性不足的群体表现出歧视行为的倾向反映了模型不能对不同的群体同等地执行。在这些情况下，诸如[采样和重新加权](https://core.ac.uk/download/pdf/81728147.pdf)等技术可以通过调整数据中不同组的平衡来减少偏差，从而增加模型的学习机会。

另一方面，如果历史偏见和歧视是数据中偏见的根本原因，如招聘示例，重新标记或数据转换更可能是减少偏见的最佳方法。即使您已经确保数据中没有任何要素充当敏感属性的代理，有偏差的标注仍可能导致模型通过性能误差呈现偏差，例如组之间的假阳性或假阴性有显著差异。由于模型无法为相似但属于不同组且具有不同标记结果的记录找到有意义的模式，因此模型可能表现出不确定性。这些不稳定的预测会导致对某些群体的偏见。

例如，考虑来自不同群体(例如种族、性别)的两个候选人，他们具有相同的特征值集—他们上同一所大学，具有相同的工作经验和相同的技能集—并且他们已经从数据中删除了任何受保护或敏感的属性及其代理，但是他们每个人都具有不同的目标值，一个被雇用，一个没有被雇用。当相似的记录导致不同的标签时，模型将很难学习，因此将无法高度确定地预测结果。通过使用[改变相似记录的标签](https://core.ac.uk/download/pdf/81728147.pdf)的技术，你将因此改进模型的学习过程并减少预测中的偏差。

在不同的情况下，除了有偏差的标签，如果怀疑存在代理特征，[转换数据](http://sorelle.friedler.net/papers/kdd_disparate_impact.pdf)以显著降低或消除敏感属性和其他特征以及[目标](https://krvarshney.github.io/pubs/CalmonWVRV_nips2017.pdf)之间的相关性更适用。当数据中包含代理要素时，基于排除敏感属性的要素列表构建的模型仍然可以间接推断出单个记录与这些敏感属性中不同组的关联。例如，如果邮政编码或运动是要素的一部分，模型可以从记录中推断出种族或性别。这种推断使模型能够从数据中学习歧视行为，并将其编码到预测中。为了减轻这种情况，同步的特征变换和标记对于降低模型的推理能力是至关重要的。

正如我们在这里和之前的博客中所讨论的，这些技术有可能减少训练数据中的偏差。对于数据科学家由于公司政策或法律限制而无法访问敏感属性的情况，可以与数据所有者共享这些技术，以便在与数据科学家共享之前应用于数据。

不幸的是，由于这些技术对模型的数据推断的盲目性，某种程度的偏差仍然会蔓延到模型预测中。在本系列的下一篇文章中，我将通过对处理中和处理后建模阶段的技术进行同样的概述来解决这个问题，在处理中和处理后建模阶段，模型的推理被直接访问。

# 参考资料:

[1]卡米兰，费萨尔和考尔德斯，图恩。无区别分类的数据预处理技术。知识与信息系统，33(1):1–33，2012

[2] Calmon，f .，Wei，d .，Vinzamuri，b .，Ramamurthy，K. N .，和 Varshney，K. R .为防止歧视而优化预处理。神经信息处理系统进展 30，2017。

[3] M. Feldman、S. A. Friedler、J. Moeller、C. Scheidegger 和 S. Venkatasubramanian。验证和消除不同的影响。2015 年在 KDD。

[5]“成人——UCI 机器学习。”5 月 1 日。1996 年，【http://archive.ics.uci.edu/ml/datasets/Adult】T4。

[6] R. K. E. Bellamy 等人，“AI Fairness 360:用于检测和减轻算法偏差的可扩展工具包”，载于《IBM 研究与发展杂志》，第 63 卷，第 4/5 期，第 4:1–4:15 页，2019 年 7 月 1 日-9 月。