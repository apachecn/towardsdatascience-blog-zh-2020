# 贝叶斯网络和合成节点

> 原文：<https://towardsdatascience.com/bayesian-networks-and-synthetic-nodes-721de16c47e2?source=collection_archive---------37----------------------->

之前，我已经直观地介绍了什么是 bn以及如何构建它们。在这篇文章中，我给出了一个更正式的观点，并讨论了建模的一个重要元素:合成节点。

虽然神经网络基于可用数据给出答案，但贝叶斯网络(BNs)包括与我们的研究相关的非样本或先验人类专业知识。通常，采访专家询问几个参数的影响是收集所有信息的最佳方式，这使得贝叶斯网络比其他技术更丰富。将这种专业知识与样本数据相结合使这种技术变得强大。此外，他们提出了模型的图形表示结构，在这种情况下，这比神经网络等黑盒模型更好。更容易解释获得的结果并与专家交流:当与不是建模技术专家而是商业领域(即医疗保健或风险管理)专家的人一起工作时，这提供了优势。BNs 的另一个优势是它们能够通过专家知识和原始数据来构建，即使先前的知识是不完整的。可以从专家的知识开始，用数据提炼，然后用专家的知识进行反馈，等等。

# 贝叶斯网络综述

贝叶斯网络(BN)是概率模型的一部分，该概率模型通过图表示一组变量及其依赖关系，即一对 G = (V，e)，其中 v 是不同节点的有限集合，E ⊆ V×V 是弧的集合。有序对( *u，v* ) ∈ E 表示从节点 *u* 到节点 *v* 的有向弧， *u* 被称为 *v* 的父节点， *v* 是 *u* 的子节点(Pearl 1988)。

BN 通常是表示概率因果关系的有向无环图(DAG ),其中节点表示变量，弧线表示变量之间的依赖关系。更准确地说，节点是随机变量的状态，从父节点指向子节点的弧线是两个节点之间的因果条件依赖。假设父节点状态的概率不同，则因果关系由节点状态的概率表示。

BN 使用条件概率来描述事件。任何关于事件或假设的不确定性的信念都是暂时的。这被称为先验概率或“P(H)”。这个先验概率被新的经验“e”更新，提供了关于“H”的不确定性的修正信念。给定证据的新概率称为后验概率或“P(H|e)”。贝叶斯定理描述了后验概率和先验概率之间的关系“P(e|H)”是假设假设为真，证据为真的概率，而“P(e)”表示在所有可能的假设下，新证据为真的概率。

![](img/f4a1764b93b11f7fcc475146c0060874.png)

条件概率表(CPT)展示了节点之间的概率关系。下图在三个基本图表上显示了这种关系。在这个例子中，每个节点有两种状态:真(T)和假(F)。该图还显示了每个节点配置的不同 CPT。

![](img/c2d6a28b42a0c61d52cb244d97017b06.png)

三个基本的 BN 模型

对于 BN，条件概率分布可以表示为一组参数:

![](img/c2366c7f34d8abece4eea004878c72e0.png)

其中 *i* = 1，…， *n* 定义每个节点； *k* = 1，…，r *i* 定义每个 r *i* 变量值(节点的状态)；并且 j= 1，…，qi 定义了父变量节点的 qi 变量配置的集合(例如上图中的每个图形配置)。因此，对于父节点的 q 个 *i 个*有效配置中的每一个，存在具有向量的多项式分布

![](img/18c1a7a4913d6bb8678011a11d2781db.png)

例如，在上图的*共同效果*图中，黄色 P(Z=T | X=T，Y=F)中的参数表示假设 X 为真，Y 为假，Z 为真的条件概率。

BN 配置的参数化需要矢量的完全估计。随后，两种类型的分析是可能的:(1)反向推理，它允许给定的一个观察发现最可能的原因中的假设(诊断)，和(2)自上而下的推理，它允许估计概率的一个观察给定的假设(预测)(Pearl 1988)。

# 使用合成节点

