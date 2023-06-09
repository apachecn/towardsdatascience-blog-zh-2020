# 指数跟踪——注意差距！

> 原文：<https://towardsdatascience.com/index-tracking-mind-the-gap-3dc745bbc36f?source=collection_archive---------44----------------------->

## 使用衍生工具的实际挑战和策略

![](img/1aa9570ec683c21d03bf1b9367597985.png)

你在密切跟踪吗？本·帕丁森在 [Unsplash](https://unsplash.com/s/photos/follow?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

# 为什么要进行指数跟踪

许多机构和散户投资者面临的一个共同挑战是有效控制各种市场因素的风险敞口。有各种各样的指数旨在提供跨部门和资产类别的不同类型的风险，包括股票、固定收益、商品、货币、信用风险等。

这些指数中的一些可能很难或不可能直接交易，但投资者可以交易相关的金融衍生品，如果它们在市场上可用的话。例如，CBOE 波动率指数(VIX)，通常被称为恐惧指数，不可直接交易，但投资者可以通过交易 VIX 的期货和期权获得该指数，并可能对冲市场动荡。

# 波动指数(VIX)

为了说明持有 VIX 债券的好处，可以考虑一下 2011 年标准普尔下调美国信用评级的事件。2011 年 4 月 18 日，S&P 对美国信用评级持负面展望的消息传出。如图 1(a)所示，在 2011 年 8 月 5 日官方降级后的几个月里，仅持有 SPDR 标准普尔 500 交易所交易基金(SPY)的投资组合将继续下跌约 10%。

![](img/7acc52d02bb9b42e5fb0cab5bc992190.png)

(a)2011 年 4 月 1 日至 2011 年 9 月 30 日，以及(b)2014 年 1 月 1 日至 2014 年 12 月 31 日期间，100%投资于 SPY，90%投资于 SPY，10%投资于 VIX 的投资组合的历史投资组合价值。

相比之下，一个混合了间谍(90%)和 VIX (10%)的假设投资组合在降级期间将保持稳定，最终获得正回报。图 1(b)显示了 2014 年同一对投资组合。

两者都获得了大致相同的 15%的回报，尽管《间谍》一书明显比《间谍》和 VIX 的投资组合更不稳定。VIX 股市上涨应对了大规模的下跌(例如 2014 年 10 月 15 日)，对投资组合的价值产生了稳定效应。

这个例子激发了对直接跟踪 VIX 和其他指数的交易策略的研究，或者实现任何关于指数或市场因素的预先指定的暴露。

# 指数跟踪的挑战

许多 ETF 或 etn 被宣传为通过维护与指数相关的证券组合(如期货、期权和掉期)来提供指数敞口。然而，一些 ETF 或 etn 经常达不到它们的既定目标，一些 ETF 或 etn 的表现往往远远低于既定目标。

![](img/19ed2a35d7ae82befc0e7fb7d126a5d9.png)

VXX(蓝色)明显偏离 VIX(红色)，在过去几年中损失了 93%以上。

一个例子是巴克莱的 iPath 标准普尔 500 VIX 短期期货 ETN (VXX)，这也是最受欢迎的 VIX 交易所交易产品。3 VXX 跟踪 VIX 失败是有据可查的。事实上，这些 ETF 或 etn 大多遵循静态策略或时间确定性配置，不适应快速变化的市场。

跟踪问题与所有资产类别都相关，衍生品的使用也相当普遍。例如，许多投资者寻求投资黄金来对冲市场动荡。然而，由于储存成本，直接投资金条是困难的。为了获得敞口，投资者可能会在许多黄金 ETF 和衍生品中进行选择。

# 新的方法论

在我们最近的[论文](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2976500)中，我们讨论了使用衍生品进行指数跟踪和风险敞口控制的一般方法。在市场和相关风险因素的非常一般的框架下，我们推导出一个公式，该公式将嵌入在衍生产品组合中的风险敞口(针对不同的风险因素)联系起来。

投资组合的对数收益可以分解如下:

![](img/e5dec2d214231696680453e18e2bf9d7.png)

右边的前两项表示投资组合的对数收益(LHS)与指数 s 及其驱动因子 Yᵢ的对数收益成比例，比例系数(β,ηᵢ)等于期望的风险敞口。然而，投资组合的对数收益受制于滑移过程 z。

**滑点过程**可用于量化投资组合收益与指数及其因素目标收益的背离程度。它不仅是潜在因素的已实现方差的函数，也是指数和因素之间的已实现协方差的函数。

> *滑点揭示了风险因素之间相互作用产生的潜在价值侵蚀。*

指数跟踪可以看作是衍生品动态套期保值的逆问题。在传统的套期保值问题中，目标是交易基础资产，以便复制所讨论的衍生产品的价格演变，因此，基础资产的可交易性至关重要。

在我们提出的范式中，指数和随机因素可能不直接交易，但存在写在其上的交易衍生品。我们使用衍生工具以*路径方式*跟踪或更一般地控制与指数回报相关的风险敞口。因此，我们可以研究衍生产品的各种投资组合所产生的路径属性，并量化投资组合与预先指定的基准之间的差异(如果有的话)。我们的方法还允许投资者获得与模型中相关因素相关的杠杆或非杠杆风险。

# 回到 VIX

受 VIX 的启发，我们探索了我们的方法在 VIX 一些模型下的应用和意义。特别是，我们的方法和实例揭示了 VIX 均值回复行为与 VIX 衍生品定价和跟踪该指数及其相关因素之间的联系。我们考虑 CIR 模型下的跟踪和风险暴露控制问题

![](img/f1782098e35da2254e03748644caa4fb.png)

和双因子级联平方根(CSQR)模型

![](img/684da55fce0150f01f02c3697ec1d7eb.png)

在我们的发现中，我们推导出使用期权或期货跟踪 VIX 或实现指数和/或其因素的任何敞口的交易策略。我们的投资组合采用明确的*路径自适应* *策略*，而不是 VXX 和其他 etn 使用的时间确定性策略。

虽然我们选择了 VIX 作为我们的主要例子，我们的分析适用于其他均值回复价格过程或市场因素。

# 参考

T.Leung 和 B. Ward，使用衍生工具的动态指数跟踪和曝光控制[[pdf](https://www.google.com/url?q=https%3A%2F%2Fssrn.com%2Fabstract%3D2976500&sa=D&sntz=1&usg=AFQjCNGqiwvhI_Z8WSjJnhvRCDEHkCdULA)；[链接](https://www.google.com/url?q=https%3A%2F%2Fwww.tandfonline.com%2Fdoi%2Ffull%2F10.1080%2F1350486X.2018.1507750&sa=D&sntz=1&usg=AFQjCNHcnleVj0gYtL0L6zsV6Qeyo2UYng)，**应用数理金融**，第 25 卷第 2 期，2018 年第 180–212 页

T.Leung 和 B. Ward,《用 VIX 期货追踪 VIX:投资组合的构建和表现》;[链接](https://www.google.com/url?q=https%3A%2F%2Fwww.worldscientific.com%2Fworldscibooks%2F10.1142%2F11727&sa=D&sntz=1&usg=AFQjCNFksh7UkdTHSRqYwg2Lf5epEl3RIw)，见**应用投资研究手册，** J. Guerard 和 W. Ziemba 编辑。，世界科学出版公司，2020 年

***来自《走向数据科学》编辑的提示:*** *虽然我们允许独立作者根据我们的* [*规则和指导方针*](/questions-96667b06af5) *发表文章，但我们并不认可每个作者的贡献。你不应该在没有寻求专业建议的情况下依赖一个作者的作品。详见我们的* [*读者术语*](/readers-terms-b5d780a700a4) *。*

更多信息，请关注/联系 Linkedin:[https://www.linkedin.com/in/timstleung/](https://www.linkedin.com/in/timstleung/)