# A/B 测试实用指南

> 原文：<https://towardsdatascience.com/the-practical-guide-to-a-b-testing-28c8b3235905?source=collection_archive---------47----------------------->

## 你的统计学课本没有让你做好准备

![](img/e3062c267f6052de027de83e573952bd.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由[路易斯·里德](https://unsplash.com/@_louisreed?utm_source=medium&utm_medium=referral)拍摄的照片

[**我在 Squarespace 担任数据科学家期间，花了很多时间在 A/B 测试上**](https://www.conordewey.com/blog/tips-practical-ab-testing/) 。许多人对实验不屑一顾，认为这是“分析工作”,并且对此不太感兴趣。对我来说，A/B 测试是更多地参与产品开发的一种方式，并对出货的产品产生重大影响。老实说，我真的很喜欢。

我很早就意识到，你在统计学教科书上学到的东西和实验在实践中的运作方式之间存在着巨大的不匹配。在 A/B 测试中取得成功并不取决于分析方法。是流程和人的问题。

# 知道你在做什么测试

这不是关于 t 测试或 z 测试。这不是贝叶斯和频率主义方法的问题。除了你选择如何评估结果之外，还有不同种类的 A/B 测试。首先，你必须设定实验的背景。**测试前的不确定性导致测试后的错误决策。**

好的 A/B 测试分为三类:大赌注、健康检查和迭代。先说大赌注。这些测试会以某种方式对你的主要指标产生很大的影响。可能有一些尚未被证实的假设驱动着这个实验。这里有一个问题:如果变体和控制之间没有显著的区别，你会遵从控制。发布没有影响力的特性会导致产品混乱，并浪费时间来维护代码。

![](img/d8e0b6773aacb139581e040d70450e1f.png)

远离危险区域

像大赌注一样，健康检查是产品中相当大的变化。它们的不同之处在于测试的上下文。这些都是你想要推出的新功能或大的产品变化。它们可能是组织内较大计划的最小可行版本，或者它们只是为用户提供了更好的体验。您不需要检测出显著的差异来发布这些更改。您只需要确保它们不会有意义地损害度量标准。思考这些测试的一个聪明的方法是，第一个版本代表了这个变体可能的“底线”。当然，这取决于后续工作流程。如果没有“下一步”的愿景，那么这是一个危险信号，你可能会把一个大赌注误认为是一次健康检查。

好的 A/B 测试落入的最后一个绑定是迭代。当大多数人想到 A/B 测试时，想到的就是这个。这就是我们熟知并喜爱的 [50 种蓝色](https://www.theguardian.com/technology/2014/feb/05/why-google-engineers-designers)的例子。不要期望这些测试会产生巨大的影响，但是如果你有足够的流量，它们会很强大。值得注意的是，对于大多数组织来说，这是一个很大的“如果”。在这里认真对待功耗分析。如果测试需要 2 个月的时间，那么它还不足以成为 A/B 测试的优势。**那里有更低的悬挂，更有影响力的水果。**

在上面的可视化中，还有一个象限我没有触及。危险区域是当您预期对您的主要指标有小的影响，但即使没有显著差异也愿意推出它。如果你是谷歌，也许这是有道理的。如果你不是谷歌，这是一个不必要的预防措施，会占用带宽，导致没有可操作的结果。为了安全起见，我通常建议首先推出这一阶段的测试，然后在之后监控指标。

# 把一切都写下来

在开始 A/B 测试之前，你有很多理由想把所有的事情都写下来。这不是一个新颖的建议，但它也是我不得不提及的许多常见失误的根本原因。

**大规模进行 A/B 测试是一项跨职能的努力。**可能会涉及数据科学和分析、产品、工程，可能还包括设计。对于所有这些不同的接触点，你需要一个“真相来源”文档。这是你可以给人们指出足够的背景的东西。

考试前把事情写在纸上的另一个好处是——它帮助你避免偏见。产品负责人应该清楚地陈述他们运行测试的假设和前提。这有助于其他人回顾并确保他们理解。在测试完成后拥有它也很好，这样你就可以很容易地检查假设是有效的还是无效的。

最后，文档是关键。在一个集中的、可搜索的地方保存这些 A/B 测试文档的运行日志将会在以后带来巨大的好处。这变成了你在构建产品时所学一切的知识库。团队中的老手将参考它来获得产品见解，而新手将能够更快地建立对产品的理解。

> “纸是用来写下我们需要记住的东西的。我们的大脑是用来思考的。”——阿尔伯特·爱因斯坦

# 了解您的主要衡量标准

与最后一个写下来的要点相关，你应该在测试之前陈述你所关心的指标。在大多数情况下，我喜欢将这些分为主要的、次要的和“将监控”的。

很多人出错的地方在于他们想要跟踪太多的指标。有一系列次要的和“将被监控”的指标是可以的，但是你只能有一个主要的指标。这是你的主要决策标准。如果你试图在多个数据点之间进行权衡，你会偏向于扭曲数据，使[偏向于你的先入之见](https://www.conordewey.com/blog/thinking-sherlock-holmes/)。

这看起来很简单，但可能很难。如果您正在运行一个结账优化测试，并且您发现变体提高了转换数量，但是降低了平均购买价值，该怎么办？你如何处理这些相互冲突的变量？需要考虑的因素很多，但是预先对哪些指标最重要有一个统一的看法会让您在决策时更加轻松。

# 如果需要，与工程部门合作

我不确定 A/B 测试基础设施在您的组织中是如何建立的。我发现不同的公司有很大的不同。有大的科技公司，他们什么都有，也有小的创业公司，他们在西部蛮荒。**如果你不是前者，赋值逻辑永远不会像看起来那么简单。**

您应该在书面文档中详细说明谁将被分配，他们将被分配到什么唯一的 id，以及该分配何时发生。如果您的基础设施不能为您处理这种复杂性，那么就需要处理这种复杂性。你可能需要与工程合作，以正确的方式实现事情。这不是世界上最有趣的工作，但值得投入时间和精力来做好这件事。否则，到了评估时间，你会发现自己在试图拼凑破碎的作业，而你不会过得很愉快。

# 洞察力转化为未来的测试

因此，您最终运行了测试，并耐心等待结果。这就是事情变得令人兴奋的地方！奇怪的是，数据科学家在这里变得懒惰。他们报告关键指标，命名获胜的变体，然后收工。这是一个错过的机会！

A/B 测试中最有趣的部分隐藏在分析中。这是你了解人们如何使用你的产品的地方。你应该写下这个分析，并作为你报告的一部分，与参与测试过程的每个人分享。这种分析通常会暴露其他假设，导致更多的测试等等。这就是实验的周期性。**测试不是线性的。它们相互补充。**

![](img/c177962a2232c2a7ae92511f967dacd0.png)

[精益启动](https://twitter.com/johncutlefish/status/1023618936758136832)

# 将你的思维产品化

当您的组织达到一定规模时，您将遇到这个奇怪的中间地带，您有一个数据科学团队准备好处理更专业的问题，但 A/B 测试仍然占用了过多的时间。你在这里做什么？

如果你想在你的组织中推广 A/B 测试，那么你需要将你的想法产品化。你听说过 Airbnb 和脸书的工具，员工可以用它们来发起和评估测试，[都是自助式的](https://medium.com/airbnb-engineering/experiment-reporting-framework-4e3fcd29e6c0)。这是一个将数据科学过程封装到任何人都可以使用的工具中的很好的例子。从技术上和文化上来说，这是一个艰难的转变，但这是一个你总有一天要完成的转变。**这应该是你的想法，最好是在为时已晚之前。**

# 离别的思绪

我之前提到过 A/B 测试是一项跨职能的工作。像任何团队运动一样，有时你必须为了更大的利益而妥协。这可能意味着以不太准确、更容易理解的方式呈现结果。这可能意味着在考试前花更多的时间写下你的思维过程。这可能意味着在测试启动后将破碎的任务数据拼凑起来。

这些权衡在每次测试中都在发生。你可以忽略它们，或者承认它们的存在，并一起努力达到可能的最佳状态。**当你选择后者时，最终会收获颇丰。**

向 Josh Laurito、Greg Allen、Andrew Bartholomew 和我在 Squarespace 一起工作的所有人大声喊出来，同时缓慢但坚定地捡起这些东西。

感谢阅读！在 [**Twitter**](https://twitter.com/cdeweyx) 上找到我，不要忘记 [**订阅**](https://www.conordewey.com/) 我的每周简讯，获取任何新帖子和有趣的链接。看看下面一些类似的帖子:

*   [A 型数据科学家的颂歌](https://www.conordewey.com/blog/an-ode-to-the-type-a-data-scientist/)
*   [如何搜索创业公司](https://www.conordewey.com/blog/how-to-search-for-startups/)
*   [数据科学面试资源大单](https://www.conordewey.com/blog/the-big-list-of-data-science-interview-resources/)