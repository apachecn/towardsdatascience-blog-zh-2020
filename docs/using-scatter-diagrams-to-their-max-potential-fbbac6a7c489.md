# 将散点图发挥到极致

> 原文：<https://towardsdatascience.com/using-scatter-diagrams-to-their-max-potential-fbbac6a7c489?source=collection_archive---------23----------------------->

## 制图指南

## 我会教你散点图的来龙去脉；如何获得见解，以及如何以最具影响力的方式展示这些见解。啪啪！

![](img/37b92c032cd3811246bbc71615cbe761.png)

> “简单性可以归结为两步:
> 
> 识别本质。
> 
> 排除其他的。”—利奥·巴伯塔

我记得当我第一次开始为工作创建报告时，我想通过展示各种图形和图表来展示我的技能。我的想法是通过从每个角度呈现每个数据点，包括尽可能多的细节到一个图表中，来最大化我的报告和演示。我现在一想到这个就害怕。随着时间的推移，我了解到每个图表都有一个正确的情况，当涉及到用数据有效地传达一个故事时，越少越好。这就是我今天想和大家分享的信息。

无论您是专家还是新手，我相信这篇文章对任何想要提高或更新图形知识的人来说都是一个很好的资源。在这篇文章中，我想回顾以下内容:

1.  何时使用散点图
2.  如何在散点图中表示数据
3.  理解和解释你的散点图

通过这些部分，我的目标是帮助你识别不必要的琐碎和噪音，为你的观众呈现一个简单、直白的故事，同时尽量避免过于专业。

# 何时使用散点图

散点图主要用于确定一对数值数据点之间是否存在因果关系。散点图在显示关系方面很有效，因为它可以很好地显示任何部分的数据点范围。如果我们使用条形图或折线图，我们能得出的最好结果就是数据的趋势。我们会错过很多其他潜在的见解。让我们看一个例子:

![](img/3971a1de9a3854e69950e210f4cccffe.png)![](img/7e2cd5b343dd23cf9bf868b310d3549f.png)

这里的图形表示相同的数据点，但是表示为折线图和散点图(忽略我不会画直线)。数据点是虚构的。它们并不代表任何已开展研究的实际数据。

假设我们有一组弓箭手的数据以及他们的高度和射击精度。如果我们用这些数据画一个线形图，我们可以看到身高和准确性之间有一个积极的趋势:射手越高，射得越准。但是这条线的方向并没有给我们带来额外的意义，并且使图表更加混乱。两点之间的线一般代表一段时间(通常是时间)内的变化，而不是其他数值。如果我们将数据绘制成散点图格式，我们可以看到高度和准确度对之间的趋势，并正确地看到值的范围。如果数据点没有趋势，那么折线图就不会给我们任何信息。我们只会看到像意大利面条一样的混乱，唯一可以接受的时候是当你是一个蹒跚学步的孩子发脾气的时候。

这里有一些问题，你可以问自己，以确定是否应该使用散点图:

1.  我的数据需要用时间来表示吗？
2.  我的数据需要汇总吗(取数据的平均值或总和)
3.  我的数据是否少于两个非日期/时间变量？

如果你对这三个问题都回答了**否**，那么使用散点图应该没问题。

因此，在比较两个变量(其中一个不是时间)时，最好用散点图来表示数据，以便于阅读和分析。

# 如何在散点图中表示数据

现在我们知道了什么时候使用散点图，让我们花一些时间来确定如何最好地表示我们的图表。根据散点图的结果，我们可以专注于讲述一个特定的故事或发现。以下是我们强调我们发现的方法。

## 趋势线

趋势线是显示数据对之间关系的好方法。数据显示的是正相关还是负相关？数据对之间的相关性有多强？

![](img/52f04a416e82f77644af012e2383b050.png)![](img/5e1d0dbb9716255f69a87cd635a0dbf2.png)

正相关还是负相关？左图显示了身高和准确度之间的正相关关系，而左图显示了负相关关系。

看左边的图表，我们可以看到趋势线向上倾斜，显示了射手的高度和准确性之间的正相关，但这些点离趋势线相当远，表示弱相关。相比之下，右边的图表显示数据点向下倾斜并接近趋势线，表明有很强的负相关性。

