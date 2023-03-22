# 你是否花了太多的钱来标记数据？

> 原文：<https://towardsdatascience.com/are-you-spending-too-much-money-labeling-data-70a712123df1?source=collection_archive---------30----------------------->

## 如何在不牺牲模型质量的情况下节省数据标注

技术专家将会记住 2010 年是大数据的十年。

数据存储变得足够便宜，以至于公司开始囤积数据，甚至不知道如何处理这些数据。数据收集变得无处不在，这在很大程度上要归功于物联网，它允许全新的有价值、可操作的数据流。数据处理极大地受益于 GPU 和 TPU 的新兴能力，以训练更强大的深度学习模型。

一般来说，拥有优势数据来推动业务运营是一件非常积极的事情。但是，今天生产的 90%的 ML 模型使用监督学习方法，这些项目的成功在很大程度上取决于公司准确有效地标记其数据的能力。

这说起来容易做起来难。

# 标签质量

如果您不熟悉通常收集标签的方式，您可能会认为标注是一项简单的任务。那些职业生涯致力于数据标签的人知道这与事实相去甚远。

当然，注解的*概念*本身看似简单。通常情况下，数据由负责生成被专家称为“基本事实”的人进行注释。生成的标签(如果标签比简单的值更复杂，我们称之为*注释*，就像在分段或边界框注释的情况下)是我们希望在该数据集上训练的模型为该特定数据点预测的类或值。举个简单的例子，注释器可能会查看一个图像，并从预先存在的类本体中标记一个对象。标签被输入机器进行学习。在某种意义上，标记是将人类知识注入到机器中，这使得它成为开发高性能 ML 模型的关键步骤。冒着被简化的风险，好的标签驱动好的模型。

问题是，在现实世界中，仅仅因为这些标签表面上看起来很容易，并不意味着它们在实践中很容易。

这里，我们有一个简单的图像和一些简单的说明。一个人类注释者被要求围绕他在原始的、未标记的图像中看到的任何人画一个矩形。很简单，对吧？这里，形象清晰；只有一个人，并且这个人没有被遮挡。然而，有很多方法会出错:例如，画一个太大的方框可能会导致模型过度适应背景噪声，并失去确定相关模式的能力。画一个太小的盒子，你可能会错过有趣的图案。这还没有考虑到注释者在压力下处理数据更快或赚更多钱的情况，或者犯了错误(诚实与否！)或未能正确理解说明。

![](img/9bfeb44a55fdadfb34357d39b7cad047.png)

