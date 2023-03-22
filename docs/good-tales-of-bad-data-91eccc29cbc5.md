# 坏数据的好故事

> 原文：<https://towardsdatascience.com/good-tales-of-bad-data-91eccc29cbc5?source=collection_archive---------50----------------------->

## *当数据中断而无人听到时，它会发出声音吗？*

![](img/0a5c111ca7c7994d51a22b757136c105.png)

本文中的所有插图均由马丁·阿隆索·拉戈提供。

遇见茱莉亚。她是一名数据工程师。Julia 负责确保您的数据仓库和湖泊不会变成数据沼泽，并且一般来说，您的数据管道处于良好的工作状态。

![](img/58f89ecbe19b43cc2ff715954bc3f939.png)

Julia 很高兴什么都没发生，但像任何优秀的工程师一样，她知道这几乎是不可能的。所以，她只是想第一个知道问题何时出现，这样她就可以解决它们。

![](img/cd0488f13a5a7b80263c723ad52e2bce.png)

见见泰德。他是数据分析师。Ted 被他的公司称为“SQL 大王”,因为他是他们的营销、客户支持和运营团队的查询负责人。他是 Tableau 的专家，知道所有 Excel 的窍门。泰德也很高兴什么都没发生，和朱莉娅一样，知道这是不可能的。然而，Ted 不希望糟糕的数据毁了他的分析，让他和他的利益相关者的生活变得痛苦(后面会有更多)。

![](img/3c1fb8b8bc153f80c438e4c47483daeb.png)

见见亚历克斯。亚历克斯是一个数据消费者。她可能是数据科学家、产品经理、营销副总裁，甚至是你的 CEO。Alex 利用数据做出更明智的决策，无论是她的新产品应该叫什么名字，还是她应该穿哪双幸运袜去参加明天的董事会议。

Alex，或者公司的其他人，如果不能信任他们的数据，就无法完成他们的工作。我们将这种现象称为数据停机。 [**数据宕机**](https://www.montecarlodata.com/blog/) 指的是数据不准确、丢失或出现其他错误的一段时间，无人幸免，有点像死亡和税收。然而，与死亡和税收不同的是，如果立即采取行动，数据停机是可以很容易避免的。

![](img/7923a314c7c06f339fe0b61ee94c2b4f.png)

当原始数据被您的数据管道消费时，它本身就是抽象的和无意义的。如果有数据停机，这真的无关紧要，因为除了 Julia，没有人真正利用它来传递数据。问题是，她并不总是知道数据是否被破坏。

![](img/e4d3f86f8c1bedd551af426086dd79b2.png)

随着数据在管道中移动，它变得更加具体。一旦它到达公司的商业智能工具，Ted 可以开始使用它，将以前模糊和抽象的东西转化为 Excel 电子表格、Tableau 仪表板和其他美丽的知识容器。

然后，Ted 可以将这些数据(现已接近成熟)转化为可供公司其他部门使用的见解。现在，Alex 可以使用这些数据创建营销宣传材料、pdf 和客户资料，这些数据经过精心处理，非常具体，必将拯救世界。或者是？

![](img/928f4ac8fa417ce584e34a3223ed5159.png)

随着数据错误沿着管道向下移动，数据宕机的严重性会增加。有越来越多的 ted 和 Alexs 使用这些数据，他们中的许多人都不知道他们所看到的是对的、错的还是介于两者之间，直到为时已晚。

你可能会问，什么时候太晚了？

为时已晚的是，Julia 在周一凌晨 3 点被 Ted 呼叫，他的上级经理兼销售副总裁 Alex 打电话给他，就在几分钟前，他还在谈论第二天早上应该向他们的首席执行官提交的一份不可靠的报告。当你浪费了时间、损失了收入、侵蚀了 Alex 和其他人宝贵的信任时，就太晚了。

![](img/0a5c111ca7c7994d51a22b757136c105.png)

> 从 Julia 的原始表格中获得的数据越具体、越远，影响就越严重。我们称之为数据焦虑的**锥体**。

灾难降临了，朱莉娅不知道为什么，更不用说它已经发生了。如果她能在数据宕机发生时立即抓住它，而不是通过 Alex 和她的其他数据消费者(在焦虑的圆锥下)，灾难就可以避免。

最糟糕的是，她正在做一生一次的梦。棉花糖云，巧克力喷泉瀑布，没有空值。与她周一凌晨 3 点面对的现实完全相反。

听起来很熟悉？是的，我支持你。

***如果您经历过数据停机，我们希望听到您的反馈！*** [***伸手***](http://montecarlodata.com?utm_source=bog&utm_medium=medium&utm_campaign=good_tales_bad_data&utm_term=august) ***向巴尔亮出自己的好消息坏数据。***

*本文由* [*巴尔摩西*](https://www.linkedin.com/in/barrmoses/)*&*[*马丁阿隆索拉戈*](https://www.linkedin.com/in/martinalonso/) *共同撰写。*