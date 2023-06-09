# 神经网络:弗兰克尔的奇迹

> 原文：<https://towardsdatascience.com/neural-networks-frankles-miracle-dfbd031ae1be?source=collection_archive---------59----------------------->

## ~ *最新的剪枝协议是一个万亿美元的火箭~*

![](img/b7e00782722b73c98721be9850357a17.png)

由[亚历克斯·霍利奥克](https://unsplash.com/@stairhopper?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/bonsai?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

**TL；凭借彩票成名的**博士乔纳森·弗兰克尔和迈克尔·卡宾，以及亚历克斯·伦达，已经做出了 [*完美的修枝剪*](https://arxiv.org/pdf/2003.02389.pdf) ，尽你所能地缩小神经网络，**而**不会牺牲准确性。而且，这个方法非常简单。当你把在边缘获得的效用加起来*时，这些研究人员在加利福尼亚是值得的。不夸张。*

**本书**

保罗·鄂尔多斯，上个世纪最伟大也是迄今为止最多产的数学家之一，会爱上那些证明和定理，它们以其绝对的简单、优雅、广泛的影响和富有洞察力的技巧，必定来自“那本书”。

这里，鄂尔多斯的意思是上帝用来创造世界的真理卷轴。数学家们像朝圣者一样聚集在这些证据周围。正是它们激励我们花几十年时间进行徒劳的斗争。所以，当我听到这个消息，看到弗兰克尔的论文时，他的评论让我不寒而栗:“**这是……从书上来的。**“我怀疑他感觉好像有一份金色的礼物飘进了他的大腿。这些真理是如此简单，以至于它们似乎是迷宫中的错误转弯，然而它们却打开了不可能的新前景。

而且，当我们看到从这种根本性转变演变而来的一连串影响时，我们应该清楚这是一个强大的工具——赫菲斯托斯的铁砧。

**自主滑行**

为了说明弗兰克尔的修剪有什么价值，想象一下你刚刚花了 1000 美元买了一辆自动驾驶汽车，作为出租车的副业来赚取收入。那辆车要在六年内付清，每天需要留出 50 美分——利润需要比这更多，如果利润大得多，就会刺激更多的出租车。

现在，把它和一台价值 1000 美元的数控机床做个比较，每两周*就会吐出另一辆自动出租车*。哇哦。这将很快收回成本，并产生巨大的利润。每个人都会想买那辆 CNC，因为它的**成本**是**分摊**在*越来越多的自动驾驶出租车*上。

你不仅被这些利润所激励；增加的供应降低了价格，更低的单位 T2 资本成本让你继续在这些价格上获利。因此，消费者和生产者都带着更多的钱离开，与此同时，出租车服务非常丰富，本身就产生了巨大的价值。

那么，剪枝算法是如何为神经网络做这种事情的呢？

**法兰克林**

当谷歌训练其最新的自然语言模型时，它必须在大规模并行专用处理器机架上运行数周。最近的其他巨头也是如此；每一个**吸收计算机的使用**—**一个**超级计算机，**一次一个** *有用服务*实例。如果对该服务的需求增加，您将需要更多的机架，因此它仍然昂贵，部分抑制了需求，这意味着它为市场提供的总价值减少了。

相比之下，如果你能把这个庞然大物缩小到一个茶杯里，那么每个人的手机或笔记本电脑就足以产生这种有用的服务。而且，向数亿用户推出这项服务实际上是免费的。所以，最初的超级计算机时间*每翻一次*产生更多的美元。此外，最重要的是，计算机可以继续开发更多手机应用大小的人工智能，就像我们制造自动出租车的数控机器一样。这些应用程序中的每一个都以最低的成本为如此多的人提供了实用工具，这将比其他方式更快地推动对每一个定制应用程序的投资*。*

*这与杰冯悖论有关——当机器变得更加节能时，每一美元的能源都会产生更多的收入，所以你最终会使用更多的能源，因为它是高效的。能源总需求*增加*。考虑到有多少个数量级的**与科学相关的网络更便宜，以及推出众多专家是多么容易，我预计对能源、计算、数据、人才、洞察力的需求将大大增加，*加速整个行业的开发和部署*。***

***向上跳跃一个指数***

*正如我们的全球危机令人痛苦地表明的那样，一条指数曲线即使只是稍微陡一点点就会变得势不可挡。而且，如果你能*将*延迟一个指数级的时间，哪怕是很短的时间，那*的百分比损失*就会在未来的每一个时刻持续下去，累积的贴现成本*至少是延迟时刻*的损失的 8 倍。因此，每三天增加一倍的疾病，延迟六天，在未来的所有时间里有四分之一的人患病。*

*同样，如果你以指数形式向前*跳跃*，你将获得巨大的累积贴现收益。增加该指数的陡度甚至更多。据我所知，弗兰克尔的美丽盆景是一个越来越陡峭的曲线。如果 10 亿人每人每天受益超过*35 美分，那么按照保守的估计，这就值几万亿。每部手机上的超级计算机人工智能可能会有更大的帮助。**

**最让我惊讶的是这种技术*竟然可以存在*！在抽象、虚幻的数学世界中，是什么让这种方法成功了呢？弗兰克一定听到了拉马努金天使的低语。正是这种美丽而神秘的巧合让我对毕达哥拉斯的故事肃然起敬——“宇宙是由数字组成的。”**