# 停止置换功能

> 原文：<https://towardsdatascience.com/stop-permuting-features-c1412e31b63f?source=collection_archive---------14----------------------->

![](img/a7def88dec532b8349f19ad14b5b2ba5.png)

众所周知，荷马·辛普森是一个头脑简单的人，时不时会做出一些愚蠢的事情。在这里，他决定用煤气炉烹饪面包、熏肉和鸡蛋，因为这是一堆篝火；不适合这种用途的工具。我们发现看起来很有趣，但同时，我们倾向于在数据科学中做类似的事情。不要像荷马那样，使用适当的工具。《辛普森一家》(《荷马史诗》第七季第 17 集)中的这个镜头被认为是合理使用

数据科学家需要为各种任务进行特征重要性计算。重要性可以帮助我们了解我们的数据是否有偏差，或者模型是否有缺陷。此外，重要性经常用于理解底层流程和制定业务决策。事实上，该模型最重要的特性可能会给我们进一步的特性工程带来灵感，并对正在发生的事情提供见解。

现在有很多方法可以计算特征的重要性。它们中的一些基于模型的类型，例如，线性回归的系数、基于树的模型中的增益重要性、或者神经网络中的批量范数参数(BN 参数通常用于 NN 修剪，即神经网络压缩；例如，[这篇论文](https://arxiv.org/pdf/1802.00124.pdf)描述了 CNN 网络，但是同样的逻辑也适用于全连接网络。虽然其他方法是“通用的”，但它们可以应用于几乎任何模型:如 SHAP 值、排列重要性、丢弃-再学习方法等方法。

虽然模型的黑盒拆箱是模型开发流程中不可或缺的一部分，但 Harmanpreet 等人进行的一项研究([解读可解释性:理解数据科学家对机器学习可解释性工具的使用](http://www-personal.umich.edu/~harmank/Papers/CHI2020_Interpretability.pdf))表明，并非所有的数据科学家都知道如何正确地完成这项工作。这些方法的可用性和简单性使它们成为“金锤”。事实上，如果一个人可以运行“pip install lib，lib.explain(model)”，为什么要为背后的理论费心呢？

在这篇文章中，我想提出一个在寻找有影响的特征时过度使用排列重要性的偏见。我将说明在某些情况下，排列重要性会给出错误的、误导性的结果。

# 排列重要性

排列重要性是一种常用的特征重要性类型。它显示了用随机排列的值替换该特征时得分的下降。它是通过几个简单的步骤计算出来的。

1.  带训练数据的训练模型 *X_train* ，*y _ train*；
2.  对一个训练数据集*X _ train*—*y _ hat*进行预测，并计算得分— *score* (得分越高越好)；
3.  为了计算每个特征的置换重要性 *feature_i* ，执行以下操作:
    (1)置换训练数据集中的 *feature_i* 值，同时保持所有其他特征“原样”——*X _ train _ permuted*；
    (2)使用 *X_train_permuted* 和之前训练的模型— *y_hat_permuted* 进行预测；
    (3)计算置换数据集上的得分—*score _ permuted*；
    (4)特征的重要性等于 *score_permuted — score* 。delta 越低，特征越重要。
4.  该过程被重复几次以减少随机排列的影响，并且分数或等级在运行中被平均。

说明计算的代码片段:

排列重要性易于解释、实现和使用。尽管计算需要对训练数据进行 n 次预测，但与模型再训练或精确的 SHAP 值计算相比，这不是实质性的操作。此外，排列重要性允许您选择要素:如果排列数据集的得分高于正常得分，这是移除该要素并重新训练模型的明显信号。由于这些原因，排列重要性被广泛应用于许多机器学习流水线中。

# 问题

虽然对于模型解释来说，排列重要性是一个非常有吸引力的选择，但它有几个问题，尤其是在处理相关要素时。贾尔斯·胡克和卢卡斯·门奇在他们的论文《请停止置换特征的解释和选择》中将它们结合起来:

1.  [施特罗布尔等人(2007)](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-8-25) 调查分类并注意到，基于购物车构建树中置换出袋(OOB)误差的重要性测量偏向于与其他特征相关和/或具有许多类别的特征，并进一步表明自举夸大了这些影响；
2.  [Archer 和 Kimes (2008)](https://www.sciencedirect.com/science/article/abs/pii/S0167947307003076) 探索了类似的设置，并注意到当真实特征(实际上与响应相关的特征)与噪声特征不相关时，性能得到改善；
3.  [Nicodemus 等人(2010)](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-11-110) 在大规模模拟研究中调查了这些特征偏好的主张，并再次发现 OOB 测量高估了相关预测因子的重要性。

对此可能的解释是模型的外推。假设，该模型使用两个高度正相关的特征 *x1* 和 *x2* 进行训练(下图左边的图)。为了计算特征 *x1* 的重要性，我们对特征进行混洗，并对“混洗”后的点(中心图上的红点)进行预测。但是模型没见过左上角和右下角有 *x1* 的训练例子。因此，为了进行预测，它必须外推至以前未见过的区域(右图)。所有模型的推断都很糟糕，因此做出了意想不到的预测。这些“来自新区域的点”强烈影响最终得分，并因此影响排列重要性。

![](img/b9931104fe02e8f487e0007c0ece9b45.png)

图一。排列重要性问题的直观说明——未知区域

Giles Hooker 和 Lucas Mentch 提出了几种替代排列重要性的方法:

1.  条件变量重要性-根据剩余要素的值有条件地置换要素，以避免“看不见的区域”；
2.  丢弃变量重要性—相当于雷等人在[中探讨的留一个协变量的方法](https://arxiv.org/abs/1604.04173):丢弃特征、重新训练模型、比较分数。
3.  置换和重新学习的重要性——该方法在 [Mentch 和 Hooker](http://jmlr.org/papers/volume17/14-168/14-168.pdf) 中采用:置换特征、重新训练模型、比较分数。

# 实验

为了理解特征相关性如何严重影响排列重要性和其他特征重要性方法，我进行了以下实验。

## 实验设置

首先，我生成了一个具有指定数量的特征和样本的正态分布数据集( *n_features* =50，*n _ samples*= 10000)。所有特征的平均值等于 0，标准偏差等于 1。所有数据集特征通过 *max_correlation* 关联相互关联。

生成数据集后，我给每个特征添加了均匀分布的噪声。每个特征的噪声幅度从*[-0.5 *噪声幅度最大值，0.5 *噪声幅度最大值]* ，*噪声幅度最大值=变量*之间的均匀分布中随机选择。这样做是为了降低特征相关性。任务的特性已经准备好了！

现在我们需要创建一个目标。对于每个特征，我生成了一个权重，它是从具有指定伽马和比例参数的伽马分布中采样的(*伽马* =1，*比例* =1)。选择伽马分布是因为它看起来非常类似于典型的特征重要性分布。然后将每个特征权重除以权重之和，使权重之和等于 1。这样做是为了减少随机权重生成对最终结果的影响。

![](img/f84ee76e3553d56c9f4d4371c55269e0.png)

图二。左侧为随机森林要素重要性(旋转)的示例。每个条形显示了 ML 模型中一个特性的重要性。右边是排序的总和比例伽马分布的条形图。每个条显示了特征在目标代的线性组合中的权重，这本身就是特征重要性。[左图来源](https://scikit-learn.org/stable/auto_examples/inspection/plot_permutation_importance.html)

然后，目标的 logit 被计算为特征和相应特征权重的线性组合(随机选择特征权重的符号)。sigmoid 函数应用于目标的标准标度 logit。为了得到标签，我对结果进行了四舍五入。目标准备好了！

对于生成的数据集和目标，我使用以下参数训练了一个 LightGBM 模型:

```
learning_rate: 0.01
n_estimators: 100
random_state: 42
```

所有其他参数都是默认值。我使用内置的增益重要度、SHAP 重要度和排列重要度(排列重复五次，求增量分数的平均值)来计算每个特性的重要度。

然后，我计算了计算的重要性和特性的实际重要性之间的 Spearman 等级相关性。实际重要性等于*等级(-权重)*。最可能的相关性是 1.0，即要素重要性与实际重要性(要素权重)处于同一顺序。

每个实验的数据(数据集相关性统计、内置增益重要性的模型重要性和特征的实际重要性之间的 Spearman 等级相关性、SHAP 重要性和排列重要性)被保存用于进一步分析。使用不同的种子和 *max_correlation* 和 *noise_magnitude_max* 的不同组合，实验运行五十次。我还用“丢弃并重新学习”和“置换并重新学习”的方法进行了相同的实验，但是由于需要大量的计算，只进行了五次。

实验的代码和分析可以在项目的资源库中找到:

[](https://github.com/DenisVorotyntsev/StopPermutingFeatures) [## DenisVorotyntsev/StopPermutingFeatures

### 这个库包含了我在关于置换重要性的博客文章中描述的实验的代码——停止置换…

github.com](https://github.com/DenisVorotyntsev/StopPermutingFeatures) 

## 例子

为了让你熟悉正在发生的事情，我将举例说明一个实验。实验图解笔记本可以在这里找到:[实验图解](https://github.com/DenisVorotyntsev/StopPermutingFeatures/blob/master/notebooks/0-experiment-illustration.ipynb)。实验的参数是:

```
TASK = "classification"
OBJECTIVE = "binary"
METRIC = roc_auc_scoreMU = 0
VAR = 1
N_FEATUES = 50
N_SAMPLES = 10_000NOISE_MAGNITUDE_MAX = 1
SEED = 42
```

生成的数据集的相关矩阵的一部分:

![](img/3520aa9a1ff62d929127577ae401b062.png)

图 3。要素数据集 R2 相关矩阵的一部分

我们可以看到，这些特征彼此之间高度相关(平均绝对相关系数约为 0.96)。相关性统计:

![](img/9c1f96a0d52bb3c7ddca3d5f4b75e99f.png)

图 4。特征数据集相关性的统计。abs_*前缀代表相关度的绝对值(注意:数据集中的要素可能相互负相关或正相关)

生成要素权重的分布:

![](img/f24d56422903bad790d00628012c3371.png)

图 5。实际特征权重分布。只有几个特性是重要的，其余的都不重要。ML 任务中的常见情况

特征的计算重要性和实际重要性之间的计算 Spearman 等级相关性:

```
Model's score [train data]: 0.9998
Permutation spearman corr: 0.5724
SHAP spearman corr: 0.4721
LGB gain spearman corr: 0.4567
```

以及预期和计算功能重要性等级的说明:

![](img/bb7fd50a331d94775cb20d0d0994e1d0.png)

图 6。预期和计算的等级(排列重要性)，NOISE_MAGNITUDE_MAX=1

我们可能会在这里看到几个问题(用绿色圆圈标记):

1.  最重要和第二重要的功能等级不匹配
2.  根据排列重要性，第三最重要的特征应该是第九；
3.  如果我们相信排列的重要性，那么实际的第 8 个重要特性会下降到第 39 位。

以下是相同实验参数的预期和计算的特征重要性等级的图示，除了*噪声 _ 幅度 _ 最大值*，其现在等于 10(*ABS _ 相关性 _ 平均值*从 0.96 下降到 0.36):

```
Model's score [train data]: 0.9663
Permutation spearman corr: 0.6430
SHAP spearman corr: 0.7139
LGB gain spearman corr: 0.6978
```

![](img/57e3d09701d0fe6615564383df7e96ec.png)

图 7。预期和计算的等级(排列重要性)，噪声 _ 幅度 _ 最大值=10

仍然不完美，但即使视觉上更好，如果我们谈论的是十大最重要的功能。

# 结果

我进行了描述的实验和绘图结果，这在本节中介绍。“排列对 SHAP 对增益”实验总共进行了 1200 次，而“排列对再学习”实验进行了 120 次。

## 置换 vs SHAP vs 增益

在这一小节中，我比较了使用排列重要性、SHAP 值和内置增益计算的特征重要性排名。

从下面的图中，我们可以看到，实际特征重要性之间的相关性以及使用排列、SHAP 值和增益计算的相关性与预期的特征相关性的平均值和最大值负相关。排列重要性受高度相关特征的影响最大。使用内置增益的 SHAP 计算的重要性没有区别。

此外，我们可以看到，实际特征重要性和计算值之间的相关性取决于模型的分数:分数越高，相关性越低(图 10-Spearman 特征等级相关性= f(模型的分数))。不清楚为什么会发生这种情况，但我可以假设，更多的相关特征导致更准确的模型(从图 11 可以看出，模型的得分= f(特征相关性的平均值))，因为更密集的特征空间和更少的“未知”区域。

![](img/818b52ac6aceae1f1c2cfb6cb20b7315.png)

图 8——Spearman 特征等级相关性= f(特征相关性平均值)

![](img/4dc98e672fdf68f4e38070ddb8563b41.png)

图 9-Spearman 特征等级相关性= f(最大特征相关性)

![](img/2cb58a0c3f82d6e98cd90320a36f269d.png)

图 10——Spearman 特征等级相关性= f(模型得分)

![](img/ffb017777c32d208c6d2a3804eaf7514.png)

图 11 —模型得分= f(特征相关性平均值)

## 置换与重新学习

在这一小节中，我比较了排列的重要性和再学习的方法。

令人惊讶的是，在所有相关性中，重新学习方法的表现明显比排列差，这可以从下面的图中看出。此外，重新学习方法花费了大约 *n_features* 倍的时间来运行。

![](img/fe8a19e887d39a18ae6c99baeeb74ef7.png)

图 12——Spearman 特征等级相关性= f(特征相关性平均值)

![](img/6ad6e309f963b3f2a9120706840d196e.png)

图 13-Spearman 特征等级相关性= f(最大特征相关性)

# 结论

1.  不要使用排列重要性来解释基于树的模型(或任何在看不见的区域内插得不好的模型)。
2.  请改用 SHAP 值或内置增益重要性。
3.  不要使用“置换并重新学习”或“丢弃并重新学习”的方法来寻找重要的特性。

# 摘要

在这篇文章中，我描述了排列重要性方法和与之相关的问题。我展示了高度相关的特性如何以及为什么会影响排列的重要性，这将给出误导性的结果。我进行了一个实验，实验表明排列重要性受高度相关特征的影响最大(在使用 SHAP 值和增益计算的重要性中)。我还表明，尽管重新学习的方法有望成功，但它们的表现不如排列重要性，并且需要更多的时间来运行。

我希望这篇文章能帮助数据科学家正确地解释他们的模型。

# 承认属实

帖子的主题和进行的实验受到了贾尔斯·胡克和卢卡斯·门奇所做的“[请停止置换功能的解释和替代品](https://arxiv.org/abs/1905.03151)”的启发。

# 附加链接

如果你喜欢这个，你可能会有兴趣阅读我的另一篇关于石灰重要性问题的文章:

[](/whats-wrong-with-lime-86b335f34612) [## 酸橙有什么不好

### 虽然是解释任何分类器预测的最流行的方法之一，石灰有几个主要的…

towardsdatascience.com](/whats-wrong-with-lime-86b335f34612)