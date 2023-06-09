# 特征工程的力量

> 原文：<https://towardsdatascience.com/the-power-of-feature-engineering-b6f3bb7de39c?source=collection_archive---------22----------------------->

## 为什么您可能只应该使用逻辑回归来建模非线性决策边界(使用 Python 代码)

作为一名数据科学家，我不禁被复杂的机器学习技术所吸引。用一些深度神经网络(DNN)获得额外的 1%的精度，并且在这个过程中必须旋转一个 GPU 实例，这是一件非常令人满意的事情。然而，这些技术经常把思考留给计算机，让我们对模型的工作原理知之甚少。所以，我想回到基础。

![](img/783d1d1d45fad7ff28667c49fc2ad3dc.png)

在这篇文章中，我希望教你一些关于特征工程的知识，以及如何用它来建模一个非线性的决策边界。我们将探讨两种技术的优缺点:逻辑回归(使用特征工程)和神经网络分类器。将给出用于拟合这些模型以及可视化其决策边界的 Python 代码。你也可以在 [GitHub[1]](https://github.com/conorosully/medium-articles) 上找到完整的项目。最后，我希望让你理解为什么特征工程可能是其他非线性建模技术的更好的替代方案。

# 什么是特征工程

每当从原始数据创建要素或将现有要素的函数添加到数据集中时，您都在进行要素工程。这通常是利用特定领域的领域知识来完成的[【2】](https://web.stanford.edu/~hastie/ElemStatLearn/)。例如，假设我们想要预测一个人从手术中恢复所需要的时间(Y)。从之前的手术中，我们已经捕捉到了患者的恢复时间、身高和体重。根据这些数据，我们还可以计算出每个患者的身体质量指数=身高/体重。通过计算并在数据集中包含身体质量指数，我们正在进行要素工程。

## 为什么我们要做特征工程

特征工程是强大的，因为它允许我们将非线性问题重新表述为线性问题。为了说明这一点，假设恢复时间与身高和体重有如下关系:

y =β₀+β₁(height)+β₂(weight)+β₃(height/weight)+噪音

看第 3 项，我们可以看到 Y 和身高体重不是线性关系。这意味着我们可能不会期望线性模型(如线性回归)在估计β系数方面做得很好。你可以尝试使用非线性模型，比如 DNN，或者我们可以通过做一些特征工程来帮助我们的模型。如果我们决定将身体质量指数作为一个特征，则关系变为:

y =β₀+β₁(height)+β₂(weight)+β₃(bmi)+噪音

y 现在可以建模为我们 3 个变量的线性关系。因此，我们期望线性回归在估计系数方面做得更好。稍后，我们将看到同样的想法适用于分类问题。

## 为什么不让计算机来做这项工作呢

如果你想得到技术，特征工程本质上是核心技巧，因为我们将特征映射到一个更高的平面[【3】](https://statinfer.com/203-6-5-the-non-linear-decision-boundary/)。虽然，对于内核技巧，通常涉及的思想较少。内核函数被视为一个超参数，可以使用蛮力找到最佳函数——尝试不同函数变量的负载。使用正确的核函数，您可以建立非线性关系的模型。给定适当数量的隐藏层/节点，DNN 还将自动构建你的特征的非线性函数[【2】](https://web.stanford.edu/~hastie/ElemStatLearn/)。那么，如果这些方法可以模拟非线性关系，我们为什么还要为特征工程费心呢？

我们在上面解释了特征工程如何允许我们捕捉数据中的非线性关系，即使是线性模型。这意味着，根据问题的不同，我们可以获得与非线性模型相似的性能。我们将在本文的后面详细讨论一个例子。除此之外，使用特征工程还有其他的好处，使这项技术值得一试。

![](img/4d95da3ba4db63cbb00c16ee61029f03.png)

首先，你会对模型的工作原理有更好的理解。这是因为您确切地知道模型使用什么信息来进行预测。此外，通过直接查看特征系数，可以很容易地解释像逻辑回归这样的模型。第二个原因源于第一个原因，即该模型更容易解释。如果你在工业界工作，这一点尤其重要。你的同事也更有可能接触到一些更简单的模型。第三个原因是，您的模型不太可能过度符合训练数据。通过强力加载不同的超参数，很容易在数据中模拟噪声。相比之下，通过深思熟虑的特性，你的模型将是直观的，并可能模拟真实的潜在趋势。

# 资料组

让我们深入一个实际的例子。为了让事情尽可能清楚，将使用人工生成的数据集。为了避免这个例子变得令人难以置信的枯燥，我们将围绕它创建一个叙述。那么，假设您的人力资源部门要求您创建一个模型来预测某个员工是否会得到晋升。该模型应考虑员工的年龄和绩效得分。

我们在下面的代码中为 2000 名假设的雇员创建特性。雇员的年龄可以在 18 到 60 岁之间。性能分数可以在-10 到 10 之间(10 为最高)。两个特征都被混洗，因此它们不相关。然后，我们使用以下年龄(a)和表现(p)的函数来生成目标变量:

γ(a，p)= 100(a)+200(p)+500(a/p)-10000+500(噪声)

当γ(a，p)≥ 0 时，员工被提升；当γ(a，p) < 0 时，员工不被提升。我们可以看到，术语 a/p 包含在上面的函数中。这意味着决策界限将不是年龄和表现的线性函数。随机噪声也包括在内，因此数据不能完全分离。换句话说，一个模型不可能 100%准确。

如果上面的步骤有点混乱，也不用担心。我们可以用下面的代码可视化数据集，让事情变得更清楚。这里我们创建了一个数据散点图，结果如图 1 所示。只有两个特征，很容易看出到底发生了什么。y 轴代表员工的绩效得分，x 轴代表员工的年龄。获得晋升的员工的分数为红色，未获得晋升的员工的分数为蓝色。最终，2000 名员工中有 459 人(23%)获得了晋升。对于不同的随机样本，该比率会略有变化。

![](img/9c2527dff4c0c8a7b81ea1b0f65a319a.png)

图 1:促销数据散点图

虽然这个数据是生成的，但是我们还是可以为剧情想出一个现实的解释。在图 1 中，我们可以看到 3 组不同的员工。首先是绩效得分在 0 分以下的群体。由于表现不佳，这些员工中的大多数没有得到提升，我们也可以预计他们中的一些人已经被解雇。我们可以期待得分高于 0 的员工要么获得晋升，要么接受其他地方的聘用。分数特别高的员工往往会离职。这可能是因为它们的需求量很大，而且在别处有更好的报价。然而，随着雇主年龄的增长，他们需要更高的绩效分数才能离开。这可能是因为年纪大的员工在目前的职位上更自在。

无论叙述如何，很明显，决策边界不是线性的。换句话说，不可能画一条直线来很好地区分提升组和未提升组。因此，我们不会期望线性模型做得很好。让我们通过尝试仅使用年龄和表现这两个特征来拟合逻辑回归模型来演示这一点。

# 逻辑回归

在下面的代码中，我们将 2000 名员工分成一个训练集(70%)和一个测试集(30%)。我们使用训练集来训练逻辑回归模型。然后，使用这个模型，我们对测试集进行预测。测试集上的准确率为 82%。这似乎不算太糟，但我们应该考虑到只有不到 23%的员工获得了晋升。因此，如果我们只是猜测没有一个员工会得到晋升，我们应该预计准确率在 77%左右。

通过使用下面的代码可视化它的决策边界，我们可以更好地理解模型在做什么。这里我们在样本空间内生成一百万个点。然后，我们使用逻辑回归模型对所有这些点进行预测。就像图 1 中的散点图一样，我们可以画出这些点。每个点的颜色由模型的预测决定——如果模型预测促销，则为粉红色，否则为浅蓝色。这为我们提供了一个很好的决策边界近似值，如图 2 所示。然后我们可以在这些点上绘制实际的数据集。

查看决策边界，我们可以看到模型做得很糟糕。该公司预测有晋升机会的员工中，大约有一半没有得到晋升。然后，对于大多数获得晋升的员工，它预测他们没有获得晋升。请注意，决策边界是一条直线。这强调了逻辑回归是一个线性分类器。换句话说，模型只能构建一个决策边界，它是您给它的特征的线性函数。在这一点上，我们可能会尝试不同的模型，但让我们看看是否可以使用特征工程来提高性能。

![](img/0272553dd4b82c783bfb88b9e7ca6884.png)

图 2:逻辑回归模型的决策边界

# 特征工程逻辑回归

首先，如下面的代码所示，我们添加了额外的特性(即年龄与性能的比率)。从那时起，我们遵循与先前模型相同的过程。列车测试分割与我们对“随机状态”使用的值相同。最终，该模型实现了 98%的准确率，这是一个显著的改进。

该模型仍然只需要雇员的年龄和表现来进行预测。这是因为附加特征是年龄和表现的函数。这允许我们像以前一样可视化决策边界。这是通过在样本空间中的每个年龄表现点使用模型的预测。我们可以看到，在图 3 中，通过添加额外的功能，逻辑回归模型能够模拟一个非线性的决策边界。从技术上来说，这是年龄和表现的非线性函数，但它仍然是所有 3 个特征的线性函数。

![](img/81a7758dd1be2702c053102509eff9a5.png)

图 3:具有特征工程的逻辑回归模型的决策边界

使用逻辑回归的另一个好处是模型是可解释的。这意味着模型可以用人类的术语来解释[【4】](https://www.kdnuggets.com/2018/12/machine-learning-explainability-interpretability-ai.html)。换句话说，我们可以直接查看模型系数来了解它是如何工作的。我们可以在表 1 中看到模型特征的系数及其 p 值。我们不会涉及太多的细节，但是这些系数可以让你从获得晋升几率的变化来解释特征的变化。如果一个特性有一个正的系数，那么这个特性值的增加会导致升职机会的增加。

![](img/c66b5254b1c7e657c2cda5dfa8af830f.png)

表 1:逻辑回归模型总结

从表 1 中我们可以看出，随着年龄的增长，升职的可能性也在增加。另一方面，对于性能来说，这种关系并不明显。性能的提高也会降低年龄/性能比。这意味着绩效提高的效果取决于员工的年龄。这很直观，因为它与我们在散点图中看到的一致。在这种情况下，可能没有必要以这种方式使用系数来解释模型。仅仅可视化决策边界就足够了，但是随着我们增加特征的数量，做到这一点变得更加困难。在这种情况下，模型系数是理解模型如何工作的重要工具。

同样，p 值可以帮助我们理解模型。由于系数是统计估计值，它们周围有一些不确定性。低 p 值允许我们确定我们的系数不同于 0。换句话说，我们可以确定一个系数要么是正的，要么是负的。这一点很重要，因为如果我们不能确定系数的符号，就很难用概率的变化来解释特征的变化。从表 1 可以看出，所有系数都具有统计学意义。这并不奇怪，因为我们使用特征的函数生成数据。

总的来说，当我们生成数据时，上面的分析非常直接。因为我们知道使用了什么函数来生成数据，所以很明显，这个附加功能将提高模型的准确性。实际上，事情不会这么简单。如果你对数据没有很好的理解，你可能需要和人力资源部的人谈谈。他们也许能告诉你他们过去看到的任何趋势。否则，通过使用各种图和汇总统计数据来研究这些数据，您可以了解哪些特征可能是重要的。但是，假设我们不想做所有这些艰苦的工作。

# 神经网络

为了比较，让我们使用一个非线性模型。在下面的代码中，我们使用 Keras 来拟合神经网络。我们只使用年龄和表现作为特征，因此神经网络的输入层的维数为 2。有 2 个隐藏层，分别有 20 个和 15 个节点。两个隐藏层都具有 relu 激活函数，而输出层具有 sigmoid 激活函数。为了训练模型，我们使用 10 和 100 个时期的批量大小。训练集大小为 1400 时，我们有 14000 步。最终，该模型在测试集上取得了 98%的准确率。这与逻辑回归模型的精度相同，但是我们不需要做任何特征工程。

查看图 4 中 NN 的决策边界，我们可以看到为什么它被认为是一个非线性分类算法。即使我们只给出模型年龄和性能，它仍然能够构建非线性决策边界。所以，在一定程度上，模型为我们做了艰苦的工作。你可以说模型的隐藏层已经自动完成了特征工程。那么，考虑到这个模型具有很高的准确性，并且需要我们付出较少的努力，我们为什么还要考虑逻辑回归呢？

![](img/e596904a78708e7749ba33c54b1fe9bd.png)

图 4:神经网络的决策边界

神经网络的缺点是它只能被解释。这意味着，与逻辑回归不同，我们不能直接查看模型的参数来了解它是如何工作的。我们可以使用其他方法，但最终，理解神经网络的工作原理会更加困难。向非技术人员(如人力资源主管)解释这一点就更难了。这使得逻辑回归模型在行业环境中更有价值。

在工业界和学术界都有许多问题，其中大部分比本文给出的例子更复杂。所提出的方法显然不是解决所有这些问题的最佳方案。例如，如果你试图做图像识别，你不会用逻辑回归得到任何东西。对于更简单的问题，逻辑回归和对数据的充分理解通常是你所需要的。

## 图像来源

所有图片都是我自己的或从[www.flaticon.com](http://www.flaticon.com)获得的。在后者的情况下，我拥有他们的[高级计划](https://support.flaticon.com/hc/en-us/articles/202798201-What-are-Flaticon-Premium-licenses-)中定义的“完全许可”。

## 参考

[1]奥沙利文(C. O'Sullivan)，medium-articles(2020)，【https://github.com/conorosully/m】T4edium-articles

[2] T .哈斯蒂，r .蒂布希拉尼，j .弗里德曼，
统计学习的要素【第 150 页】(2017)，[https://web.stanford.edu/~hastie/ElemStatLearn/](https://web.stanford.edu/~hastie/ElemStatLearn/)

[3] Statinfer，非线性决策边界(2017)，[https://statin fer . com/203-6-5-The-Non-Linear-Decision-Boundary/](https://statinfer.com/203-6-5-the-non-linear-decision-boundary/)

[4] R. Gall，机器学习可解释性 vs 可解释性:两个可以帮助恢复对 AI 信任的概念(2018)，[https://www . kdnugges . com/2018/12/Machine-Learning-explability-interpretatibility-AI . html](https://www.kdnuggets.com/2018/12/machine-learning-explainability-interpretability-ai.html)

[5] UCLA，我如何解读 Logistic 回归中的优势比？(2020 年)，[https://stats . idre . UCLA . edu/stata/FAQ/how-do-I-interpret-odds-ratios-in-logistic-regression/](https://stats.idre.ucla.edu/stata/faq/how-do-i-interpret-odds-ratios-in-logistic-regression/)