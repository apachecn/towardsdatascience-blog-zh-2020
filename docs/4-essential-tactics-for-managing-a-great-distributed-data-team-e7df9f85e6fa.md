# 管理大型分布式数据团队的 4 个基本策略

> 原文：<https://towardsdatascience.com/4-essential-tactics-for-managing-a-great-distributed-data-team-e7df9f85e6fa?source=collection_archive---------46----------------------->

## 给我们远程第一世界的数据领导者的建议。

![](img/bfc1976611009ce0557d0730c695bda4.png)

图片由[克里斯·蒙哥马利](https://unsplash.com/photos/smgTvepind4)在 [Unsplash](http://unsplash.com) 上提供。

*新冠肺炎已经迫使几乎每个组织适应新的劳动力现实:分布式团队。我们分享四个关键策略，让您的远程数据团队成为整个公司的力量倍增器。*

现在是第 6 个月(还是 72 个月？很难说)全球疫情，尽管从你的卧室到餐桌的通勤时间很短，但你仍在适应这种新常态。

您的团队负责所有相同的任务(处理临时查询、修复损坏的管道、实现新的规则和逻辑等)。)，但是对损坏的数据进行故障排除只会变得更加困难。当你们彼此相距 5 英尺远时，确定一个 [**数据停机**](https://www.montecarlodata.com/the-rise-of-data-downtime/) 事件的根本原因已经足够困难了；当你在不同的时区工作时，这要困难 10 倍。

分布式团队并不新奇，事实上，在过去的几十年里，它们变得越来越普遍，但是在疫情期间工作对每个人来说都是新的。虽然这种转变扩大了地理人才库，但这种规模的合作会带来不可预见的障碍，特别是在处理实时数据时。

你每天的站立只能让你到此为止。

以下是管理大型分布式数据团队的 4 个基本步骤:

# 记录所有的事情

当团队被分配时，关于哪些表和列是“好的或坏的”的信息被分解。我们在一家领先的电子商务公司采访的一位数据科学家告诉我们，团队需要花 9 个月的时间来开发一种蜘蛛感知能力，了解哪些数据位于何处，哪些表是“正确的”，哪些列是健康的，哪些是实验性的。

答案？**考虑投资数据目录或沿袭解决方案**。这种技术提供了一个关于团队数据资产的真实来源，并使理解数据输入的格式和样式指南变得容易。当数据治理和法规遵从性开始发挥作用时，数据目录变得尤为重要，这是金融服务、医疗保健和许多其他行业的数据团队最关心的问题。

# 为数据设置 SLA 和 SLO

不仅要确保数据团队成员之间的一致性，还要确保与数据消费者(即营销、高管或运营团队)的一致性，这一点非常重要。要做到这一点，我们建议从[站点可靠性工程](https://landing.google.com/sre/)书籍中抽出一页，为数据设置并调整清晰的服务级别协议(SLA)和服务级别目标(SLO)。围绕数据新鲜度、数量和分布的期望 SLA，以及可观察性的其他[支柱](https://www.montecarlodata.com/what-is-data-observability/)，在这里将是至关重要的。

[Reddit 的数据科学经理 Katie Bauer](https://www.linkedin.com/in/mkatiebauer) 建议分布式数据团队保留一份重要项目的预期交付日期的中心文件，并每周审查该文件。

她说:“当利益相关者提出问题时，我可以很容易地访问这份文件来寻找答案，而不是在一周内 ping 我的团队进行更新。”“这让我们专注于交付工作，避免不必要的转移。”

# 投资自助工具

投资自助式数据工具(包括像雪花和红移这样的云仓库，以及像 Mode、Tableau 和 Looker 这样的数据分析解决方案)将简化数据民主化，无论数据用户的位置或角色如何。

同样，自助式版本控制系统有助于每个人在大型工作流上进行协作时保持一致，这在跨时区利用实时数据时变得极其重要。

# 优先考虑数据可靠性

负责管理 PII 和其他敏感客户信息的行业，如医疗保健和金融服务，对错误的容忍度很低。数据团队需要确信，从消费到输出，数据在整个管道中都是安全和准确的。围绕数据可靠性的正确流程和程序可以防止此类[数据停机事件](https://www.montecarlodata.com/the-rise-of-data-downtime/)并恢复对您数据的信任。

许多年来，数据质量监控是数据团队捕获不完整数据的主要方式，但这种方式不再适用，尤其是当实时数据和分布式团队成为常态时。我们的远程优先世界需要一个更全面的解决方案，能够无缝跟踪数据可观察性的五大支柱以及根据您组织的需求量身定制的其他重要数据健康指标。

# 记住:不好也是好的

我们希望这些建议能帮助你接受甚至拥抱数据世界的新常态。

然而，除了这些更具战术性的建议之外，记住**不好也没关系**也无妨。[git lab 的第一位数据分析师 Emilie Schario](https://www.linkedin.com/in/emilieschario) ，现在是内部战略顾问，说得好:“这不是普通的远程工作。在全球疫情的强制远程工作期间取得成功的要素与“照常远程工作”的含义不同。”

*我们很想听听你对领导分布式团队的建议！向* [*巴尔摩西*](https://www.linkedin.com/in/barrmoses) *伸出你的智慧之言。*

这篇文章是由[威尔·罗宾斯](https://www.linkedin.com/in/will-robins/) & [巴尔·摩西](https://www.linkedin.com/in/barrmoses/)写的。