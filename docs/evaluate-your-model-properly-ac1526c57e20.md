# 正确评估你的模型

> 原文：<https://towardsdatascience.com/evaluate-your-model-properly-ac1526c57e20?source=collection_archive---------51----------------------->

## 这不全是统计数据

我们在机器学习方面看到的进步是不可否认的，在任何一周，我们都看到新的算法被研究和理论化，新的库被发布到开源社区，新的准确性基准被超越。毫无疑问，数据科学社区正在开发越来越擅长优化目标的工具。但这不是我今天想谈的。当我们越来越擅长达到目标时，我想问这个目标是否一直是正确的。随着模型拟合变得越来越复杂，模型评估似乎保持不变。这似乎是有道理的，因为只有这么多的指标可以用来评估模型的预测，但实际上，模型评估不仅仅是统计误差和偏差。

让我们看一个真实的例子。当我们观看比赛时，我们通过单圈时间来衡量赛车性能，这是速度和操控性以及其他更详细指标的函数。当我们买车时，它能跑多快可能不是我们评价标准中最重要的。当我们考虑投资一家汽车公司时，他们的车能跑多快几乎无关紧要。在定义明确的比赛环境中，简单的速度指标至关重要，但随着我们进入更广泛的背景，它的重要性逐渐减弱。这个简单的例子告诉我们，我们的评估标准会根据我们所处的环境发生显著变化，我们以前都经历过。然而，当涉及到机器学习模型和数据科学项目的评估时，这个简单的逻辑似乎被层层的技术概念所掩盖。

![](img/9f0fd927f968be9db6e33521c66b2900.png)

威廉·沃比在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

我经常看到的当前方法是试图向一位企业高管解释，为什么将均方根误差提高几个百分点很重要。这类似于我们试图决定是否应该投资一家汽车制造商，因为如果我们继续前面的例子，他们的新车在最高速度上有轻微的改善。难怪关于技术度量改进的对话从未真正传达给高级涉众。我认为值得注意的是，我并不是说技术指标不重要，它们绝对重要，但是当我们从技术解决方案转移到业务解决方案时，我们需要相应地度量正确的指标。

# 衡量什么是重要的

到目前为止，我们应该已经知道，在高效地进行数据科学研究时，提出正确的问题并找到正确的问题来解决是非常重要的。但是，在评价的时候，我们往往不会在另一边跟进。例如，如果我们想要评估客户流失预测模型是否有助于留住客户以增加经常性收入。了解客户流失的可能性只是等式的一部分。我们还需要考虑其他因素，比如我们能在多大程度上说服客户不要流失，这样做要花多少钱，我们有什么资源等。最终，我们应该根据保留的预测收入来评估我们的模型，因为这是我们所关心的。使用正确的指标将确保我们不会浪费时间优化无关紧要的事情。

这一点经常被忽视，因为不像建模算法，我们可以安装一个库并使用，没有标准的度量标准可以完全适用于我们的具体情况。作为分析专业人员，这是我们需要花时间思考什么是正确的评估标准的地方，因为我们有责任确保我们的解决方案在付诸实践时是有效的。

# 开始的时候要有目的

我经常看到的另一个常见的陷阱是，我们在没有确定如何评估输出的情况下就开始分析。毫无疑问，直接进入项目是令人兴奋的，但如果我们不预先定义评估标准，我们可能会偏向于我们已经建立的解决方案，因为我们致力于它。在我们开始构建解决方案之前设计评估流程并标准化评估流程，可以确保我们客观地评估不同的想法。

# 选择的悖论

有多少次，当涉及到模型诊断时，我们发现自己迷失在度量的海洋中。以一个简单的分类问题为例，我们可以使用混淆矩阵、ROC 曲线和 F1 分数等来评估模型。正如我们之前所讨论的，这些指标都不应该是我们用来评估模型的最终指标，因为它们不能反映全部情况，但是这并不意味着它们没有帮助。这些诊断度量使我们能够理解模型正在做什么，并且它们帮助我们识别我们可以迭代的改进区域。理解什么样的指标对什么样的场景有用，以及理解它们之间的关系是很重要的。

# 找到正确的业务指标

数据科学是使用数据解决业务问题的过程。我们了解将业务问题转化为可以用数据解决的技术问题的重要性，我们还需要了解我们需要将结果转化为更广泛的公司能够理解的业务问题。这是一个建立业务模型、理解不同业务部门之间的关系以及什么指标对他们来说是重要的过程。虽然这看起来不像是一个“技术性”的练习，但这是将一个表现良好的模型转化为有用的解决方案的关键部分。这也是领域专业知识发挥作用的地方，因为这将有助于将技术指标转化为业务指标。

# 回归基础

与算法开发不同，模型评估与复杂性和寻找更好的优化方法无关。模型评估是关于简单性和找到性能的正确表示。如果一个好的机器学习模型是一辆快车，那么一个好的模型评估就是一个好的导航系统。如果我们想到达正确的目的地，我们需要同时关注这两个方面。所以下一次，当你构建一个解决方案的时候，回到基础，想想什么样的指标是重要的，以及你如何用它来评估你的方法。

*如果你喜欢我的内容并分享我对这个话题的看法，请在 https://jchoi.solutions/subscribe*[](https://jchoi.solutions/subscribe)*注册*