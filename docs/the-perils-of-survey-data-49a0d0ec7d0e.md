# 调查数据的风险

> 原文：<https://towardsdatascience.com/the-perils-of-survey-data-49a0d0ec7d0e?source=collection_archive---------34----------------------->

![](img/c1af0055fb0bb802d03d94238a043f16.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由 [Helloquence](https://unsplash.com/@helloquence?utm_source=medium&utm_medium=referral) 拍摄的照片

## 不要落入这些调查数据的陷阱

尽管调查很少是理想的，但在某些情况下，它是获取数据的唯一途径。直接问一个人问题意味着数据会有偏差，不一定反映事实。任何数据科学家都知道，分析的好坏取决于数据，所以数据最好是好的。

在本文中，我将概述一些常见的调查陷阱，以及如何避免它们以设计更好的在线调查。

# 陷阱 1:从众偏差(社会合意性偏差)。

从众偏见是指调查者意识到他们*应该*根据群体中的从众心理回答什么，而不是他们实际上的想法。

例如，给定问题“你的大学经历如何？”从哈佛或斯坦福这样的名牌大学毕业的人可能会偏向于给出更高的分数，因为他们觉得自己属于“精英”群体。回答一个人的大学经历不愉快，从某种意义上说，就是把大学和这个人分开。因此，如果 Bob 不喜欢耶鲁，他很有可能会在匿名调查中回答说他有过积极的经历。如果他回答“不，我有过糟糕的经历”，他可能会觉得自己不是真正的耶鲁校友。

另一个例子是洛杉矶的政治中立公民，他们不太关注政治。当问及他们的政治观点时，他们可能会支持民主党的理想，以符合他们的社区和朋友。

重要的是要认识到匿名并不能解决偏见。人们在调查中有意识地带着偏见回答，不是因为他们关心调查者看到了什么；他们用有意识的偏见来回答，比如从众偏见，因为这让他们自我感觉更好。在从众偏见的情况下，如果他们的回答更像他们的社区或朋友，他们会觉得不那么孤独。在处理意识偏见时，这是一个需要理解的重要概念。

减少从众偏见的一个方法是将人口统计学问题放在调查的最后。研究已经表明，通过将引起从众偏见和社区的问题放在调查的最后，用户可以更诚实地回答问题。

像“你的最高教育水平是什么”、“你来自哪个地理区域”、“你是什么性别”、“你是哪个种族”等问题会强化会导致从众偏见的社区意识。

# 陷阱 2:"从 1 到 5 排列 *x*

主观排名是调查中的一大缺陷。要求用户从“1 到 5”进行排序的问题容易受到 1 和 5 的主观含义的影响。在数据分析中，客观才是王道。

当互联网文化中心 Reddit 被设计的时候，它的创造者最初考虑了一个 5 星级系统来对帖子进行排名，但选择了一个向上投票-向下投票系统，因为在 5 星级系统中有太多的主观性。毕竟，对鲍勃来说是 2，对汤姆来说是 4。

当使用等级问题时，考虑自由和主观之间的平衡是很重要的。具有更多评级选项的系统将为分析师提供更多数据，但也增加了主观性，因此降低了数据质量。在 Reddit 的例子中，不需要 5 星评分，因为 Reddit 需要的只是用户是否喜欢它，而不是*量级*(他们喜欢与否的程度)。Reddit 拥有如此海量的数据，以至于每个用户的数量级都微不足道。设计调查时，请记住问题试图为分析师完成什么。

甚至李克特量表(强烈不同意，不同意，中立，同意，强烈同意)也可以判定。一项去除了李克特“中性”选项的研究产生了更真实的结果，因为“中性”是一个快速的下一个问题按钮，几乎不需要思考。通过迫使调查者同意或不同意，它可以给你比“中立”更多的见解。但是，如何使用它取决于问题场景。

设计问题时，选择给出的最佳选项数量。试着给每个数字或选项的含义附上一个客观的衡量标准，并且永远记住分析师。

# 陷阱 3:问太多问题

不要问太多问题。这似乎是显而易见的，但调查创建者往往会塞进一些不必要的问题，心想，“*这只是两个问题。不会有太大影响。*

在设计调查之前，记住目标——每个问题都应该回答目标的一部分。问太多的问题(尤其是在无报酬的调查中)会减少完成调查的人数，并使完成调查的受访者匆忙完成问题。

问更多的问题也不一定意味着分析师有更多的数据。分析师知道，对带有大量噪音和与目标无关的问题的数据执行统计模型会使分析师的生活变得更加困难。如果数据集中有足够多的噪声，噪声就不再是噪声，因为它在统计上变得很重要。

把几个问题缩小成一个问题，是信息量和信息质量的平衡。一个上升，另一个下降。每个问题的设计都应该考虑到分析师——正是他们从调查数据中挖掘见解。

如果你的调查足够短，显示“ *x* 分钟完成”，其中 *x* 足够短，结合一个简短的关于调查参与者可能产生的积极影响的简介，将会提高参与度。当问题数量较少时，收件人会在每个问题上花费更长的时间和更多的思考。

# 陷阱 4:分配不均

当你发布公众调查时，你应该有一个目标受众。重要的是要意识到用于分发调查的模式如何影响哪类人对调查做出回应。

例如，针对某个州的在线总统选举投票可能会减少那些没有常规互联网接入的贫困选民。

确保调查受访者代表目标受众是很重要的。毕竟，调查是基于这样一种想法进行的，即某些随机选择的人代表了一个总体。

有许多传播媒介。重要的是要认识到每一个人如何减少特定的人口统计数据(或放大目标人口统计数据)。

重要的是要认识到，在测量中，数量不一定是质量。类似于增加冗余问题的数量，将更多不属于目标受众的人添加到调查受访者中会增加分析的噪音。如果有太多的噪音，它会扭曲分析。

# 总之…

当你设计调查时，

*   尽量把人口统计学问题留到最后，避免引发从众偏见。
*   确保选项是客观的，并且只根据分析师的意图为问题选择合适的选项。
*   设计调查时，每个问题都应该回答调查大目标的很大一部分。不要问不必要的问题。
*   注意你如何分发你的调查——不均匀的分发会误导分析。确定目标受众，并确保几乎所有接受调查的人都是该受众的一部分。