质量注释(这张照片的所有版本由 [Clem Onojeghuo](https://unsplash.com/@clemono2?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上进行内部注释)

![](img/7333dd6bb62a2e498ddbd55fbf200fea.png)

较低质量的注释

![](img/685e23333bd35bf425537604cec5d90f.png)

更低质量的注释

![](img/c2771a01401ce6b8eabe34a74789ffbf.png)

一句“你在努力吗？”注释

现在认为这实际上是一个简单的用例，因为图像不包含太多的对象(现实生活中的情况实际上看起来更混乱)，并且手头的任务是客观的。有多个部分遮挡的人的图像更难处理。同样的道理也适用于情感分析，其中存在固有的主观性。

我们可以继续。但关键是:即使是简单的标记任务也充满了潜在的错误。这些错误相当于你提供给你的模型的坏数据。很有可能，你知道这会导致什么。

# 相信暴徒！

面对所有这些潜在的挑战，收集足够高质量的标签来训练一个像样的 ML 模型会变得更加困难。然而，在过去几年里，有监督的机器学习仍然取得了巨大的进步。那么是什么原因呢？

“诀窍”是，虽然信任单个人类注释者是不明智的，但是依赖一个更大的群体实际上通常会让我们走得很远。这是因为如果一个注释者犯了一个错误，另一个注释者就不太可能犯同样的错误。换句话说，通过从多个人那里收集每条记录的标签，我们可能会去除大多数离群值，并确保标签更有可能是真实的。

例如，如果一个注释者在一个二进制用例中有 10%的机会出错，那么两个注释者出错的概率已经下降到 0.1 x 0.1 = 0.01 = 1%，这当然更好，但是对于每个(甚至大多数)应用程序来说还不够。三四个注释者会进一步减少这个数字。

![](img/756b2f113a017bcf80c0f4db77f3c7f0.png)

注释中的小差异可以累积成大问题(图像来源: [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) 数据集)

# 质量与数量:数量能弥补不好的标签吗？

下一个问题是，你能否用越来越多的训练数据来对抗不准确标记的训练数据。换句话说，量可以对抗质差吗？我们在其他地方讨论了其中的一些权衡，但我们能够表明的一件事是，一些类比其他类更可能对*坏*标签敏感，并且修复坏标签的影响所需的额外数据量在整个数据集中变化很大。使用什么型号并不重要。糟糕的标签会对训练数据造成更大的污染，而且比只有少量标签良好的数据更有害。

换句话说，当涉及到标注时，并不是所有的数据都应该得到同样的关注。我们还证明了对标记噪声的敏感性几乎与模型无关。这是一个好消息，因为这意味着可以使用通用模型来识别需要更高标记准确性的有问题的数据簇，并在标记数据时战略性地依赖该信息。

# 什么是主动学习，它与数据标注有什么关系？

换句话说，拥有一个智能标签策略比你想象的要重要得多。不可否认，这并不像研究最新的模型那样有趣，但是对于将一个成功的模型推向生产来说，这常常是更重要的。如果你问任何数据标注专家在讨论如何减少标注预算时想到了什么，他们通常会说主动学习。

主动学习是 ML 算法的一个类别，是半监督学习的一个子集，它依赖于增量学习方法，并提供了一个优雅的框架，允许 ML 科学家处理仅部分标记的数据集。

主动学习基于一个简单而强大的假设，即并非所有数据都对模型有同等影响，并且模型不会以相同的速度学习所有数据。这是因为数据集通常包含大量重复的信息(这意味着一些记录可能单独有价值，但当与类似的记录一起使用时，提供的增量改进非常少)，也因为一些数据不包含任何相关信息。

一个例子？假设您想要训练 OCR(光学字符识别)算法，但是有一个数据集，其中大部分记录根本不包含任何文本。通过增量添加更多的训练记录，主动学习动态地找到模型最难学习的记录(或最有益的记录)，从而允许 ML 科学家首先关注最重要的数据。也就是说，主动学习选择“正确的”记录来标记。这是预算持有人可以欣赏的。

但是主动学习忽略了一些重要的东西。它*不能*必然推测给定记录需要收集的注释数量。

一般来说，公司一直将贴标频率(或每条记录的注释数量)视为静态参数，必须根据其贴标预算和所需的贴标精度预先确定。换句话说:你给每张图片贴五次标签，或者给每个句子贴三次标签。在如何选择最佳频率方面，真的没有理论支持，也没有框架来动态地调整频率，作为记录对模型的重要性、对噪声的容忍度以及标记它的难度的函数。

我们最近的研究改变了这一点。我们现在有数据来模拟标签准确性对模型准确性的影响，并建立策略来优化如何花费我们的标签预算。了解哪些记录需要更多标签，哪些不需要，这为智能优化标签预算策略打开了大门。

# 如何用更好的标签策略省钱

因此:标注准确性是每个记录的注释数量和错误标注记录的概率的函数，而模型准确性是标注过程的准确性和训练集大小的函数。当你把这些结合起来。你可以开始考虑如何将一个模型的准确性和它的标签预算结合起来。

我们模拟了一个 250，000 样本数据集的情况，其中每个标注的成本为 25 英镑，假设整个数据集的误标注概率为 40%，并获得了以下标注预算与 5 个不同训练数据量的模型准确性之间的关系:

![](img/4687a99ea0d0ab9d4b7ca67c715d2b78.png)

在上面的图表中，每行的每个点代表一个额外的标签(图表由作者创建)

马上，您可以看到优化预算的战略标准实际上不是数据的*量*，而是每条记录的注释数量。

例如，预算为 50K 美元，客户最好将 50K 记录标记 4 次。与一次标记 200，000 条记录相比，这种策略的准确率提高了 16%。

然而，如果客户需要她的模型达到 86%的模型准确度，她会做出更好的选择，使用 200K 训练记录 3 次；与在 150，000 条记录的训练集上每条记录 5 个标签的策略相比，这将为她节省大约 50，000 美元(超过 25%)。

![](img/be539ea9df31bca548bc1f361b0edb29.png)

精确度与成本的对比分析(图表由作者创建)

如果我们现在表示相同的模拟数据，但是按照每条记录的注释数量对其进行分组，那么很明显，为每条记录标记一次数据是一个糟糕的主意。即使是两个注释也远远胜过一个容易出错的标签。大多数情况下，为每条记录添加 3 次注释似乎是一个安全的赌注，但是如果超过 3 次，你可能会对这一成本的合理性产生疑问。

现在，需要注意的是，到目前为止，我们仍然选择对所有记录使用固定数量的注释。但是自从最近[我们能够确定一些类比其他类对标记噪声更敏感](https://medium.com/alectio/can-you-lie-to-your-model-1-3-e03309e41291?source=collection_home---4------3-----------------------)以来，尝试利用这一事实来进一步调整和优化我们的标记预算似乎是合理的。

在另一个模拟中，我们现在在一个平衡的 500K 数据集上有一个二元分类图像分类问题，假设一个更有利的误标记概率为 25%,并对一个对噪声的敏感度明显高于另一个的类进行建模。我们针对这个问题分析了四种不同的标记策略:

*   策略 1:我们将最不敏感的类标记两次，将最敏感的类标记三次
*   策略 2:我们将最不敏感的类标记三次，将最敏感的类标记两次
*   策略 3:我们将两个类标记三次
*   策略 4:我们将两个类标记两次

![](img/da2eeec40dbb854bca69acba63896273.png)

作者创建的图表

我们可以看到，应用于整个数据集的策略 3 导致最强的准确性；然而，它比策略 1 好不了多少，策略 1 要便宜得多。策略 1 似乎最适合低标签预算，而策略 4 更适合中等预算。

在类级别上调整标签策略当然会导致一个先有鸡还是先有蛋的问题，因为标签是对数据进行分类所必需的；然而，同样的敏感性研究可以与无监督的方法相结合，并应用于聚类而不是类；这项研究是我们目前的重点领域之一。

# 结论

那么这一切给我们留下了什么？首先，我们希望你已经意识到更多的数据并不总是一件好事。另一方面，更干净、标记更好、更准确的数据是。

但实际上，从我们的实验中最重要的是:你可能花了太多的钱来标记数据。如果你像许多 ML 从业者一样，你可能会贴太多标签，而没有深入研究质量，以及你的好标签和坏标签对你的模型有多大影响。记住:不同的类和不同的问题需要不同的标签模式。利用主动学习来了解哪些类需要贴标机的额外关注，有望以现在所需的一小部分成本和时间建立更准确的模型。这应该让你公司的每个人都参与进来。