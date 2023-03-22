# 数据科学术语:数据插补

> 原文：<https://towardsdatascience.com/data-science-buzzwords-data-imputation-da093abf9c4d?source=collection_archive---------28----------------------->

## 数据科学有很多词汇需要学习。这是一个不到 5 分钟的数据插补快速总结。

## 它是什么，我们为什么需要它？

数据插补是指处理数据集中缺失的数据。我们需要它，因为有些算法不接受空值，还因为如果我们填充数据，我们可以建立更准确的预测模型。我们将在本文中探讨如何很好地填充这些数据。

![](img/37e000bec04962f48084fd07a03f6c6f.png)

苏阿德·卡玛丁在 [Unsplash](https://unsplash.com/s/photos/mind-the-gap?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

## 需要注意什么

首先，我们需要看一下我们的数据——缺失数据有趋势吗？

缺失数据主要有 3 类:

*完全随机缺失(MCAR)* —这是唯一可以验证的缺失数据类型。当数据是 MCAR 时，这意味着缺失的数据点绝对没有模式。这可以通过将数据随机分为已完成的行和缺少数据的行来检查。如果两个子数据集的特征不同，则意味着您的数据是 MCAR。

*随机缺失(MAR)——*当数据被标记时，意味着数据缺失是由于可以观察到的系统性原因，但与缺失数据本身无关。例如，在包含两列(年龄和性别)的数据集中，通过计算每一列的缺失值，您可能会注意到男性年龄中缺失的数据比女性多。

*非随机缺失(MNAR)* —当数据是 MNAR 时，这是因为在另一个因素和缺失数据之间存在关系。例如，如果你有一个调查，问他们的第一个宠物的名字，它可能会被那些从未养过宠物的人留为空白。有一个系统性的原因是数据缺失。

## 那么我们能对丢失的数据做些什么呢？

我将概述几种处理缺失数据的常用方法。还有很多，但这只是对你能做的一些事情的一个洞察。

*删除丢失的数据* —根据丢失的数据量，我们可以忽略丢失数据的行。如果当您有 10，000 行时，这只是数据的一小部分，也许是百分之几，这可能是最简单的选择，不会对您的结果产生太大影响。

*替换为数据的平均值* —这个有很多变化，取决于你在数据中找到什么。首先，我们有三种类型的平均值:均值、中值和众数。对于非数字数据，您当然不能使用均值或中值，因此您唯一的选择是用模式填充缺失的数据。然而，对于数字数据，所有三个平均值都是可能的。使用这些方法时需要注意的是，您是在人为地减少数据的方差，这可能会影响根据数据训练的模型在新数据上的表现。您选择的平均值取决于您的数据集，例如，如果缺少数据的列在其分布中有很大的偏差，您可以选择中位数。

这种方法可以用于整个数据集，也可以将其分解。例如，如果您试图用平均值填充年龄列，您可以取所有相关数据的平均值并填充空值，或者您可以查看另一列，假设您有一个性别列，并且您意识到男性的平均年龄为 25 岁，而女性的平均年龄为 35 岁，因此选择用两种性别各自计算的平均值来填充缺失的年龄值。但是请注意，您对数据集进行的分解越多，计算的开销就越大，花费的时间也可能越长。

*回归* —您可以使用回归技术，根据数据中的其他变量来预测空值。回归有许多不同的类型，这取决于数据的类型以及它们之间的关系。理论上，你可以使用任何合适的回归算法来估算你的数据。这是另一种计算开销很大的方法，具体取决于数据量和回归算法的复杂程度。

**还要考虑别的事情** …

M *多重插补* —为了补偿输入数据的潜在偏差，可以在计算值中引入一些自然变化。基于数据的分布计算变化；该算法可以估计所创建的值应该有多少变化。这是一种计算开销很大的方法，但值得考虑，尤其是如果您的数据来自一个可能会有自然变化的来源。

***要点:*** *确保只对训练数据进行计算，这样就不会有数据泄露。如果你用你的测试/验证数据进行计算，你可能会发现你的算法非常准确，但当你得到全新的数据时，你会得到非常低的准确性。*

## 带回家的信息

填充缺失数据的方法有很多种，根据数据集和缺失的数据量，您选择的方法会有所不同。你的插补算法越复杂，花费的时间就越长。在你估算的复杂性和它给你的回报之间进行权衡是很重要的。