# 数据科学是一个谎言

> 原文：<https://towardsdatascience.com/data-science-is-a-lie-d9157b9ed29c?source=collection_archive---------20----------------------->

## 你一直被欺骗着

![](img/b1616cd31903aec483fe805a7bfcdf93.png)

由[约书亚·赫内](https://unsplash.com/@mrthetrain?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄的照片

# 所以你认为你可以预测未来…

> 很难做出预测，尤其是对未来的预测
> 
> — **丹麦谚语**

数据科学就是为预测创建模型(并围绕数据创造故事，稍后会详细介绍)。逻辑似乎很可靠:我们有数据，我们发现模式，我们将这些模式投射到未来，我们获利。这背后的理论一点也不新:它被称为统计学，并且至少已经流传了两个世纪。随着时间的推移，许多术语来描述预测任务的一些方面，如数据挖掘、分析、商业智能、运筹学和房间里最新的大象，称为数据科学。但是让我们不要深究`statistics == data_science`这个话题，也不要对那些为了从数据中获取信息的过程而创造出来的无数流行语吹毛求疵。我想谈一些更现实的东西。

TL；大卫:你无法预测未来。是的，你已经知道了。尽管如此，你还是假装你在一次会议上展示了那张漂亮的图表。你相信所有这些数据中一定有一些知识。稍微有点错误的地图总比没有地图好，对吧？

纳西姆·塔勒布在他最著名的书[中，用了一个简单的比喻来证明我们以前的知识在预测未来方面是多么的脆弱。几个世纪以来，旧世界的人们认为黑天鹅不存在，因为他们从未见过黑天鹅。只有当第一批探险者到达澳大利亚时，他们才意识到天鹅可能有黑色的羽毛。](https://en.wikipedia.org/wiki/The_Black_Swan:_The_Impact_of_the_Highly_Improbable)

这就足以推翻流传了几个世纪的“白天鹅理论”:一只黑色的家禽。这不是一个新的理念。哲学家卡尔·波普尔(1902-1994)将科学理想化为伪造理论并且从不宣称它们是真实的事业。波普尔说，理论只能是错误的，因为我们需要无限的证据来证明理论的完全真实性，而这是不可能的。

我几乎能听到你说*“不错的鸟类哲学，伙计，可惜我生活在勇敢的现实世界里！”*。所以让我们实际一点，好吗？看看国际货币基金组织(IMF)2020 年 1 月的 GDP 增长预测:

![](img/ae7cd59849db76542056084fe9849cba.png)

国际货币基金组织对截至 2020 年 1 月[的 GDP 增长预测](https://www.imf.org/en/Publications/WEO/Issues/2020/01/20/weo-update-january2020)

以下是 2020 年 4 月的预测:

![](img/cd7b0fc9b3132a015debbd5b624fd58b.png)

国际货币基金组织对截至【2020 年 4 月的 GDP 增长预测

他们怎么能在几个月内如此突然地改变自己的预测呢？如果你在文章发表后不久读到这篇文章，你可能知道答案。2019 年 12 月 31 日，中国当局[报告了](https://www.japantimes.co.jp/news/2019/12/31/asia-pacific/science-health-asia-pacific/outbreak-sars-like-pneumonia-investigated-china/)武汉市发生*“连续系列不明原因肺炎患者”*，武汉市将在几周内被命名为新冠肺炎，并被世界卫生组织认为是疫情。通过人类接触传播，它将关闭几乎整个世界的经济。

国际货币基金组织是预测经济的主要机构之一，它可以如此迅速地改变主意，这一事实应该会让你对你可能遇到的任何预测产生怀疑。如果你碰巧是一个所谓的“数据科学家”，我希望你也把这种怀疑应用到你自己的预测中。

你可能会辩称，IMF 从未打算完美预测未来。他们的预测仅仅是对可能情况的估计，以帮助决策者。我同意你，但那不是重点。关键是，一个有可能将持续的经济增长转变为疯狂的过山车的事件根本没有被考虑在内。在接下来的几个月里，他们的“单纯估计”错过了对任何决策者来说最重要的事情。国际货币基金组织这样做不是因为无能或恶意，而是因为他们不可能预料到这一点。这就是塔勒布想说的:最重要的事件是无法预测的，因为我们没有导致它们发生的信息。数据既不隐藏也不难以获取。就是不在那里！

所以，祝你好运，在下一次疫情、自然灾害或热核战争之前几周，你要知道，这些事件才是真正重要的。对于黑天鹅来说，数据——即使你称之为大数据——也帮不了你。

# 为什么我还是不富裕？

> 股票市场预测了过去五次衰退中的九次。
> 
> —保罗·萨缪尔森

如果你仍然被数据科学的魔力所诱惑，你应该马上停止你正在做的一切。是的，别再看这篇文章了。把你的时间花在更有利可图的事情上:股票市场。

对于数据科学家来说，没有比股票市场更好的场景了。有大量的数字数据，公开可用且格式良好。事实上，一些关于机器学习的介绍性文本都是以股市预测为主要任务的。继续努力，尽你所能建立最好的模型。如果你的预测是正确的，你就有资格赚一大笔钱。卖出下跌的股票，买入上涨的股票。冲洗并重复。我已经可以想象你坐在自己的私人飞机上。

可悲的是，这是行不通的。我敢打赌。

根据 T2(一家跟踪全球市场股票价值平均值的公司)的说法，“积极管理的基金在短期和长期内往往表现不佳”。主动管理型基金是那些雇人预测市场趋势并建议应该买入或卖出哪只股票的基金(如果你愿意，你可以称他们为金融数据科学家)。尽管如此，他们还是不能超过他们的基准，这意味着任何人只要在市场上买一点股票就能获得平均回报，就会做得更好。

试图利用过去的数据预测股票市场在交易中有着悠久的传统，被称为*技术分析*(也被称为更好的名字*图表*)。这是一个有争议的话题，直到今天，一些人还信誓旦旦地说这是有效的。他们认为，已经证明市场存在趋势，更重要的是，有一些千万富翁将他们的财富归功于对数据信号的利用。

也许他们是对的。也许股票市场的图表中有趋势。但是，80%的公司，其唯一的工作是战胜市场，不能利用这一点，即使这是真的。都是因为旧的趋势消失了，新的趋势出来了。原来世界不是静止的。事情变化太快，任何预测都变得毫无用处。在这种情况下，投资者最好根本没有地图。

数据科学方法在股票市场预测上的明显失败很能说明问题。现在将上面故事中的“股票市场”改为“公司收入”、“用户偏好”或你的老板让你预测的任何感兴趣的东西。你还对你提供的数字有信心吗？

目前的情况是，我们无法预测最重要的事情——即使它们即将发生——对于我们可以预测的不太重要的事情，我们可能无法从中提取任何价值。但是如果我们设法产生好的、可操作的预测呢？

# 数字和叙述

> 未来无法预测，但未来可以被发明。
> 
> —丹尼斯·加博尔

*【好的】你说*“我还是想玩我的玩具，因为，如果有的话，它们在正常时间工作”*。我问:他们有吗？*

*正如我前面所说的，我们从数据中提取信息的业务已经持续了至少整整两个世纪。所以我们一定非常擅长预测所谓的正常时期的事情。如果我们称某人为专家，那么，他一定是他所在领域的最佳预测者之一，对吗？*

*Philip Tetlock 调查了这种情况是否属实，并询问了许多专家对未来重大事件的预测。不仅专家的表现和外行人几乎一样，所有人都勉强胜过随机猜测。*

*为什么我们仍然称一个记录如此糟糕的人为专家？我的理论是，虽然那些人不太擅长预测，但他们擅长*创造叙事*。他们到处挑选一些数据来创造一个故事。我们喜欢故事！*

*专家们也足够谨慎，不会做出事后容易引起争议的预测，而且他们从来不会精确预测时间。他们说“我们将面临困难时期”，但对困难的时间和程度却有不同的解释。*

*所以，是的，我们可以用数字(对别人或自己)撒谎，这里没有什么大新闻。但是，数据科学家并没有把它作为一个主要问题来解决，而是把它作为他们工作的一个重要部分。*说故事*，他们说。显然，现在它被认为是一种用数字说服人们的技能。或者，正如我最喜欢的 [TED 演讲者](https://www.youtube.com/watch?v=8S0FDjFBj8o)所说的那样，*“为了在这里添加更多的填充符，我将给出几个数字供您考虑”*。*

*在任何公司，员工都会面临交付成果的压力。因此，在泰特洛克的意义上，数据科学家处于成为数据“专家”的特殊地位。在所有的企业政治游戏中，不难想象一些分析师会使用各种各样的讲故事技巧来提出他们能够做出的最佳预测，即使它来自一些虚假的相关性，除了测试数据集之外没有任何预测能力。*

*我甚至不会谈论人类在处理数据时容易受到的所有偏见，无论是在生成预测还是解释预测时。维基百科上列出的所有认知偏见都以某种形式适用于数据科学世界。*

*如果你是从数据科学家那里获得预测的人，问问你自己:这些数字告诉我一些重要的东西吗，或者它们是为了显示你想要的东西而特设的程序的结果？没办法说实话。这就是为什么学术界的严肃研究需要一个[预注册协议](https://en.wikipedia.org/wiki/Preregistration)。一个研究者应该在寻找答案之前问这个问题，否则他可能会被诱惑去回答数据显示的任何问题。我并不是说一家公司应该作为一项科学事业来经营。我要说的是，你至少应该接受这些数字可能是胡言乱语，不管它们背后的模型有多复杂。*

# *结论*

> *所有的模型都是错的，但有些是有用的。*
> 
> *—乔治·博克斯*

*归根结底，这就是数据科学家给公司带来的价值:*

*   *一个无法解释最重要、最意想不到的事件的预测——记住黑天鹅。*
*   *即使在地平线上没有意外事件，并且数据中有一些重要的模式，该模式也可能不再可用，因为当你看到它时，世界已经发生了变化——记住主动基金。*
*   *即使趋势看起来足够一致，可以被利用，预测也可能是精心编造的谎言的结果——记住“专家”。*

*这并不是说数据科学没有地位。人们会做出决定，不管是基于 T2 午餐吃了什么还是基于数据。我会选择后者。如果有的话，数据科学鼓励实验，这导致更快地发现错误。*

*但是如果你已经被炒作所迷惑，变成了一个数据迷，**你就做错了。独角兽创业公司是否在这么做并不重要，因为(1)相关性并不意味着因果关系(也许他们的成功是出于另一个原因),以及(2)你没有考虑到所有不折不扣地遵循数据圣经的失败公司(用塔勒布的话说，它们被埋葬在字母的墓地里)。***

*我在这篇文章中相当讽刺的语气有一个目的:把你从数据驱动世界的乌托邦中带下来。模型的输出不能代替人类比机器做得更好的事情:思考。数据科学不是银弹，有许多缺陷，应该持保留态度。如果你假装不知道，我预测你最终会远离你每天钻研的数据池中的任何真相。*