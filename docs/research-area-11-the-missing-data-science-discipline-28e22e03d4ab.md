# 研究领域 11:缺失的数据科学学科

> 原文：<https://towardsdatascience.com/research-area-11-the-missing-data-science-discipline-28e22e03d4ab?source=collection_archive---------56----------------------->

![](img/78f4bc029030ee0fdda213038b5d30f6.png)

[活动发起人](https://unsplash.com/@campaign_creators?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/database?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

上个月末，麻省理工学院出版社发表了一篇[文章](https://hdsr.mitpress.mit.edu/pub/d9j96ne4/release/2)，向学术数据科学社区提出了 10 个研究课题。作为一名与许多数据科学家密切合作的数据工程师，我从未想过我自己也可能是一名数据科学家。我当然不认为自己是一个学者，但是本文中提出的大部分研究领域比我的数据科学同事更接近我作为数据工程师的工作。这篇文章启发我重新考虑我自己的工作如何与学术学科相适应。一路走来，我意识到数据工程自动化中的巨大漏洞，以及最终这篇文章，是我想了很多(可能太多)的东西。

随着数据爱好者将数据引入公司的生态系统，您的数据工程师的效率和支持他们工作的技术会对您公司的其他数据专业人员产生下游影响。作为数据工程师目前面临的最大挑战，研究领域 11 最终是当今以数据为中心的公司面临的最大障碍。

# **研究领域 11:数据映射自动化**

***有什么问题？***

数据科学家经常开玩笑说，他们 90%的工作涉及准备数据以供分析。他们开玩笑，但这是真的。数据集的准备非常耗时，充满了错误，并且是费力的手动操作。这就是为什么大公司雇佣数据工程师，专注于将原始数据流转化为分析友好的数据库。将这项工作从获得博士学位的数据科学家身上卸下，使他们能够专注于他们花了数年时间完善的分析技术。这一转变是整个行业令人难以置信的进步。

数据工程师是数据科学家转变为软件工程师，或者软件工程师转变为数据科学家，他们的大脑预先忙于处理最杂乱的数据，并将其转换为逻辑和内容相关的数据结构。数据工程师不断应对极其复杂的挑战。虽然有一些数据集成工具可以帮助存储和查询非常大的数据，还有一些工具有助于向分析师公开数据，但数据工程师的大部分工作负载都不受任何现有工具的支持。不幸的是，他们的大部分工作都是手工的。

***为什么会这样？***

如果我们可以获取原始数据，并将其输入到一个可以理解其内容并将其重塑为您的数据模型的工具中，这难道不可思议吗？所有的数据都需要整合和规范化，而且没有任何技术可以自动完成这一关键步骤。构建这种自动化技术的障碍是缺乏对这种工具所需的复杂数据科学技术的关注和认可。

***这个学科的重点是什么？***

整合和规范化需要对数据的含义有一个人类层面的理解，即语义。

假设我们有两个数据集，它们具有以下编码方案:

**例 1**

*婚姻状况:已婚、单身、离婚、与重要的其他人同居*

*has_partner: TRUE，FALSE*

这些数据没有完全重叠，前者提供了更细粒度的数据。如果我们要规范化这两列，我们将把列 1 转换成列 2；值 1 和 4 表示真，而其他值将被编码为假。这个挑战花了我几秒钟就解决了，但是更复杂的情况呢？

**例 2**

*故障 _ 睡眠:真，假*

*睡眠质量:非常差，有点差，有点好，非常好*

我们不仅需要定义希望合并的列之间的映射，还需要确保我们只在包含相同信息的列之间创建映射。在匆忙中，您可能会试图通过将包含单词“bad”的值转换为 TRUE，将包含单词“good”的值转换为 FALSE 来转换后者。我自己最近也差点这样做，但最终还是决定咨询一位同事，他让我相信这两个属性虽然相关，但实际上是两个不同的概念。比方说，一个人在睡眠方面很专业，但是在早上感觉很糟糕。他们睡眠质量很差，但绝对没有睡眠问题。

不用说，跨数据库映射概念是极其微妙的。如果您的数据科学小组着手处理非常简单的数据集或很少获得新的数据流，这种手动工作在小范围内是可以管理的，但这项任务在不断扩大的数据公司中会迅速放大。

***这样的自动化会做什么？***

为了实现这种类型的自动化，新数据集需要经历一个逐步的过程。

**模式合成**

所有数据都有预先确定的结构。模式对数据的表名(如果适用)、属性名、属性类型、数据类型、引用规则(如果适用)以及是否需要空值进行分类。当这些信息可用时，它提供了一个很好的起点。通常情况下，该模式不可用或已过期。

如果缺少这些信息还不够的话，标准模式缺少很多最相关的信息。例如，文本字段是用最少的规则手写的自由形式的文本，还是种族或性别等分类属性？它是否是有序字段，如五分制？只有 1 和 0 的数字列是布尔值吗？

麻省理工学院的学生旨在创造一种检测关系模式的方法，你可以在这里找到他们的期末论文。

**语义数据类型化**

模式包含丰富的信息，但很少揭示数据所表达的含义。您可能会从“婚姻状况”和“睡眠问题”等信息性短语中得到一些提示，但是如果表名和列名像“msta”和“tsbool”这样毫无意义，该怎么办呢？如果遇到过大的规范化字典引用表怎么办？突然间，您的属性现在包含不止一个概念。

语义数据类型采用一系列类别标签和一系列示例值，在[夏洛克](https://sherlock.media.mit.edu/)的情况下，应用神经网络将新数据归类到这些预定义的类别中。在医疗保健等行业，数据旨在遵循一套标准的代码，像夏洛克这样的机器学习方法有着巨大的前景。

**映射语义紧密度**

回想一下我上面的例子，计算机是如何计算出已婚或与一个重要的人同居意味着某人有伴侣的呢？当两个数据库以相同的方式存储数据时，映射很容易，但是当它们以不同的方式存储时，我们如何自动检测相似的信息呢？更重要的是，我们如何对这些映射进行评分，以确保关于同一主题的不同信息不会被错误地合并？像 [GloVe](/text-summarization-with-glove-embeddings-1e969ef9a452) 嵌入这样的技术旨在用数学方法表示单词的概念接近度。像阿莱格拉和沙丁胺醇这样的词，它们都是用于不同情况的药物。

数据映射自动化是任何早期数据生命周期自动化的关键步骤；这是一个真实且始终存在的限制因素，影响着公司将输入数据纳入其分析资产的速度。目前没有多少数据集成工具可以帮助您的公司克服这一障碍。自动数据映射是自然语言处理技术的一个特殊应用，需要独特的考虑。因此，我认为这是它自己的数据科学研究领域。