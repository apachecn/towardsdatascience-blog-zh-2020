# 如何在你的预测模型中加入偏见

> 原文：<https://towardsdatascience.com/how-to-incorporate-bias-in-your-predictive-models-d9fef364ece2?source=collection_archive---------49----------------------->

## 不要做这些事情，除非你想要一个有偏见的生产模型，做出不准确的，有时是昂贵的预测。

![](img/cf97a5522a08bf22e4783a34b609e5de.png)

[廷杰伤害律师事务所](https://unsplash.com/@tingeyinjurylawfirm?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

你真的不想让一个有偏见的模型为你做预测，是吗？尽管有大量高质量的机器学习(ML)实践者和技术进步，但现实生活中不乏 ML 失败。

让我们先回顾一下这些引人注目的 ML 和 AI 失败，其中潜在的偏差模型是失败的原因之一，如果不是主要原因的话，然后再讨论可能影响预测模型的偏差来源。

## 英国 GCSE 和 A-Levels 成绩惨败

由于新冠肺炎停课，英国学生今年没有参加 GCSE 和 A-Levels 考试。相反，英国考试监管机构 Ofqual 利用一种算法来确定学生的预期成绩，其基础是:

*   由学生的老师确定的估计分数
*   与同一所学校中具有相似估计分数的其他学生的相对排名
*   学校在过去三年中每一科目的表现

然而，在 8 月 13 日公布成绩的那一天，发生了一场彻底的灾难:将近 40%的 A-Levels 成绩低于老师的评估。这引起了相当大的骚动，导致政府在 8 月 17 日来了个 180 度大转弯，宣布将修改学生成绩，以反映最初老师的评估和模型输出中的较高者。

## IBM 的“肿瘤学沃森”的失败

2013 年 10 月，IBM 与 MD 安德森癌症中心(MD Anderson)合作，基于其沃森超级计算机开发了一种人工智能解决方案来治疗癌症。然而，它辜负了人们的期望。

福布斯【2017 年 2 月报道称，MD Anderson 搁置了其 Watson for Oncology 项目，并积极寻找其他合作伙伴取代 IBM，继续其未来的研究。2018 年 7 月晚些时候，STAT 的一份[报告显示，基于对 IBM 内部文件的分析，沃森提出了多项完全错误的癌症治疗建议，一些客户报告了“多个不安全和不正确治疗建议的例子”。](https://www.statnews.com/2018/07/25/ibm-watson-recommended-unsafe-incorrect-treatments/)

## 亚马逊的厌女症人工智能招聘

亚马逊的工程师在 2014 年开始开发一种自动化招聘工具，以审查求职者的简历。然而，路透社[在 2018 年报道](https://www.reuters.com/article/us-amazon-com-jobs-automation-insight/amazon-scraps-secret-ai-recruiting-tool-that-showed-bias-against-women-idUSKCN1MK08G)称，到 2015 年，“该公司意识到其新系统没有以性别中立的方式评估软件开发人员和其他技术职位的候选人”。

显然，该模型是根据 10 年来主要来自男性的求职申请进行训练的，这表明了当时男性在科技行业的主导地位。该项目随后被搁置，该团队于 2017 年初解散。

# ML 模型中偏差的来源

特定的 ML 模型可能会以一种微妙的方式产生偏差，其他的则不会——如上所示。模型有偏差的一些潜在原因包括:

## 有偏数据/采样偏差

有偏见的训练数据最终会变成有偏见的模型——这是 GIGO 的格言！这在上面的亚马逊例子中很明显，训练数据中女性申请者的短缺迫使模型优先考虑男性申请者。该模型没有足够性别公正的数据来进行训练和学习。这些数据往往反映了社会的现状和当前的偏见(不管是好是坏)。

适当的数据收集和采样策略对于确保获得相关的、有代表性的、合适的和足够多样化的数据至关重要。数据科学家 80%的工作都围绕着数据收集和特性工程，这是有原因的。

## 算法偏差

ML 算法由于其各种与基础训练数据无关的数学和统计假设而具有其自身固有的偏差。有偏算法更严格，假设并要求严格定义的数据分布，并且更能抵抗数据中的噪声。然而，他们在学习复杂的数据时会有困难。相比之下，偏差较低的算法可以处理更复杂的数据，但通常不适用于生产中的数据。

这种冲突的情况通常被称为偏差/方差权衡。它需要 ML 从业者进行微妙的平衡，以确保最佳的偏差(根据定义，还有方差)。

## 排斥偏差

当我们从数据集中排除特定的特征或变量时，就会发生这种情况，因为我们错误地假设它们对手头的预测问题没有用，而没有首先验证该假设。

在丢弃任何特征之前，始终测试预测值和目标变量之间的相关性。我在[之前的一篇](/how-to-find-the-best-predictors-for-ml-algorithms-4b28a71a8a80)文章中提到了针对各种变量类型的一些特征选择策略。

## 测量偏差

例如设备的错误测量会导致数据的系统性失真和测量偏差。例如，如果称重设备始终少报相同数量的重量，那么利用该故障设备产生的数据的任何模型都将是不准确的。带有“引导性”问题的设计不当的调查是测量偏差的另一个常见来源。

## 观察者偏差

当数据收集或特征工程策略受到数据分析师的先入为主(通常是错误的)观念的影响时，就会出现观察者偏差。例如，如果我对悉尼人有偏见(我不是)，那么我可能会让我的偏见以潜意识的方式潜入我的数据。观察者偏见的一个经典例子是伯特事件。

检测观察者偏差通常很困难，但是可以通过结合培训和筛选策略以及明确定义和实施的政策和程序来防止。

## 反馈回路

考虑一个 ML 模型，它以某种方式影响数据的生成，然后被用于预测。因此，模型做出的预测会偏向于它有发言权的数据。然而，这种反馈循环也可以是一种设计特征，而不一定是一个值得关注的原因——通常在内容个性化和推荐系统中。

## 系统漂移

在这个上下文中，漂移指的是生成用于建模的数据的系统或应用程序随时间的变化。例如，延迟支付的业务定义的变化(在违约预测问题的情况下)或用户交互的新模式的增加。

通过适当的变更管理和错误跟踪实践以及定期的模型更新和培训，这种偏差是最容易防止和检测的。

# 结论

以上是可能影响预测模型性能的一些潜在偏差来源。根据我的经验，通过评估和重新评估数据收集和采样策略，以及彻底的测试/验证程序，可以充分处理上述大部分问题。

如果您想讨论任何与数据分析、机器学习、金融或信用分析相关的问题，请随时联系 [me](https://www.finlyticshub.com) 。

下次见，摇滚起来！