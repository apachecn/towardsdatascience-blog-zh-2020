# 深度学习，认识聪明的汉斯

> 原文：<https://towardsdatascience.com/deep-learning-meet-clever-hans-3576144dc5a9?source=collection_archive---------26----------------------->

## 一篇关于 DNNs 犯下的隐藏错误，为什么它们真的不是错误的文章，还有一匹德国马。

![](img/d084ea3b122db08f1251ad4eaf0d8e73.png)

基拉·奥德·海德在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄的照片

【1900 年左右，一位德国农民[做出了一个惊人的声明](https://www.britannica.com/topic/Clever-Hans):他教会了一匹马基本的算术，甚至识字和拼写！事实上，在公开演示中，这匹名为“聪明的汉斯”的马能够通过一连串的蹄子敲击正确地回答主人的所有问题。

当时柏林大学的心理学家 Oskar Pfungst 不太相信这种动物真的拥有类似人类的能力，他设计了一系列实验来证明这位农民的说法是错误的。1907 年，他发表了关于这个问题的著名报告，做出了令人惊讶的观察:只有当提问的实验者知道答案时，聪明的汉斯才会给出正确的答案！

这匹马实际上并没有学会通过计算或阅读来解决问题，而是通过识别实验者身体语言中的微妙线索来判断出它所期望的答案。

[时至今日](https://www.tandfonline.com/doi/full/10.4161/cib.27122)，心理学研究中(人或动物)测试对象的行为受实验者预期影响的现象被称为“聪明的汉斯现象”。通常，要特别注意防止受试者在没有解决实际问题的情况下给出正确的答案。

> 等等。我以为这篇文章是关于深度学习的？

事实上，在现代尖端的深度学习系统(甚至是简单回归)中，我们遇到了同样的问题！当数据中存在与正确结果高度相关的特征(如实验者的肢体语言)时，可能会出现聪明的汉斯现象，或传统统计学文献中的*虚假相关性*，但不是答案正确(如正确计算)的*原因*。

Lapuschkin 等人最近在《自然》杂志上发表的一篇文章漂亮地说明了这种效应确实发生在现代深度学习模型中，例如图像识别或玩雅达利游戏。(更多示例见下文。)

那么，我们为什么要关心模型使用什么信息呢？模型终究是在输出正确的答案。

对你的训练和测试数据来说是这样的。

> *但是它在部署时仍然正确吗？它会因为依赖错误的特性而轻易被愚弄吗？*

例如，想象你有一个区分狼和哈士奇的算法，但它主要是通过图像中出现的雪来区分狼和哈士奇。或者，想象一下你想要识别火车和船只(例如，给定 [PASCAL VOC 2012 数据集](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/))，但是你的[算法实际上学会了识别水和铁轨](https://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Bach_Analyzing_Classifiers_Fisher_CVPR_2016_paper.pdf)。这对任何严肃的应用程序来说都是灾难。如果你注意的话，你可以在文献中找到很多例子:

*   [基于孩子的存在识别](https://arxiv.org/abs/1608.00507)“父亲”。
*   [根据手术标记识别](https://pubmed.ncbi.nlm.nih.gov/31411641/)黑色素瘤。
*   [学习](https://ai.googleblog.com/2015/06/inceptionism-going-deeper-into-neural.html)手握哑铃作为关节概念。
*   [把穿红色衣服的亚洲人归类为乒乓球。](https://arxiv.org/abs/1711.11443)
*   [将](http://www.stat.ucla.edu/~sczhu/papers/Conf_2018/AAAI_2018_DNN_Learning_Bias.pdf) *领带*与*男性*联系起来，将*红润的脸颊*与*涂口红*联系起来。
*   [根据*微笑*和*戴眼镜*预测](https://arxiv.org/abs/2003.07631)年龄。

现在，你仍然可以争辩说，它并没有那么糟糕；毕竟网络正确地解决了任务，只是问题没有以好的方式提出——只是修复数据！如果你这样做了，你是在一个很好的公司。莱昂·博图(Léon Bottou)是目前在脸书人工智能公司工作的著名研究员，他认为修正我们的问题陈述可以走很长的路。

这有什么大不了的？为什么聪明的汉斯类型的错误如此糟糕，以至于我们必须独立于典型的分类错误来关心它们？

事实是，发现你的网络是否犯了聪明的汉斯类型的错误真的不容易，准确地说是*，因为*它们没有反映在分类错误中。基本上，你必须依赖于一个无偏差的数据集或者一个足够高质量的测试集。从上面的例子来看，不太令人放心。

如果你正在使用[可解释性方法](/why-how-interpretable-ml-7288c5aa55e4)，并且知道要寻找什么，你*可能*通过查看网络实际使用的功能来发现聪明的汉斯类型的错误。但是对于大数据集，这是不可行的。研究人员开始以可扩展的方式解决这个问题，但是还有很长的路要走。

作为研究人员和实践者，重要的是要意识到聪明的汉斯类型的错误，并知道从哪里开始(试图)发现它们。除此之外，祝你好运！

希望你学到了有用的东西！