斜率也告诉我们趋势线是完全水平还是垂直。水平趋势线表示 x 轴上的变量不影响 y 轴上的变量，而垂直趋势线告诉我们 x 轴变量与 y 轴变量无关。这两个结果是可以互换的，因为我们可以将 x 轴和 y 轴设置为任意一个变量。

使用趋势线，我们可以更容易地解释我们绘制的数据的性质。我在下面添加了趋势线能告诉我们的更简洁的定义:

**趋势线斜率:**趋势线的陡度告诉我们 y 轴的变化率是由 x 轴引起的。从原点向上或向下的斜率分别代表正向或负向趋势。完全水平的趋势线表示 y 轴没有变化，这取决于 x 轴的变量。垂直趋势线将显示 y 轴上的变化是由 x 轴上使用的变量之外的其他变量引起的。

**趋势线的数据密度:**趋势线的数据密度告诉我们变量之间的相互依赖程度。如果数据点接近趋势线，它们是非常依赖的。较低的密度(远离趋势线的数据点)表示其他因素可能与 y 轴或 x 轴相关。

**趋势线的曲率:**一条直的趋势线代表一个恒定的比率变化:对于 x 中的每个值，y 中的一个定义值都会发生变化。如果我们看到一条曲线趋势线(抛物线)，那么变化率可能沿着 x 轴加速或减速。

如果您需要更多详细信息，下面是一个很好的资源，提供了有关趋势线、如何理解其斜率以及在坐标几何中的一般用途的更多信息:

