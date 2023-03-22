# 消费者选择模型的 5 个技巧

> 原文：<https://towardsdatascience.com/consumer-preference-models-85e297887b1b?source=collection_archive---------37----------------------->

## 本文分享了构建集体消费者选择模型时需要牢记的 5 大技巧！

你有没有想过——我们人类一天会做出多少选择？———估计有 35000 人！

![](img/371ccd416876b28fd1d35a160de36d1a.png)

照片由 [Nathália Rosa](https://unsplash.com/@nathaliarosa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/choices-in-retail-store?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

随着每天都有新产品推出，这些选择不断增加，如果不是呈指数增长的话。从在杂货店选择牛奶罐到选择下一个最佳职业步骤，一方面“是什么”对决策者来说很重要，另一方面，公司继续寻找背后的“为什么”。每个零售或制造公司以及服务提供机构都很想知道他们的客户是如何“做出选择”的 

*   是什么让他们选择一瓶洗发水而不是旁边的另一瓶？
*   *是什么促使他们购买一辆车而不是另一辆？*
*   *他们更愿意为产品支付什么，为什么？*
*   *他们可以为某些功能多付多少钱，为什么？*
*   *他们最喜欢在什么时候购买？*
*   他们想买多少？

这些长长的问题列表令人兴奋，消费者模型也是如此。总体而言，有 3 种类型的消费者模型:

*   ***数数——他们买了多少***
*   ***时机——他们什么时候买***
*   ***选择——他们买什么***

*本文阐述了* ***【消费者选择车型】*** *。选择模型试图找到答案——顾客如何选择最终产品，即顾客如何根据某种潜在的尺度(如“效用”,即顾客对每件商品的“感知价值”)对给定商品进行排序。例如，给定一组 4 个项目，比如洗发水，消费者倾向于评估每个选项的效用，并根据个人偏好对它们进行排序。价格、是否无硫、香味、品牌的商誉、公众评价、个人经历等因素起着重要作用。显然，这种“效用”会因人而异。同样，对于消费者来说，它还取决于其他因素，比如年龄、性别、所在地、职业、收入，有时还有像性格这样复杂的因素。*

这些具有挑战性的问题使得“消费者选择建模”变得更加有趣。虽然寻找这些问题的答案是令人兴奋的，但为客户提供更好的选择同样重要，如果不是更重要的话。最终， ***一个消费者想要最好的产品，一个公司最想卖出去！***

***目标很简单——做的越多，卖的就越多！***

因此**，选择建模**使数据科学家能够利用购买交易、调查和产品评论的大量消费者数据，找出描述、规定和预测消费者选择决策行为的模型，使企业能够制定更好的战略。随着人工智能高级应用的出现，出现了许多新的想法。例如，研究消费者在扫描货架时不断变化的面部表情，分析消费者在发现感兴趣的产品时的肢体语言，或者理解消费者在购物时的总体兴奋感，这提供了更深入的见解，从而提供了更深入的知识来改善消费者体验。

*正如维基百科的定义一样，* ***选择建模*** *试图通过在一个或多个特定上下文中显示的偏好或陈述的偏好，对个人或群体的决策过程进行建模。*

现在，想到的下一个有趣的问题是— ***如何定义这些客户？*** *—一个群体的整体？在一定数量的细分市场中(如果是，那么是多少)？还是在个人层面上分别对待每个客户？*

毕竟，每个人都是不同的，他们的偏好也是不同的。答案在于高复杂度结果的粒度**与更简单结果的**一般化之间的权衡。这只不过是他们在机器学习语言中所说的老派“偏差-方差”权衡。人们可以根据最终目标、业务知识以及可用数据的大小和特征来做出决策。

# 因此，从高层次来看，有 3 种类型的消费者选择模型:

集体选择模型:它假设每个顾客都会以同样的顺序排列某些商品——例如，当一家快速消费品公司创造一种新产品时——通常它是基于假定的集体消费者偏好

**2)基于细分市场的选择模型:**一旦在给定业务、业务问题和最终目标的情况下找到最佳数量的细分市场，它就将整个消费者群划分为这些细分市场，并假设同一细分市场中的每个客户都会以相同的顺序对集合中的项目进行排序，而不同细分市场中的客户会对项目进行排序，使得至少有一个排序会不同。例如，当不同的优惠、折扣和产品被提供给根据各种标准(如忠诚度、频率、新近度、位置、性别等)分组的客户时。

