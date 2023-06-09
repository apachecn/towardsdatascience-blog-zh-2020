# 数据科学家的商业 101

> 原文：<https://towardsdatascience.com/business-101-for-data-scientists-1bc49c0a67bc?source=collection_archive---------44----------------------->

![](img/7f066099490d79471509ed1f8c4707e5.png)

马丁·比约克在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 为数据科学家量身定制的业务要点

# 为什么要看这篇文章？

数据科学家通常来自 STEM 课程(科学、技术、工程和数学)，非常擅长数字和解决框架清晰的问题。然而，当我们开始处理业务问题时，它可能会变得有点混乱:项目目标并不总是清晰的，问题需要主观输入，因为没有数据可用，执行管理层并不总是热衷于 100%依赖数据来做出决策。

为了处理这些情况，让我们的心态适应这个新环境是一个好主意，最重要的是，通过将“数据行话”翻译成“业务行话”，能够和你的同事说同样的语言。记住这一点，让我们回顾一下商业的基础，以及如何用数据处理商业问题，同时还能以每个人都能理解的方式说出自己的想法。

# 商务必备

![](img/a4c43951f9a75f0e315766046ca40c16.png)

照片由[尼基塔·卡恰诺夫斯基](https://unsplash.com/@nkachanovskyyy?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

## 营销

营销的目标是通过找到你的理想目标市场，选择最佳价格并确定针对这些客户的策略，向尽可能多的人、尽可能多的次数和尽可能高的价格销售尽可能多的产品。

这看起来像一个优化问题，对不对？不完全是。在实践中，有太多的问题需要妥善解决:你如何定义一个理想的目标市场？如何测试不同的价格？你如何确定应对客户的策略？你应该使用哪个时间段？

因此，重要的是使用特定领域的知识来提出特定的问题，并使用数据来指导过程并提出答案。例如，要找到你的理想价格，测试需求对不同价格的反应并找到最佳点是不够的:这也是一个品牌问题，以及与竞争对手相比，你希望你的产品或服务如何被感知。如果你在劳力士工作，即使你注意到对他们手表的需求对价格非常敏感(每次你进行促销和给予特别折扣，需求都会大幅增加)，过分降低价格也不一定是一个好策略:你会在一段时间内获得丰厚的利润，然后人们就不会认为劳力士是一个如此高端的奢侈品牌，失去了很多价值。

理解定义价格和目标市场不仅仅是在短期内优化它，而是了解客户如何看待你的产品/服务，以及他们将如何应对营销策略的变化。与竞争对手相比，你希望你的产品被如何看待？这实际上不是一个可以用数据来回答的问题:它需要一个主观的答案，然后决定你将如何使用数据来解决其他问题。

定义营销策略时，你应该熟悉的一个关键营销概念是 4 P:产品、地点、价格、促销。

*   *产品*是关于你的产品的特性以及潜在客户对它们的看法:品牌名称、外观、特点等。
*   *地点*是关于你的分销渠道:你的客户将在哪里购买你的产品，谁将出售它，等等。
*   *价格*是围绕产品价格的一切:你的客户有多看重你的产品？你希望你的产品如何被感知(更贵，更便宜…)？您的客户对价格有多敏感？
*   促销将说明你计划如何接触你的顾客:电视、广播、直接邮寄？联系他们的最佳时间是什么时候？市场有季节性吗？

另一个重要的概念是细分:将你的客户分成具有相似特征的不同群体。例如，根据消费金额，您可以将客户分为*新*和*旧*或*大*和*小*。一个经典的细分方法是 RFM，它使用 3 个维度对客户进行细分:最近(他们最后一次购买是什么时候？)，频率(他们多久买一次？)和货币价值(他们的平均购买金额是多少？).这些通常是主观的概念，但是您也可以使用经典的聚类方法，例如 K-Means，来发现新的细分。然而，重要的是要理解，数据驱动的细分方法不一定比更主观的方法更好，最佳方法将取决于您的目标。

最后，你应该理解*角色的概念。*通过查看数据，您可以确定客户的平均年龄、收入以及主要的性别。然而，这些数字可能过于抽象，在创建产品功能或营销策略时没有用处。这就是为什么营销人员经常提到*角色*(*角色*的复数)，这是一种将抽象概念转化为“真实人物”的具体方法。你不用称呼住在乡下、年龄在 50 到 60 岁之间的白人男子，而是创造一个角色:霍华德，55 岁，是住在德克萨斯州海恩斯维尔的退休消防员。当想象我们的市场将如何应对不同的策略时，它帮助我们避开统计抽象。

在试图用数据回答问题之前，这些概念可以帮助你框定你的问题，并将它们视为一个更广泛系统的一部分。

## 金融

![](img/38bf68da56e6d06b473ce348398a7775.png)

照片由 [Fabian Blank](https://unsplash.com/@blankerwahnsinn?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

财务的核心其实很简单:就是赚的钱比你花的多，理想情况下，能够推迟你的成本并预测你的收入。控制这两种流动的最好方法是记账。会计是一项相当古老的活动，被一些人认为不太性感。不过，在欺诈检测和收入预测等领域，它可以从数据科学中受益匪浅。

收入预测已经存在一段时间了，许多公司仍然使用过时的方法来预测他们明年会赚多少钱。这些信息非常有价值，因为企业用它来决定他们的预算:给每个部门或项目分配多少钱。尽管目前的方法很简单，但它们通常比更复杂的方法效果更好，因此在该领域仍有很大的改进空间。

几个关键概念是*利润率、* *加价*和*机会成本*。

> 利润率=(收入-成本)/收入

因此，如果你有 10%的利润率，那么每 100 美元的销售额中，10 美元实际上会变成利润。利润率是你的收入中有多少实际上变成了利润。

> 加价=(价格-成本)/成本

公司有时使用加价来决定价格:例如，他们采用期望的 30%的加价，并应用于产品成本以得出最终价格。

*机会成本*是用你本来可以做的事情来衡量做某事的成本。想象一下，你在一家大公司担任经理，正在考虑攻读全日制 MBA 的可能性:这将产生与学费、书籍等相关的直接成本。，但这也会有机会成本，因为你将不得不停止工作一年或更长时间，并且在此期间不会有任何工资(也不会获得专业经验)，这也应该在你做决定时加以考虑。企业也是如此:比如，想想持有现金。一家企业的现金越多，它就越能为销售下降或意外成本等困难时期做好准备。然而，当这笔钱作为现金持有时，公司就错过了将其投资于金融产品或企业本身的机会。即使把钱存在银行也有成本，即机会成本，所以公司在决定现金水平时必须考虑这种权衡。

![](img/0b00102257944a95d5201d925cc030c0.png)

由 [Guillaume Bolduc](https://unsplash.com/@guibolduc?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

## 操作

业务运营处理公司向客户交付价值所需的一切，包括优化生产、设备配置、人员配备等。

这里有很多优化，不一定是数据科学，但它肯定可以使用具有数学知识的人。这些部门通常会从*流程*和*系统*的角度考虑很多，他们希望确保流程尽可能平稳高效地运行。

这里一个有用的概念是*精益方法*，它起源于制造业，并以*敏捷方法*的形式扩展到软件开发。所以，你所知道的关于敏捷软件开发的一切，也可以应用到传统制造业中，不断迭代和改进。

另一种用于流程优化的著名方法是[六适马](https://en.wikipedia.org/wiki/Six_Sigma)。详细解释这一点超出了本文的范围，但是，一般来说，六适马是一组数据驱动的技术，用于通过减少过程输出的方差来改进过程，从而使过程更加可预测。它在 20 世纪 80 年代和 90 年代非常流行，其根源在于使用基本的统计方法来提高业务流程和运营的质量，因此数据科学家应该有兴趣阅读更多关于它的内容。

最后，从运营角度来看，另一个重要问题是库存水平。大多数企业都有某种库存，而库存通常伴随着一种权衡:你的库存越多，你对意外事件的准备就越充分，比如需求高峰。然而，保持过多的库存有一些成本，如存储成本本身(空间和维护)和机会成本(如上所述)，因为用于过多库存的钱可以花在其他地方。

![](img/cc54402974f856dd0075a2afd693ef41.png)

费利克斯·米特迈尔在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 战略

商业战略是一个高层次、广泛的主题，它包含了许多不同的概念和领域，很难概括。因此，让我们先了解一些关键概念，然后讨论它如何与数据科学相互作用。

商业战略通常被定义为“公司为达到特定目标的高层计划”，这是准确的，但相当模糊。从确定价格策略，到公司将试图征服哪些类型的业务，以及明年将试图进入哪些国家。然而，所有这些决策都应该源于公司的*使命*和*愿景*声明及其*核心价值观*。它的使命陈述是公司自身的*存在理由*，它陈述了公司为什么存在，它为谁服务，它的目的是什么。例如，看看 IBM 的使命声明:

> “在创造、开发和制造行业最先进的信息技术方面处于领先地位，包括计算机系统、软件、网络系统、存储设备和微电子技术。我们遍布全球的 IBM 解决方案和服务专家网络将这些先进技术转化为客户的商业价值。我们通过全球范围内的专业解决方案、服务和咨询业务，将这些先进技术转化为客户价值。”

另一方面，一家公司的*愿景声明*定义了公司未来的目标，即它期望在未来几年内实现的目标。同样，这是 IBM 的愿景声明:

> “成为世界上最成功、最重要的信息技术公司。成功帮助客户应用技术解决他们的问题。成功地向新客户介绍了这项非凡的技术。这很重要，因为我们将继续成为该行业大部分投资的基础资源。”

最后，公司的*核心价值观*提醒每个人什么对那个公司是重要的，以指导重要的决策。IBM 的价值观如下:

> "多样性和包容性，创新，做你自己，关注变化."

所有这三个概念都是在公司进行战略规划时定义的(通常在执行层面)，但小企业也可以定义它们，通常首先在他们的*商业计划*中定义，这是企业家用来帮助他们在有商业想法时不仅定义他们的战略，还为每个商业领域规划布局，包括财务预测，以检查他们的想法是否实际可行。当一个企业家来要求贷款来开始他们的生意时，商业计划有时被银行要求。

然而，有些人认为商业计划是过时的工具，不能代表现实，尤其是对初创公司而言。对于小型科技公司来说，一个更受欢迎的工具(尽管目标不同)是 [*商业模型画布*](https://www.strategyzer.com/canvas/business-model-canvas) ，它本质上是一个公司如何交付价值、向谁交付价值以及如何在财务上可行的图形表示。

为了做出战略决策，高管们可能需要大量数据，但通常情况下，这些数据并不复杂:他们很大程度上依赖于*商业智能*和简单的*关键绩效指标*(KPI)，这些指标显示了业务的进展情况、有前景的市场、高绩效部门等。比起执行复杂的统计转换，选择正确的数字以及如何解释它们更重要(尽管这有时可能会导致错误)。

# 你现在如何应用你刚刚学到的东西？

这里介绍的概念可以帮助你更好地与公司的不同部门沟通，理解他们在说什么，也可以用他们能理解的术语更好地表达你的想法。通过更好地了解整个行业，他们还可以帮助你提出更好的想法。

最后，我希望它能激励你对商业或某些特定的主题做更多的研究。没有多少数据科学家从整体上理解业务，所以理解基础知识可以真正帮助你为公司创造价值。

# 更进一步

为了帮助你继续研究，这里列出了几本书，可以帮助你更详细地了解这里讨论的一些主题:

*   埃里克·里斯的《精益创业》
*   *商业模式生成*作者:Alexander Osterwalder 和 Yves Pigneur
*   乔希·考夫曼的个人 MBA 课程
*   迈克尔·波特的竞争战略
*   杰瑞米·大卫·丘鲁苏的《数据驱动:21 世纪管理咨询导论》
*   《商业预测交易:揭露神话，消除不良行为，提供切实可行的解决方案》迈克尔·吉利兰著
*   创业者的财商:你真正需要知道的数字