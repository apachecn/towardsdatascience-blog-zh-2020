# 博弈论 101

> 原文：<https://towardsdatascience.com/game-theory-101-f1edef74b742?source=collection_archive---------45----------------------->

## 单人决策问题

![](img/0a476198ea77b31b9b2264e7eaea968f.png)

[拉杆脚轮](https://medium.com/u/4d32c78bd7f8?source=post_page-----f1edef74b742--------------------------------)

博弈论无处不在。它如此普遍，以至于我们常常意识不到它的存在。经济学、市场营销、政治学、游戏设计和人工智能的学生每天都在使用博弈论版本。在每一门学科中，主要目标是理解人们在面对特定情况或决定时的反应。一个细心的观察者会在任何政治选举或营销活动中看到这一幕。

虽然博弈论只是描绘了现实的图景，但它是一个非常有用的工具，而且效果惊人地好。博弈论利用一个框架来处理理性决策者之间的冲突和妥协。传统上，一个理性的决策是在遵守一组给定的约束条件的同时最大化一个人的收益。

和任何学科一样，博弈论有自己的词汇和结构。本文将通过最基本的决策问题——单人决策来介绍其术语和原则。

# 玩家

在单人决策中，只有一个参与人。*玩家*在博弈论中是指任何有能力做出决定的实体。博弈论的一部分是对玩家的行为做出假设。我们的结果和我们的假设一样好。因此，博弈论的一个重要部分要求我们挑战我们的假设。但是今天的课，我们会保持简单。

我们每天都面临着多种选择。国会议员决定如何投票表决一个特定的法案。一个产品经理决定在发布日期之前删除一个特性。甚至关于穿哪件衬衫的琐碎决定也是每天都会发生的事情。我们面临的每个决定都有三个部分。

# 行动、结果和偏好

*   行动是我们可以选择的所有选项。
*   结果是行动的结果。
*   偏好是对可能结果的排序，从最理想到最不理想。

让我们用之前提到的选择当天衬衫的小决定。你有两件衬衫，红色的没有图案，另一件是蓝色的有图案。

我们将集合动作表示为 *A* = { *r* ， *b* }，其中 *r* 代表选择你的红色衬衫， *b* 代表选择你的蓝色衬衫。

现在让我们定义一组结果。在这种情况下， *X* = { *x* ， *y* }其中 *x* 穿着红色衬衫， *y* 穿着蓝色衬衫。

举这样一个简单的例子，行动和结果之间的差别是微妙的。行动是选择一件特定的衬衫，结果实际上是穿着一件特定的衬衫。但是你还是会明白的。

结果和行动并不总是如此一致。例如，一项行动可能是减少开支。结果将是大量裁员。虽然结果仍然是所选择的行动的结果，但它们彼此非常不同。

此外，可能的动作列表并不总是像我们的两件衬衫的例子那样分散。也许你有 5000 万美元的可用预算，但你并不需要花掉它。你的行动范围可能是 *A* = [$0，$ 5000 万]。请注意，方括号表示 0 到 5000 万美元的区间，而不是表示离散行动的{}。

现在，我们来介绍一下偏好。想象你最喜欢的颜色是红色，因此，你更喜欢穿红色的衬衫。在博弈论中，我们用符号 *x* ≿ *y* 来表示这种偏好。这个符号结构读作“ *x* 至少和 *y* 一样好。”这只是博弈论表达你更喜欢你的红色球衣的公式化方式。

当然，“ *x* 至少和 *y* 一样好”这种偏好是很弱的。我们就是这么称呼它的。排名很弱。还有另外两种形式的排名，也是借鉴传统经济学和决策理论。一个是表示严格偏好的≻，“ *x* 严格优于 *y* ，”和~表示无所谓，“ *x* 和 *y* 一样好。”

在我们继续之前，让我们先介绍一下对玩家的要求。玩家不允许在任何两个结果之间犹豫不决。这叫做**完备性公理**。如果出现结果 *x* 和 *y* ，玩家必须选择 *x* ≿ *y* 或 *y* ≿ *x* 。

除了完整性公理之外，我们还强加了另一个叫做**的规则，即传递性公理**。它陈述了对于任何三个结果，如果 *x* ≿ *y* 和 *y* ≿ *z* ，那么 *x* ≿ *z* 。在真实的话语和具体的想法中，这意味着如果我们有第三件带有圆点的紫色衬衫，我们更喜欢红色衬衫而不是蓝色衬衫，我们也更喜欢蓝色衬衫而不是紫色衬衫，那么我们一定更喜欢红色衬衫而不是紫色衬衫。

总而言之，完备性公理保证了任何两个结果可以相互排序；比起蓝色的衬衫，我更喜欢红色的。传递性公理确保了这些排序之间不会有矛盾。如果没有这两条规则，我们可能会以一个不确定的场景结束。博弈论禁止使用优柔寡断的玩家。既完全又可传递的偏好关系称为**理性偏好关系。**

请记住，如果我们的模型中包含不止一个参与者，即使每个参与者都是理性的，也有可能以非理性群体告终。但是我们的单人决策问题不会遇到这种情况。

# 支付函数

在大多数情况下，偏好和结果一起形成了一个支付函数。通常，在商业中，支付函数返回一个美元值。但是唯一的要求是一个顺序值，这样值越高，收益越好。

当处理一些足够简单的事情时，比如为一天选择一件衬衫，我们的偏好通常是支付函数的同义词。在这些情况下，我们基于偏好为每个结果分配一个支付函数值，这样如果 *x* ≿ *y* ，那么支付函数为 *x* 返回的值大于为 *y* 返回的值。

回到我们的三件衬衫的例子，我们记得偏好是*红色* ≿ *蓝色*和*蓝色* ≿ *紫色*，因此，*红色* ≿ *紫色*。我们给红色的*分配 10 的收益值，给蓝色*的*分配 5 的收益值，给紫色*的*分配 1 的收益值。这些数字是任意的，除了红色的值必须大于蓝色的值，蓝色的值必须大于紫色的值。对于红色、蓝色和紫色，我们可以分别使用 2000、1000 和 1。规模无关紧要。*

如果我们将玩家、期权和每个收益之间的关系看作一棵决策树，它将类似于下图。

![](img/79b94a12589147bf8829d62e3ccc32ba.png)

[拉杆脚轮](https://medium.com/u/4d32c78bd7f8?source=post_page-----f1edef74b742--------------------------------)

# 理性选择范式

最后，我们得出了完整的概念。记住，我们需要一个理性的代理人作为参与者。这被称为**理性选择范式**。它认为决策者会理性地选择自己的最佳行动。为了保持这一点，我们假设玩家知道所有可能的行动，所有可能的结果，准确地说选择每个行动将如何在结果中表现出来，以及他对所有结果的偏好。

这个假设列表可能看起来势不可挡，甚至不现实，但是如果我们牺牲其中任何一个，我们就不能断言理性选择的想法。本文中的决策示例保持简单，处于入门水平。支付函数的值很容易确定，并且清楚地表明了行动的最佳选择。然而，一些支付函数是需要微积分的数学公式。在这些情况下，你可能需要画出收益函数的结果来选择最佳行动。

博弈论是许多学科不可或缺的一部分，如果应用得当，它能提供巨大的价值。对它的理解，即使是最基本的理解，也会对在当今更复杂的商业决策中做出合理的选择大有帮助。