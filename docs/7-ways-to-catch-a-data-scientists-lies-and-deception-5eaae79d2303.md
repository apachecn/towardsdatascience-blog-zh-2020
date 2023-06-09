# 识破数据科学家谎言和欺骗的 7 种方法

> 原文：<https://towardsdatascience.com/7-ways-to-catch-a-data-scientists-lies-and-deception-5eaae79d2303?source=collection_archive---------7----------------------->

![](img/d71a8be5e831313a2761419bc9f40e37.png)

亚历克斯·利特温在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 确保你不会被卖给你“人工智能”和“机器学习”的人利用的 7 个简单原则

> 声明:所有表达的观点都是我自己的。

W 无论你是商业领袖、企业家、天使投资人、公司中层管理人员、黑客马拉松的评委，还是参与‘科技’的人，在某个时候，你都可能会遇到有人试图向你‘出售’他们的“人工智能产品”、“机器学习软件”或其他一些时髦词汇的情况。如果你发现自己处于这种情况，很自然地会觉得自己没有足够的知识和专业技能来做出明智的决定。坚持自己的立场，不要被压倒！以下是 7 个常识性的方法，可以帮助你将信号从噪音中分离出来。这些将帮助你切入正题，并帮助你理解你所推销的机器学习解决方案的核心价值主张。

# 1.“我们用人工智能来……”

![](img/40792ad086432c6079a377a50fd70f6f.png)

