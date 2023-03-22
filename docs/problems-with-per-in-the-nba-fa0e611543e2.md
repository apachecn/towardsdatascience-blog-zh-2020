# NBA 中与 PER 的问题

> 原文：<https://towardsdatascience.com/problems-with-per-in-the-nba-fa0e611543e2?source=collection_archive---------16----------------------->

## 您可以轻松避免的 3 个常见数据科学错误

![](img/9583ba3f810a99dea757bc2c2a0bce2a.png)

在 [Unsplash](https://unsplash.com/s/photos/nba?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上由[棕柽柳](https://unsplash.com/@tamarcusbrown?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)拍摄的照片

如果你是 NBA 篮球的粉丝，也是分析的粉丝，那你一定听说过 PER。

PER 是霍林格开发的一种综合统计。约翰目前为《运动报》撰稿，曾是孟菲斯灰熊队的篮球运营副总裁，也是《ESPN》和《体育画报》的专栏作家。他是四本篮球分析书籍的作者，是 NBA 分析社区的巨人。

根据霍林格的说法:

> 玩家效率等级(PER)是玩家每分钟生产力的等级。

PER 被正确地称为篮球高级分析运动的教父级统计数据之一。这是第一个调整比赛节奏、调整比赛时间和跨赛季标准化数据的篮球测量方法之一(该测量方法为每个赛季分配了 15%的平均球员)。《公共关系条例》仍然经常在广播和媒体中被引用。

它也有很大的缺陷。

有人说 PER 过于复杂。有人说它不足以解释防御。其他人说它高估了得分。

虽然上述说法可能是正确的，但真正的问题在于方法——这与数学无关，而与导致其不完善的数据分析方法有关。今天，我想把重点放在霍林格的 PER 研究方法上，希望我们所有人——作为数据科学家——在未来避免类似的错误。

# 方法学

在研究中，科学家遵循几个一般步骤:

1.  **观察一种现象。**你看到了世界上的一些东西，想知道更多关于它是如何运作的。
2.  **开发研究问题。基于你所看到的，你提出你想要得到答案的问题。**
3.  **寻找现有理论，必要时发展一种理论。对于大多数研究领域，有人已经做了一些工作。通过找到现有的理论，你就有了一个理解你所观察到的现象的很好的起点。有时候，你只需要现有的理论，但是——如果你找不到任何适合这种情况的理论——你可以发展自己的理论来恰当地描述世界上正在发生的事情。**
4.  **创造一个可证伪的假设。**这通常是最难的一步。为了测试一个理论，你必须找到一种表达方式，这样你就可以*证明这个理论是错误的。*例如，如果你的假设是“披头士是有史以来最伟大的乐队”，就没有办法证明或反驳这一说法。然而，如果你说“披头士是有史以来最畅销的乐队”，你可以看看实际的衡量标准，看看这种说法是否正确。确保你的假设遵循这个公式。
5.  **确定措施。**现在，您已经创建了一个可证伪的假设，您可以确定哪些可观察的测量将有助于您测试该假设。
6.  **收集数据。前进并测量那边的变量。**
7.  **分析数据。**分析这些测量值，看看你的理论是否能准确解释观察到的数据，如果它们确实有解释力，你可以看看它们对你的数据集有多大的影响。
8.  更新你的信念。如果你的数据符合某个理论，你现在就有了该理论的工作证据。如果你的数据不符合某个理论，那么你应该改变你对该理论真实性的信念(如果你不直接拒绝它的话)。
9.  **如果需要，运行更多测试。进行一次测试很少足以证实你的信念，而且你最终会根据你的发现提出更多的问题，这些问题可以在未来的分析中得到解答。**

现在我们已经对研究方法有了基本的了解，让我们从理论上来看一下如何计算 NBA 的每分钟生产率。

## 我们理论上的 NBA 生产力研究项目

1.  我们观察到一些 NBA 球员帮助他们的球队比其他人赢得更多。
2.  我们想知道我们是否可以用一个单一的指标来衡量 NBA 球员每分钟的生产率。我们想看看我们是否能根据这个标准预测他们的团队有多成功。换句话说，我们想要创建一个预测团队胜利的玩家指标。
3.  迪安·奥利佛斯有一个篮球成功的四因素理论。但是，它由四个因素组成，而不是一个，而且与团队成功更相关。因此，我们发展了一个理论，即个人球员的生产力可以通过基于我们对篮球运动的一系列信念的 boxscore 统计的综合测量来衡量。
4.  我们陈述了我们的假设，玩家的生产力可以用一个单一的指标来衡量。如果这是真的，我们假设我们创建的玩家指标将显著预测玩家团队的生产力(即，玩家在我们的指标上的分数将预测他们的团队赢了多少场比赛)。
5.  我们使用 boxscore 统计数据和我们对篮球的信念创建了一个我们的指标版本。这是我们的独立变量。我们用团队获胜的数量来衡量生产率，这是我们的因变量。
6.  我们收集衡量指标和团队胜利的数据。
7.  我们分析数据，看看我们的指标是否能预测团队获胜，以及我们的度量的效果大小(即，它预测实际团队获胜的“多少”),如果它确实能预测团队获胜的话。
8.  我们根据指标与数据的吻合程度对指标进行修改，或者因为指标不符合数据而完全停止使用。
9.  我们对我们的指标进行了更多的测试，并开发了更多的研究问题来回答我们的指标作为感兴趣的变量。

让我们把这个和我们看到的霍林格和佩尔的作品进行比较。

## 霍林格 PER 法

1.  约翰观察到一些球员帮助球队比其他人赢得更多。
2.  约翰想看看是否一个单一的指标可以预测球员的生产力。
3.  约翰的工作基于迪安·奥利弗的四个因素，同时也根据他对篮球的信念增加了自己的权重。
4.  John 提出了一个关于单个衡量标准的假设——后来成为 PER——但没有对此做出可证伪的陈述(例如，PER 预测团队获胜)
5.  John 创建了他的 PER measure。他没有具体说明任何结果变量。
6.  约翰收集他的测量数据。
7.  John 没有提供任何统计分析来验证 PER 是否能有效地预测生产率，因为他没有具体说明结果变量。我们也没有任何规定的 PER 效果大小。
8.  尚未根据分析更新 PER。
9.  那些仍然使用 PER 作为衡量球员生产力的标准的人没有对 PER 进行额外的测试。

霍林格写道:

然而，PER 能做的是用一个数字总结一个球员的统计成绩。这让我们能够统一我们试图在头脑中跟踪的每个球员的不同数据[……]，这样我们就可以继续评估统计数据中可能缺少的东西。

本质上，霍林格着手:

*   用一种方法总结 NBA 球员的统计成绩
*   确保该方法能够有效地测量每分钟的生产率

他用 PER 实现了前一个目标，但在这个过程中，他未能进行基本的科学分析，以确保他的指标在实现后一个目标时在统计上是有效的。

# 数据科学需要遵循科学的方法

为霍林格说句公道话，他可能不认为自己是数据科学家。见鬼，他可能认为 PER 主要是他用来写作的工具，他可能已经更新了他对 PER 的个人信念。

但是他用 PER 所做的工作肯定属于数据科学的范畴，并且 PER 还没有作为一种统计方法被更新。如果他从一开始就遵循了基本的科学方法原则，那么他就可以很容易地避免一些错误。

此外，因为 PER 如此受欢迎，篮球分析社区的许多其他数据科学家也在犯霍林格犯的同样的错误。

让我们试着阻止它。以下是如何轻松地从 PER 中学习(并避免)数据科学错误的方法。

# 你应该避免的 3 个数据科学错误

## 1.不够具体

在数据分析中，非常重要的一点是要明确项目的各个方面。确保您:

*   对你的假设有一个可证伪的陈述
*   记住具体的因变量和自变量，以便进行有效的分析

如果你在开始提取数据之前不这样做，你基本上是在瞎跑，浪费很多时间。

如果霍林格对他的 PER 方法有更具体的描述，我们将很容易看到 PER 是否是一个有效的度量。就目前情况而言，我们不知道约翰所说的“生产力”在 PER 的上下文中是什么。我们都有自己的想法——我的想法是生产率应该以团队的胜利来衡量——但这都是基于我们个人的定义，而不是进行研究的科学家的明确定义。

## 2.未报告显著性和效应大小

这与前一点有联系——因为霍林格没有具体的结果变量，所以没有报道的发现。仍然使用 PER 的网站不报告 PER 是否能有效预测胜率，它预测胜率的百分比，或者任何其他关于潜在结果变量的发现。

对于你做的任何项目，*必须*报告你感兴趣的任何因变量的显著性和影响大小。

## 3.不基于数据更新

Basketball-Reference.com 和 ESPN 网站的 PER 值保持不变——这个指标从一开始就没变过。如果你打算做数据科学，你必须准备好基于你的发现进行迭代。

仅仅因为你以前对某件事有信念，并不意味着如果你发现了与此相反的证据，你就不应该更新这些信念。让数据引导你找到更好的理论和模型。

# 为什么 PER 仍然如此受欢迎？

尽管有缺陷，PER 仍然是一个被大量使用的 NBA 数据。这是为什么呢？

嗯，首先，我很确定它确实预测了*团队胜利中的一些*数量的差异(即使效果大小还没有明确说明)。还有文化相关性的问题——PER 现在已经深深地融入了 NBA 文化。

它的文化相关性归结为两件主要的事情:

1.  这是第一个试图回答所有 NBA 球迷都感兴趣的问题的综合指标之一:谁是联盟中最有生产力的球员？
2.  它以一种能引起普通 NBA 球迷共鸣的方式抓住了人们的兴趣。

15——平均每分——是一个相关的篮球得分。如果有人在篮球比赛中得了 15 分，我们认为他是一个好球员。如果有人得分在 20 多或 30 多，我们认为他们是伟大的球员。

从这个意义上说，PER 是聪明的。霍林格了解 NBA 球迷的心理，并确保他的测量是他的读者很容易认同的。

## 你应该在研究中使用 PER 吗？

见鬼。是的。

同样，PER 不是一个完美的衡量标准。但是通过将它包含在你的研究中，我们可以更好地理解它作为一种衡量标准的有效性——由于我们上面提到的问题，这是目前所缺乏的。您还可以将其他指标的功效与 PER 进行比较，为我们提供一个指标效率的基线。

解决 PER 问题的唯一方法是在数据科学环境中实际观察 PER——即使我们发现它不是我们所依赖的*指标。*

# 结论

就像乔治郝佳不应该被认为是有史以来最伟大的篮球运动员一样，我们也不应该被认为是篮球分析的目标。聪明的球队似乎已经不再用它来衡量球员的评价。希望广播公司和媒体成员也会远离它，因为我们对篮球比赛应该如何用统计方法来衡量有了更多的了解。

同时，PER 是*篮球分析的*文化基石。当我说我认为它应该被载入奈史密斯篮球名人堂时，我不是在开玩笑。

它可能不符合一些简单的科学原理，但如果没有它，我们可能仍然停留在篮球统计的黑暗时代。

作为数据科学家，我们应该尊重霍林格的所作所为，然后学会做得更好。

# 来源

根据 Basketball-reference.com 计算

霍林格，[什么是 PER？](https://www.espn.com/nba/columns/story?columnist=hollinger_john&id=2850240) (2007)，ESPN

[四大因素](https://www.basketball-reference.com/about/factors.html)、Basketball-reference.com