**3)个人选择模型:**它假设每个顾客会对商品进行不同的排序。虽然，即使只有有限的排列是可能的，每个人都被单独评估和对待，在更精细的层次上考虑个人偏好和个性，例如电子商务网站上的推荐系统

*让我分享一下我最近创建消费者偏好模型的经验吧！*

作为哥伦比亚大学 capstone 项目的一部分，我有机会与四位出色的队友一起为北美一家顶级汽车制造公司创建消费者偏好模型。在这篇文章中，我分享了我从每个数据科学家那里学到的，基于这个项目建立一个成功的集体消费者偏好模型的 5 大技巧。

***目标是什么？***

许多公司的生产不是基于订单，而是一次批量生产——因此，就像任何企业一样，他们也想知道他们的客户偏好。因此，我们开始创建集体消费者偏好模型，以了解消费者更喜欢哪种汽车功能！

因此，以下是我们在从事该项目时发现的 5 大经验，我们很乐意与大家分享:

***1)选择影响选择模型*** —数据科学家应该问自己的第一个问题，**“消费者的购买决策之旅是什么？”**不清楚对不对？以这种方式思考——你买牛奶和买笔记本电脑有什么不同？这两种情况都涉及到消费者。两种情况下都要做出选择。在这两种情况下，有多种选择，可能有相似数量的选择。那么这两种决策和购买行为有什么不同呢？—区别在于这个问题的答案——消费者如何以及通过什么心理决策做出最终决定？虽然牛奶罐的选择取决于商店的库存，消费者通常会从货架上的所有选项中选择任何一个选项，但购买笔记本电脑需要几天的研究、集思广益，而不是只去预计会有所需选项的商店。此外，某些选择依赖于商店库存，然而，在所选择的备选项中，诸如品牌、RAM、价格等特征的某些其他选择比库存本身更依赖于消费者的“预设”偏好。选择模型假设消费者在特定时间看到所有的选择，并根据他们的效用排序做出决定。因此，根据业务设置，人们可能需要改变选择模型，创建复杂的约束，假设复杂的功能来创建一个好的模型。阅读更多关于选择模型的理论，解决它们的每种方法背后的假设，并加强自己的概率和统计游戏，例如， [**这**](https://onlinelibrary.wiley.com/doi/pdf/10.1002/9781119197096.app03) 是一个很好的汇编，可以带来很大的见解和更好的建模。

***2)变量缩减 v/s 信息损失*** —这种权衡是数据科学家在解决业务问题时需要做出的最重要的决策之一。假设您的数据集有汽车的颜色，并且有 100 多种独特的颜色。作为一名数据科学家，您首先想到的是什么？让我们减少这些颜色类别，因为在一次性编码之后，它将导致 100 列！！！

***什么！！100 列只是为了颜色！？***

