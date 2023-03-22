# 动物穿越评论的情感分析

> 原文：<https://towardsdatascience.com/sentiment-analysis-of-animal-crossing-reviews-7ae98bc91dd3?source=collection_archive---------43----------------------->

在对星谷的狂热之后，我想我再也不会回到任何需要耕种/囤积/捕鱼/采矿的游戏中去了。但是我在这里:自从我 3 月 22 日买了《动物穿越:新视野》(ACNH)以来，总共花了 100 个小时，这比 BotW 还多小时。说真的，ACNH 不是一个我认为我会喜欢的游戏:没有什么太令人兴奋的，只是一堆研磨。但它很可爱，而且它来得正是时候，让我(和许多人)在保持社交距离的同时与朋友联系。Polygon 上有一篇关于这种游戏中的研磨元素如何提供一定程度的放松和舒适的文章。因此，自 3 月 20 日发布以来，ACNH 的销量直线上升就不足为奇了，谷歌对 ACNH 的搜索量也是如此。

![](img/8d00d5d7d969739ca9ca196e337e798d.png)

谷歌搜索对动物穿越和任天堂 Switch 的兴趣

该图还显示，对 ACNH 的兴趣增加也增加了对任天堂 Switch 的兴趣。而且，任天堂 Switch 现在几乎在所有地方都卖光了，包括在 T2。[新闻](https://www.gamesindustry.biz/articles/2020-03-25-animal-crossing-new-horizons-breaks-switch-sales-records-in-japan)报道 ACNH 打破了任天堂 Switch 冠军在日本的销售记录。亚马逊上的 ACNH 纸质版的价格也几乎翻了一番。我大胆的推断是，任天堂 Switch 销量的增加和 ACNH 销量的增加是正相关的。

似乎 ACNH 很受玩家欢迎。然而，当我在一些游戏网站上查看评论时，如 GameSpot 和 Metacritic，平均用户评分分别为 6.4 和 5.2/10，尽管该网站的官方评级为 9/10。那么，为什么玩家对这款游戏的评价比官方评测人员差呢？我对用户评分感到惊讶(我会给 7/10，比神奇宝贝剑与盾更好)，我很好奇用户对 ACNH 的看法。

所以，我做了一个快速的**情感分析**(因为我刚刚从克里斯·毛雷尔教授本周的文本分析课上学到了它)。我首先使用 Python 上的[beautiful soup](/web-scraping-metacritic-reviews-using-beautifulsoup-63801bbe200e)从 Metacritic 中删除评审数据。然后，在使用 r 进行情感分析之前，我对 CSV 文件进行了一点格式化。我比较了来自[词典](https://cran.r-project.org/web/packages/lexicon/lexicon.pdf)包的几个词典，并决定 Hu-Liu、Jockers-Rinker 和 NRC 词典最适合我在分析元评论时使用，因为它们在情感评分方面具有一致性。

## 用户评论的平均情感分数

![](img/35972a5731aefc87a57396b70463cf90.png)

平均情绪得分

由三个词典生成的平均情感得分表明，用户评论通常不太正面(0 为中性，1 为正面)。然而，在最近的评论中有一个越来越积极的趋势。评论中不太积极的情绪得分并不令人惊讶，因为在 3450 个用户评级中，几乎有 50%是负面的。高度正面的评论可以被高度负面的评论抵消，从而得到相对中性的分数。

## 用户评论中的正面词和负面词

那么，这些 Metacritic 用户在评论中谈论的是什么呢？我整理了由胡-刘和 Jockers-Rinker 词典(未显示)生成的消极和积极词汇的列表，并根据它们的频率制作了词云。

![](img/bfd7cc60cb9d8ba4fe0778abbe0b7818.png)

否定词云

我猜人们不喜欢这个游戏中的资本主义思想，并把汤姆·努克描述成独裁者，而我们(玩家)是他的奴隶(支付我们的住房贷款)。限制”是最常出现的负面词汇。我推断这种频繁发生是由于用户抱怨每个控制台一个岛的限制(也许？). '“失望”出现，表明由于炒作，这些用户的期望很高。

![](img/f753b0ee178f15193721fc5d91e512e2.png)

正词云

这个正面词云以“好玩”为最常出现的正面词。像“享受”、“享受”和“享受”这样的词经常出现，足以推断一些用户确实喜欢这个游戏。

这两个字云恰恰说明了喜欢游戏的人对游戏的趣味性和创意元素赞不绝口，认为这个游戏很神奇(等等。).他们非常喜欢这个游戏，因此给予了积极的评价和很高的评分。那些不喜欢游戏的人给了很低的分数(读“0”)，并在他们的评论中使用更严厉的词语，如“独裁者”、“奴隶”、“失望”。这些恰恰说明 ACNH 是一个收到两极分化意见的游戏。

## 用户评论中的情感

![](img/a532b82837958d2c3b81447c93a84317.png)

词语及其与情感的关联

我还用 NRC 的词典研究了与这些评论相关的情绪。尽管用户最常使用与信任相关的词，但像“系统”、“账户”和“系列”这样的词并不能表达用户对游戏的态度。像“长”、“等待”和“开始”这样的期待词在这里也没有太多意义。表示快乐的单词似乎也出现得更频繁。悲伤、厌恶、愤怒和恐惧是在这个评论集中检测到的负面情绪。他们最有可能与那些评价低的评论联系在一起。

![](img/0963c195bb67259dda96698428a984e8.png)

情感-词词云

出于好奇，我做了这个分析。似乎 Metacritic 用户对 ACNH 的意见两极分化，如中性情绪得分、正面和负面词云以及网站上的评级百分比所示。但这种感性的分析并没有讲述 ACNH 评论的全部故事。我意识到这个分析的局限性，尤其是关于情感的分析。Metacritic 用户也不能很好地代表 ACNH 玩家，因为它只是为数不多的游戏评论网站之一。YouTube 可能是另一个平台，玩家可以在这里谈论游戏并分享他们的经历。