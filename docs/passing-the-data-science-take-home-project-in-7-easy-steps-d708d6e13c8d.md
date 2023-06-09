# 通过 7 个简单步骤完成数据科学带回家项目

> 原文：<https://towardsdatascience.com/passing-the-data-science-take-home-project-in-7-easy-steps-d708d6e13c8d?source=collection_archive---------23----------------------->

## 易于遵循的指南。

![](img/5ab14c2edb4775a70693b55a223bce83.png)

尼克·舒利亚欣在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

祝贺你，你通过了最初的面试，进入了数据科学项目！招聘人员在这一点上给了你一套极其模糊的指示。你可能会发现自己在凌晨 2 点盯着电脑，就像上图中的那个人。

> 这个项目应该只需要几个小时就可以完成，但是我们会给你一周的时间交上来

面试过程的这一部分不应该这么难。我将帮助您通过数据挑战，并成功进入面试流程的下一部分。

请记住，他们不希望你建立最成功的模型，他们有大量的资源，花费几个月的时间为手头的问题创建可行的模型。他们更关心你如何处理一个复杂的问题，你的代码、注释、解释和组织。

以下是数据科学项目中要遵循的 7 个步骤。

**对您的项目有帮助的其他有用信息。**

[](/know-your-audience-how-to-present-your-data-science-project-96a3c5d4d475) [## 了解你的观众。如何展示你的数据科学项目！

### 如何定义和调用将您的冗长代码隐藏在别处的函数。

towardsdatascience.com](/know-your-audience-how-to-present-your-data-science-project-96a3c5d4d475) 

# **1。简介**

S 挞着干嘛。为什么这个项目很重要，谁会从定义良好的模型和解决方案中受益？公司为什么会在意？

抓住机会展示您识别数据挑战的业务需求的能力。通常公司会给你一个和他们业务相关的题目。作为一名数据科学家，这是您将项目绑定到一个有意义的故事的机会。

*示例(欺诈案例模型):*

> 作为信用卡提供商，重要的是要有防范措施来打击欺诈。对于 2019 财年，欺诈交易占 150 万美元[从数据中收集]。这不仅会造成金钱损失，还会影响客户对公司保护他们的信任…

# 2.探索性数据分析

![](img/e529a37334742b98c9aeb201c2a1d98a.png)

照片由 [Isaac Smith](https://unsplash.com/@isaacmsmith?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

**探索探索探索！**

请记住，你的大量时间(在工作中)将用于争论数据。使用此部分创建一些图表并深入了解数据。

需要考虑的一些图表:

*   直方图(欺诈-非欺诈交易)
*   相关热图
*   一段时间内的平均交易。

**永远**记得探索缺失的数据。丢失信息是这个过程的一部分，能够识别它是至关重要的。要寻找的东西:

*   NA，Nan，空
*   空字符串" "
*   “缺失”或“空白”这个词

*现在不是创造新功能的时候。相反，使用这一部分来奠定基础。*

您应该花时间确定您将如何处理丢失的数据，要么丢弃它们(在丢弃它们时确保检查目标变量分布)，要么输入值(平均值、中值、众数)。

# **3。基线—简单模型**

我们如何确定我们的模型性能是成功的？成功是一个相对的术语。与当前流程相比，模型是成功的。例如，你可以建立一个准确率为 95% (65%)的模型，但是如果当前的方法准确率为 97% (55%)，你就没有增加价值。

这一部分将用于创建基线模型。这个模型将是基础，以便可以比较其他复杂的模型。因为这是你对这个问题的“第一次尝试”,它不需要过于复杂或微调。您可以在本节开始时声明，您将把数据扔给一个模型(简单模型),看看它做得有多好。

**解释，解释，解释！**

当选择基线模型(或任何模型)时，您必须解释为什么选择建模技术。没有正确的答案，但是有一个答案会说明你在建模之前就考虑到了这个问题。

一个可以接受的答案是:

> “这个模型既简单又直观，在过渡到更复杂的模型之前，它将是一个很好的基线。在向业务涉众解释模型时，简单性具有优势。”

最后，展示成功指标(RMSE、精确度/召回率、混淆矩阵、ROC 曲线)并(再次)解释它。**如果模型表现不佳，不要惊慌。**

# **4。特征工程**

现在，您可以开始根据现有数据创建一些新要素。提醒一下，他们不是在寻找一些抽象的赢得世界的特性。创建一些你认为重要的特性，并解释为什么你认为它们会有助于提高性能。其中一些特性将源自 EDA 部分，在这里您可以深入了解数据集。

继续我们的欺诈示例，这里有两个特征:

*   **Over_Avg** :当前交易>是否为平均交易？
*   **Credit_Util:** 卡内余额/信用额度

# 5.超参数调整和复杂模型

至此，您已经为业务问题奠定了基础。现在您正处于十字路口，您可以通过调整超参数和实现新功能来扩充基线模型，或者运行不同的模型(例如，从逻辑回归改为随机森林)。无论你做出哪个选择，一定要**解释**背后的原因。

如果时间允许，我倾向于两样都做。

![](img/679b52e5fec4fdd8be1878636eff95d5.png)

由[马库斯·温克勒](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

再次强调成功指标并解释结果。希望模型比基线表现得更好。

# 6.后续步骤

差不多了，再坚持几个小时吧！你可能很想回到第 5 步，对模型进行更多的调整，以获得“**完美的**”结果，但是在这个任务中没有所谓的完美。相反，如果你在这项任务上花了更多的时间，你应该概述下一步你会做什么。

需要考虑的写作内容:

*   为什么你的模型失败了——有证据表明过度拟合吗？
*   额外的超参数调整-使用交叉验证来搜索网格。
*   您希望开发的其他功能
*   平衡数据集，以便更好地表示每个类

当您概述下一步时，也包括一个您认为它将如何提高模型性能的简要描述。

# 7.结论

![](img/90a32a54544c7f90ecf637262e2bfdfe.png)

Ian Stauffer 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

请记住，您正在讲述一个数据故事。重申为什么这个项目很重要，以及你想解决的问题。总结您在探索部分收集的见解以及模型的表现。最后，解释你的模型将如何解决这个问题。

在你发出那个项目之前，一定要做一些最后的任务。校对你的演示文稿，确保在整个代码中都有注释，并且组织得很好。

**祝好运！**

感谢您的阅读，感谢您的评论和反馈。你可以在 LinkedIn 上找到我！