来源:[https://media2.giphy.com](https://media2.giphy.com/media/MMvuqCP1N1EUE/source.gif)

别人说“艾”的时候要特别小心。虽然这可能是一种幻想营销，但也可能是一种真诚的努力，试图抽象出令人痛苦的复杂细节，以便不打扰你。假定他们是无辜的**但是**要深入细节。**进一步了解他们使用了哪种特定的机器学习模型。**让他们举一反三给你解释一下。

> 如果不能简单的解释，说明你理解的不够好。——阿尔伯特·爱因斯坦

这里有几个要问的其他关键问题:

1.  您尝试过哪些其他方法(模型/算法/技术),结果与选择的解决方案相比如何？(如有可能，要求提供图形证据)
2.  你为什么选择这种方法而不是其他方法？
3.  为什么你认为这种方法在这个数据上优于其他方法？
4.  有人解决过类似的问题吗？如果是，他们使用了哪种方法？

起初，你可能不一定理解这些问题答案的所有细节，但你应该尽可能多地询问、澄清和理解。

在我的经验中，我还没有遇到一个机器学习概念不能用类比来解释。所以，如果交流太多的技术细节是一个挑战的话，要求一个高层次的解释。这样的审视不仅会扩展你的理解，还会表明解决方案考虑得有多周全。(这也将证明你的会议室是一个禁止废话的区域😎)

# 2.适应者的生存

![](img/844029d8b132b96686d800cfe36c3f14.png)

来源:https://i.pinimg.com

在 20 世纪 90 年代和 21 世纪初，电子邮件收件箱中的垃圾邮件过滤器会寻找拼写错误和其他简单的指标，自动将垃圾邮件放入垃圾邮件文件夹。现在，垃圾邮件发送者变得越来越聪明，垃圾邮件也变得越来越难以检测。现代电子邮件提供商使用的机器学习模型必须适应并变得更加复杂，才能正确识别垃圾邮件。

> “所有的失败都是适应的失败，所有的成功都是成功的适应。”——马克斯·麦克欧文

你必须澄清的一件事是，随着时间的推移和输入数据的演变，**机器学习模型在新数据上重新训练或被更具性能的模型取代的难易程度如何**。这一点至关重要，因为你有权知道出售给你的解决方案是否有“到期日”。

# 3.垃圾进垃圾出

![](img/bfb94d599841b9a5f4dac9d990863c0e.png)

来源:https://media.tenor.com

机器学习模型的好坏取决于它的数据。因此，**你应该确定用于训练机器学习模型的数据质量。**虽然“质量”很难定义，并且可能因环境而异，但了解训练数据质量的一个简单方法是询问— **与模型将面对的“真实世界”数据相比，训练数据的相似性和代表性如何。**

> “我们相信上帝，所有其他人都会带来(高质量的)数据。”爱德华·戴明

无论一个机器学习模型有多么花哨或者多么先进，如果训练它的数据质量很差，结果肯定会很糟糕。

# 4.更多，更多，更多！

![](img/4d787aec2f142978a243a0b1e3f60f07.png)

来源:[https://media1.tenor.com/](https://media1.tenor.com/images/f0a150cb643ab8e32bb882ac26e7fa08/tenor.gif?itemid=11867918)

一般来说，模型训练的数据越多，它的表现就越好(其他条件相同)。深度学习模型更是如此。你可以把一个机器学习模型想象成一个高中生为了 sat 而练习做题。练习更多种类的问题会增加学生在 sat 考试中表现更好的可能性。

> "在没有(充分的)数据之前就建立理论是一个严重的错误."—夏洛克·福尔摩斯

**确保在训练任何机器学习模型时使用了充足的数据是至关重要的。**多少数据才够？很难说需要多少数据，但是越多越好！理想情况下，数据应该来自可靠的来源，并且应该尽可能地使用这些来源。

# 5.可解释性

![](img/289f3ea434d97fb8b6de291213ab48dd.png)

来源:[https://lh3.googleusercontent.com](https://lh3.googleusercontent.com/proxy/DZowzERG2Sxie-iYiKjKnNaGV0FCp5jXsZu-K2J4mDYNBKQ8xGkGs7iAsfi8_7O3j_0h73u8QUpnxMa6LjLj_LzliGIEDwNZwrN5D0v09_A9VOyAPB9ftNAG5k5uMl6eFg)

在机器学习中，模型的表现如何，以及其表现(尤其是糟糕的表现)可以被解释的难易程度之间，往往存在权衡。一般来说，对于复杂的数据，更精密和复杂的模型往往做得更好。然而，由于这些模型更加复杂，因此很难解释输入数据对输出结果的影响。例如，让我们想象一下，你正在使用一个非常复杂的机器学习模型来预测一种产品的销量。这个模型的输入是花在电视、报纸和广播广告上的钱。复杂的模型可能会给你非常准确的销售预测，但可能无法告诉你电视、广播或报纸这三个广告渠道中哪一个对销售影响更大，更值得花钱。另一方面，一个更简单的模型可能会给出一个不太准确的结果，但却能够解释哪一个商店更值得花钱。**你需要意识到模型性能和可解释性之间的权衡。这是至关重要的，因为在可解释性和表现之间的平衡应该取决于目标，因此应该由你来决定。**

# 6.以正确的方式衡量正确的事情

![](img/62b9f8dda98cc27a2317a6cd119ddc1a.png)

来源:[https://media2.giphy.com](https://media2.giphy.com/media/6ZnDM7tOjKTRe/giphy-downsized-large.gif)

准确性是衡量分类机器学习模型性能的一个非常常见的指标。例如，对猫和狗的图片进行分类的机器学习模型，准确率为 96%，可以认为是非常好的。这意味着在 100 张猫和狗的图片中，模型能够猜对 96 张。现在想象一下，一家银行试图应用相同的指标对欺诈交易进行分类。欺诈分类器可能很容易达到 96%的准确率，因为欺诈交易非常罕见。然而，捕捉欺诈交易并不意味着 96%的时间都是正确的。这是关于减少**错误**和尽可能多地捕捉欺诈交易，因为错误地将 4%的交易归类为非欺诈交易会造成很大的损失。

> 测量是神话般的。除非你忙着衡量什么是容易衡量的，而不是什么是重要的。——塞思·戈丁

对于银行欺诈的例子，假阴性的数量比准确性更能说明模型的性能。根据问题的不同，应该使用其他一些指标，如精确度、召回率、特异性和 F1 分数，而不是精确度。这里有一篇由 [Mohammed Sunasra](https://medium.com/u/7bd4c7adcfd0?source=post_page-----5eaae79d2303--------------------------------) 撰写的[的精彩文章](https://medium.com/thalus-ai/performance-metrics-for-classification-problems-in-machine-learning-part-i-b085d432082b),讲述了这些工具应该在什么时候使用。因此，至关重要的是**尽可能注意使用正确的指标和各种指标。**

# 7.那么…你的优势和劣势是什么？

![](img/8229a2a1ced5a882dfebacb13a8e2686.png)

来源:[https://i2.wp.com](https://i2.wp.com/www.blogmaza.com/wp-content/uploads/2019/04/strength-wekness.gif?fit=400%2C220&ssl=1)

在企业面试中，优势-劣势问题是一个老生常谈的问题，当试图评估机器学习解决方案时，这个问题会非常方便。当有人提出机器学习解决方案时，你绝对应该**询问他们解决方案的局限性**。了解回答两个关键问题的局限性是非常重要的:

1.  实施该解决方案的优势是否足以超过限制？
2.  这些限制会影响未来的表现吗？

> “成功的关键是了解自己的弱点，并成功地弥补它们。缺乏这种能力的人会长期失败。”—雷伊·达里奥

从实现有效和可持续的机器学习解决方案的角度来看，了解其局限性对其成功至关重要。此外，要求支持者坦白他们解决方案的局限性会让你了解他们的透明度。它将表明解决方案考虑得有多周全，以及提出解决方案的人有多值得信任。

# 结论

不管你感到多么缺乏知识和不知所措，你有一个秘密武器可以帮助你——一个引导你穿过迷雾的手电筒。这个秘密武器就是你提问的能力。提问！质疑、澄清和审视你不确定的一切。上面提到的这 7 个想法会给你一个整体策略和 7 个关键维度，你可以沿着这 7 个维度提问。你可以依靠它们来增强你的理解，并合理地评估机器学习解决方案。