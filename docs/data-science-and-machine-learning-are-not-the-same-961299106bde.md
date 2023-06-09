# 数据科学和机器学习不一样

> 原文：<https://towardsdatascience.com/data-science-and-machine-learning-are-not-the-same-961299106bde?source=collection_archive---------54----------------------->

## 虽然数据科学随着机器学习和人工智能的进步而变得流行，但*科学*是一个更广泛的话题。

![](img/a99ccc39c8e5a3fa1863e60d11af1e8b.png)

图片来自[维基共享](https://commons.wikimedia.org/wiki/File:The_Big_Red_Button_(3085157011).jpg)，根据[知识共享](https://en.wikipedia.org/wiki/en:Creative_Commons) [署名-共享 2.0 通用](https://creativecommons.org/licenses/by-sa/2.0/deed.en)许可改编。

在过去的几年里，机器学习、人工智能以及最终的数据科学成为了行业的热门词汇。

当然，这种现象是有原因的。新的算法和新的硬件使得复杂的预测系统对许多公司来说是负担得起的。不难在行业中找到一个用例，说明他们如何使用一个千层卷积神经网络来克服一个巨大的问题。真的，这是一件好事。

> 谁从来不想要水晶球？

然而，几十年来，机器学习和人工智能一直是学术界的研究主题。它们不是新的。现在，他们只是更容易接近。几乎任何人都可以运行 python 笔记本，导入 scikit-learn，加载 pandas 数据框，并…安装它。

> *🎶*装就装，装就装，装就装，
> 
> 没有人想被打败*🎵*

![](img/0a739011d5f63250cf5d428512c0a736.png)

照片由[蒂姆·莫斯霍尔德](https://unsplash.com/@timmossholder?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

没错。没有人想在市场上被打败。互联网上充斥着如何训练你的̶d̶r̶a̶g̶o̶n̶模型的教程。你只需要小心过度适应的怪物。对吗？

号码

不要误解我。网络上有大量有价值的内容，学习这些内容很重要。然而，根据我的经验，如果你想成为一名成功的数据科学家，你需要超越机器学习食谱。以下是我认为所有数据科学家都需要掌握(或培养)的三项高级技能:

1.  科学方法
2.  如何为企业创造价值
3.  如何恰当地传达调查结果？

一方面，具有扎实学术背景的数据科学家通常擅长科学方法。然而，他们常常过于兴奋地钻研有趣的研究，可能会忘记企业真正需要的是什么。另一方面，行业中成长起来的数据科学家往往会忽视科学方法的严谨性。

第三个技能真的是除了的东西。我坚信这取决于个人的经历，甚至可能与他或她的个性有关。

好消息是:即使你缺少这些技能中的一项，你也可以学习它们并发展自己。

今天，我要讲第一个:

# 科学方法

![](img/2ba585b923e8f2349a7b66d2b0c7ce2b.png)

普里西拉·杜·普里兹在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

我们把*科学*这个词放在‘数据科学’里是有原因的。如果你不知道如何进行科学实验，你应该学习(即使你不是数据科学家，因为科学是为每个人服务的)。一个数据科学家必须理解科学是什么，并且知道如何正确地批评它。这包括知道如何审视自己的科学工作。

> 以数据为基础的科学

这就是数据科学的一般含义。我们使用历史观察来证明或拒绝假设。在这个意义上，人们可以说数据科学是基于证据的研究。一个多世纪以来，人们一直在其他领域(如医学)这样做。因此，当您执行数据科学任务时，请在科学方法中考虑它:

*   你的问题是什么？
*   你的假设是什么？
*   你将如何检验你的假设？
*   结果如何支持你的主张？

此外，如果在这个过程中出现了新的见解或证据，你随时可以重新开始这个过程。它叫做:

> 科学实验生命周期！

> 但是机器学习管道看起来不像科学方法。

我完全不同意。让我们举一个*普通*的例子:

**问题:**什么原因导致堵车？

**假设:**下雨导致交通堵塞。

**方法:**训练一个 ML 模型，根据历史降雨数据进行交通预测。用看不见的观测值预测流量并测量误差。此外，基于历史平均值作为基线模型来估计流量，并测量误差。

**分析:**比较误差分布。ML 模型的误差*是否明显低于基线误差*？

当我强调'*显著更低'*时，是因为你不能只说'它比我证明的假设低 5% '。你最好使用假设检验，这是一种统计工具，不幸的是，许多数据科学家不知道如何使用。

我的方法可能不是测试下雨是否造成交通堵塞的最佳方法。实际上，这只是一个可能的方法，而且，还是一个普通的例子。我的观点更多的是关于你应该如何看待数据科学任务。我们不应该因为需要预测流量而按下“适合按钮”,而是应该思考我们试图回答什么，我们将如何回答，以及我们的结果是否真的比更简单甚至随机的结果更好。

现在，我希望你同意我的观点，数据科学和机器学习是不一样的。除了我提到的高级技能之外，一名数据科学家还应该掌握许多其他技术科目。但这是另一篇博文的主题。

如果你喜欢这本书，你可以在 Medium 或者 [Twitter](https://twitter.com/escrevejonas) 上找到我。此外，如果您想通过电子邮件获得关于数据科学的提示和想法，请订阅[我的简讯](https://mailchi.mp/56e8e3f8eeb0/join-my-newsletter)。这是一封每月一封的电子邮件，可能会附带:书籍建议、flash 小说、关于音乐的讨论等等。