在 BN 中，对于由 *pa* (Xi)表示的节点 Xi 的一组父节点，节点值的联合概率分布可以写成每个节点及其父节点的局部概率分布的乘积:

![](img/db8d2d1a011fde2ccefc38fe4d4f019e.png)

计算目标节点的概率分布所需的变量的数量随着父节点的数量及其状态的数量而增加，这是耗时的。合成节点应该减少计算目标节点 CPT 所需的数据量。正如(康斯坦蒂努等人，2016)提到的，*“合成节点是一个简单地由它的父节点的值使用一些专家驱动的组合规则*定义的节点”。因此，合成节点对于减少因果复杂性和 CPT 中组合爆炸的有害影响是有用的。此外，这些节点改善了 BNs 的结构，即因果关系的可视化。通过使用合成节点，CPT 的大小和复杂性“*大大降低，提高了模型的计算速度和准确性*(Fenton 和 Neil 2013)。

例如，上图(a 部分和 b 部分)显示了从简单网络开始使用合成节点的方案。在这个例子中，网络有四个变量 a、b、c 和 d，每个变量有四个状态，计算 P(A|D，b，c)的 CPT 的概率值的数目是 4^4 = 256。相反，通过引入合成节点 s，该计算可以简化为两个表 P(A|B，s)和 P(S|C，d)。现在，该模型需要使用 4^3 + 4^3 = 64 值而不是 256 值来计算 s 和 a 的两个 CPT。

![](img/52d7caf73c19fd6881736f68bc68a52f.png)

(Neil 等人，2000)中描述的合成节点的使用示例

*“从从业者的角度来看，考虑到当前算法的准确性和速度，使用最新的软件工具编译和执行 BN 的过程相对来说没有痛苦。然而，为特定问题构建完整的 BN 的问题仍然存在，即* ***如何构建图结构以及如何为图*** *的每个节点定义节点概率表。”*(尼尔、芬顿和尼尔森 2000)。

# 感谢阅读！！

如果你想理解贝叶斯网络的逻辑(一个更基本的信息)，我推荐你这篇文章:

[](/will-you-become-a-zombie-if-a-99-accuracy-test-result-positive-3da371f5134) [## 贝叶斯思维导论:从贝叶斯定理到贝叶斯网络

### 假设世界上存在一种非常罕见的疾病。你患这种疾病的几率只有千分之一。你想要…

towardsdatascience.com](/will-you-become-a-zombie-if-a-99-accuracy-test-result-positive-3da371f5134) 

如果你想了解构建贝叶斯网络的参数(和超参数)是什么，我建议你这样做:

[](/the-hyperparameter-tuning-problem-in-bayesian-networks-1371590f470) [## 贝叶斯网络中的超参数调整问题

### 在这段历史中，我们讨论了在基于贝叶斯理论建立模型时要考虑的结构标准

towardsdatascience.com](/the-hyperparameter-tuning-problem-in-bayesian-networks-1371590f470) 

**参考书目**

康斯坦蒂努、安东尼·科斯塔、诺曼·芬顿、威廉·马什和卢卡斯·拉德林斯基。2016."从复杂的问卷调查和访谈数据到用于医疗决策支持的智能贝叶斯网络模型."医学中的人工智能 67:75–93。[](https://doi.org/10.1016/j.artmed.2016.01.002.)

*芬顿、诺曼和马丁·尼尔。2013.用贝叶斯网络进行风险评估和决策分析。Crc 出版社编辑。*

*尼尔、马丁、诺曼·芬顿和拉斯·尼尔森。2000."建立大规模贝叶斯网络."知识工程评论 15(3):257–284。[*https://doi.org/10.1017/S0269888900003039.*](https://doi.org/10.1017/S0269888900003039.)*

**珠儿，朱迪亚。1988."智能系统中的概率推理."摩根考夫曼圣马特奥。*[*https://doi.org/10.2307/2026705.*](https://doi.org/10.2307/2026705.)*