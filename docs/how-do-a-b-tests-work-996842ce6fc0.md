# A/B 测试是如何工作的？

> 原文：<https://towardsdatascience.com/how-do-a-b-tests-work-996842ce6fc0?source=collection_archive---------5----------------------->

## 深入了解科技行业最强大的工具之一

简而言之: A/B 测试就是通过创建可信的克隆来研究因果关系——两个相同的项目(或者，更典型的是，两个统计上相同的组)——然后观察不同对待它们的效果。

![](img/f719e182d8fa1de281ea6fa237de3b27.png)

当我说两个相同的项目时，我的意思是比这更相同。关键是找到“可信的克隆体”…或者让随机化加上大样本量为你创造它们。图片:[来源](https://twitter.com/JimMFelton/status/1247631838211985409)。

科学的、受控的[实验](http://bit.ly/quaesita_experiment)是不可思议的工具；他们允许你谈论什么导致什么。没有它们，你所拥有的只是[相关性](http://bit.ly/quaesita_correlation)，这通常对决策没有帮助。

> 实验是你在礼貌交谈中使用“因为”这个词的许可证。

不幸的是，很常见的是，人们自欺欺人地认为他们的推论是正确的，声称科学实验的好处，而没有进行适当的实验。当存在[不确定性](http://bit.ly/quaesita_uncertainty)时，你所做的不能算作实验，除非*所有*以下三个要素都存在:

*   **应用不同的处理**
*   **随机分配的治疗**
*   **科学假说得到验证**(见我的解释[此处](http://bit.ly/quaesita_damnedlies)

如果你需要复习这个话题和它的逻辑，看看我的文章 [*你是否因为错误地使用“实验”这个词而感到内疚？*](http://bit.ly/quaesita_experiment)

# 实验为什么有效？

为了理解为什么实验是对因果关系进行推论的工具，让我们来看看一个最简单的实验背后的逻辑:A/B 测试。

## 简短解释

如果你不想看详细的例子，看看这个 GIF，然后跳到最后一节(*“秘制酱是随机化的”*):

![](img/15f6a1cb23741fb6180332b9194c6a90.png)

## 冗长的解释

如果你喜欢一个全面的例子，我已经为你准备好了。

想象一下，你的公司有一个灰色的标志已经有几年了。既然你所有的竞争对手都有灰色标识(模仿是最真诚的奉承)，你的高管们坚持要换成更明亮的颜色……但是是哪一种呢？

![](img/8b26a522c45e395526e557212a2f58d2.png)

您的用户看到的徽标是灰色的，但这种情况即将改变。

在仔细评估了你公司的网站配色方案的实用性后，你的设计团队确定了仅有的两个可行的候选色:蓝色和橙色。

CEO 最喜欢的颜色是蓝色，所以她选择*批准蓝色*作为 [***默认动作***](http://bit.ly/quaesita_damnedlies) 。换句话说，她是说如果没有进一步的信息，她很乐意选择蓝色。对你来说幸运的是，她是一个强有力的数据驱动型领导，愿意允许数据改变主意。

为了切换到*的 [***替代动作***](http://bit.ly/quaesita_damnedlies) 批准一个橙色标志*，CEO 需要证据证明一个橙色标志 ***导致*** 你当前的[用户群](http://bit.ly/quaesita_vocab)在你网站的特定部分点击更多(相对于蓝色)。

你是公司的高级数据科学家，所以你要竖起耳朵。从*frequentist statist**中，你立即发现你的 CEO 的决策方法符合[框架。](http://bit.ly/quaesita_damnedlies)*仔细听完她的话后，你确认她的*无效假设和替代假设*与因果关系有关。这意味着你需要做一个实验！总结她告诉你的话:

***默认动作:*** 批准蓝色标志。
***替代动作:*** 批准橙色标志。
***无效假设:*** 橙色标志 ***不会导致*** 比蓝色标志至少多 10%的点击量。
***替代假设:*** 橙色标志 ***确实会导致*** 比蓝色标志多至少 10%的点击量。

为什么是 10%？这是你的 CEO 愿意接受的最小 ***效应大小*** 。如果决策者关心效果的大小，那么这些应该在一开始就纳入假设检验。测试“无差异”的*零假设*是一个明确的声明，你根本不在乎效果的大小。

对于这样的设置，A/B 测试是完美的实验设计。(对于其他因果决定，可能需要其他设计。虽然我在这里只讨论 A/B 测试，但是更复杂的设计背后的逻辑是相似的。)

所以，我们来做个 A/B 测试吧！

# 现场交通实验

有各种各样的方法来运行 A/B 测试。你在心理学实验室(和焦点小组研究)看到的往往是邀请街上的人，随机向不同的人展示不同的刺激，然后问他们问题。唉，你的首席执行官正在寻找更困难的事情。她的问题只能用一个*实时流量* *实验*来回答，听起来确实是这样的:当不同的用户在你的网站上处理日常事务时，你将为他们提供不同版本的 logo。

# 实验基础设施

如果你想运行一个真实的交通实验，你需要一些特殊的基础设施。与您的工程师合作，建立随机为不同用户提供不同治疗的能力，以及根据治疗条件跟踪您的 CEO 所需指标(某些网站元素的点击率)的能力。

(如果你想知道为什么每个人都不总是做实时交通实验，答案通常与重新配置一个没有考虑实验的生产系统的高昂前期成本有关。虽然像 [Google 这样的公司在我们甚至知道我们想要运行什么实验之前就在我们的大部分系统中构建了实验基础设施](https://bit.ly/livetrafficexpt)，但传统组织可能会忘记在一开始就添加这一功能，结果可能会发现自己落后于更懂技术的竞争对手。顺便提一下，如果你想进入应用的 [ML/AI 游戏](http://bit.ly/quaesita_dmguide)，实验基础设施是必须的。)

# 样品

因为你非常谨慎，所以你不会用一个突然出现的新 logo 让所有用户感到惊讶。更明智的做法是[为您的实验抽取](http://bit.ly/quaesita_vocab)一部分用户，然后逐步推广(如果您的更改造成了不可预见的灾难，可以选择回滚到灰色)。

# 控制

![](img/472bb652646a3676a5a6d5a46f6847cb.png)

图片:[来源](https://twitter.com/fp2p/status/893110061119266818)

如果你有兴趣了解用户对新奇事物的反应——他们是否会因为商标改变而点击更多，而不管它变成了什么？—你可以使用灰色标志作为你的对照组。然而，这不是你的首席执行官想要回答的问题。她对隔离橙色相对于蓝色的因果影响感兴趣，因此考虑到她构建决策的方式，控制组应该是显示蓝色标志的用户。

![](img/17d7eb4d57a0215e1351763d7de0afb7.png)

首先，您的系统尝试性地将蓝色徽标基线应用于样本中的所有用户。

但在系统实际向他们展示蓝色标志之前，实验基础设施投掷一枚虚拟硬币，随机将一些用户重新分配到橙色治疗中，并向他们展示橙色而不是蓝色。

![](img/f594b2e2bba9fbb0f978d59410f38069.png)

然后——随机地——你向一些用户展示橙色版本，但不向其他用户展示。

如果你随后观察到橙色版本的平均点击率更高，你将能够说是橙色处理导致了行为的差异。如果这一差异在统计上高于 10%，你的首席执行官会像她承诺的那样，愉快地换成橙色。如果没有，她会选择蓝色。

![](img/6e3880af08963bc4f67b0a79575e9c84.png)

如果用户在橙色处理条件下的反应不同于控制条件，你可以说显示橙色版本* *比蓝色版本导致** 更多的点击。

# 秘方是随机化

如果你没有随机地这样做，如果你给所有登录的用户橙色处理，而给其他人显示蓝色处理，你不能说是橙色处理造成了差异。也许你的登录用户只是对你的公司更忠诚，更喜欢你的产品，不管你把 logo 做成什么颜色。也许你的登录用户有更高的点击倾向，无论你向他们展示什么颜色。

> 随机化是关键。*这是让你得出因果结论的秘方。*

这就是为什么随机性是如此重要。在大样本量的情况下(没有大量的[统计能力](http://bit.ly/quaesita_statistics)实验就无法进行)，随机选择会产生差异明显的群体。从统计学上来说，这两个群体是彼此可信的克隆体。

![](img/089728ef4866d3b40091ba315cc506f0.png)

你的决策标准越简单，样本量越大，你的实验设计就越简单。A/B 测试很棒，但更花哨的实验设计允许您明确控制一些混淆因素(例如，2x2 设计，您将登录用户与未登录用户分开，并在每个组中运行迷你 A/B 测试，让随机性为您处理其余的问题)。当您强烈预感到橙色徽标会对登录用户产生不同的影响，并且希望将这一点纳入您的决策时，这一点尤其有用。无论哪种方式，随机选择都是必须的！图片:[来源](https://pixabay.com/illustrations/abstract-colorful-background-1900585/)

由于随机选择，在 A/B 测试的蓝色和橙色条件下的用户群体在所有方面都是相似的(总的来说),人们传统上认为他们会挑选参与者来平衡他们的学业:相似的性别，种族，年龄，教育水平，政治观点，宗教信仰……但他们在所有你可能没有想到要控制的方面也是相似的:相似的爱猫者，喝茶者，游戏者，哥特人，高尔夫球手，尤克里里所有者，慷慨的给予者，优秀的游泳者，暗中讨厌他们的配偶的人，没有这样做的人

> 当你使用随机化来创建两个大的组时，你得到了一个统计空白画布。

这就是大样本和随机选择相结合的好处。你不必依靠你的聪明来想出正确的混杂因素来控制。当你使用随机化来创建两个大组时，你得到了一个统计空白画布——你的两个组在统计上在各方面都是相同的，除了一点:你要对他们做什么。

> 除了一点:你要对他们做什么之外，你的两组在统计上完全相同。

如果你观察到两组结果之间的实质性差异，你将能够说所发生的差异是*由于* *你所做的*。你可以说是*你的治疗*造成的。这就是(适当的)实验的惊人力量！

> 如果我们做了一个真正的实验，并在小组结果中发现了显著的差异，我们可以把这归咎于我们所做的！

![](img/eb18331b80731f24ad134ba804f7830d.png)

开怀大笑之后，互联网对这些猫做的第一件事就是玩一个非常吹毛求疵的游戏“找出差异”如果你展示两个劣质的“克隆体”并试图将不同的结果归咎于不同的治疗方法，科学家也会这么做。没有大样本，你怎么知道不是鼻子下面的那个小点导致了你可能观察到的任何结果？图片:[来源](https://twitter.com/JimMFelton/status/1247631838211985409)。

# 感谢阅读！喜欢作者？

如果你渴望阅读更多我的作品，这篇文章中的大部分链接会带你去我的其他思考。不能选择？试试这个:

[](/statistics-for-people-in-a-hurry-a9613c0ed0b) [## 为赶时间的人统计

### 曾经希望有人能告诉你统计学的意义是什么，术语用简单的英语表达是什么意思吗？让…

towardsdatascience.com](/statistics-for-people-in-a-hurry-a9613c0ed0b) 

# 与凯西·科兹尔科夫联系

让我们做朋友吧！你可以在 [Twitter](https://twitter.com/quaesita) 、 [YouTube](https://www.youtube.com/channel/UCbOX--VOebPe-MMRkatFRxw) 、 [Substack](http://decision.substack.com) 和 [LinkedIn](https://www.linkedin.com/in/kozyrkov/) 上找到我。有兴趣让我在你的活动上发言吗？使用[表格](http://bit.ly/makecassietalk)取得联系。

# 人工智能课程怎么样？

如果你想尝试一门为初学者和专家设计的有趣的应用人工智能课程，这里有一个我为你制作的娱乐课程:

在这里欣赏整个课程播放列表:[bit.ly/machinefriend](http://bit.ly/machinefriend)