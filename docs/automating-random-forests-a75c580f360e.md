# 自动化随机森林

> 原文：<https://towardsdatascience.com/automating-random-forests-a75c580f360e?source=collection_archive---------55----------------------->

## 建立你自己的自动机器学习系统的教程。

![](img/f5833b233efec20d3a9b980b45d377ed.png)

克里斯里德在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

我最近完成了一个[网站](https://nocodeml.herokuapp.com/)的开发，它可以进行端到端的机器学习(作为一个 GUI ),也就是说，它可以自动完成以下步骤:

*   使用表单从用户处获取培训数据和测试数据。
*   清理数据并使其可用于机器学习模型(如填充缺失值、处理分类变量等。).
*   根据数据训练随机森林并调整其超参数。
*   对数据执行特征工程。
*   为最终模型绘制特征重要性图。
*   根据测试数据生成预测，并将结果和功能重要性图发送到用户提供的电子邮件地址。

所以在这篇博客中，我将带你浏览设置这样一个系统的代码。你可以在这里找到包含网站[机器学习部分核心代码的 GitHub repo。](https://github.com/shaan2909/Automating-RF-Website/blob/master/ml/mlcode.py)

我们将使用旧的 fastai 库(v0.7)的一部分作为开始的初始基础(代码直到第 500 行包含来自库的片段和其他将被使用的必要导入)。您可以复制代码片段或安装库。我们将从这里开始编码！

我将一段一段地解释代码。所以让我们开始吧！

上面的代码定义了一些函数，随着我们的深入，这些函数将被重复使用。两个功能最为突出:

*   “print_score”:它将用于评估我们的模型在训练和验证数据集上的性能。
*   “auto_train”:它将用于使用给定的超参数来训练随机森林。

下一个函数“data_trainer”有点长，所以我将把它分成两部分来解释给你听。它将用于执行以下任务:

*   清理数据，处理分类变量，从日期(如果有的话)中提取信息，并填充缺失的值。
*   训练随机森林并调整其超参数。
*   特征工程。
*   删除多余的变量。
*   绘制特征重要性图。

所以，让我们开始吧！我已经添加了注释来划分与每个过程相对应的部分。

上述代码(“data_trainer”的第一部分)执行以下任务:

1.  它从日期列(如果有的话)中提取数据，比如年、日、月、季度末与否、年末与否等等。
2.  它将分类变量转换成机器学习模型可以使用的格式。它还会填充缺失的值。
3.  它将数据分成训练和验证数据集。
4.  如果数据集非常大，它将使用“RF _ sampling”(fastai 中的一种加速方法)。
5.  然后，它将使用循环开始调整随机森林的超参数，即“min_samples_leaf”和“max_features ”,以获得最佳结果。

上面的代码(“data_trainer”的第二部分)将执行特征工程，并删除不影响我们的目标变量或多余的变量。
之后，该函数将返回最佳超参数和用于训练最终模型的特征列表。

上面的代码定义了一个函数来预测测试数据集，并生成和保存特征重要性图。它执行以下所有操作:

*   像我们对训练数据集所做的那样，从日期列(如果有)中提取信息。
*   在整个数据集(训练+验证)上训练随机森林(使用在先前函数中获得的超参数和特征工程信息),并将其应用于测试数据集以生成预测。
*   生成特征重要性图并保存。

现在剩下要做的就是将所有先前定义的函数捆绑在一起，通过适当的输入以适当的顺序调用它们，这就是下面要做的。

总结:
我们首先定义了一个函数来清理训练数据，找到最佳超参数，并执行特征工程(称为“data_trainer”)。然后，我们定义了一个函数，使用从上述函数获得的信息来训练模型，并使用它来生成测试数据集的功能重要性图和预测(称为“auto_applyer”)。然后，我们使用一个名为“auto_predictor”的函数将一切联系起来。此外，如果你想建立一个电子邮件系统来发送包含结果的电子邮件，你可以在这里找到代码[。](https://gist.github.com/shaan-shah/dfc51a2988964f42564baf1ca63dbf2b)
瞧！我们建立了自己的自动化机器学习系统。

你可以查看网站(端到端 GUI) [这里](https://nocodeml.herokuapp.com/)这里是 GitHub repo [。](https://github.com/shaan2909/Automating-RF-Website)

非常感谢你阅读这个博客！

附言
如有任何问题或建议，请随时通过 [LinkedIn](https://www.linkedin.com/in/shaan-shah-88085819b/) 与我联系。