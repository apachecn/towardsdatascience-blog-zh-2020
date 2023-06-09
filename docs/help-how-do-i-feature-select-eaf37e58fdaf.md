# 救命啊！我如何选择特征？

> 原文：<https://towardsdatascience.com/help-how-do-i-feature-select-eaf37e58fdaf?source=collection_archive---------43----------------------->

很多时候，我们不确定如何选择我们的特征。这只是一个帮助选择的小指南。(免责声明:现在我将谈论二进制分类。)

很多时候，当我们非常兴奋地使用一种奇特的机器学习算法进行预测，并且几乎准备好应用我们的模型对测试数据集进行分析和分类时——我们不知道应该选择什么特征。通常情况下，功能的数量可以从几十个到几千个不等，并且不太清楚如何选择与*相关的*功能，以及我们应该如何选择*许多*功能。有时将*的特性组合在一起也不失为一个好主意，这也被称为特性工程。这方面的一个常见例子，你可能在机器学习中听说过——是*主成分分析(PCA)* ，其中数据矩阵 X 被分解为其奇异值分解(SVD) *U*∑*V* ，其中∑是具有奇异值的对角矩阵，你选择的奇异值数量决定了*多少个*主成分。你可以把主成分看作是减少数据集维度的一种方式。PCA 的惊人之处在于，新的工程特征或“主成分”是原始特征的线性组合。这太棒了！我们喜欢线性组合，因为它只涉及加法和标量乘法，并且它们不难理解。例如，如果你对一个关于房价回归的数据集进行主成分分析，假设你只选择了 2 个主成分。那么第一个组件 PC1 可以是: *c1** (卧室数量)+ *c2** (#平方英尺)。PC2 可能是类似的东西。*

主成分的限制是，你创造的新的特征仅仅是一些旧特征的线性组合。这意味着你不能利用非线性的特征组合。这是神经网络所擅长的；他们可以创建大量的非线性特征组合/功能。但是他们有一个更大的问题:新功能的可解释性。工程特征基本上隐藏在网络不同层之间的权重矩阵乘法中(这只是非线性函数的组合)。具有额外非线性的神经网络在敌对攻击下往往会变得脆弱和崩溃，例如对卷积神经网络的几个像素攻击，或者[欺骗神经网络将一只熊猫和一个黑色方块错误地分类为秃鹫](https://codewords.recurse.com/issues/five/why-do-neural-networks-think-a-panda-is-a-vulture)——诸如此类怪异、无意义的事情。

那么，该如何处理特性呢？？好吧，如果我们设计新功能的方式有点有限，我们可以总是只选择我们已经拥有的功能的子集！但是你需要小心。有许多方法可以做到这一点，但并不是所有的都是可靠和一致的。比如随机森林。诚然，在使用分类器的最后，Python 会用随机森林的 *feature_importances* 方法输出相关特征。但是让我们想一想:随机森林是通过训练一组决策树来工作的，每一个决策树都基于训练数据的随机子集。因此，如果你一直重复 RF 模型，你可能每次都得到不同的特性重要性，这是不健壮的或者不一致的。作为一名数据科学家或 ML 工程师，看到每次都弹出不同的相关特性集，不会感到困惑吗？你显然没有改变数据集！那么，你为什么要相信不同的“重要性”特征呢？这样做的问题是，你选择的“重要性”特征取决于随机森林模型本身——即使 RF 具有很高的精度，选择仅基于数据集*、*的特征也比首先包括重型模型更有意义。

选择一致的、不混乱的、健壮的特性的关键可能是这样的:独立于你的模型选择特性*。无论是否使用神经网络、RF、逻辑回归或任何其他监督学习模型，您选择的相关特征都应该是相关的*。这样，当你试图同时选择不可靠的特征时，你就不必担心你的机器学习模型的预测能力。**

*那么，如何挑选独立于模型的特征呢？Scikit-Learn 有几个选项。其中我最喜欢的一个叫做*互信息*。这是概率论中的一个重要概念。基本上，它计算你的特征变量和你的标签变量*相对于*的相关性，假设它们是独立的。一种更简单的说法是测量你的类标签对某个特性的依赖程度。*

*例如，假设您通过查看数据集中的一系列特征列(如几何面积、位置、色调等)来预测某人是否患有肿瘤。如果你试图选择与你的预测相关的特征，你可以使用互信息来谈论每个类别标签如何依赖于肿瘤的几何面积、位置和色调。这是从数据中直接得到的测量值；它从一开始就不涉及使用预测模型。*

*您还可以使用 Sci-kit Learn 的 *chi-2* ，或“卡方”来确定特性的重要性。这是在特征和标签之间使用卡方检验来确定哪些特征与标签相关，哪些特征与标签无关。你可以把这种方法看作是测试一个“零假设”H0:特征独立于分类标签吗？为此，您需要基于数据表计算卡方统计量，获得 p 值，并确定哪些要素是独立的或不独立的。然后你把独立的特性扔掉(为什么？因为根据你的测试，它们独立于标签的*，所以它们不提供任何信息)并保留依赖的标签。**

*这个测试实际上是基于与上面讨论的互信息计算相似的原理。然而， *chi2* 确实做出了重要的假设，即数据集中取连续值(比如 5.3，pi，sqrt(2)，诸如此类)的要素是正态分布的。通常对于大的训练数据集来说，这不是问题，但是对于小的训练数据集来说，这个假设可能会违反，所以在这些情况下计算互信息可能会更可靠。*

*基本点是这样的:互信息和卡方特征选择方法对预测模型是稳健的。您的预测模型可能非常不准确，但是您收集的数据是静态的，不会在表中更改，因此在没有模型的情况下计算您的要素更加一致。*

*其他特征选择方式包括递归特征消除(RFE)，它使用预先固定的模型(比如逻辑/线性回归或随机森林)，并使用预先固定的模型测试几乎所有的特征子集*，并通过查看哪个特征子集给出最低精度误差来决定哪些特征是最好的。(从技术上讲，随机森林在 Scikit Learn 中使用了一个额外的方法，称为 *feature_importance* ，但我在这里不会深入讨论。)然而，RFE 确实需要很多时间，因为如果你有 K 个特征，那么大约有 2 到 K 个特征子集，所以需要很长时间来计算每个子集的模型并获得分数。**

*我反对 RFE 和类似技术的另一个重要原因是，它基本上是一种依赖于模型的特征选择技术。如果你的模型不准确，或者过度拟合，或者两者兼而有之，并且用户无法理解——那么你选择的特性实际上不是你选择的，而是模型选择的。所以。特征重要性可能无法准确表示哪些特征实际上是基于数据集的*预测。**

*那么我们能从这些中学到什么呢？好吧，最后，如果你不知道如何用主成分分析来解释你的工程特征，特征选择是非常重要的。然而，当你选择特征时，同样重要的是要注意*你是如何选择特征的*，以及计算时间。你的方法在计算机上花费太多时间吗？你的特征选择是基于首先使用特定的模型吗？理想情况下，不管你用什么型号的,你都会想要特征选择*,所以在你的 Jupyter 笔记本里，你会想要在型号*之前做一个特征选择的单元格*——就像这样:**

```
*from sklearn.feature_selection import SelectKBest
from sklearn.feature_selection import mutual_info_classif
# "mutual_info_classif" is the mutual-information way of selecting
# the K most dependent features based on the class-labelK = 3
selector = SelectKBest(mutual_info_classif, K)
X = new_df.iloc[:, :-1]
y = new_df.iloc[:, -1]
X_reduced = selector.fit_transform(X,y) 

features_selected = selector.get_support()*
```

*首先，我做了特征选择(如上)。*

```
*from sklearn.model_selection import train_test_splitX_train, X_test, y_train, y_test = train_test_split(X_reduced, y, 
train_size=0.7)
# use logistic regression as a model
logreg = LogisticRegression(C=0.1, max_iter=1000, solver='lbfgs')
logreg.fit(X_train, y_train)*
```

*然后我训练了模型(上图)！:)*