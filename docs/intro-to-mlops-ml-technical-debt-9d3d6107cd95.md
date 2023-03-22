# MLOps 简介:ML 技术债务

> 原文：<https://towardsdatascience.com/intro-to-mlops-ml-technical-debt-9d3d6107cd95?source=collection_archive---------13----------------------->

## 我对 ML 工程师和数据科学家的建议

## 为什么 ML 会成为你最大的噩梦

![](img/f253a51e433b1d0944838f4b5fe9c655.png)

来源: [Unsplash](https://unsplash.com/photos/-2vD8lIhdnw)

# 你最大的噩梦

> (凌晨 3 点)快来！我们的定价全搞砸了！我们以 100 美元的价格出售 13，000 美元的相机！ [**亚马逊最佳黄金日**](https://www.washingtonpost.com/technology/2019/07/20/amazons-best-prime-day-deal-was-likely-an-accident/) 期间 ML 出错

假设你是亚马逊 ML 工程师之一，你的团队刚刚发布了一个新的 RNN 定价模型，根据购买趋势自动设置价格，你已经煞费苦心地回测和调整了无数次。你 2 年的努力终于有了成果，预计每年将产生 100 万英镑的额外收入。

你太高兴了，所以你订了一个昂贵的假期来庆祝。你在去巴哈马的路上，直到你收到…坏消息。

你的 ML 模型出了问题，错误地给所有商品定价。您疯狂地打开集成管理器进行回滚。但为时已晚，系统已经交货了；你的“尖端 ML 模型”让你的公司损失了 300 万美元。

第二天，您决定调试您的模型。你测试了模型。它看起来很好。价格分布有变化吗？资料准备有没有耍流氓？还是近期下游变化的质量数据？你疯狂地绞尽脑汁，但还是一无所知。因此，您决定用虚拟机和不同的配置文件隔离每个下游数据，从头开始重建模型，并再次逐个测试它们。你失去了对每个版本更新的跟踪，直到花了几个不眠之夜来修复问题。

> 在数据或集成变更期间，您最先进的 ML 模型变成了您最大的噩梦

# 输入技术债务

![](img/cc3ddea8ee5cf4fbad3dfdf8d2d6e56d.png)

来源[去飞溅](https://unsplash.com/photos/4kIM7ED8F1A)

> **技术债务**是在代码实施过程中所做的权宜决策的持续成本。它是由为了更早的软件发布和更快的上市时间的短期利益而采取的捷径造成的。技术债务倾向于复合。推迟工作以获得回报会导致成本增加、系统脆弱和创新率降低。

1992 年，沃德·坎宁安创造了这个术语来解释产品利益相关者对重构的需求。对于那些还不明白的人。技术债务是玛丽·近藤的反义词，说“让我们把脏衣服扫到床底下，问题就解决了”

![](img/93739e55fb71cc9054d382ba85f2fe3d.png)

来源( [giphy](https://giphy.com/gifs/netflix-konmari-mariekondo-tidyingup-fCUCbWXe9JONVsJSUd) )

同样，在人工智能和机器学习中，我们都倾向于增加技术债。我们喜欢做“忍者修复”，走捷径，比如硬编码功能、臭代码和不负责任的复制粘贴。如果您赶时间或交付概念证明(POC ),这些都是非常好且必要的。但是如果不付钱的话，这是非常危险的。

> 不是所有的债务都是坏的，但是未偿还的债务是复合的——
> 
> [D·斯卡利，在机器学习系统中的隐藏债务](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf)

我们的 AI 和 ML 是靠数据运行的。垃圾进垃圾出。您使用的功能越多，它就变得越不稳定，尤其是当这些功能依赖于系统的许多部分时。

## 你脆弱的军情系统

想象一下使用 CRM(客户关系管理)系统建立价格歧视的定价系统(类似于飞机票)。定价系统的质量将高度依赖于来自 CRM 的数据，缺失的功能将破坏 ML 中的所有结果。

现在，想象它通过更加互联的 ML 和其他系统连接到来自更多上游的特征。你的 ML 模型往好里说是脆弱的，往坏里说是破碎的，会影响到它的下游。

在一个快节奏的基于人工智能的创业公司中，这已经成为常态，因为他们疯狂地赶时间线，以实现他们的产品，并将其呈现给他们的利益相关者。我和一个在人工智能初创公司的朋友聊过，他提到他们从来没有使用适当的版本控制(Git)、问题跟踪(吉拉)或任何开发运营管理工具来开发他们的 ML 系统。令人震惊的是，许多其他人在没有适当的 DevOps 和技术债务管理的情况下跳入 ML/AI 炒作。这和用牙签造机器人是一样的。

> 对于软件工程来说，DevOps 很重要。但是对于 ML Productions 来说，MLOps 是不可分割的

# **4 大 ML 管道事故**

![](img/ff094372c55ed1def0c29b19c0ac0678.png)

来源: [Unsplash](https://unsplash.com/s/photos/deadend)

## **1)纠缠**

ML 系统是有数据的机器。通常很难做出孤立的改变(改变任何事情，改变一切——CACE)。这适用于特征工程、最大似然调整、正则化、数据采样等。

比方说，你的定价模型在除吸尘器之外的所有产品上都非常有效(因为它很烂:)。您通过提高清洁产品定价的敏感度来固定吸尘器的定价，但您发现您导致了定价分配与洗碗机不匹配。吸尘器的价格分布不适用于洗碗机的价格分布，洗碗机的价格分布更窄。您现在需要创建一个可能影响其他产品的不同规则。

你会意识到数据和见解是纠缠在一起的。不同的调优和模型公式将导致难以隔离的一般洞察力变化。

> 纠缠在一起的数据和系统会给隔离和调试问题带来困难

## 2) **复杂管道(管道丛林)**

人工智能和人工智能系统由许多不同的工作流管道组成，这些管道按顺序负责复杂的工作。您的 ML 系统将由许多工程师构建，并与许多不同的系统和数据源互连。

在一个适当的 ML 管道中，你将需要设计许多工作，包括抓取、生成数据、ETL、验证数据清洁度、交叉验证、监控性能和部署。很快你的模型就会变得非常复杂。如果没有合适的工具和标准的操作，在使用不同语言的多个系统和遗留系统之间进行简单的更改将需要几个小时。

> 复杂的管道导致您的工程工作缓慢且漏洞百出。如果治疗不好，你可能需要几个小时来做简单的改变。

## 3) **隐藏的反馈回路**

现实世界的系统最终影响了我们的数据。假设您的销售代表发布了一项营销活动，旨在接触儿童，并积极地将他们纳入您的定价模型所使用的 CRM 系统中。

ML 模型会感知到大部分顾客购买玩具。因此，ML 模型提高了玩具价格，并过度打折昂贵的产品。然而，监控你的价格飙升，你的竞争对手的定价模型也自动填充了玩具过高的价格市场。你的系统也会这样做，恶性循环就出现了。

> 隐藏的反馈循环给你的 ML 系统带来了麻烦，同时由于 ML 系统之外的相互关联的数据依赖，使得调试更加困难

## **4)脆弱的数据依赖**

想象一下，你的定价模型依赖于你的客户的性别。如果一个男生浏览化妆品，很可能他会买给妻子/女朋友作为礼物，所以支付意愿更高。你的机器学习已经准备好根据性别来决定定价了。

但是，您的业务代表在上游 CRM 中的“性别”功能之外添加了一个标签。如果你的 ML 系统看到的不是男性或女性的值，它会崩溃吗？现在模特会如何给化妆品定价？与代码依赖相比，这是非常脆弱的，因为这意味着无论何时上游系统被更新，您的模型都可能被破坏，并给出未被怀疑的特性。

> 在特征工程和标记过程中，由于语义不匹配，数据依赖性导致逻辑错误和质量下降。

# 支付你的 ML 技术债务

![](img/76dc537dab4a898410c55de347c05c20.png)

[资料来源:Unsplash](https://unsplash.com/photos/9upRLljfKP8)

技术债是一种痛苦。作为 Visa 的前数据工程师和谷歌的数据科学家，我必须确保一个适当可靠的渠道保持透明和负责。我需要一个标准的操作来管理机器学习的技术和数据方面，并确保质量不会随着时间的推移而下降。

## **有三个小技巧可以帮助您最大限度地减少 MLOps 技术债务。**

## **1)测试你的代码和数据**

测试是技术领域最重要但不性感的角色之一。考虑测试以限制技术债务并确保 ML 生产质量仍然非常重要。在 DevOps 中，我们学习了两种类型的测试:**单元测试(测试单一功能)**和**集成测试(测试集成功能**)。然而，在 MLOps 中，我们需要建立一个 canary 流程，在投入生产之前测试 ML 管道质量。这包括测试数据依赖预分析能力以识别看不见的数据(想象一下男性/女性性别的例子)。

## **2)测试训练和服务值的一致性**

训练模型时，您使用的是日志数据(预先记录/观察到的日志)。然而，在生产中，您将需要处理实时数据，由于时区(时间序列)、相机(图像)质量、语言等许多问题，这些数据可能会给出不同的值。跟踪记录的和实时的数据以确保质量一致性是非常重要的。

## **3)保守评分**

对你的 ML 模型的每个测试阶段进行评分。在四个不同部门应用管道健康评分:

*   **ML 基础设施:**测试下游和上游数据流质量。
*   **ML 模型开发:**测试模型不包含任何被人工确定为不适合使用的特征。
*   **特性和采样:**测试每个特性的分布是否符合您的预期。
*   **运行 ML 系统:**在训练和服务中测试所有创建输入特性的代码和数据质量。

所有这些阶段对于部署和维护模型都很重要。将每个阶段的最低得分作为整个系统的最终得分。在投入生产之前，确保您可以最大限度地提高最低评分，以建立正确的健康标准。

简单地说，对抗技术债务就是在你的 ML 管道生命周期中的任何时候清楚地了解它。这包括数据样本、模型生成、测试以及最终的部署。

> 如果做得正确，您将能够:快速开发，可预测地运行您的模型，并可靠地向您的客户交付价值。

# 下一步是什么…

关于本文的参考资料，请参考 D.Sculley 和谷歌团队的这篇论文。

我还将谈到 Tensorflow Extended (TFX)作为一个开源工具来启动和维护您的 ML 模型。这一框架已被许多大型科技公司广泛使用，如谷歌、Twitter 和 AirBnb。希望你能和我的媒体频道保持同步。

我相信了解这一点是将你的 ML 努力转化为强大而有效的 ML 系统的第一步。

# 最后…

我真的希望这是一本很棒的读物，是你发展和创新的灵感来源。

请**在下面评论**提出建议和反馈。就像你一样，我也在学习如何成为一名更好的数据科学家和工程师。请帮助我改进，以便我可以在后续的文章发布中更好地帮助您。

谢谢大家，编码快乐:)

# 关于作者

Vincent Tatan 是一名数据和技术爱好者，拥有在 Google LLC、Visa Inc .和 Lazada 实施微服务架构、商业智能和分析管道项目[的相关工作经验。](https://bit.ly/2I8jkWV.?source=post_page---------------------------)

Vincent 是土生土长的印度尼西亚人，在解决问题方面成绩斐然，擅长全栈开发、数据分析和战略规划。

他一直积极咨询 SMU BI & Analytics Club，指导来自不同背景的有抱负的数据科学家和工程师，并为企业开发他们的产品开放他的专业知识。

最后，请通过 [**LinkedIn**](http://www.linkedin.com/in/vincenttatan/?source=post_page---------------------------) **，**[**Medium**](https://medium.com/@vincentkernn?source=post_page---------------------------)**或** [**Youtube 频道**](https://www.youtube.com/user/vincelance1/videos?source=post_page---------------------------) 联系文森特