来源: [Giphy](https://giphy.com/gifs/dodgeball-jaw-drop-OluyzCAatv35C)

我们，数据科学家，有这种尽可能减少变量的诱惑，因为 ***我们的*** *目标是*做出稳健的模型。这仍然是一个从较少变量开始的好策略。为了应对这个充满变数的问题，我们的旅程是这样的:

我们的第一个想法是根据 RGB 分数将颜色分组**但是！**等一下！…消费者在购买汽车时是否会将黑色、深蓝色和深绿色汽车视为相似颜色的汽车？不要！他们的看法完全不同！因此，尽管“数学上”基于 RGB 代码对颜色进行分组听起来是最符合逻辑的论点，但它去除了“顾客如何感知汽车颜色”的本质。

*注意:不正确的分组比没有分组更糟糕(即没有变量约简)！*

因此，这种变量的减少会导致信息的丢失，而我们正在某个地方寻找我们的模型来捕捉这些信息，然后希望它学会做出一个好的预测！

我们的下一个想法是根据流行度对颜色进行分组 **—** 最初，我们认为根据频率进行分组将是最佳选择，因为将所有出现频率极低的颜色分组在一起将减少数据，而不会损失太多“信息”。不管怎样，我们正在去除颜色的纹理，因为数据科学家喜欢不择手段地减少变量 但是，这里也发生了信息丢失！ ***黑色“哑光”和黑色“金属色”看起来完全不同！***

*毕竟哑光就是哑光！*

![](img/1775393f3ac1daf4f0c084c75734c87b.png)

照片由 [Philippe Oursel](https://unsplash.com/@ourselp?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/black-matte-car?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

通过去除这种粒度来使生活变得更容易是没有意义的，因此，结果是通过保持颜色原样来实现的！

***3)选择合适的目标变量*** —目标变量是先建模再预测的因变量。有时这个目标不能是明确的，相反，它必须根据要解决的最终目标，在商业敏锐度的基础上创建或决定。选择模型中的目标变量通常是二元变量，如果客户选择了特定的选择，则使用机器学习或最大似然估计对其进行建模。最重要的是，必须确保数据集遵循选择模型背后的基本假设。例如，在我们的班级中，汽车在一个特定的经销店按顺序售完，我们有每天售出多少辆汽车的数据。应用这种简单的选择模型会迫使模型**‘假设’**每个客户在特定的一天看到了所有的选项，这在现实中是不正确的。事实上，在现实中，**‘最受消费者青睐的选项’**首先会被抢购一空，我们的模型会将其视为被拒绝。因此，我们最终将“汽车在经销商处的库存时间”作为目标变量，因为它表明了汽车的“受欢迎程度”——汽车停留的时间越长，受欢迎程度就越低，越早售罄，就越受欢迎。其次，在对这个新创建的目标变量应用回归时，模型表现不佳。难道不是很直观吗？对于一个 1000k x k 维的小数据集，模型准确预测一辆汽车将在 35 天或 36 天内售出有意义吗？不仅仅是感觉，更重要的是，我们的业务问题需要解决吗？因此，我们将该变量转换为二元变量，其中根据经销商(即其服务的细分市场)选择临界值或“流行库存时间阈值”。该 XGBoost 模型优于所有模型，给出了 80%的平均 AUC。

***4)消费者市场/细分*** —集体选择模型，虽然简单，但处理 ***的问题过于一般化*** 而丢失了关于—变化的客户行为的重要信息。即使您的客户或业务问题要求创建一个**集体**消费者偏好模型，数据科学家也应该经常问自己——**我能在预测中纳入这些不同的客户行为吗？**我们可以选择为每个汽车经销商创建单独的模型，这些经销商通常相距 50 英里以上。如果后者的平均 AUC 有所提高或没有提高，制作一个集体和单独的市场/区域模型并比较它们总是一个好主意。后者的缺点是“数据量减少”。因此，必须仔细分析这种权衡，牢记我们正在解决的业务问题 ***！***

***5)现实世界的实现*** —当我们创建一个成功的模型时会发生什么？—我们把它交给客户？—对吗？—事情是这样的:在一次通话中，我们告诉团队，我们已经成功地制作了精度为 xx 的模型！有一些赞赏，但缺乏预期的兴奋，这是有道理的？最终使用模型的人，通常不会被期望精通机器学习？—他们能否将新输入转换成所需的格式，然后成功调用预测函数？不是吧？这很有挑战性！因此，我了解到，一个数据科学项目，尤其是解决业务问题的项目，如果没有用户界面是不完整的，即使是 Jupyter 笔记本本身内置的基本界面也是如此。他们必须能够在现实世界中实现该模型。在接下来的通话中，当我们向他们展示了一个非常基本的用户界面，他们可以在其中插入所有输入内容时，他们大吃一惊！型号是一样的，只是 UI 增加了**舒适性和便利性**，这就完全不同了！

*感谢阅读！*

> 希望你喜欢阅读这篇文章，请分享你的宝贵反馈！