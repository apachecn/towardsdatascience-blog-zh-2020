# 显著性检验的无意义性

> 原文：<https://towardsdatascience.com/the-insignificance-of-significance-testing-6f6a5a91589?source=collection_archive---------26----------------------->

## 克服 p 值的案例

![](img/891d3dca71355d1b98d712bc1d615c1b.png)

卢克·切瑟在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

什么时候科学发现才是真正的发现？什么时候对可能是真的事情的预感会变成人类集体认为是真的事情？

世界是复杂的，很难找到既有意义又能经得起严格测试和复制的新见解。如果我们进入社会科学和生物医学科学的更复杂的领域，这一点尤其如此:大多数研究人员没有物理学家的奢侈，物理学家可以在严格控制的环境中进行数百万次测量(想想大型强子对撞机)，直到对一项发现的有效性只有一丝怀疑。

近年来，许多怀疑的阴影笼罩在看似确定的结果上。社会科学领域的[复制危机](https://en.wikipedia.org/wiki/Replication_crisis)让这些问题更加广泛地为公众所知，这场危机持续至今。以心理学为例:多年来被认为坚如磐石的社会启动等现代范式正在失去可信度，这篇 [Nature 文章](https://www.nature.com/articles/d41586-019-03755-2)称*“许多研究人员表示，他们现在认为社会启动与其说是一种影响人们无意识行为的方式，不如说是一种实物课程，说明不可靠的统计方法如何欺骗科学家发表不可复制的结果。”*这一发现不是例外，而是规律:[根据 2018 年对 200 项元分析的调查，“心理学研究平均来说受到低统计能力的困扰”](https://www.semanticscholar.org/paper/What-Meta-Analyses-Reveal-About-the-Replicability-Stanley-Carter/eb675485c851aba114219799c53d4729d64cd0e7)。

也许这不应该是一个大惊喜:涉及人类或其他复杂生命系统的实验更难控制，增加样本量并找到所有可能的误差源以保护它们的努力可能相当费力。这使得错误很容易溜进来。

## 显著性检定

因此，科学家自然关心找到好的标准来判断他们获得的结果是否真的值得报道。显著性检验的想法试图建立客观的衡量标准，帮助区分科学的好坏。

统计显著性最流行的标准可能是(我 95%确定)p 值。但正如我们将看到的，这个看似“最佳”的标准可能会导致一系列全新的问题。它可以使可疑的结果看起来很可靠，不能给任何东西以有意义的气氛，可以把糟糕的研究隐藏在欺骗性的客观性后面。

p 值，而不是帮助我们，在许多情况下，可能会参与到科学面临的复制危机中。显著性检验并不能取代好的科学，但它可以让人们觉得它确实如此。这就是它的危险所在。

## p 值

p 值是一个相当简单的概念。

如果你在我获取的一些数据中观察到一种效果，并且如果你在数据中有一种导致这种效果的理论(假设你在一项双盲研究中给予药物治疗，并治愈了一组中一定数量的患者和对照组中一定数量的患者)，即使干预根本没有任何效果，你观察到这种效果的可能性有多大(*)？用更抽象的话来说，你在看的变量[是不是彼此没有关系](https://www.simplypsychology.org/p-value.html)？*

*举个例子:假设你把 100 名接受真正药物治疗的病人和 100 名接受安慰剂治疗的病人分成一组。进行试验后，第一组中有 60 人被治愈，而另一组中只有 48 人被治愈。有多大可能这只是一种随机效应，以至于即使药物没有任何作用，你还是会做出这种观察？*

*这种概率与 p 值有关，通常的做法是将其设置为 p <0.05, meaning that the odds of observing the effect, even if the null hypothesis were correct, ***需要小于 5 %,以使结果有效*** 。*

*一般程序[可概述为](https://web.csulb.edu/~msaintg/ppa696/696stsig.htm)如下:*

1.  ***挑选研究假设***
2.  ***陈述零假设***
3.  ***选择错误等级阈值的概率(p 值)***
4.  ***计算统计显著性检验***

## *p 值的问题*

*在我关于糟糕的统计数据的文章中，我谈到了数字给我们带来的虚假的确定性。计算给定假设的小 p 值将实验的成功及其假设的有效性 ***归结为一个小的客观数字*** 。*

*但是这个数字的客观性和有效性是值得怀疑的，原因有很多。*

*p 值与零假设密切相关。但是零假设从何而来，它真正陈述了什么？在理想的环境中，零假设是对零效应的尖锐点估计，然而这只有在绝对最优的实验*中才有意义，其中所有其他可能的效应都被排除在外。**

**但是每一项旨在检验现实生活效果的现实生活研究都是 ***一般地嘈杂，事实上，是系统地如此。每一个真正的零假设都是一个有缺陷的理想化，它假装不再存在系统误差/噪声源，这甚至在大多数高度受控的物理实验中都不成立，更不用说医学或社会科学了。*****

**相应地，在他们 2019 年的论文“[放弃统计显著性](https://www.tandfonline.com/doi/full/10.1080/00031305.2018.1527253)”中，McShane 等人。写**

> **“……用于计算 p 值的统计模型的充分性……以及任何和所有形式的系统误差或非抽样误差，这些误差因场而异，但包括测量误差；信度和效度的问题；有偏样本；非随机治疗分配；思念；无响应；
> 双盲的失败；不合规；令人困惑。生物医学和社会科学的这些特征与零效应和零系统误差的尖锐的零假设的结合是非常成问题的。**

**从纯噪声中可以获得显著的 p 值，如已公布的例子所示(例如在 [Carney，2010](https://www.ncbi.nlm.nih.gov/pubmed/20855902) )。结合一个理想化的零假设并坚持 p 值会导致荒谬的效果，即 ***噪音更大的研究比更多受控的、更干净的研究更有可能(或更容易)产生重要的(但错误的)结果*** ，因此，基于 p 值标准， ***更有可能被发表！*****

**然后 p 值阈值 0.05 完全是任意的。没有真正的科学依据将证据分为统计上显著的和统计上不显著的两类,假设一个看似合理的阈值对于所有学科的所有实验和假设都是完全相同的也是幼稚的。**

**实例化一个任意的阈值对科学思维是有害的，科学思维应该总是 ***包含许多不同的、潜在的未被发现的解释*** 。**

**顺便提一下，这些未被发现的解释也不包括在零假设中。正如安德鲁·盖尔曼[在这里写的](https://stat.columbia.edu/~gelman/research/published/asa_pvalues.pdf)，零假设本身不是一个好的假设，而是 ***扮演了另一个假设*** 的稻草人。将你的假设与一个坏的假设相比较，并不能否定所有其他的，关于数据中正在发生的事情的潜在的更好的假设。**

**最后但同样重要的是，p 值经常被误解，这只会加剧问题。[一项对 791 篇论文的元研究显示，49 %(!)误用了 p 值，并将统计上不显著的结果归类为表明不存在影响](https://www.nature.com/articles/d41586-019-00857-9)。**

## **放弃显著性检验**

> **统计很难。**
> 
> *****麦克沙恩等人。*****

**由于复制危机仍在持续，迫切需要解决方案来提高科学研究的质量。关于 p 值及其滥用的讨论尤其活跃。**

**那怎么办呢？麦克肖恩等人。建议，科学界应该摆脱 p 值，或者至少引入一个远离任何固定阈值的更连续的观点，并将其与试图判断实验结果的许多其他标准平等对待。**

**科学应该减少它在发表过程中的权力，只发表 p 值阈值为 0.05 的论文和报告结果。许多科学家最近站出来反对统计学意义(见这篇[自然文章](https://www.nature.com/articles/d41586-019-00857-9))，看起来一个范式转变是应该的。然而，如果在基础统计学课程中更广泛地教授对统计重要性的批判性观点，这种转变就不会发生。**

**这并没有让我们从对证据采取整体观点的麻烦中解脱出来，这种观点需要根据实验和领域的需要手工定制。根据 p 值高于或低于阈值这一简单事实，用二元陈述得出“有影响”或“无影响”的结论，这是一种危险的倾向。**

**但这需要时间，而学术界的政治也助长了这一问题。例如，作为第一作者发表出版物的压力不鼓励汇集数据:最好是“发现”并发表两个有噪音的结果，而不是将数据集与竞争对手结合起来，以便更好地处理噪音并分享一无所获的可疑名声。**

**问题是:统计学思维对做好科学研究至关重要，但统计学很难，做好科学研究也很难，尤其是在嘈杂和难以控制的环境中。p 值是一个诱人的出路。我们的大脑喜欢将不确定性转化为确定性(正如我在关于[贝叶斯大脑假说](/the-bayesian-brain-hypothesis-35b98847d331#362f)的文章中所探讨的那样)，但这总是冒着将偏见引入我们思维的风险，并且不应该成为 ***【不确定性洗钱】*** 的理由，正如[格尔曼漂亮地指出的](https://stat.columbia.edu/~gelman/research/published/asa_pvalues.pdf)。**

**紧紧抓住统计意义不放，并在此基础上将证据一分为二，这损害了许多科学的质量，最终损害了社会对科学的信任以及他们从中看到的价值。**

**所以是时候放手了。**