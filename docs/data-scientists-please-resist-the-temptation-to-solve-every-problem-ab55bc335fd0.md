# “想要解决所有问题”是数据科学家的陷阱

> 原文：<https://towardsdatascience.com/data-scientists-please-resist-the-temptation-to-solve-every-problem-ab55bc335fd0?source=collection_archive---------44----------------------->

## 意见

## 选择相关的和有影响力的，远离其他的

![](img/102799cd7b1853a55007d84ff1a030ad.png)

照片由来自 Pexels.com[的](https://www.pexels.com/photo/analytics-text-185576/)帖木儿·萨格兰比莱克拍摄

几乎每一个我参与的数据科学项目，我都从*那里学到了至少*一个新的教训。在我之前的[帖子](https://medium.com/an-idea/my-data-science-project-failed-and-the-reason-is-a-no-brainer-bd020f3ded75)中，我分享了缺乏明确定义/一致的目标会导致失败。在这篇文章中，我想谈谈我经常陷入的一个陷阱——用算法解决几乎所有问题的诱惑。

## 解决问题是不可抗拒的。对数据科学家来说更是如此

我们人类是天生的问题寻求者和问题解决者。当我们解决了别人解决不了的问题时，我们的大脑会感到兴奋。虽然非数据科学家群体使用分析、逻辑和经验学习来解决问题，但数据科学家已经在理论、技术和应用方法方面接受了实践培训。吸引数据科学家的不仅仅是培训和技能。

## 技术已经成熟，为机器学习和人工智能创造了最有利的环境

*   在过去的十年中，公司已经进行了大量的投资来组织和存储他们能够得到的每一个数据。
*   许多外部(公司外部)数据已经大众化，很容易访问。
*   云公司简化了建立技术基础设施的过程。
*   开源文化导致了对经过试验和测试的算法及其源代码的可访问性
*   大学已经培养了足够多精通基础统计学、机器学习和人工智能的毕业生。

## 数据科学家是拥有最好凿子的好奇雕塑家

有了所有这些，数据科学家就像熟练的木匠，他们手里拿着最好的工具，站在树皮前。每一块木头看起来都像是一件艺术品的候选者。每一个问题看起来都不可抗拒地需要被触摸和解决。

我们拥有之前抱怨没有的一切。最重要的是，我们在每个行业都有问题要解决。既有真实的问题，也有编造的问题。那么，为什么我们不解决所有的问题呢？这正是我们陷入的陷阱——一个叫做“用数据科学解决所有问题”的陷阱

*“对拿着锤子的人来说，一切看起来都像钉子”*——马克·吐温

## 限定问题。如果算法不合适，敢于说“不”。

很多时候，一开始就说“不”是正确的——为了公司，为了团队，也为了你自己。然而，生存的压力，证明的压力通常会将我们带到“让我们尽力而为”和“让我们看看我们能做什么”的方向，这最终会使团队辜负他们自己和他们的客户，损失金钱和时间，让每个人都感到沮丧，也失去了对技术/数据科学的信任。

正确的做法是花时间鉴定问题，仔细评估它们，最重要的是把那些可能浪费时间和精力的问题推到一边。以下是我的经验清单。

## **类型#1:根本不值得解决的问题**

![](img/6b604cb1fcac28d271a37d142c01a6ad.png)

汤姆·利什曼在 Pexels.com[拍摄的照片](https://www.pexels.com/photo/astronaut-using-a-laptop-5258257/)

有问题，然后有约束。有时候以解决问题的名义，试图解决约束。

在我的一个销售预测项目中，我和我的团队被要求对一场酝酿中的飓风的预期路径进行建模，并将其用于预测算法中。目标是预测哪些商店可能会在飓风的路径上，以及什么产品需要发送给他们以及何时发送。

理由如下——我们有过去的天气数据，我们有飓风预报，我们有过去飓风期间客户购物行为的历史记录，当然我们可以提供预报。当我们着手解决时，我们了解到:

*   **缺乏准确可靠的输入数据:**飓风的路径不断变化。每个飓风都不尽相同。根据飓风的严重程度，客户对飓风的反应也会有所不同。如果我通常开车 5 英里去一家商店进行每周一次的备货，如果发布了严重的飓风警报，我可能愿意开车 70 英里去为整个月备货。
*   对结果采取行动是不切实际的:确定飓风半径 5 英里范围内的哪些商店应该备货是不太准确的。即使我们这样做了，也有可能仓库(为这些商店服务)被损坏，道路被损坏，该地区停电，服务商店的备用路线等。这增加了决定哪些区域将受到影响以及哪些商店将向服务客户开放的复杂性
*   **学习:**在花费了大量的时间和金钱之后，我们决定(并了解到)建立一个由商家、供应链团队、气象团队、政府机构和当地区域经理组成的作战室来管理每天和每周发生的事情是一个不错的主意。

> 有时，专家的意见甚至优于复杂的机器学习模型。工作几个月后昂贵的学习！尽早对替代方法保持开放的心态！

## 类型 2:不值得解决的问题(ROI)

![](img/176300a5ebd643dbd5e5513b898a6af3.png)

图[波琳娜·坦基列维奇](https://www.pexels.com/photo/photo-of-person-squeezing-lemon-3873195/)在 Pexels.com[的](https://www.pexels.com/photo/photo-of-person-squeezing-lemon-3873195/)

没有什么东西不能从“增量改进”中获益。还有另一个陷阱。大多数时候，在增量改进的借口下，项目用最少的 ROI 来挑选问题。

我目睹过零售商业务团队要求 104 周的销售预测。

**它将如何用于什么？:**大多数情况下，除了具有长交付周期计划的产品，这种预测主要是出于预算原因。有如此多的因素影响着零售业，第 104 周的数字只是一个指引。

**预测的准确性有多重要:**问题是，我们为什么要投资建立一个复杂的模型来预测未来 2 年的情况。

学习:我学到了问令人不舒服的问题是很重要的。“是的。这是一个差距/问题。但是，它有多大呢？还有其他更值得解决的事情吗？”我们最终采用了一种简单的估算方法，使用去年的实际数据，并根据预测的增长/下降进行了调整

> 有时，简单的基于 excel 的解决方案比复杂的统计模型效果更好。

## 类型 3:使用非数据科学方法可以更好地解决问题

![](img/6e9a2dae32a9015e0c94c2e881b25a5a.png)

[图米索](https://pixabay.com/photos/ethics-right-wrong-ethical-moral-2991600/)在[Pixabay.com](https://pixabay.com/photos/ethics-right-wrong-ethical-moral-2991600/)拍摄的照片

我曾经领导过一个项目，要求预测从海外进口的产品到达美国客户手中需要多长时间。目标是能够向客户和/或零售店传达预期的交付日期。一开始，它似乎是数据科学的一个很好的候选者。但是，直到我们发现了影响预期预测准确性的两个内在原因。

*   **受不可控不确定性影响的输入数据:**集装箱在海上花费的时间。一个来自中国的集装箱可能通过不同的路径到达美国的港口。它们通常是提前计划好的，但事情可能会在最后一刻发生变化。此外，在到达美国之前，这艘船通常会在其他几个港口中转/停留。船只的全球定位系统数据对于船只在某个时间点的位置是一个相当好的输入。但也有其他事件，如海上的恶劣天气，跨国政治紧张局势，导致船只中途改道。所有这些都会影响船只预计到达其航线上的下一个中转站的时间。
*   **流程缺乏可见性:**一批货物在港口清关所需的时间有很大的可变性。不知道您跟踪的第一个或最后一个卸载集装箱上的产品是否未知。由于卸货(和离港)时间从 2 天到 1 周不等，任何历史数据都是不可用的。
*   **学习**:在这种情况下，正确的方法不是预测。正确的解决方案是提供准确、实时的集装箱状态数据，寻求与数据机构合作的方式来改善这种状况，并实现对当地港口集装箱卸载时间表的实时跟踪。告诉客户进口产品大约需要“x”天，我们会“在交货日期临近时通知您”，这可能是个好主意。提供不准确的预测会导致客户不满。

> 我们不必假设对数据科学团队的每个请求都意味着必须使用复杂的统计模型来解决。

## **类型 4:问题，即使解决了，也不会被发现，除非整个支持业务流程的生态系统发生变化**

![](img/10d4a6b7a92fc47839861a6c71fb4635.png)

来源: [Pixabay](https://pixabay.com/vectors/question-asking-questioning-wonder-25527/)

有一次，我被要求预测商店每小时的库存情况，这样商店的产品就不会缺货。对于这个大公司来说，其供应链完全是为了规模经济而设计的，当卡车每天只离开仓库一次时，求解每小时的库存位置没有任何帮助。

是的，建立一个复杂的算法来解决这个问题是可能的——但是它不会被使用。所以，这就辜负了“我们将如何使用它？”测试。

**学习:**总是询问如何将洞察力付诸行动。

> 有时候，洞察力要求采取与公司整体战略和方向不一致的行动。这是为失败的项目做准备。

## **类型#5:需要创建数据的问题。**

![](img/5549d69455c225bb66582a5756ef2735.png)

西蒙·辛伯格在 Pexels.com[拍摄的照片](https://www.pexels.com/photo/person-in-blue-denim-jeans-standing-holding-brown-wooden-log-3278129/)

我们在数据科学项目中犯的另一个大错误是没有*彻底*评估*产生结果所需的*关键数据的可用性。虽然我们都知道垃圾进=垃圾出，但我们无法避免犯这个错误。

这是一个决定 1000 个床上用品系列产品的“正确”销售价格的项目。

**方法和固有缺陷:**我们采用的方法是使用可用的数据，即历史销售数据。是的，历史数据包含了尺寸、面料、线数、颜色、图案如何计入历史零售价格的信息，以及销售对此的反应。

**缺失的部分:T** 决定一件商品的*正确*价格的最重要的数据是顾客对该产品的看法。换句话说，相对于比这个产品差一个级别的产品，客户愿意为这个产品多付多少美元。在顾客心目中，决定产品与其他产品相比是劣等还是优等的参数是什么？与客房相比，顾客愿意在主卧床上用品(通常是特大号)上投资多少？这些数据点最好是通过精心的调查或使用模拟购物环境创建的数据来收集。

**学习:**使用先前的购物模式试图欺骗模型，使其认为顾客的决定是相同的。

> 错过一个关键的数据元素并决定“让我们尽最大努力利用现有资源”会导致精力和时间的浪费。

## 数据科学具有变革潜力。让我们明智地使用它！

不可否认，数据科学可以产生变革性的影响。公司依靠他们在高级分析和人工智能方面的大量投资来重振业务，拓展新的领域。

> 然而，数据科学产生的影响与所解决问题的类型和相关性成正比。必须花很多时间来鉴定这个问题。

我们应该记住，数据科学专业人员不仅有责任解决方案，而且有更大的责任选择哪些方案。

> *“成功的解决问题需要为正确的问题找到正确的解决方案。我们失败更多是因为我们解决了错误的问题，而不是因为我们用错误的方法解决了正确的问题。”——罗素·L·艾可夫*

让我们下定决心，利用最好的数据、计算和机器学习来推动真正有影响力的成果。让我们远离解决“一切”的诱惑吧！

本文原载于[一个想法](https://medium.com/an-idea)。