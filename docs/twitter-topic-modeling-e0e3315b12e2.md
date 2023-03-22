# Twitter 主题建模

> 原文：<https://towardsdatascience.com/twitter-topic-modeling-e0e3315b12e2?source=collection_archive---------10----------------------->

![](img/a0601d9173e99e5676f0f2450404d894.png)

[晨酿不溅通道](https://unsplash.com/photos/V6CdmV277nY)

## 使用机器学习( [Gensim 线性判别分析](https://radimrehurek.com/gensim/models/ldamodel.html) — LDA)来探索你的追随者最关注的话题是什么。

![](img/7444fbe78b44774f6e32c6bb1023b96f.png)

经过 24 轮超参数调整后，从 LDA 基本模型到模型 6.3

我是一个机器学习极客，我想把机器学习应用到我能做的一切事情上，只是为了看看结果。另一方面，我在 [SoMe(社交媒体管理平台)](https://www.so-me.net/)开始了一个新的角色，在数据科学团队中，我们不断围绕使用机器学习来为我们的用户创造更多价值，并帮助他们扩大粉丝群。我们想了很久，想出了最好的主意，在这个过程中，我们意识到第一步是让用户对他们的粉丝群有一个整体的了解。

有许多数据科学和机器学习技术可以用来更好地了解你的粉丝，从在 Instagram 上应用 CNN(卷积神经网络)到在 Twitter、Linkedin 或任何其他基于文本的数据上应用自然语言处理技术。我们的大多数用户使用 [SoMe](https://www.so-me.net/) 来排序和安排他们未来在 Twitter 上的帖子，所以作为第一步，我们决定向我们的用户提供关于他们的 Twitter 追随者最关注的话题的见解。要做到这一点，我们首先必须定义和记录追随者的参与度。经过长时间的讨论，我们将关注者参与度定义和评分为“当一个关注者与用户发布的内容互动 1。转发(5/5) — 2。转发评论(4/5) — 3。喜欢(3/5) —4。评论(2/5) — 5。提及(1/5)”。

下一步实际上是从 Twitter api 获取数据，我将在未来的帖子中写申请 Twitter api 并使用 [Tweepy](https://www.tweepy.org/) 和其他工具来提取数据和提炼数据，以获得您需要的 api 数据。您可以对任何类型的文本数据使用以下技术，并找出数据集中讨论的最重要的主题。

# 加载所需的包

根据您选择的 python notebook，您将需要安装和加载以下包来执行主题建模。在一些数据科学团队中，我们使用各种笔记本电脑选项，从 Azure 到 Jupyter labs 和 notebook。然而，我个人最喜欢的是 Google Colab。我建议在 Google Colab 或 Jupyter notebook 上运行以下所有代码片段。我还将链接到这个项目的 Github 库，以及一个链接到我们用于参考的最终笔记本。

# 数据清理

在从 Twitter api 中提取和提炼数据并导入所需的包之后，我们必须从表情符号和 URL 中清理数据，以便我们可以在接下来的步骤中对其进行标记。您可以在下面的代码片段中找到我们使用的清理语法:

正如您在下表中看到的，在进行令牌化之前，您需要删除大量表情符号和 URL。数据清理对于最终提供准确的结果至关重要，我们不希望来自网站或表情符号的单词出现在我们的主题建模结果中，因为它们在弄清楚一袋单词的一般主题方面几乎没有价值。

![](img/62117c3bce126c39572fe01de417a03a.png)

# 数据预处理

我们在数据预处理阶段的目标是将句子转换为单词，将单词转换为其词根，并删除过于常见或与主题建模项目的目的无关的单词。我们使用了以下技术来实现我们的目标，我将分享代码并带您经历每个阶段:

*   **分词**:将文本拆分成句子，再将句子拆分成单词。将单词小写，去掉标点符号。
*   少于 3 个字符的单词将被删除。
*   所有的**停用词**都被移除。
*   单词被词条化和词干化——第三人称的单词被改成第一人称，过去时态和将来时态的动词被改成现在时态，并被还原成它们的词根形式。

## 符号化

标记化永远是我们做任何文本数据处理之前的第一步。这意味着 spaCy 将通过对每种语言应用特定的规则来将句子分割成单词、标点符号、符号等。Spacy 是一个预先训练的自然语言处理模型，能够计算出单词之间的关系。你可以在这里了解更多关于 Spacy [的信息。](/so-whats-spacy-ad65aa1949e0)

![](img/2c460e319396592637bb6fa4a6d03fa1.png)

# 词汇化

词汇化是我们将单词转换成其词根的过程。比如:'学习'变成了'学习'，'见面'变成了'见面'，'更好'，'最好'变成了'好'。这样做的好处是，我们可以减少字典中唯一单词的总数。因此，文档-单词矩阵中的列数将随着列数的减少而增加。引理化的最终目的是帮助 LDA 模型最终产生更好的主题。

![](img/bad030738e73c398b0d6bd57fcc39d5a.png)

# 主题建模

## 基础模型

我们首先生成一个基础模型，用于在我们经历超参数调整阶段时跟踪我们的进展。LDA 主题模型算法需要文档单词矩阵和字典作为主要输入。对于运行 LDA 模型之前要采取的前几个步骤，我们创建了一个字典，过滤了极端情况，并创建了一个语料库对象，它是 LDA 模型需要作为主要输入的文档矩阵。

我们准备了训练 LDA 模型所需的一切。除了语料库和词典，我们还需要提供主题的数量。我们选择 5 作为基本模型。在超参数调整阶段，我们将达到要使用的主题的最佳数量。

通过打印出 LDA 模型产生的主题，我们可以粗略地猜测与每袋单词相关的主题。值得一提的是，这个单词包是按照与每个主题最相关到最不相关的顺序排列的。

![](img/f13b35f067a7b1ffc1ed344962839e2f.png)

模型困惑和[主题连贯性](https://rare-technologies.com/what-is-topic-coherence/)提供了一个方便的衡量标准来判断一个给定的主题模型有多好。以我的经验来看，话题连贯性评分尤其有用。

我们的一致性得分为 0.17，这对于几乎所有 LDA 模型来说都是非常低的分数，但请记住这只是基础模型，我们将对其进行大幅改进。

![](img/c226c876abf76939b7dbcd7db9fcbe8e.png)

既然构建了 LDA 模型，下一步就是检查生成的主题和相关的关键字。没有比 pyLDAvis package 的交互式图表更好的工具了，它的设计可以很好地与 Google Colab 和 Jupyter 笔记本配合使用。

![](img/cdc538970c681cfc65810e5e28c435c9.png)

那么如何推断 pyLDAvis 的输出呢？

左侧图中的每个气泡代表一个主题。泡沫越大，这个话题就越流行。一个好的主题模型会有相当大的、不重叠的气泡分散在整个图表中，而不是聚集在一个象限中。一个有太多主题的模型，通常会有许多重叠，小气泡聚集在图表的一个区域。

好的，如果我们将光标移到其中一个气泡上，右边的单词和条将会更新。这些词是构成所选主题的突出关键词。我们已经成功地构建了一个好看的主题模型。接下来，我们将通过使用 [Scikit-learn 的](https://scikit-learn.org/stable/index.html)网格搜索来改进该模型(超参数调整),然后我们将关注如何在 LDA 模型中获得主题和其他变量的最佳数量。

# 超参数调谐

## 网格搜索

LDA 模型最重要的调整参数是 n_components(主题数)。此外，我们还将搜索 learning_decay(控制学习速率)。除此之外，其他可能的搜索参数可以是 learning_offset(降低早期迭代的权重)。应该> 1)和 max_iter。如果你有足够的时间和计算资源，这些都是值得尝试的。

注意，网格搜索为 param_grid 字典中参数值的所有可能组合构建多个 LDA 模型。所以，这个过程会消耗大量的时间和资源。

![](img/62cd418c6ad17516cae79571fd3a5da0.png)

我们知道主题的数量很有可能远远超过 10，但是通过网格搜索，我们发现 10 个主题比其他数量的主题表现得更好。这让我们对结果进行了深入思考，我们发现 Scikit-learn 的网格搜索跟踪的是困惑而不是一致性值，对于我们的用例，一致性值提供了最好的结果。下一步，我们将获得最佳数量的主题。

## 最佳主题数量

我们寻找最佳主题数量的方法是建立许多具有不同主题数量值的 LDA 模型，并选择一个给出最高一致性值的模型。

选择一些标志着话题连贯性快速增长结束的话题通常会提供有意义和可解释的话题。选择更高的值有时可以提供更细粒度的子主题。如果你看到相同的关键词在多个主题中重复出现，这可能是“主题数量”太大的信号。通过遵循这些原则，我们选择了 68 个主题作为我们用例的最佳主题数量。

## 最佳通过次数

Passes、chunksize 和 update_every 是具有 EM/variable 关系的参数。我们不打算在这里深入 EM/variable Bayes 的细节，但如果你好奇，可以看看这个[谷歌论坛帖子](https://groups.google.com/forum/#!topic/gensim/z0wG3cojywM)和它引用的论文[这里](https://www.google.com/url?q=https%3A%2F%2Fwww.cs.princeton.edu%2F~blei%2Fpapers%2FHoffmanBleiBach2010b.pdf&sa=D&sntz=1&usg=AFQjCNEqb96J5aHxeTva_s_ieCKGzOBbDA)。对于我们的用例，考虑到 chuncksize 不是实质性的，update_every 在最终结果中不会有太大变化，超参数调整次数就足够了。

我们尝试了许多遍，20 遍似乎能产生最好的结果。虽然不是很大，只有几个小数点。

## 阿尔法类型

α是狄利克雷先验的超参数。狄利克雷先验是我们从中得出θ的分布。θ成为决定主题分布形状的参数。所以本质上，alpha 影响了我们绘制主题分布的方式。这就是为什么我们要尝试超参数调整，以选择最佳的阿尔法类型，给你一个更好的主题分布。

![](img/cd58aa56d10a1f32c02f745bfa96344a.png)

在我们的用例中，对称 alpha 提供了一个更好的结果，不是很好，但是我们将为我们的 LDA 模型使用对称 alpha。

## 衰退

学习衰减控制模型的学习速率。由于您只能选择 0.5、0.7 和 0.9，我们将尝试所有三个选项，看看哪个选项能提供最佳的一致性值。

在我们的使用案例中，0.5 衰减提供了最佳的相干值。事实上，在我们的用例中，衰减和一致性值似乎是负相关的。

## 最佳迭代次数

迭代在某种程度上是技术性的，但本质上它控制了我们对每个文档重复特定循环的频率。将“迭代”次数设置得足够高是很重要的。

在我们的用例中，我们尝试了 50 到 100 次迭代，但是因为我们想防止模型过度拟合，所以我们选择了 70 次，这表明一致性分数有了相当大的提高。

## 最小概率

该超参数忽略分配概率低于分配概率的主题。不能低于 0.01，也不能高于 0.1。

我们尝试了 0.01 到 0.1 的整个范围，coherence 值在整个范围内保持不变，因此我们将其保留为默认值 0.01，以获得尽可能多的主题。

## 进度跟踪表

从一开始就跟踪你的进步总是一个好习惯。我们已经通过 24 次模型超参数调整迭代跟踪了我们的进展，我们的最佳模型提供了 0.47 的一致性值，考虑到用户追随者群体中可以讨论的广泛主题，这是一个非常好的数字。

# 最终模型和结果

我们终于完成了我们的最终模型。我们目前使用下面片段中的模型在 [SoMe](https://www.so-me.net/) 向我们的用户提供他们的追随者互动最多的话题。

如果我们仔细看看最终模型产生的主题，我们可以以很高的准确度猜测每个主题是什么。现在我们必须记住，它们是按重要性从高到低排序的。例如，如果我们看第一个主题，我们认为它是关于新冠肺炎危机的，因为前三个词是“防病毒封锁”，而不是关于“黄金”，因为“黄金”是单词包中第四个没有反映高概率的单词。

![](img/fde104841139ecbff2c14bdf45e7f789.png)

正如我们之前所介绍的，一个好的主题模型将为每个主题提供非重叠的、相当大的 blob，如果我们根据用例增加主题的数量，我们将拥有更小的 blob，并且在某些情况下会有一些重叠，但总的来说，我们可以在最终的模型中看到，分布和重叠有了显著的改善。这里好像是这样的。所以，我们没事了。

![](img/3eccad19a1db437e5bdfc24a9975d138.png)

# 结论

在这篇文章中，我们讨论了一些前沿的主题建模方法。我们不断努力为用户构建新功能，并利用机器学习的力量为用户提供更好的体验。为了改进这个模型，你可以通过使用 [gensim LDA Mallet](https://radimrehurek.com/gensim/models/wrappers/ldamallet.html) 来探索修改它，这在某些情况下会提供更准确的结果。对于那些在构建主题模型时关心时间、内存消耗和主题多样性的人，请查看 LDA 上的 [gensim 教程。](https://www.machinelearningplus.com/nlp/topic-modeling-gensim-python/)

最后，我必须感谢数据科学团队的其他成员，尤其是雅各布·帕吉特和劳伦斯·金姆西。在某些情况下，我们坚信开源软件，您可以在这里找到我们所有的分析模型笔记本。