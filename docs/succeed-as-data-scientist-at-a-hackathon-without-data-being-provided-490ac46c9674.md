# 在没有提供数据的情况下，作为一名数据科学家在黑客马拉松中取得成功

> 原文：<https://towardsdatascience.com/succeed-as-data-scientist-at-a-hackathon-without-data-being-provided-490ac46c9674?source=collection_archive---------66----------------------->

## 黑客马拉松应该做什么，不应该做什么

![](img/6cf40e1bf7659afc21fa6401d4559a54.png)

# **简介**

上个月，我参加了我的第一次黑客马拉松，因为我收到了一封来自我的大学的随机广告邮件，这封邮件宣传了一个听起来很酷的东西。我点击它，看到他们正在寻找不同技能的团队，也包括数据科学家。**牛逼**我以为**，我进去了！**

> 我报名、申请并被录取了。答对了。

> 简单介绍一下我的背景可能会有帮助。我目前在德国攻读计算机科学硕士学位的第一年，我在兼职做机器学习工程师。所以我知道一些基础知识，但是，我想黑客马拉松也是为了让新手加入游戏，让他们与志同道合的人交往。

由于这是我的第一次黑客马拉松，我认为一个月的持续时间或多或少是正常的。我查了一下其他的黑客马拉松，是**不是**！

> 艰难时期。

我最终加入了一个由来自世界各地的 9 人组成的随机团队。这些人真的很了不起，非常有野心，这也是游戏走到这一步的动力。

# **黑客马拉松开始**

正式开始了。我们先打了几个电话，相互了解了一下，头几天除了头脑风暴什么也没做。由于这次黑客马拉松持续时间特别长，我们有时间思考，所以没关系。但是等等…我是团队的数据科学家，对吗？我注册时期望我会收到一些数据。甚至在开始之前，我就已经想好了我要分析什么东西！

*   销售？
*   营销？
*   也许是一些产品研究？

三天过去了。没有收到。玩得好的黑客马拉松公司！好吧，该怎么办？我可以从网上搜集数据。由于我是做营销或者销售为主的数据科学，所以先查了一下:*如何刮 Instagram。*

可能会有用，但是，嘿，那是第三天，我们不知道我们想要哪个产品和策略，所以我不知道从 Instagram 上刮什么。

> *旁注:半决赛在头两周之后举行，在被选入前七名的团队之后，我们还有十天的时间提交最终报告。*

第一周已经过去了，我们对产品有了一些粗略的计划。我基本上转换成了想法产生者的角色，因为没有其他事情可做。在此期间，我发现有很多像 Statista 这样的网站提供的产品相关的销售数据。我认为很好，但是……这要花钱(€)。

你可能觉得现在是我刮 Instagram 数据做营销分析的时候了。让我感兴趣的是，在过去的几个月/几年中，为了找到我们产品的趋势，如何使用和搜索特定的关键词或标签。哦不！我很容易抓取图片和它们的标签，但 Instagram 的关键词分析也是如此..花钱(€)。

> 旁注:在此期间，我有考试和工作要做，所以我不能像其他人一样，花整整一个月的时间在这个黑客马拉松上。

# 进入决赛——只有前七名的队伍。

事实证明我的团队非常聪明。在展示了我们的半决赛展示后，我们被选中进入决赛。我提供了许多想法和想法，但数据科学相关的见解？**还没有！**我现在真的很想为决赛做一些数据科学方面的工作。

> *我有主意了！*

这是怎么回事..一个是，一个**调查**！

事实证明，用 Google Survey 建立一个调查是相当容易的。我花了几个小时想了一些好问题，尽管我以前从未这样做过。我想我不想用一个 10 分钟就能完成的调查来烦扰人们。因此，我只选择了七个问题，并试图涵盖尽可能多的内容，例如:

*   人口统计学
*   收入
*   愿意使用这种新品种和其他一些品种
*   愿意花多少钱

在想出清晰具体的问题后，我把它发给了我所有的联系人。我所有的团队成员都把它发给了他们的联系人。但是，这还不够！

> 如果黑客马拉松公司不想向我提供数据，他们至少应该承担责任，将我的调查分发给他们公司的实习生。

## ***我的调查 400 票~万岁😊***

收集了两天的投票，从 Google Survey 下载了结果为 **CSV** 文件，超级好看。最后，是时候做一些数据分析了。不幸的是，我不能展示我的任何图，因为这是*机密*和*机密*信息，但让我这样说吧，Seaborn 发布了一个新版本，其中他们制作了带有*hist plot*pre eetient 的二元图，很好且易于使用。

[https://seaborn.pydata.org/tutorial/distributions.html](https://seaborn.pydata.org/tutorial/distributions.html)

现在，我可以根据调查问题，用所谓的**人物角色**来支持我的团队。这是一项营销工作，用来识别和描述最有可能购买我们产品的人。

我还可以评估其他指标来支持销售团队，并评估用户行为，以便向我们的设计师提出这个问题，并以这种方式调整产品设计。

# **结论**

总的来说，我学到了很多。我不会再参加为期一个月的黑客马拉松，但肯定会参加一个更短的。我学到的是，我现在提前询问数据是否将由**提供**或**而不是**。也许这是我参加的这次黑客马拉松的一个特例，因为它不太像黑客马拉松，而更像是一次创意推介。

如果你计划参加这样的活动，请记住这一点。

> *强烈推荐！*

## 等等，你不能不告诉我们你赢了就走！

我们没有。我们在 130 名参与者和 30 个团队中获得了第二名**名，并赢得了丰厚的奖品。足够好我猜:)。**

*感谢阅读。*