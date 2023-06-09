# 迈克尔·乔丹是低方差之王吗？

> 原文：<https://towardsdatascience.com/is-michael-jordan-the-king-of-low-variance-7f059e81955?source=collection_archive---------86----------------------->

## 继《最后的舞蹈》网飞纪录片系列之后，这里有三个你在统计网站上从未见过的“有史以来最伟大”决心的一致性测试。

《最后的舞蹈》将迈克尔·乔丹和整个 80-90 年代的篮球时代带回了我们的生活。但随之而来的是关于谁是“山羊”或历史上最伟大的人的无休止的争论，在这方面，乔丹在数据上并没有明显的优势——他没有比尔·拉塞尔赢得那么多冠军，没有卡里姆、卡尔·马龙、威尔特·张伯伦甚至仍然活跃的勒布朗·詹姆斯得那么多分。他场均得分最多，但仅比威尔特·张伯伦高出一点点。那么是什么让他如此特别呢？或者把他当成山羊只是 NBA 推广者和耐克公司的一个营销噱头，注入了我们天真的 90 年代孩子的记忆？嗯，我想考虑纪录片中反复提到的最后一个辩护-

乔丹总是表演。

他来赢得每一场比赛，并在每一场比赛中为观众中从未看过他现场表演的小孩表演。

也许我们可以在数据中看到这一点？如果迈克尔·乔丹是一个稳定的表演者，我们会期望看到他没有很多“糟糕的夜晚”。这意味着他的场均得分通常不会比他的平均得分低很多。方差的度量应该能够捕捉到这一点。

# 我们如何检验我们的假设？

我们想把乔丹和其他伟大的得分手做比较——我们会拿科比、拉里·伯德、威尔特·张伯伦和勒布朗·詹姆斯做比较。我们也想只选择他们平均得分高的赛季，否则，方差比较就没什么意思了。想象一下，如果有人平均每场比赛得 5 分，并且从未超过 10 分，这个玩家的方差很低，但他不是好玩家。我们正在寻找方差为 5 的每个游戏玩家的 30 分。此外，许多球员在新秀年需要时间热身，在联盟的最后几年有一些下降，所以我们想把这些排除在分析之外。出于这个目的，我们将只选择那些球员平均得分超过 25，并且至少打了 50 场比赛的赛季。我们还将展示该赛季平均值方差的标准化版本，这样像威尔特·张伯伦这样的球员在赛季中每场比赛平均得分超过 50 分(这有多疯狂..？)，正如我们提到的，它可能固有地具有更高的方差。我们将把常规赛和季后赛结合起来进行方差估计。我们的数据来源将是非常详细的[https://www.basketball-reference.com](https://www.basketball-reference.com)

对于伯德，我们选择了 1984/1985-1987/1988 赛季，张伯伦 1959/1960-1965/1966 赛季，1969/1970 赛季，乔丹-1984/1985 赛季，1986/1987-1992/1993 赛季，1995/1996-1997/1998 赛季，科比-2000/2001-2002 赛季)

# 所以…结果是:

## 标准偏差，非平均值标准化:

勒布朗-7.731231136445559

鸟——8 . 58860 . 88888888881

约旦——8 . 19860 . 888888888615

神户——9 岁。39960.89989899991

萎蔫——12 . 59861868612

## 标准偏差，按平均值标准化:

**勒布朗—8.3877441**

**约旦— 8.36280090045399**

枯萎——9 . 59860 . 99989999989

鸟——9 . 59980 . 99999999991

神户——9 岁。39860.89989898991

勒布朗和乔丹有几乎相同的方差。我们能为一致性设计一些更好的估计吗？

我们最后一次尝试如下-

我们不想在更高的分数中测量方差——高方差分数惩罚了拥有 50-60 分惊人表现的玩家，因为它与他的平均水平非常不同。我们只想惩罚“糟糕的夜晚”，我们希望所有的玩家都通过某种全球尺度来衡量，类似于我们对归一化方差所做的那样，因为如果你是一个 5 分玩家游戏，仅仅衡量与自己平均水平的距离不会算作你有许多糟糕的夜晚(因为你的平均水平一开始就不太好)。所以我们用这个公式

![](img/09082a2e4dc97216ae30f488fb3f26c8.png)

其中 P 是所有游戏分数的集合。

## 现在结果发生了巨大的变化:

枯萎——3.6269300860010376

约旦——4 . 54860 . 48648668661

勒布朗——6 岁。36660.66666666661

神户——7 岁。36860.78777878767

鸟——7 . 59867 . 38777787871

**整个数据直方图供您目测:**

![](img/e00a7caffda2808c4c6850c710299113.png)

所以你有它。胜利肯定不属于乔丹，但他在稳定性方面非常强。除了威尔特·张伯伦，我认为很难找到有类似表现的球员，尽管这需要更深入的研究来验证。当然，得分并不代表一切——例如，比尔·拉塞尔根本不是一个好的得分手，魔术师约翰逊也不怎么样，除了助攻、篮板、盖帽和抢断等其他统计数据，他们还在风格、赢球态度和关键时刻得到衡量。奇怪的是，当二阶矩统计在常规统计工作中如此普遍时，你却从未在游戏分析中看到它们。基本上一切都是关于平均值，最好的情况是关于条件预期(“65%的球队在季后赛中以 3-1 领先…”)

[![](img/d1c1cf5307a9b25a182f4069172834ee.png)](https://twitter.com/Suflaky)