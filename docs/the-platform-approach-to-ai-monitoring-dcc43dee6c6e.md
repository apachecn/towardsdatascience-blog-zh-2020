# 人工智能监控的平台方法

> 原文：<https://towardsdatascience.com/the-platform-approach-to-ai-monitoring-dcc43dee6c6e?source=collection_archive---------54----------------------->

## 不要相信开箱即用的监控解决方案。你的意见至关重要。

![](img/bf3a61a9f2bdd2508c22022c0dd8b007.png)

资料来源:莫纳实验室公司。

如果你一直在努力让你的人工智能模型在生产中的表现变得透明，你在一个好公司里。监控复杂的系统总是一项挑战。监控具有内在不透明性的复杂人工智能系统是一个根本性的挑战。

随着企业中人工智能方法、底层技术和用例的激增，人工智能系统正变得越来越独特。为了满足他们的业务需求，每个数据科学团队最终都会构建一些非常独特的东西；每个人工智能系统都是一片雪花。

人工智能技术、使用案例和数据环境的巨大多样性消除了一刀切的监控解决方案的可能性。例如，自主监控解决方案通常是不够的，因为它们自然不会扩展到少数用例之外。对于这些解决方案来说，扩展或扩展是一个巨大的挑战，因为要在没有用户上下文的情况下监控人工智能系统，人们必须对指标、它们的预期行为以及它们发生变化的可能根本原因做出大量假设。

一个显而易见的解决方案是为每个用例构建独立的点解决方案，但是这是不可扩展的。那么，有没有一个框架或解决方案是为(几乎)所有人设计的呢？

***是的。这是平台方法。***

# 监控黑匣子的平台方法

人工智能系统监控的平台方法是*通用自主方法*和*定制方法*之间的最佳点。这意味着，一方面，监控系统根据用户人工智能系统的独特特征进行配置，另一方面，它可以毫不费力地进行扩展，以满足新的模型、解决方案架构和监控环境。

这是通过实施通用监控构建模块来实现的，然后由用户动态配置，以实现定制的专用监控解决方案。这个监控环境适用于任何开发和部署栈(以及任何模型类型或 AI 技术)。此外，由于监控平台是独立的，并且与堆栈分离，因此它可以实现超级快速的集成，不会影响开发和部署流程，更重要的是，监控可以跨越堆栈中的所有层。

系统的可配置性意味着数据团队不局限于他们系统的预制定义:他们实际上由一个“工程部门”授权，该部门给予他们对监控策略和执行的完全控制。

# 灵活、适应性强的解决方案

除了平台方法可以解决行业的监控问题之外，其无限的灵活性以行业特定的自主解决方案所不具备的方式使用户受益。这听起来可能是一个反直觉的假设，因此这里有几个不可知系统中固有的特性的例子，这些特性通过自主解决方案根本无法实现，即使这些特性是行业特定的:

**通过上下文(或系统)监控，而不是通过模型。**如果在模型运行一段时间后，您获得了基本事实(或关于成功/失败的客观反馈),那么您会希望将新信息与推理时捕获的信息关联起来。这种场景的一个例子是营销活动目标模型，该模型接收关于活动成功的反馈(转化率、CTR 等)。)几周之内。在这样的用例中，我们希望监控能够将模型的预测和业务结果联系起来。

如果您正在比较运行在相同数据上的两个不同的模型版本(在“影子部署”场景中)，那么通过上下文进行监控也是非常宝贵的。

如果您有多个运行在相同数据上下文中的模型，并且可能相互依赖，那么您需要有一种方法来推断一个模型失败的真正根本原因是否与另一个模型相关。例如，在 NLP 设置中，如果您的语言检测模型的准确性下降，下游的情感分析模型也可能表现不佳。

**配置你的异常检测。**异常总是在上下文中出现，因此在许多情况下，明显的异常(甚至表现不佳)是可以接受的，数据科学家可以忽略它。配置您的异常检测的能力意味着监控解决方案不会简单地检测一般的性能不佳，而是定义哪些定制配置的异常可能指示性能不佳。

![](img/02132de189b12b6dbb4c941649fcfe09.png)

来源:莫纳实验室公司；人工智能监控中有三种异常类别:异常值(左)、漂移(中)、突变(右)

比如:你分析推文的情绪。监控解决方案发现，20 个字符以下的推文(短推文)的预测可信度降低。你可能会接受这种缺点(例如，如果这符合客户的期望)。然后，您的监控解决方案应该使您能够从分析中排除这一部分(短推文)，以避免扭曲其余数据的测量结果(如果短推文占数据的很大一部分，这一点尤为重要)。

在任何阶段跟踪任何指标。最常见的情况是，团队会跟踪和检查模型精度和召回率(这需要“标记数据”)。即使没有这样的“基本事实”,也可能有许多重要的指标需要跟踪，这些指标可能指示模型的不当行为。例如:如果您有一个文本类别分类器，您可能希望跟踪没有类别得分超过某个阈值的推文的相对流行程度，作为低分类置信度的指标。这种度量需要从原始结果中计算出来，因此它不是微不足道的，并且不是现成的。

此外，可以根据度量行为可能发生变化的多个维度对每个度量进行进一步细分(例如，如果您的度量是文本分类置信度，那么维度可能是文本的长度或编写文本的语言。)

此外，如果您只关注模型的输入和输出，那么您会错过对您的预测可能不重要但对治理却至关重要的维度。例如:种族和性别不是(也不应该是)贷款算法中的特征，但它们是评估模型行为的重要维度。

# 没有人比你更了解你的人工智能

一个强大的监控解决方案可以为您的人工智能系统提供真实、有价值的见解，它需要与您独特的技术和环境相关，并且能够灵活地适应您的特定用例以及未来的开发需求。

这样的系统应该是 stack **不可知的**，所以你可以自由地使用任何技术或方法进行生产和培训。它需要全面地看待你的人工智能系统**，这样特定的生产和性能领域就不会被视为筒仓，而是在整个系统的**环境中**。最重要的是，它需要在您独特的背景下审视您的系统，只有您能够提供和微调。人工智能监控的平台方法旨在实现这一目标。**

***原载于 2020 年 8 月 12 日*[*https://www . monalabs . io*](https://www.monalabs.io/mona-blog/platformapproach)*。***