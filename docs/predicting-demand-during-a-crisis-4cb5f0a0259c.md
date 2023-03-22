# 预测危机期间的需求

> 原文：<https://towardsdatascience.com/predicting-demand-during-a-crisis-4cb5f0a0259c?source=collection_archive---------50----------------------->

## 在不确定的世界中做出更好的需求计划决策

![](img/14149cb8fcddcffd0f451b3c35e62cbb.png)

Fikri Rasyid 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

鉴于我们全球供应链的[脆弱状态，预测制造什么、运输什么、储存什么在今天比在最近的记忆中更重要。鉴于过去三周我们看到的购买行为的转变，确保消费者能够在当地杂货店找到他们需要的产品极其困难:](https://www.theguardian.com/global-development/2020/mar/26/coronavirus-measures-could-cause-global-food-shortage-un-warns)

*   新冠肺炎封锁彻底改变了我们生活的方方面面，包括我们购物的内容、方式、地点、时间和原因
*   经过十多年的持续增长后，我们正在进入衰退
*   许多人做出购买决定是出于恐惧而不是需求

随着供应链重新成为焦点，许多企业都在努力理解为什么他们的需求计划流程不起作用，以及他们可以做些什么来修复它们。以下是我和别人谈过这个问题后的看法。

# 短期内，预测应该退居二线

在封闭的世界中，消费者需求有着根本的不同:历史数据和基于这些数据的建模基础设施不再代表我们今天生活的世界。某些产品类别将比其他类别更能感受到这种转变的影响，但我们可以假设 2020 年 2 月之前大多数产品商店的观察是有偏差的。许多人问，其他危机事件是否可以代表我们当前的情况(例如，飓风或暴风雪使人们在室内呆了一周；12 月/1 月来自中国的早期观察)，但这些事件和今天持续的全球封锁之间有太多的差异，我们无法相信这是事实。

不幸的是，留给我们的代表性数据样本非常少。集合模型(如 XGBoost)在如此小的样本量下可能会欠拟合，而时间序列模型(如 ARIMA)在零售商过去两周观察到的极端销售差异下会过拟合。在这种情况下能做些什么？

鉴于我们的观测数据如此之少，而形势发展如此之快，**我们不应指望在短期内可靠地预测未来**。这个疫情带来的文化和经济挑战才刚刚开始:我们现在开发的任何点估计都将非常不准确。即使我们在建模阶段很幸运，我们也没有足够的观测值来可靠地测量样本外误差。在我们有足够的数据来验证我们的预测方法之前，我们最好把时间花在别的地方。

# 在不确定性中做出明智的决策

鉴于我们无法再做出准确的预测，问题就变成了“在一个不确定的世界里，我们如何做出更好的供应链决策？”。

首先，我们应该强调**未来几周我们将做出的许多艰难决定没有“正确”的答案**。“完美是好的敌人”当然适用于这种情况:减少偏见，保持开放的心态，保持敏捷比在这个阶段纠结于数据更重要。

第二，我们应该**有目的地调整我们的心智模式**来进行需求规划。历史数据和稳定的预测应该打折扣，以利于新近加权模型、实时分析和已经在管理层得到验证的明智假设。我们衡量成功的方式可能必须改变，以 a)保持货架上关键消费品的可用性，b)避免可能影响我们核心业务的现金流问题。像这样的选择需要权衡，嵌入式数据科学团队非常适合就每个决策的相关风险提出建议。

最后，我们可以**建立专家系统和 ML 基础设施来提醒我们何时应该重新考虑我们的假设**。特别是像[帕累托/NBD 和帕累托/GGG](http://Resample your data) 这样的生成模型，可以讲述看似不稳定的购买行为背后丰富的故事。通过可视化它们随时间的后验分布，并观察它们的移动和形状变化，我们可以观察需求的转折点，并推断美国各地商店的真实情况。这些概率模型也不会给我们精确的点估计，但没关系:查看概率分布将有助于规划者自信地约束他们的决策。[所有型号都是错的](https://en.wikipedia.org/wiki/All_models_are_wrong)，但是我们的还可以用。

随着封锁解除，我们的生活变得更加确定，我们可以用短期贝叶斯预测、定制损失函数和新冠状病毒相关特征来改进我们的集合模型。在那之前，我们会做出明智的决定，将破产的风险降到最低。