[](https://www.mathopenref.com/coordslope.html) [## 线的斜率(m)(坐标几何)-数学开放参考

### 定义:直线的斜率是一个衡量其“陡度”的数字，通常用字母 m 表示。它是…

www.mathopenref.com](https://www.mathopenref.com/coordslope.html) 

将趋势线与图表的各个部分结合起来可以帮助我们讲述关于数据的更具体的故事。

## 横截面

根据我们试图告诉观众的故事，我们可以专注于散点图的某些部分。通常，从对数据的一般性解释开始，然后进行更深入的研究是一个好主意。这有助于你的观众理解并参与故事。

![](img/27b4955cbb1670438bd6f34c33766bc6.png)

创建你的散点部分将有助于吸引你的观众的眼睛到与你的故事相关的信息。

从上图中，我们可以看出弓箭手数据的两个特点:

1.  平均身高在 5 英尺 4 英寸到 5 英尺 6 英寸之间的弓箭手的准确度低于平均水平。我们可以做出这样的推断，因为该范围内的大多数数据点都低于趋势线。
2.  6 '到 6' 8 "之间的弓箭手往往是平均身高和准确度。我们看到大多数数据点聚集在这个区域，代表平均值。

分割散点图的各个区域是关注平均值、高于/低于平均值的比率，甚至数据集的异常的好方法。使用这种技巧将真正帮助我们引导我们的观众通过我们试图讲述的故事。

## 环绕星团

当我们绘制散点图时，我们不一定会生成带有明显趋势线的图表，但这并不意味着我们不能从数据中获得洞察力。正如我们在趋势线部分所讨论的，我们可以有一个散点图，其中趋势线可以是垂直的或水平的。见下文:

![](img/62731293d6bf7c66e14494b7c2e78787.png)

同样，这个图表不是用任何事实数据构建的。其目的是为了说明一个观点。具体来说，要说明很多点！(双关绝对有意)。

这里我们有一个不同的数据集(最后，我也厌倦了弓箭手的数据)。x 轴代表作家使用的平均字数，y 轴代表他们的经验年限。让我们通过圈出数据点的聚类来看看我们能从这个数据集看出什么。

![](img/4da5eb75f55e89d8966d67479ac6cf65.png)

是的，我确实意识到我说过散点图不应该与时间间隔一起使用，但是在这个场景中，年不是作为一个连续的时间间隔使用的。岁月是对一个人有多少经验的定量衡量，而不是过去了多少时间。

看上面图表中圈出的数据，似乎有几年写作经验的作家，以及有更多年写作经验的作家，倾向于使用更短的词。另一方面，中等写作经验范围内的作家使用更长的单词。我们可以从中得出的结论是:

> 新写手的词汇量更小/更简单，因此单词长度更短。随着作者变得更有经验，词汇量扩大，使用更长的单词。最有经验的作家会重新使用较短的词语，因为经验告诉他们，易读性有助于更好的写作和更广泛的受众。

我们不需要寻找一种趋势来确定一种模式。我们可以把重点放在聚类或异常上，看看我们是否能理解这些数据，或者下一步把我们的研究重点放在哪里。

# 理解和解释你的散点图

我们花了大量时间讨论解释和呈现数据的不同方式，但知道如何真正理解和解释数据所呈现的内容同样重要。从散点图中很容易做出有偏见的假设，所以让我们来看看一些潜在的陷阱，看看我们如何避免犯这些错误。

## 确保样本具有总体代表性

我们的散点图很少包含我们试图考虑的全部人口。包括我们自身偏见在内的不同因素会影响我们对数据的采样方式。谷歌新闻就是一个很好的例子。根据你过去的搜索历史，谷歌会向你展示“相关的”新闻话题和广告，但这些话题和广告并不代表整个人群，它只是你感兴趣的范围。

如果你想了解更多关于如何让谷歌新闻表面不偏不倚的文章，你可以在这里查看我早先的媒体帖子:

[](https://medium.com/@irfanhashmi/using-google-news-for-unbiased-information-why-it-matters-6d0fba31138f) [## 使用谷歌新闻获取公正的信息:为什么它很重要

### 在我们这个以技术进步、数字化和几乎无限制为特征的全球社会中…

medium.com](https://medium.com/@irfanhashmi/using-google-news-for-unbiased-information-why-it-matters-6d0fba31138f) 

让我们看看下面的图表，更深入地了解这一现象。

![](img/698252376997b73055e45accc0036cc5.png)

代表财富和爱猫/爱狗人士平均分配的图表。(这是我不介意进入的朋友区)。

让我们假设我们生活在一个财富与某人更喜欢狗还是猫没有关联的世界。在这个世界上，事实是富有的爱狗人士和不那么富有的爱狗人士一样多，猫也是如此——人口分布均匀。现在让我们假设你**主要**和富有的养猫人在一起。如果你根据对你相处过的人的调查制作了一个散点图，你会错误地看到爱猫的人和更富有的人之间的相关性。你会错过调查铁杆爱狗人士和财富地位较低的人。

这里有另一个例子:你向所有 1000 名订户发送了一封电子邮件，宣传一种要出售的新产品。您的 100 名订户购买了该产品。其中 60 人住在俄亥俄州，其余 40 人住在其他州。你可以使用 100，并确定:*“哇，俄亥俄州人特别喜欢我的产品！”*现在，假设你的 1000 名用户中有 800 名来自俄亥俄州。这改变了现在的故事，不是吗？你刚刚向比其他州更多的俄亥俄州人推销。俄亥俄州人不一定喜欢你的产品，只有 7.5%的人买了你的产品。另一方面，20%的非俄亥俄州人也购买了你们的产品。(不过，俄亥俄州人很喜欢你，所以订阅了你的博客)。

为了确保您有一个良好的样本集，请确保您使用的数据真正代表您试图描绘的洞察力。一个很好的练习是:

1.  记下你试图评估的行为或活动。
2.  确定进行评估需要考虑的所有变量。
3.  检查您当前的取样方法是否足够彻底，能够包含步骤 2 中确定的变量。

## 相关性并不总是可传递的

每个人都得到一个坚韧不拔的重启这些天…smh

如果所有的鲍勃都是建筑工人，并且所有的建筑工人都能修理它，那么所有的鲍勃都能修理它吗？是的，他们可以。因为能够“修复”是 bob 的传递相关性。但是在这个例子中，关键字是**所有**。我们做了一个非常笼统的陈述。如果我们说如果所有的 bob 都是建造者，并且一些建造者可以修复它，那么不是所有的 bob 都可以修复它。

所以当我们制作多重散点图时，我们必须小心不要假设不同的相关性和它们的变量是相互关联的。它们并不总是可传递的。

这里有一个更非 SAT 风格的场景。假设我们绘制了两个图表:

1.  睡眠时间与生产时间的对比图
2.  生产小时数与一天内写的文章数的关系图。

如果两个图表都显示了每个变量的正相关，那么似乎合乎逻辑地说*“一个睡得更多的人可以在一天内写更多的文章。”这可能是真的，但我们无法推断出这个结论。我们不知道相关性是否传递。一个人写更多的文章可能是因为他们吃了富含碳水化合物的早餐，为他们的大脑提供了能量。我们真的不知道。所以最好避免这种比较，*除非我们能证明相关性是传递的*。如果你能花时间证明传递性的存在，那么添加这些细节可能是值得的。*

![](img/1a2288bf15c751355e1b6ccbe57a1304.png)

老实说，这是我在会议中最喜欢画的图表之一。(请随意使用它来获得“房间里最聪明的人”奖。我知道，出于同样的原因，我也很内疚。

让我们用上面的图表来说明这个例子。这包括一些多维图形，我们不会在这里深入讨论(关于理解这一点的参考资料在文章的底部)。可以说,“x”是一个向量，代表我们的样本的所有睡眠时间,“y”是一个向量，代表我们的同一样本的所有生产时间,“z”是一个向量，代表同一样本撰写的所有文章。相差小于 90 度的矢量被称为相关矢量，因为它们通常在同一方向运动。这些是向量 x 和 y，y 和 z。如果我们观察矢量‘x’和‘z ’,它们有一个大于 90 度的差，表明这两个矢量是**不**相关的。

所以为什么要费这么大的劲来解释这个呢？因为，作为讲故事的人，你的工作是引导你的听众，帮助他们避免对你的发现的误解。我个人发现在白板上使用向量示例对解释这个概念非常有帮助。许多企业将根据这些发现做出决策，因此确保我们帮助他们做出最好、最准确的决策非常重要。

## 决定先有鸡还是先有蛋的问题

我们已经学到了很多关于从散点图中可以做出什么样的推论，但是我们仍然需要确定先有鸡还是先有蛋？

我们已经看到了弓箭手的身高和他们的准确性之间的正相关关系，但是是高的弓箭手更准确还是射击准确的弓箭手变高了？这可能听起来像是一个荒谬的问题，但这是一个你必须以某种方式证明的观点。

这里有一个更模糊的例子。让我们假设比一般孩子更爱发脾气的孩子和学校成绩差之间存在关联。哪个是原因，哪个是结果？成绩差会让孩子发更多的脾气吗，或者发脾气的孩子成绩更差吗？鸡还是蛋？

隔离相关结果的一个好方法，或者像我喜欢说的，“快速和肮脏的方法”，是创建更多的可能因素的图表。我们可以检查营养如何影响成绩吗？我们还可以检查单亲家庭或双亲家庭是否有所不同吗？可能会发生很多反复，但在我们向观众讲述之前，我们作为故事讲述者有责任确定真相。

如你所见，我们可以做很多事情，甚至在创建散点图时需要考虑更多。为了帮助总结它们，下次创建散点图时，请记住以下问题:

1.  我想向我的观众展示什么故事或推荐？
2.  使用散点图是表示我的数据的最佳方式吗？
3.  关于我绘制的数据，我的趋势线告诉了我什么？或者还有其他出现的模式吗？
4.  我的数据集能代表整个人口吗？
5.  我是否恰当地关联了我的发现？
6.  我是否采取了足够的步骤来确定真正的因果性质？

浏览这些步骤将帮助您识别数据中最重要和最相关的方面，并恰当地呈现它们。由于我们还进行了一些关于如何思考你的发现的心理练习，你将能够在演示环境中自信地对你的观众说话。

如果你喜欢学习散点图和可以深入其中的思想，我强烈推荐阅读[乔丹·艾伦伯格的书《如何不出错:数学思维的力量](https://www.amazon.com/gp/product/0143127535/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0143127535&linkCode=as2&tag=thoughtcoffee-20&linkId=fa452fabb1e34e3f539fd635d61965f8)**。**

*这是我 2019 年最喜欢的读物，你可以从中学习很多很好的概念，并将其应用到日常工作中。本书的第 4 部分， *Regressions，*有很多关于如何从概念上看待数据以及从中可以得出什么含义的详细内容。这本书那一部分大量使用了散点图。它还包含了许多其他易于理解和有力使用的数学概念。(上述链接是一个附属链接，我可能会通过该链接的销售佣金得到补偿)。*

*我喜欢收到对我工作的反馈，所以请随意评论或给我发消息。如果你对我写的任何东西有任何问题或需要澄清，请随时给我发消息[这里](https://thought.coffee/contact-me)。我很乐意尽我所能帮忙！*

*快乐学习！*