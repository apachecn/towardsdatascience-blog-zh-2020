# 主成分分析最温和的介绍

> 原文：<https://towardsdatascience.com/the-most-gentle-introduction-to-principal-component-analysis-9ffae371e93b?source=collection_archive---------9----------------------->

![](img/5e284b5bcd00dd39cea973f48589d218.png)

来源: [Skitterphoto](https://pixabay.com/users/skitterphoto-324082/) @ pixabay —免费股票图片

## 包括特征向量和特征值

在过去的几个月里，我花了相当多的时间重温一些我已经遗忘的数学知识。这让我最终理解了机器学习中的一些关键概念，这些概念我以前有点理解，但从来没有深入到以一种清晰的方式向其他人解释它们。所以今天，我们要测试一下我自己，看我能多清楚地解释一个概念，比如主成分分析。

这个故事的目的是给出一个关于它是如何工作的强烈直觉，而不是过多地进入本质的数学细节。然而，解释一些基本概念是不可避免的。我很乐意阅读您在评论部分的反馈，因为我们的想法是继续写这类故事，为没有坚实数学背景的数据爱好者涵盖机器学习的关键概念。

让我们从理解什么是主成分分析开始，从现在开始我们称之为 PCA。来自维基百科， **PCA 是一种统计过程，将一组可能相关变量的观察值转换为一组线性不相关变量的值，称为主成分**。简单来说，PCA 常用于简化数据、降低噪声、寻找不可测的“潜在变量”。这意味着主成分分析将帮助我们**找到数量减少的特征，这些特征将以压缩的方式表示我们的原始数据集，根据我们最终选择的新特征的数量，捕捉其方差的特定部分**。这种转换的定义方式是，第一个主成分具有最大的可能方差(即，尽可能多地解释数据中的可变性)，而每个后续成分依次具有最大的可能方差。

前一段提到了一些重要的事情，但在深入之前，让我们快速回顾一下一些基本概念。

在整个故事中，我们将使用 Kaggle 上的[数据集的一个子集，该数据集由哥伦比亚商学院的教授汇编，试图找到一个问题的答案，即什么影响一见钟情？数据是从 2002 年至 2004 年的实验性速配活动参与者那里收集的。在活动期间，参与者将与其他异性参与者进行四分钟的“第一次约会”。在四分钟结束时，参与者被问及是否愿意再次见到他们的约会对象。他们还被要求从六个方面评价他们的约会对象:吸引力、真诚、智力、乐趣、雄心和共同兴趣。](https://www.kaggle.com/annavictoria/speed-dating-experiment)

我们的数据集名为' **sd** '(快速约会的首字母缩写)，总共包含 551 行和以下 29 个特征:

```
sd.columnsIndex([‘subject_id’, ‘wave’, ‘like_sports’, ‘like_tvsports’, ‘like_exercise’, ‘like_food’, ‘like_museums’, ‘like_art’, ‘like_hiking’, ‘like_gaming’, ‘like_clubbing’, ‘like_reading’, ‘like_tv’, ‘like_theater’, ‘like_movies’, ‘like_concerts’, ‘like_music’, ‘like_shopping’, ‘like_yoga’, ‘subjective_attractiveness’, ‘subjective_sincerity’, ‘subjective_intelligence’, ‘subjective_fun’, ‘subjective_ambition’, ‘objective_attractiveness’, ‘objective_sincerity’, ‘objective_intelligence’, ‘objective_fun’, ‘objective_ambition’], dtype=’object’)
```

如您所见，这些列代表了兴趣和看法。其中一些可能是相互关联的。比如欣赏音乐和电影，或者喜欢体育和电视体育。这就是为什么，尽管 29 列并不多，我们的目标是，在这个故事的结尾，将列的总数减少到几个不相关的特征，解释兴趣和认知之间的大部分关系。也就是**我们希望以一个更小的特征集来解释数据集**的初始列之间的原始关系。我们将使用线性代数和主成分分析来实现。

让我们开始记住，每次我们处理任何给定的数据集时，我们只有一个巨大的矩阵，每个特征包含一个向量。

![](img/024dcff911a5c157cde5a41c9dbf7cf5.png)

作者图片

如前所述，我们数据集的这些特征或多或少是相关的，也就是说，如果我们在我们的特征矩阵中绘制两个向量，其中一些将呈现相似的趋势，一些可能走向相反的方向，一些可能几乎相同，然后，当然，我们可以找到中间的任何东西。**对两个向量之间关系的强度和方向的测量就是相关性**。

如果我们在散点图上绘制相关性很强的两个特征，图表上的数据点将会非常接近。最终值越接近 1 或 1，这些特性之间的关系就越密切:

*   1 强反比关系
*   +1 强直接关系

当相关性较弱时，数据点分散得更开。相关性越接近 0，关系越弱:

![](img/bdb7c42e76f870dd79ec2cb63e3a3c8d.png)

作者图片

两个变量之间的相关方程看起来很混乱，但实际上很简单:

![](img/36e8b385c41c0a29b62b9ed92809c9c1.png)

作者图片

其中:

*   和 Yi 分别是向量 X 和 Y 的元素，
*   x-条和 y-条是每个矢量的平均值

如果我们测量数据集中所有要素之间的相关性，我们最终会得到一个 nxn 矩阵，其中 n 是数据集中要素的总数，对角线表示每个要素与其自身的相关性。您可以使用 pandas 在 Python 中轻松找到这个矩阵:

```
sd.corr()
```

![](img/04fdbc4aef83c8653b73c9ed9dfd3e6a.png)

作者图片

我们可以很容易地看到一些功能实际上是相当相关的。例如，可能出乎意料的是， *like_exercise* 和 *like_tvsports* 显示出 0.489 的相关性……相当强！而其他一些如*喜欢阅读*和*喜欢徒步*相关性很弱。

以非常相似的方式，我们可以对两个变量之间的协方差感兴趣，而不是相关性。虽然相关性告诉我们关于两个特征如何彼此变化的方向和幅度的信息，但协方差只给我们两个量彼此变化的方向，即某个变量相对于另一个变量具有正协方差，它们一起增加或减少。在我们上面的例子中， *like_tvsports* 和 *like_sports* 之间的协方差是 3.91，而 *like_shopping* 和 *like_hikinig* 之间的协方差是-0.37。

酷，为了更好地理解 PCA 中的两个关键概念:特征值和特征向量，让我们暂时搁置这个概念。

让我们从基础开始，矩阵和向量当然不仅仅是解释数据集的另一种方式。在这个故事中，不可能介绍矩阵和向量的所有情况和用途，但是为了理解特征值和特征向量，其中有一个特别重要:变换。

长话短说，向量指出了一个特征或变量在某个空间的跨度(是的，在任何愤怒的数学家加入之前，我知道这不是完美的技术定义…只是想保持简单😄).例如，假设我正在买橘子和苹果，出于某种原因，我决定去超市两次。第一次，我买了 2 个橘子和 3 个苹果，而第二次我买了 10 个橘子和 1 个苹果。如果我们把苹果和橘子的价格加到分析中，这可以用几种方式来表示:

1.  作为单独的功能
2.  作为单独的向量
3.  作为一个矩阵

![](img/68e3cb66897706ecf6274f622fd46b15.png)

作者图片

如果我们知道这些苹果和橘子的价格分别是 3 和 2，我们现在就可以得到一个新的价格向量，我们可以用它来做一个矩阵乘法，并找到我们的总支出:

![](img/2396fe29ea99baa164ebf578d850b252.png)

作者图片

因此，我们的方程组，即我们的矩阵，是问我需要什么价格向量才能在位置[12，32]得到一个变换的乘积？换句话说，我们的矩阵只是将我们的原始价格向量[3，2]转换成我们的总支出向量[12，32]

![](img/1645b35b20a6b4a147ac1358b01a1221.png)

作者图片

当我们在机器学习中拟合任何类型的线性回归时，这也是后面发生的一部分；我们只是试图找到一个系数向量，当它与我们的特征矩阵相乘时，会给我们一个目标变量向量的最佳近似值。然而，在不深入了解这种复杂情况下会发生什么的情况下，矩阵可以对向量执行某些类型的变换，了解这些变换非常重要:

*   对角线上有任意数而其余部分都是零的矩阵称为拉伸矩阵。并且它执行**拉伸变换**。其中沿着对角线的正数将有效地拉伸空间中的每个向量，而负数将翻转轴，沿着对角线的任何位置的分数都将挤压一切。让我们来看一个例子，使用所谓的基向量，即跨越点[1，0]和[0，1]的向量:

![](img/57e9cd27877bebf862fb31418420d0aa.png)

作者图片

*   我们可以找到的另一种变换是**剪切**，其中沿着给定直线的所有点保持固定，而其他点被移动:

![](img/f9d12a554ca780817cdfb3d2ef0d6b6c.png)

作者图片

*   我们还可以进行**轮换**:

![](img/54130c125adbe5b3240065940a313000.png)

作者图片

*   然后有一个矩阵什么都不做。只有前面提到的基向量的矩阵:单位矩阵:

![](img/2802d715263f14a2ab0a56142cb9cce1.png)

作者图片

然后，我们可以组合所有这些变换，甚至是更复杂的多维情况。但是，这些基础知识应该足够让你坚持下去了。我们已经建立了我们的代数理解，现在我们准备最终讨论特征向量和特征值。然而，对于这一点，重要的是要理解，尽管我们一直说变换只应用于一个向量，但它们通常适用于空间中的每个向量。理解主成分分析的关键是，即使一些向量会完全改变它们的位置，一些其他的会落在它们开始的同一条线上。举以下例子:

![](img/912a76e39a9f1579d24d60bde07e03d8.png)

作者图片

正如你在上面的图像中看到的，水平向量保持相同的长度，指向相同的方向。垂直向量指向相同的方向，但是它的长度改变了。对角向量完全改变了它的角度和长度。**水平和垂直向量将成为该变换的特征向量**。此外，**假设水平向量完全没有变化，我们可以说它的特征值为 1，而垂直向量增加了它的长度，因此它可能具有例如 2** 的相关特征值。

你能在下面的剪切变换中找出特征向量吗？🤔

![](img/08dad5dd461d1de790325e6a0ae48800.png)

作者图片

只是水平向量没有变化。在这种情况下，我们只有一个特征向量。

在继续之前，让我们快速总结一下:

*   **特征向量**:变换前后位于同一跨度的向量
*   **特征值**:每个向量拉伸或压缩的量

嗯，这太好了！特征向量和特征值的概念现在应该很清楚了。至少通过观察，我们可以很容易地在图表中找到它们。当然，只要我们处理简单的情况，就像我们刚刚看到的。想象一下，现在我们不是在做 2D 操作，而是有一个多维空间😬🤔。缩放、剪切和我们提到的所有变换都将以类似的方式运行，但它们将更难或不可能被发现。此外，我们可以有一个转换的组合。就像剪切加上垂直旋转。

我们需要一种新的方法来确定我们的特征向量和值。让我们试着用方程的形式将我们的发现推广到所有类型的向量和矩阵:

![](img/12374d21d11e20179979b15c27830383.png)

作者图片

在上面的等式中，A 是一个 n 维矩阵，这意味着它是一个 nxn 矩阵，因此 X 必须是一个 n 维向量。还记得我们之前看到的一个例子吗:

![](img/196ec70bc9d16520c344efd7906c53df.png)

作者图片

我们现在可以重新排列这个等式。但是为此，我们必须使用我们之前提到的一个概念:单位矩阵。这个矩阵根本不执行任何转换:

![](img/92c1f8194057eeae2e10b3287ab037be.png)

作者图片

现在，我们对向量 X 为零的情况不感兴趣，因为它没有长度和方向。**所以我们将寻找括号中的部分为零**。

为了向前推进，我们必须引入一个新概念:**矩阵的行列式**。我们可以广泛地讨论这个概念，因为它是机器学习和数据科学中几个工具的一部分。然而，主要思想是，行列式是可以从方阵(即具有相同行数和列数的矩阵)的元素中计算出的数，并且对矩阵所描述的线性变换的某些属性进行编码。**具体来说，它向我们展示了线性变换如何改变面积或体积**。举以下例子:

![](img/c8284184aa84874b5396fc4f421ff4a7.png)

作者图片

你看到发生了什么吗？🤔**一切都变大了一倍，d** 。例如，一个 2 的行列式会告诉我们，一个矩阵运算会使我们的向量空间的面积或体积加倍。酷，现在我们已经准备好理解行列式在前面等式中的位置了:

![](img/7d8f9f4775d7e2bc50803bb025696f3e.png)

作者图片

还记得我们说过，我们会寻找这个等式括号内的部分为零。你注意到那里发生了什么吗？无非就是一个矩阵运算。由于我们将标量λ乘以对角线上充满 0 和 1 的单位矩阵，最终，我们只是从矩阵中减去另一个对角线上有λ项的矩阵。然后，我们可以用矩阵形式重写上面的等式，使用行列式来解决我们的问题:

![](img/b1776f0f3fcb1ff4a6bc3e888c8c2ea0.png)

作者图片

将这两个矩阵相减会得到另一个矩阵，因为我们知道当一个矩阵的行列式为零时，它等于零，所以我们知道**它的面积或体积也为零**。评估上面的矩阵运算，我们得到下面的等式:

![](img/11cae1485b6a0e7b781c74869a4050c5.png)

作者图片

这个方程被称为特征多项式。然而，不要担心，你现在只需要知道**我们的特征值就是这个方程的解。然后我们可以把这些特征值代入我们的原始方程，找到特征向量**。让我们来看一个具体的例子:

![](img/f14b0299892fdb79c90e42d3507198aa.png)

作者图片

我们可以知道原始方程中的塞λ = 1 和λ = 2，并找到我们的特征向量:

![](img/1289a99cae3d4e97ef58f10e1937d126.png)

作者图片

这一切告诉我们什么？在λ = 1 的情况下，根据我们最终的表达式，我们需要 X2 为零。但是我们对 X1 一无所知。这是因为任何沿着水平轴指向的向量都可以是该系统的特征向量，即任何 X2 等于零并且 X1 为任何其他数的向量都将是特征向量。在λ = 2 时，结果也非常相似，但反过来:我们可以取 X2 的任何值，同时保持 X1 等于零。请参见以下示例:

![](img/fb66415c2c7c7b0fa052ba8ab6c0a8a2.png)

作者图片

哇，这真是一段不平凡的旅程！从主要概念开始，一直到实际找到变换的特征值和特征向量。然而，我们还有几件事情要处理。你还记得在开始的时候，我们谈到相关性和协方差吗？通过使用以下命令，我们可以轻松地从一见钟情数据集获得协方差矩阵:

```
sd.cov()
```

在下面的例子中，我首先删除了 *subject_id* 和 *wave* 列:

```
sd.drop(labels=[‘wave’,’subject_id’], axis=1).cov()
```

![](img/abdd60765e2e2c9069611beaa371ac83.png)

作者图片

作为参考，**在 PCA 中，当变量尺度相似时，我们使用协方差矩阵，当变量在不同尺度时，我们使用相关矩阵**。然而，我们将看到的 Sklearn 算法默认使用协方差矩阵，因此如果您的要素具有不同的比例，您必须在继续之前应用一些标准化。例如，在数据中包含体重和身高。不幸的是，我无法在这个故事中涵盖标准化，但是如果您有兴趣了解更多信息，我将留给您[来自](/data-transformation-standardisation-vs-normalisation-a47b2f38cec2) [Clar Liu](https://towardsdatascience.com/@clareyan) 的另一个故事[关于数据科学](https://towardsdatascience.com/)。

现在，酷的事情，因为我们的协方差矩阵是一个方阵，它可以用来做我们的“本征魔术”，找到本征向量和本征值。以只有两个变量/特征的场景为例:

![](img/7f24966aca8a2d6f770577973c0d9d6f.png)

作者图片

很好，我们已经拥有了理解主成分分析下发生的一切。然而，在我们找到我们的特征向量和特征值之后，整个 PCA 过程不会结束。最后一步是用我们找到的所有或部分特征向量创建一个矩阵，然后做一些称为投影的事情，将我们的原始数据集转换到我们刚刚找到的新向量空间。换句话说，**我们将使用特征向量将样本转换成一个更小的特征集，尽可能多地表达原始数据的方差**。其中我们找到的最大特征值将对应于最大的解释方差，第二大到第二大方差，依此类推。最终，我们将拥有和我们最终选择的特征值和特征向量一样多的新特征。如果前两个特征值似乎解释了我们数据集中的大部分方差，那么我们可能不需要选择比它们更多的。

对我们来说幸运的是，在 Sklearn 中实现这一切非常简单，我们实际上不需要在这个故事中涉及投影。然而，如果你有兴趣了解更多，我推荐你去看看汗学院的这组视频。

让我们通过快速查看如何使用 Sklearn 的 PCA 模块来结束这个超级长的故事吧！第一，进口:

```
from sklearn.decomposition import PCAfrom sklearn.preprocessing import StandardScaler
```

在我的例子中，我的所有要素都在相同的比例上，所以我不需要转换我的数据。但是，如果情况不是这样，您可以通过简单地运行以下命令来实现:

```
scaler = StandardScaler()transformed_data = scaler.fit_transform(data)data_transformed = pd.DataFrame(transformed, columns=data.columns)
```

酷，现在我们只需要两行代码来进行主成分分析:

```
sd_pca = PCA(n_components=5)sd_pca.fit(sd)
```

正如你所看到的，尽管我们可以找到和我们拥有的特性一样多的组件，Sklearn 允许我们指定想要保留的组件的数量，以加快计算速度。

我们现在可以检查组件，并且*explained _ variance _*ratio 属性将告诉我们原始数据中有多少差异被封装在新的组件变量中。

```
sd_exp_var_eigenvals = sd_pca.explained_variance_sd_exp_var_pct = subjective_pcasd.explained_variance_ratio_print(sd_exp_var_eigenvals)print(sd_exp_var_pct)[2.16041482 0.88925024 0.73820887 0.72229813 0.49907009][0.43128576 0.17752191 0.14736937 0.14419309 0.09962986]
```

最后，PCA 中的*变换*函数将创建新的分量变量矩阵:

```
components_matrix = sd_pca.transform(sd)
```

我们最终将只有 5 个向量，减少了数据的维数，同时最大限度地减少了损失，并占原始数据集内方差的 75.6%(0.431+0.178+0.147 = 75.6% 0.431+0.178+0.147 = 75.6%)。

嗯，我想这已经足够了😅。一如既往，我渴望阅读您的评论和反馈。

别忘了看看我的其他一些故事:

*   [检疫中的 4 门免费数学课程，提升您的 DS 技能](/4-free-maths-courses-to-do-in-quarantine-and-level-up-your-data-science-skills-f815daca56f7?source=friends_link&sk=e21d4439fe6e60160c25668377f66936)
*   [我们数据人为什么以及如何帮助对抗新冠肺炎](/why-and-how-should-we-data-people-help-fight-against-covid-19-eng-esp-a45ee5e3688a?source=friends_link&sk=d2c58fe25d52ae855400065944a4aea8)
*   [5 用于更好绘图的更多工具和技术](/5-more-tools-and-techniques-for-better-plotting-ee5ecaa358b?source=friends_link&sk=afd579f429a4890be0def79da8e28b57)

或者访问[我在 Medium](https://medium.com/@gonzaloferreirovolpi) 上的个人资料，查看我的其他故事🙂。如果你想直接在你的邮箱里收到我的最新文章，只需 [**订阅我的简讯**](https://gmail.us3.list-manage.com/subscribe?u=8190cded0d5e26657d9bc54d7&id=3e942158a2) **:)**

再见，感谢您的阅读！