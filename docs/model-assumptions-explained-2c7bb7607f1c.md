# 模型假设—已解释

> 原文：<https://towardsdatascience.com/model-assumptions-explained-2c7bb7607f1c?source=collection_archive---------27----------------------->

## 对于商业读者

听说过**模型假设**吗？它们是什么？为什么他们**重要**？模型是现实的简化版本，对于机器学习模型来说，这没有什么不同。要创建模型，我们需要做出假设，如果这些假设没有得到验证和满足，我们可能会陷入一些麻烦。

> 如果这些假设没有得到验证和满足，我们可能会陷入一些麻烦。

![](img/12a226807f9ef38e85233ad958ba5425.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上 [Marcin Jozwiak](https://unsplash.com/@marcinjozwiak?utm_source=medium&utm_medium=referral) 拍摄的照片

每个(机器学习)模型都有一套**不同的**假设。我们对**数据**、不同变量之间的**关系**以及我们用该数据创建的**模型**做出假设。**这些假设其实大部分都是可以验证的。因此，你一直想做的一件事就是问一问假设是否得到了验证。有些假设仅与**得出关于**关系**的结论**的**相关**(例如，温度上升 1 度表明冰淇淋销量增加 4%)，其他假设也与**相关**到**预测结果**(我们预测明天 x 的冰淇淋销量)。**

> 这些假设大部分实际上都是可以验证的。

让我们看看为最简单的模型所做的假设。线性回归。

## **假设 1:固定回归变量**

这实际上意味着，我们假设变量(输入数据)不是随机变量，而是固定的数字，如果我们重新进行实验(我们以同样的方式再次收集数据)，我们会得到同样的结果。

与固定回归变量相反的是随机回归变量，通常被视为从更广泛的人群中取样的数据。如果是这种情况，那么你只能根据数据得出“有条件的”结论。这意味着你可以得出同样的结论，但只是基于这些数据。您不能在数据集之外进行概化。

*结论* —如果你的数据是**人群**的(**代表**)，你就是**好**。否则，请尝试收集代表性数据，或者仅根据您创建模型的数据得出结论。

*对于商业读者* —如果你有所有客户的数据，并想预测新客户的行为，只要你的目标客户是相似类型的客户，你就没问题。如果没有，你可能会对这些新客户提供完全错误的建议或结论，并在获得他们之前失去他们。所以**向**询问**数据集**的**代表性**。

> 所以要求数据集的代表性。如果数据对总体有代表性，你就是好的。

## 假设 2:随机干扰，零均值

我们假设我们的模型的误差范围是随机的，并且在所有的观测中平均水平。这是你可以实际检查的东西。

*结论*——取所有误差项的平均值，并验证它在统计上是否明显不同于零。如果是→您可能希望**调整**您的型号，并且**包含更多**条款。

*对于商业读者*——你希望你的模型预测正确的事情。如果这个条件不满足，你要么总是 - **下的**，要么就是高估了**。例如，如果你的误差项平均为 3.5，这意味着你平均高估了 3.5。如果你预测股票价格并自动做出交易决定，这可不是一件好事。所以求误差项的平均值。**

> 求误差项的平均值，以了解你是高估还是低估了。如果平均分在 0 左右，你就是好的。

## 假设 3:同质性

扰动的方差存在并且相等。这意味着我们期望模型中的误差对于所有不同的数据点来说都具有相似的大小，有时也称为方差齐性。这仅适用于我们所观察的关系在所有不同层面上都是线性的情况。

例如，如果你在研究收入和旅游支出之间的关系。低收入人群的息差将比高收入人群的息差小得多，原因很简单，因为高收入人群将在消费方面提供更多选择。结果是你的模型被“拉”向了错误的方向(因为它假设传播在任何地方都是相等的，并试图减少误差)，高收入数据点对模型的影响比低收入数据点大得多。

此外，这将影响对参数的重要性做出结论的能力。

*结论* —如果你想用你的模型进行同质性推断测试，如果你发现你的误差项**不是均匀分布的** → **标度**(你的**变量** (s)之一)或者使用 **WLS** 。

*对于商业读者* —您希望误差项具有均匀的方差，否则，您的一些数据点可能会对模型产生太大的影响，并且**会干扰其余数据点的视图**。这不是什么大问题，你的模型仍然会预测正确的事情。因此，如果这是你所关心的，这是一个让滑。

> 如果你只是想预测，让这一个溜走。如果你想推断关系，最好做出改变。

## 假设 4:无相关性

误差项是不相关的。如果不是这样，实际上还有改进模型的潜力。这意味着，如果误差项存在相关性，仍然有“解释”的能力。违反这一假设的结果是模型系数的偏差。这些系数从误差项中“吸收”信息。

*结论*——如果你想使用你的模型进行推理，测试你的误差项中的相关性，如果你发现相关性→ **添加更多的变量。**

*对于商业读者来说*——如果你有兴趣对关系做出**结论**，用错误的术语来说**相关性**是不可行的**。误差项中的相关性也告诉你有一个**潜在的**来**改进**模型并生成**更好的** **预测**。**

> **如果存在相关性，你需要改进模型，你的预测会变得更好，你的推断也会有意义。**

## **假设 5:常数参数**

**您使用模型估计的参数是固定的未知数字。首先，如果他们是已知的，就不需要模型。我们之所以假设它们是固定的，是因为我们希望避免随着时间的推移而改变。这是指收集数据的时间。如果随着时间的推移有变化，我们可能需要包括两个不同的参数或只取最近的数据样本。**

**违规的一个例子是，如果通过询问客户向他们的养老基金支付了多少钱来收集数据，并且去年更改了年度最高金额，突然您可以再添加几千美元。在这种情况下，您的参数不是常数，您需要考虑这一点。**

***结论*——你能有把握地说手头的数据是由相同的过程产生的，没有随着时间的推移**改变**吗？→那你就好。如果不是→你会想要**调整**你的模型，并允许 n 个**新变量**进入。**

***对于商业读者来说—* 这里的关键是数据是由**相同的流程**产生的，数据收集是否随着时间的推移而改变？如果是这样的话，根据不同变量之间的关系得出的**结论**将**不成立**，并且**对即将到来的新数据的预测**实际上可能**被低估或高估**。**

> **随着时间的推移，数据收集是否发生了变化？然后调整模型，否则随着新数据的到来，你可能会高估或低估你的预测。**

## **假设 6:线性模型**

**不同变量之间的关系是线性关系。如果不是这种情况，你会有一个非线性的关系，你不能估计一个模型适合你的数据。因此，当您创建线性模型时，您需要假设线性。这不是一个线性关系，如果你这样对待它，你会估计许多人在 50 摄氏度的街道上。**

***结论*——测试线性度(散点图起作用),如果关系不是线性的→ **转换**你的变量或者使用**不同的模型****

***对于商业读者来说*——这种类型的模型**决定了**我们试图预测的内容和进入模型的内容之间的**结构**。如果结构不满足(在这种情况下是线性)，模型**无意义**。如果期望关系是线性的，可以进行逻辑思考。如果不是，并且如果测试告诉关系不是线性的→这是一个**不通过**并且模型需要调整以对关系以及预测做出结论。**

> **如果模型是线性的，但是关系不是线性的，你可以忘记推断和预测。**

## **假设 7:常态**

**这种假设认为误差项是正态分布的。我们希望验证这一点，因为我们希望能够对显著性进行测试，以及定义我们的置信区间。**

***结论—* 画出你的错误术语，并验证它们是否正常。如果**未正常分布****→再次检查您的**线性假设**。****

*****对于商业读者* —这个假设让我们可以告诉我们一些关于**我们对模型中的估计值有多确定**的事情。如果这个假设不成立，我们**无法**对**关系**做出**结论**，但是我们**可以预测**。****

> ****没有这个假设，我们就不能说我们对估计的参数有多大把握。我们可以根据新数据进行预测。****

****需要帮助吗？通过[https://aibridge.ch/contact/](https://aibridge.ch/contact/)联系我。****

****灵感来自:Christiaan Heij、Paul de Boer、Philip Hans Franses、Teun Kloek 和 Herman K. van Dijk 所著的《经济计量方法及其在商业和经济学中的应用》****

*****关于我:我是一名分析顾问，也是当地一所商学院“人工智能管理”研究的主任。我的使命是帮助组织利用人工智能创造商业价值，并创造一个数据科学家可以茁壮成长的环境。* ***报名参加我的*** [***通迅***](https://share.hsforms.com/1uW6l8qlsRYapxCl0Q_znIw4xzxr) ***获取关于 AI 管理的新文章、见解和祭品*** [***此处***](https://share.hsforms.com/1uW6l8qlsRYapxCl0Q_znIw4xzxr) ***。*******