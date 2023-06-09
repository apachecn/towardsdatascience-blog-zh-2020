# 测试你的数据，直到它受伤

> 原文：<https://towardsdatascience.com/test-your-data-until-it-hurts-306a7d7e4f84?source=collection_archive---------31----------------------->

## [理解大数据](https://towardsdatascience.com/tagged/making-sense-of-big-data)

## 数据测试故事

![](img/d503de7376fb5ae8a6f1f4de155709d8.png)

[杰伊·黑克在 Unsplash 上拍摄的照片](https://unsplash.com/photos/M6xNMyYi4H8)

如果你从事分析工作，可以肯定你已经不止一次抱怨过数据质量问题。我们都有，痛苦是真实的！

作为一名数据工程师，数据及其质量是我最关心的。我敏锐地意识到良好的数据质量是多么重要——最近这个话题引起了一些热议，例如# [数据操作](https://www.dataopsmanifesto.org/)。有很多关于这个主题的文章:只需进入 DataKitchen 的 [DataOps Medium 页面](https://medium.com/data-ops)，或者如果你更喜欢 MLOps 这个术语，也有很多内容，比如来自 [great expectations](https://greatexpectations.io/) 博客的[这篇关于 MLOps](https://greatexpectations.io/blog/ml-ops-great-expectations/) 中数据测试的博文。

还有更多——但是从我的经验来看，在实践中缺乏对系统数据测试和质量监控的采用。实际上，即使有数据测试，它也经常以一些断言被破坏到数据管道中而告终，污染了数据管道代码，并且没有创建任何数据质量问题的可见性。在这篇文章中，我想给我们的(正在进行的)数据测试之旅一些见解，以及为什么它会带来伤害！

# 数据质量

我看到的数据质量的第一个问题是，它是一个非常模糊的术语。如何定义数据质量或者哪些数据质量问题很重要的实际含义取决于您的用例以及您的数据类型。

一个常见的疑点是缺少数据/观察值，要么是因为记录不完整，要么是因为您管道中未被注意到的复制错误。企业数据存储中的上游作业发生了变化，数据中的行/观察值突然变少了。然后是错误的输入，也就是说，一个人在某个地方的字段中输入了一个明显错误或格式错误的数字。这样的例子不胜枚举。

好的，如果进入你系统的数据有问题，你输出的数据怎么办？即使你设法解决了这些问题，你能确保你发布的数据质量一流吗？另一个数据质量问题。

总而言之，在如何处理数据质量问题上，有许多事情需要考虑，还夹杂着许多噪音和不确定性。

# 你应该关心

如果您仍然认为您没有数据质量问题，因为您的代码通过了所有的自动检查，并且您模拟了所有的数据，甚至对您的样本数据进行了单元测试，那么您就错了！或者说，你现在可能是正确的，但最终当你的数据出现问题时(它们会出现)，你很可能会在不知情的情况下使用并发布一些糟糕的数据。

如果你不测试你就不知道，就这么简单。所以现在就开始测试吧！而且一旦开始测试，就要测试到疼为止。如果您只是收集显示管道运行 X 行的数据指标，这样您就可以为您的自动化技能有多棒而沾沾自喜，这不会为您产生任何价值。或者反过来，套用丹尼尔·莫尔纳尔的话:“虚荣指标是无用的”，意思是不要监控那些让你看起来不错的指标，而是监控那些让你痛苦地发现什么是错的以及你需要纠正什么的不好的事情。如果测试没有伤害你，如果它们没有让你看到错误的地方，它们就没有价值。

> 测试你的数据，直到它受伤，这样你就可以修复问题并不断改进！

让我们把这个话题转到好的方面——我们可以做些什么来开始测试？我们怎样才能感受到好的痛苦？😅

**最重要的是开始。**从简单的事情开始。在我看来，测试我们的数据时，最大的价值可以从两件事情中获得:

1.  如果数据质量不好，中断自动化管道
2.  观察数据质量和意外数据/失败的管道

第一点是显而易见的，我们不想使用或发布坏数据，所以如果数据是坏的，我们就失败了。第二个几乎同样有价值:当你开始测试数据质量时，你很可能甚至不知道好数据是什么样子，也就是说，好数据的界限是什么，或者好的数据分布是什么样子？周末和工作日的数据可能会有变化，或者是您在处理初始数据集时没有注意到的季节性趋势。因此，为了保持数据质量，你需要学习和迭代好的数据实际上是什么样子的。

# 这对我们有用

到目前为止，我一直对我们实际上如何测试含糊其辞——所以让我们来看看我们的团队如何持续测试数据的一些更具体的例子。

正如我在一篇关于数据工程实践的[文章](https://mbakunze.medium.com/develop-your-data-as-a-product-f9ba268c4e20)中所写的:保持简单！如果你和我一样，经常使用 python 和 pandas，那么 [great-expectations](https://greatexpectations.io/) 是你开始数据测试之旅的绝佳起点。

远大期望的工作原理是构建*期望套件*(基本上是测试套件)，随后用于验证数据批次。这些套件被保存为`.json`文件，与您的代码一起存在。为了建立期望，您可以使用软件包中的一些基本分析器(或者编写自己的分析器——这相当简单),从一些建议开始，或者从头开始。让我们看一个简单的例子:

上面的例子假设您已经安装并初始化了这个包(我创建了[这个 repo](https://github.com/mbakunze/great_expectation_sandbox) 来让您快速入门)。该示例展示了如何快速地将数据源添加到 great_expectations，将期望添加到期望套件，然后根据期望套件测试数据。您可以选择快速检查数据文档呈现。

## 关键特征

如前所述，我们想要瞄准的第一件事是，如果数据是坏的，就打破管道，然后我们想要观察数据质量随时间的变化。使用数据验证特性可以让您轻松地完成前一个任务:只需将验证作为管道的一部分运行，如果需要的话可以中断。后一个也包括在内，因为验证结果会告诉您哪里出错了，即哪些值是您没有预料到的。所以你马上就能知道哪里出了问题，并采取行动。

其他关键特性包括期望套件与代码共存，这对于版本控制来说是完美的。此外，您可以轻松地向您的套件添加注释，并捕获数据质量问题(它们可以很好地呈现在自动化数据文档中)。

因为所有这些都存在于您的代码库中(当然，您使用 git ),所以可以直接在团队中协作。在笔记本中添加编辑期望(带有可定制的 jinja 模板)是我们经常使用的功能:只需运行`great_expectations suite edit <suite_name>`！

**测试您的数据和数据分布。** great-expectations 允许您轻松测试数据分布。简单的均值、中值、最小值、最大值、分位数或更高级的东西，如库尔巴克-莱布勒散度。您可以使用`mostly`关键字来表示大多数期望，以容忍一定比例的异常值。简单的内在期望会让你走得很远！

当然，还有更多:您可以根据管道运行时测试数据新鲜度，并使用运行时生成的评估参数或构建您自己的预期。还有很多内容我没有介绍，比如自动化数据文档、数据分析报告，它们都带有自动的 HTML 呈现，使共享和发布变得容易。

最重要的是，你可以很容易地参与到对[代码库](https://github.com/great-expectations/great_expectations)的贡献中来——这些人非常乐于助人，非常感激！

## 我们如何使用它

我们测试每个管道运行的输入和输出数据，与管道代码无关。我们的管道作为 kubernetes 作业运行，因此我们创建了一个简单的包装器，它读取命令行参数，解析数据集名称，将它们与一个期望套件进行匹配，并验证数据。

![](img/f6a8d78f59f480eaecacf5be7eaba568.png)

数据验证(蓝色菱形)与实际的管道代码分离，控制管道的失败、警报和发布。

上图是一个简单的图表，显示了当我们的任何管道运行时会发生什么:输入得到验证，然后实际的作业才运行。作业运行后，输出数据得到验证，然后数据才会被发布。如果对输出数据的验证失败，我们发布到一个`failed`目的地，这样我们就可以在需要时检查输出。

## 疼痛

我们一把它投入生产，痛苦就开始了。我们花了大量的时间来分析数据，在非生产环境中运行所有带有新数据验证检查的管道。我们很自信。尽管如此，对于我们的数据以及数据随时间的变化，我们还有很多事情不知道。

几个星期以来，由于数据验证的原因，我们有失败的管道。有些是我们预料到的，但在某些时候，我觉得让我的一个支持轮换的同事经历这些真的很可怕:不断失败的运行，多次更新预期套件，清洗和重复。在开始的时候，很难弄清楚什么时候改变阈值/期望值，什么时候我们在看一个实际的问题。

只有痛苦。

## **增益**

第一次痛苦消退后，我们很快看到奇怪的数据问题。在一个例子中，这使我们实际上发现了一些数据转换管道中的错误，这些错误只是随着时间的推移才显现出来。我们搞定了->利润！

在另一个例子中，我们实际上阻止了发布坏的预测——结果是从企业数据存储中复制数据的一个上游作业有不完整的数据😱。之前，这个 bug 已经导致我们在一个已知的事件中给出了一些不好的预测，其中有一些真实的💰对业务的影响。因此，阻止我们这样做是一笔可观的利润！

# 结论

这是真的:一分耕耘一分收获！

我们都知道我们必须检查我们的数据质量。一旦你打开了那罐蠕虫，你将很快感受到处理你发现的所有数据质量问题的痛苦。但好消息是:这是值得的。简单的数据测试可以让你走得更远，并显著提高你的产品质量。

在团队中，我与数据科学家密切合作，他们现在喜欢数据测试。他们欣赏这个工具以及它为团队和我们的产品创造的价值。我们用它不断改进我们的数据集，我们在测试上合作，测试不会因为管道代码而出错。

因此，尽管这一旅程可能会有痛苦，但这是非常值得的。立即开始测试您的数据！💯