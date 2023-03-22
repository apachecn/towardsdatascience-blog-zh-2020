# 订阅业务数据科学家指南

> 原文：<https://towardsdatascience.com/the-data-scientists-guide-to-subscription-businesses-70b1fc4b4493?source=collection_archive---------11----------------------->

## 订阅业务指标、数据科学应用等

![](img/200306723b742456cd782ede2353100c.png)

在 [Unsplash](https://unsplash.com/s/photos/business?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上由 [Carlos Muza](https://unsplash.com/@kmuza?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄的照片

你提出的任何数据科学项目都会影响业务，除非你恰好从事数据科学研究。数据科学家应该了解业务，以便开发有效的解决方案。她还必须能够将自己的工作有效地传达给利益相关者。

![](img/f003fc1feef9100e32ee6235e4fdfdf0.png)

数据科学家的粗略估计(来源:作者)

数据科学可以通过多种方式影响业务。首先，使用数据科学的技术可以使产品更加数据驱动。一个例子是产品中的推荐系统，用于向产品用户提供及时的相关内容。

其次，统计模型可以直接优化当前的内部流程，从而提高业务和工程流程的效率，降低运营成本。例如，统计模型可以通过预测仓库的库存水平来帮助物流。

第三，数据科学可以帮助营销和产品发现工作，本质上是将消息传递给尚未了解企业产品的细分市场。我们想到了细分客户群、预测客户行为的模型，以及为行动号召(CTA)对话框生成文案的模型。像根据用户在平台上的行为向用户展示产品特性这样的小事有助于观察所述特性。

当然，这些例子只是数据科学应用的非穷尽列表。然而，所有这些计划最终都会影响企业的关键指标。业务指标有许多定义，有些是专门针对单个业务本身的。幸运的是，许多关键业务指标很容易理解，不需要 MBA 学位。

有许多商业模式，但在本文中，我们将重点关注一种主导模式:**基于订阅的业务**，特别强调数据科学如何帮助优化这些业务。

# 什么是基于订阅的业务？

简单来说，基于订阅的商业模式是一种定期向客户收取产品或服务费用的业务，通常是每月或每年一次。基于订阅的模式在软件企业中非常流行，特别是由于云的兴起，导致了许多软件即服务(SaaS)企业。

请注意，SaaS 业务不一定是基于订阅的业务，因为现收现付模式(如[雪花](https://www.googleadservices.com/pagead/aclk?sa=L&ai=DChcSEwjRyp2Poo7sAhXLq5YKHflaBFUYABAAGgJ0bA&ae=2&ohost=www.google.com&cid=CAESQOD2twesR8ePf0RFFINDUwsCMmcvFQC5qnLaSVftvxrp32Rgw9WkfdbdYYm7Cj2u-70CskfhSzTEV079HV5ZRC4&sig=AOD64_059eDFwlW_3Bxc_1xIbD3r4nF3rg&q&adurl&ved=2ahUKEwiooJSPoo7sAhX-xzgGHYWPD6oQ0Qx6BAg8EAE))确实存在。在后一种情况下，客户只需为使用量付费。然而，通常采用基于订阅的商业模式。

订阅业务的例子包括[网飞的流媒体服务](https://www.netflix.com/signup)，报纸和杂志订阅，如[纽约时报](https://www.nytimes.com/subscription)，以及 [Hello Fresh](https://www.hellofresh.com/) ，向订阅者提供预定的饭菜。

一些老牌科技企业也在采用这种模式。例如，Adobe 也一直在通过其 [Creative Cloud](https://www.adobe.com/au/creativecloud.html) 将 Photoshop 和 Lightroom 等一些知名产品转移到云上。微软的办公套件产品也已经过渡到基于订阅的模式，而不是过去的授权模式。

有些订阅业务拥有大量免费用户，而订阅(高级)用户所占比例很小。我们的目标是建立一个用户网络，这些用户提供的数据可以用来增强付费产品的用户体验。免费用户也可以通过广告赚钱，这也带来了一些用户摩擦，并可以促使他们为付费产品付费，而付费产品通常不含广告。

一个突出的例子是 Spotify 的免费和 Spotify Premium 产品，这两种产品都有。

这种业务的成功取决于随着用户群的增长，该业务如何有效地将其用户群货币化。如果大约 5%的用户群是高级服务的订户，则一个企业被认为是好的，尽管这一比例可以随着更昂贵的订阅费率而降低。

# 到度量标准上！

## 关键财务指标

基于订阅的商业模式的成功通常由两个重要指标决定:**年度经常性收入(ARR)** 和其订阅服务的**流失率**。

ARR 被定义为每个单个订阅的所有**年值的总和。由于可能存在不同等级的订阅计划，因此通常更好的做法是将收入标准化到订户基数。**每用户平均收入****【ARPU】**是对每用户收入贡献的简单平均衡量。**

![](img/5a4dab2096ebfd0898d348dfe39cab13.png)

当订户终止了她与企业的关系时，订户发生骚动。流失率就是**在固定时间段内取消订阅的用户平均数量与活跃用户数量之比**。通常，周期范围设置为 7、14 和 30 天。较长的范围有助于消除由于用户不活动(例如，由于节假日等季节性影响)而导致的不规则性。然而，这是一个滞后指标，因为它只能追溯计算。

**保留曲线**将流失率可视化。这是在队列中测量的，并在订阅开始后的几个月内进行跟踪。理想情况下，我们希望在订阅一年多后，保持较高的保留率，并保持一条平坦或更好的微笑曲线。后者意味着顾客会在几个月后再次光顾。这可以在我画的下图中看到。

![](img/50119aafb8dc9ec4a0c6044761e9abb7.png)

保留曲线(来源:作者)

至于一个真实世界的例子，这篇[文章](https://www.saasquatch.com/blog/blue-apron-addicted-to-acquisition/)有蓝色围裙、Hello Fresh、美元剃须俱乐部和网飞的保持曲线。网飞的保留度最好，而 Hello Fresh 最差。

最后一个相关指标是净收入留存，这是 SaaS 企业经常使用的指标，也是造成流失的财务原因。给定一个群组，该群组的每月经常性收入(MRR)除以一年前的 MRR。这一指标不仅反映了收入流失的影响，还反映了升级和交叉销售等其他举措带来的好处。

![](img/0c93b349ff438287d4fc95f135ab50dd.png)

## 衡量用户群

在大多数 SaaS 企业中，都有免费用户和订户。用户群对业务非常重要，因为用户网络围绕其他竞争对手构建了一条护城河。重要的不是注册的用户数量。取而代之的是产品或服务的**活跃用户**数量。

活动用户是参与产品的用户，例如登录和使用产品的功能。活跃用户的定义是特定于企业的。**日活跃用户(DAU)** 或**月活跃用户(MAU)** 将是关键指标，取决于产品/服务是日常使用的(如网飞)还是每月使用的。

同样，**每日新用户(DNU)** 或**每月新用户(MNU)** 追踪新用户。将新用户与活跃用户分开可以让我们跟踪新用户加入业务的速度。它也可以衡量营销工作的有效性。

有观点认为 DAU 和毛是虚荣心的衡量标准，因为除了吹嘘的资本之外，他们没有提供真正的价值。这些指标不能衡量用户对产品/服务的满意度，也不能衡量用户发现产品/服务的价值。另一方面，这是一个足够简单的跟踪指标(假设“活跃”的定义是可靠的)，并让利益相关者了解业务增长了多少。

## 营销指标

一个相关的概念是订阅的**生命周期价值(LTV)** 。LTV 是订阅价格和流失率的函数。它还包括一个**贴现率**，用于贴现从认购中获得的现金的未来价值。用户并不是平等的:一小部分人比大多数人拥有更高的 LTV，而这些用户是一个企业想要保持快乐的。

为简单起见，我们假设用户的(经济)生命周期永远存在。那么，公式是

![](img/b6b2082e46641b7a35c820751bf2f0c0.png)

其中留存率是 1 减去流失率，总贡献是每个客户一年的总收入。例如，有更复杂的公式来解释每月不同的保留率。

**获客成本(CAC)** 是每个新获用户的销售和营销成本。这是对营销支出效率的一种衡量。很明显，如果我们花费太多去获得一个新客户，那是一件坏事。

![](img/38ed98306532c588b1675c79e5622869.png)

我们可以计算每个营销渠道的 CAC，以便量化渠道的效率。

一个相关的措施是采取 LTV 和 CAC 之间的比率。这衡量营销支出在为企业带来高价值订户方面的表现。根据经验法则，LTV-CAC 的比率应该在 3:1 左右。1:1 的营销支出太多，5:1 的营销支出太少。这同样取决于企业的目标。

# 数据科学适合哪里？

数据科学本身在直接预测和优化这些指标方面发挥着作用，它改善了市场营销，并有助于将客户转化为订阅产品。这里有一些有用的应用。

## 直接度量预测

> ARR 和 ARPU 的预测用于了解企业是否表现良好。

时间序列分析模型用于预测 ARR 和 ARPU。由于收入受季节变化的影响， [SARIMA](https://otexts.com/fpp2/seasonal-arima.html) (季节性 ARIMA)模型及其变体将用于进行预测。幸运的是，如今许多复杂的金融预测都由强大的库来处理，比如脸书的[预言家](https://facebook.github.io/prophet/)。

## 流失预测

到目前为止，最重要的领域是**流失预测**。人们普遍认为，保持订阅产品中的客户比获得新客户更好。原因很简单:让客户满意的成本远低于吸引新客户的营销费用(广告、搜索引擎优化、增长工具)。

> 概括地说，我们可以认为数据科学应用程序在**宏观层次**和**微观层次**上进行搅动。

在宏观层面上，我们预测预定义的用户群的流失，就像上面显示的保留曲线图一样。这些是例如在诸如北美的地理区域上的用户的聚合组。其目的是随着产品推出的继续，跟踪企业的流失率，以了解产品是否随着时间的推移为用户提供了更多的价值。

通常使用某种形式的建模来计算不同的计划，以获得准确的指标。在高层次上，有基于模型的和非参数化的技术。后者包括标准的生存分析技术，如[卡普兰-迈耶估计量](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3059453/)。

值得注意的是，“订阅”这个词本身就是一个负载词。它通常掩盖了订阅的复杂性。订阅本身可以简单到每月支付固定金额。它也可以像具有多种类型的“状态”一样复杂:订阅保持、基于支付方法使用的各种折扣以激励注册，以及不同类型的计划(例如，Spotify 中的单身与家庭计划)。由于本地化工作的原因，不同的地理区域可能会有不同的订阅计划和定价。

订阅通常有不同的状态，因此适合基于模型的技术。例如，[半马尔可夫模型](https://www.sciencedirect.com/topics/computer-science/semi-markov-process)可以模拟不同的订阅状态，以及状态转换之间的订阅下降。使用半马尔可夫模型而不是马尔可夫模型，因为状态转换之间的持续时间可能遵循马尔可夫模型不能捕捉的任意持续时间分布(马尔可夫模型假设状态转换之间的时间呈[几何分布](https://en.wikipedia.org/wiki/Geometric_distribution))。

根据我的实践经验，使用简单的模型来建模和预测流失率。其中的一个主要原因是**的可解释性**:一个数据科学家经常需要解释如何做出流失预测。

推子-哈迪模型是一个简单但非常有用的客户流失预测模型。它产生的预测被用来得出对各种细分市场的用户 LTV 的估计，以给出高价值用户的样子。此外，由于从模型拟合阶段得出的贝塔分布给出了流失率的分布，因此它简单得足以解释。

微观层面是事情变得有趣的地方。在这里，机器学习模型被开发来检测处于搅动边缘的订户。这些模型考虑了关于订户的各种特征，以预测订户变动。

使用的特征主要来自两个来源:**人口统计**和**行为**信息。顾名思义，人口统计信息是用户固有的信息，例如他们来自哪里，在哪里工作，他们是什么年龄组和性别。行为信息是用户使用产品时收集的数据，比如登录次数和功能使用事件。

人口统计信息通常是静态的，不像行为信息会随着产品的变化而变化。通常，预测模型从行为信息中获得更多信息，因为用户可能会以非预期的方式使用产品。此外，产品/服务经常变化，尤其是 SaaS 企业，其变化就像一个新软件发布一样频繁，而边际分销成本几乎为零。

> 流失预测的真正目的是**在用户可能流失时进行干预**。

根据用户的流失倾向对他们进行排名，然后对那些对产品“持观望态度”的用户进行干预。所使用的干预方法在很大程度上取决于具体的业务。一些典型的方法包括电子邮件、应用内通知和折扣优惠。

传统上，干预过程与流失预测组件是分开的。现在出现了一类新兴的[提升模型](https://en.wikipedia.org/wiki/Uplift_modelling)，这也说明了干预方法在客户流失中的作用。例如，很有可能一个用户在被干预的时候被搅动，但是在没有被干预的时候保留(称为*不干扰*)。另一方面，有些订户会从及时的干预中受益，因为干预方法可能会有效地证明产品的价值(称为*说服*)。接下来的目标是从一组用户中找到可说服的人。下图显示了这些类别。

![](img/bb4197a59ac78570b7f96ff0deb80731.png)

隆起建模的四个理论课(来源:作者)

隆起建模本身是一个广泛的主题，在调查报告中有所概述。

## 线索评分

销售线索评分的目标是找到当前有可能订阅的免费用户。像流失预测一样，免费用户的人口统计和行为信息都用于训练机器学习模型，以输出倾向得分。

> 销售线索评分用于寻找产品的潜在转化者

用户*，即* **潜在客户**然后从最有可能转化到最低的顺序排列。只有最高比例的用户被推动转换为订阅。如果潜在客户是大型企业和企业的潜在客户，这个潜在客户的排序列表将被传递给销售团队。

同样，这里可以使用提升模型，以便将销售和营销支出的成本考虑在内，从而推动用户进行订阅。

# 最后的话

我们只是触及了这个非常复杂的话题的表面。还有许多其他业务指标，其中一些取决于行业。数据科学有可能通过直接瞄准这些业务指标来提高业务效率，从而优化收入。

我将引用古德哈特定律来结束我的警告:

> 当一个度量成为目标时，它就不再是一个好的度量。

度量是有用的，因为它们提供了关于业务表现如何的指导。但是重要的是不要沉迷于度量标准。任何指标都无法捕捉用户体验、对产品的满意度和道德观。

# 参考

[1] Eric Benjamin Seufert，“增值经济学:利用分析和用户细分来推动收入”，摩根考夫曼，2014 年。

[2]芙罗莉丝·德夫里恩特、耶鲁安·贝瑞沃茨、沃特·韦贝克，“[为什么你应该停止预测客户流失并开始使用提升模型](https://www.sciencedirect.com/science/article/pii/S0020025519312022)”，《信息科学》，2019 年 12 月。