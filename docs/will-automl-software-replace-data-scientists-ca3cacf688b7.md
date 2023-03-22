# AutoML 软件会取代数据科学家吗？

> 原文：<https://towardsdatascience.com/will-automl-software-replace-data-scientists-ca3cacf688b7?source=collection_archive---------43----------------------->

## AutoML 对数据科学家来说不是威胁

![](img/d6e91d53acc6ce6cdc8e20d844f37ed9.png)

马库斯·温克勒在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

在过去的几年里，已经推出了许多自动化机器学习软件。他们可以自动执行一些数据科学家通常必须手动执行的任务。它们已经达到了非常显著的复杂和有效的水平。它们是对数据科学家工作的威胁还是机遇？

# 什么是 AutoML？

AutoML 是一个通用表达式，表示自动执行机器学习任务的软件。它们通常自动执行整个流水线处理，例如清理、编码、特征和模型选择以及超参数调整。这种软件可以是 Python 库，如 Auto-Sklearn，也可以是软件程序，如 Data Robot。

软件的自动化部分取代了数据科学家工作中花费更多时间的所有无聊步骤。他们实际上对管道的几个参数(例如，空白填充值、缩放算法、模型类型、模型超参数)进行所有组合，并使用某种搜索算法(如网格或随机搜索)在 k-fold 交叉验证中选择最大化某些性能指标(如 RMSE 或 ROC 曲线下的面积)的最佳组合。

他们真的可以简化那些必须从头开始创建模型的人的生活，有时他们会探索数据科学家可能没有想到的组合和场景。

# 它会取代数据科学家的工作吗？

有人可能会认为 AutoML 取代了数据科学家的工作，并可能使这项工作在未来过时。没有比这种怀疑更错误的了。我们来看看为什么。

# 数据科学(不仅仅)是机器学习

数据科学家不仅仅是使用机器学习模型的人。数据科学家分析数据中隐藏的信息，提取有用的相关性，帮助准备正确的数据以输入 ML 管道，提供关于创建数据本身的业务的有用见解。这些东西是数据科学最重要的部分，不能完全自动化。他们依赖于对业务的深入了解，依赖于对人们所使用的商业语言的有力而有效的运用，最重要的是，依赖于业务经理所使用的商业语言。

所有这些都使得数据科学家的工作比运行机器学习模型更加复杂和有趣，这超出了 AutoML 的范围。

AutoML 软件自动化机器学习任务，而不是整个数据科学过程。机器学习只是数据科学家工作的一小部分，可能不是最重要的，也不是最具挑战性的。理解数据、信息和业务环境是数据科学家的真正挑战，如果这些任务没有完全完成，机器学习将永远不会成为解决所有问题的魔杖。

# AutoML 不是单独工作的

AutoML 是软件，所以它总是需要有合适技能的人来使用。事实上，AutoML 结果必须经过专业数据科学家的验证，以确保它们是正确的，并且在产生它们的商业环境中有意义。产生一个在理论上看起来完美的模型并不罕见，但在现实中，它不能产生任何有用的商业见解，或者在最坏的情况下，它的预测是微不足道的。这就是为什么数据科学家必须一直在那里，以确保模型告诉我们一些新的东西，而不只是咀嚼一些旧的东西。

# AutoML 对数据科学家有用吗？

是的，我认为它非常有用，因为它自动化了所有枯燥的任务，这些任务通常需要大量代码，并且很有可能出错。如果没有 AutoML，数据科学家必须从头开始创建自己的 ML 管道。每个 ML 模型都有自己的要求(例如，为神经网络缩放特征)，因此要测试的整套管道可能会变得非常复杂和耗时。使用 AutoML 工具将很容易让数据科学家创建一个好的 ML 模型，而不必太关心代码。记住:数据科学家不是软件工程师，所以他必须写尽可能少的代码，以便专注于数据和信息。

# 结论

我认为数据科学家必须跟随变化和创新，所以如果他们开始正确使用 AutoML，它可以成为他们非常有用的朋友。如果他们将枯燥的任务自动化，他们可能会有更多的时间花在分析信息上，这是数据科学家的真正目标。