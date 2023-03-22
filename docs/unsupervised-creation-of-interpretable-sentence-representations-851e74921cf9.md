# 可解释句子表示的无监督创建

> 原文：<https://towardsdatascience.com/unsupervised-creation-of-interpretable-sentence-representations-851e74921cf9?source=collection_archive---------29----------------------->

## 对于句子相似性/文档搜索应用

![](img/41562dd9ec6f84ca7a0d9ee73ff39237.png)

**图一。**用于句子相似性任务的句子表示签名的无监督创建。插图使用 BERT(BERT-大型案例)模型。

# TL；速度三角形定位法(dead reckoning)

迄今为止，模型学习句子的固定大小表示，通常有某种形式的监督，然后用于句子相似性或其他下游任务。这方面的例子有[谷歌的通用句子编码器(2018)](https://arxiv.org/pdf/1803.11175.pdf) 和[句子变形金刚(2019)](https://arxiv.org/pdf/1908.10084.pdf) 。固定大小表示的监督学习往往优于句子表示的非监督创建，只有少数例外，如最近发表的作品 [(SBERT-WK，2020 年 6 月)](https://arxiv.org/pdf/2002.06652.pdf)，其中固定句子表示是通过从 BERT 模型的不同层提取的词向量的信息内容驱动的加权平均来创建的*(然而，已经有类似的跨层* *的词向量池的先前方法，这些方法在任务中表现不太好)。*

对于句子相似性的特定任务，下面描述的替代简单方法将句子表示为单词表示的无序集合，并且按原样使用该集合，而不将其转换为固定大小的向量。单词表示由 BERT 在没有任何标记数据的情况下在预训练/微调期间学习。这种简单的句子集合表示，看起来似乎像一个单词袋表示，对于短句，其表现几乎与上面提到的模型一样好，甚至在质量上比它们更好*(需要通过全面测试进行量化)*。这可能部分是因为，组成句子的单词*(这里的“单词”用于 BERT 词汇表中的完整单词和子单词标记)*，所有这些单词都是从 BERT 的 30，000 个单词的固定大小的词汇表中提取的，并且它们的学习向量是上下文不敏感的*(例如，单词“cell”的所有含义都被压缩成一个向量)*， 仍然可以用于表示单词的上下文敏感方面，方法是将这些单词映射到 BERT 词汇表中的其他单词，这些单词捕获它们在句子中的含义，这种映射是由具有掩蔽语言模型(MLM)头的 BERT 模型完成的。

这种方法的优点是

*   与上面提到的两个监督模型不同，我们避免了对标记数据的需要。
*   句子相似性任务的表示质量不会随着句子长度而退化——这是我们在通用句子编码器、句子转换器*(下图显示了定性比较)*和无监督模型- [SBERT-WK](https://arxiv.org/pdf/2002.06652.pdf) 中观察到的限制
*   将句子表示为单词能够解释句子相似性任务的结果——学习固定表示的有用的属性模型通常是缺乏的。例如，在上面提到的所有模型中，与输入句子*(在我们可以收获相似句子的分布尾部内)*相似的句子的排序列表通常包含至少几个句子，其中与输入句子的语义关系根本不明显，即使存在一个。

这种方法的简单性不仅使我们能够在没有标记数据的情况下执行相似性任务，而且还可以作为基准性能来测试输出固定大小句子表示的未来模型，并且可能优于这种简单方法。

# 参考实施细节

正如在[的一篇早期文章](/examining-berts-raw-embeddings-fd905cb22df7)中所研究的，BERT 的原始嵌入捕获了关于任何单词的独特和可分离的信息，无论是独立的还是在句子*(使用 BERT MLM 头)*的上下文中，就其固定大小词汇表中的单词和子单词而言。这用于为句子相似性任务创建由这些单词的子集组成的句子签名。

![](img/a1597e358933f6cbaa204ab8e55b6e03.png)

**图二。** [BERT 的原始单词嵌入捕捉有用的和可分离的信息](/examining-berts-raw-embeddings-fd905cb22df7)(不同的直方图尾部)，关于 BERT 词汇表中其他单词的单词。该信息可以从原始嵌入和它们的变换版本中获得，在它们通过具有屏蔽语言模型(MLM)头的 BERT 之后。图中显示了在通过带有屏蔽语言模型头的 bert 模型之前和之后，BERT 的原始嵌入(28，996 个术语—基于 BERT 的大小写)中术语单元的前 k 个邻居。(1)输入句子。(2)输入句子的标记化版本——柯南不存在于伯特的原始词汇中。它被分成两个术语“Con”和“##nan ”,这两个术语都出现在 BERT 的词汇表中。(3)伯特的 MLM 输出在伯特的词汇中找到最接近变换向量的预测。对于单词“cell ”,前 k 个邻居(显示在右边——该图显示匹配——不是精确的排序)只包含捕获监禁的语义概念的术语。相比之下，单词“cell”在输入到 BERT 之前的前 k 个邻居(显示在左侧)捕获了该单词在其前 k 个邻居中的所有不同意义——“监禁”意义以及“生物”(蛋白质、组织)和移动电话意义(电话、移动电话)。输入之前和之后的前 k 个邻居落在距离/预测分数与计数的直方图的尾部，使得这些邻居与词汇表中的其余单词不同且可分离

例如，考虑下面更长的句子，*“康南带着手机去牢房从囚犯身上提取血细胞样本”*。这个句子的标记化版本将这个句子映射到 BERT 的大约 30，000 个标记的词汇表 *(bert-large-cased)* 。除了两个输入词“Connan”和“手机”，其余都是一对一的映射。这里的关键点是输入的标记化版本可以用来在 BERT 的词汇中找到相应的学习向量。

![](img/c1fada6811dee8c4476acdad305c82ad.png)

**图三。**细胞的不同义项在一定程度上被同一个词“细胞”在不同句子位置所映射的不同词所分隔。然而，手机和血细胞上下文之间仍然有一些重叠——“汽车”清楚地区分了手机上下文。然而，考虑到“细胞”、“细胞”和“蜂窝”这三个词，生物语境仍然与手机语境有重叠。这些意义可以通过取更多的前 k 项来分离。例如，生物上下文的第五个术语通过单词组织(上面未示出)来区分它。因此，这是我们希望从分布尾部挑选多少前 k 项与增加签名矩阵大小的性能影响之间的权衡。

当通过伯特的模型(MLM 头)时，这些标记向量被转换成表示这些单词的上下文敏感含义的向量。这可以通过检查上面句子中使用的“细胞”一词得到最好的说明。单词“cell”的前 3 个邻居*(这个选择是任意的——我们可以挑选前 k 个邻居，只要它们来自分布尾部)*一旦它们通过模型，就映射到 BERT 词汇表中的不同单词。代表监狱的“细胞”有一个 ***房间*** 的意思，而在手机上下文中使用的“细胞”则表达了一辆 ***汽车*** 的意思。“细胞”一词在生物学上下文中的含义具有生物细胞*的概念(未示出的第五个邻居是* ***组织*** *)。*本质上，即使单词“cell”的含义随着上下文而变化，我们仍然可以在 BERT 的学习词汇中找到捕捉其上下文敏感意义的相应向量。鉴于此，我们可以使用标记化文本的向量以及每个标记在通过 BERT 模型(MLM 头)后的前 k 个邻居作为该句子的签名。

选择前 k 个邻居时，会忽略显示为预测的单字符标记，如标点符号。只要尾部有足够的标记可供选择，我们就可以安全地做到这一点，实际情况就是这样。

本质上，给定一个长度为 N 的句子，假设标记化版本的长度为 M，该句子的签名将是 M*(1 + k)，其中 k 是在将该句子传递给 BERT 后我们挑选的顶部邻居的数量。句子的签名将是一个具有 M*(1+k)行和 D 列的矩阵，其中 D 是维度*(对于 bert-large-cased 为 1024)*。

## 计算句子相似度得分的步骤

一旦如上所述计算了一个句子的签名，我们就可以计算两个句子之间的相似性得分，如下面的原型/参考实现所示

![](img/62479bba5f6d104d34e5484b3734c016.png)

**图 4。**两个句子 A 和 B 之间的相似度计算

当计算输入句子与已知句子集合*(例如文档标题)*的相似性时，上面计算的成对分数用于计算输入句子与已知集合中所有句子的接近度的相对分数。

上述得分计算中的加权函数是基于参考语料库中术语的出现频率。本质上，从两个句子签名中创建的词对之间的余弦相似性的贡献由该分数对相似性计算的重要性来加权，该相似性计算是这些术语在参考语料库中出现的函数。这确保了句子中出现的像“the”、“of”这样的粘合词比真正抓住意思的词贡献少。句子对的相对长度也在分数计算中考虑，以确保短句选择相似的长句，而不是相反。当使用这种方法进行文档搜索，将文档中的句子转换为句子签名时，这尤其有用。

# 句子相似性任务中模型绩效的定性比较

使用表征短句*(平均句子长度 8 个单词)*和长句*(平均句子长度 51 个单词)*的两组句子来定性地比较三个模型*(通用句子编码器-使用、句子转换器和 SBERT-WK)* 与上述相似性计算方法。

短句集主要由 USE 和句子转换器在其出版物中展示的测试句子组成。

长句集是从快速文本数据中提取的，人类已经将句子分为 14 类。这些类别不是严格的类别，在某些情况下，一个句子可能属于多个类别。此外，一些测试句子是多个句子——几乎代表一个小段落。

属于单个簇/类别的三个句子被用来表示一个组，总共 42 个句子属于 14 个簇*(具有前面提到的关于较长句子集合具有属于多个簇的一些句子的警告)*。来自这两个测试的几个集群如下所示。

![](img/864cfdcdc0cce98817fc936e539bbc27.png)

**图 5。**由使用和句子转换器出版物中展示的测试句子组成的例句组。在标记化之前，平均句子长度约为 8 个单词

![](img/eeb5d6a1be76524191ff997e608e3b40.png)

**图 6。**来自 Fasttext 测试数据的例句组。在标记化之前，平均句子长度约为 51 个单词

总的来说，

*   所有四个模型在小句测试中都表现良好。我们可以看到所有型号的 3x3 单元沿对角线的浅色阴影。
*   在更大的测试中，使用和句子变形器的性能都有明显的下降。沿着对角线大约有 3 个浅色的 3×3 网格，而不是预期的 14 个网格。SBERT-WK 似乎沿对角线有更多的 3×3 网格，尽管它们与热图中的其余单元没有明显区别。此外，对于 SBERT-WK，热图的整体亮度从短句到长句增加，表明句子之间的相似性度量的分布尾部对于长句情况不明显。相比之下，使用和句子变形器保留了短句和长句尾部的区别，但尾部的 3x3 网格较少。

![](img/a0db11efbc9c2391bf51af07f1a5476e.png)

**图 7。** USE 以高精度捕捉句子相似性，并从左侧热图中沿对角线的 3x3 网格中回忆短句。在更长的句子对测试中，回忆明显下降——我们几乎看不到对角线上预期的 14 个网格中的 4 个。无论是短测试还是长测试，结果的分离都是一样的——热图颜色阴影范围不受句子长度的影响。

![](img/ccdb66be03163e82df0e25b5108b2352.png)

**图 8** 。Sentence transformer，像 USE 一样，可以高精度地捕捉句子相似性，并从左侧热图对角线上的 3x3 网格中回忆短句。在更长的句子对测试中，回忆明显下降——我们几乎看不到对角线上预期的 14 个网格中的 3 个。无论是短测试还是长测试，结果的分离都是一样的——热图颜色阴影范围不受句子长度的影响。

![](img/55d233bc5f8e4bbc2e1d7fe7086f3770.png)

**图九**。SBERT-WK，像 USE 和句子转换器一样执行，适用于短文本和句子。一个明显的区别是较长句子的结果分离度下降——热图颜色阴影范围随句子长度而变化，较长句子测试中的 3×3 网格变得难以分离。

![](img/c968131f44472d1a725c71cde910f68b.png)

**图 10** 。对于短句，句子签名方法的表现几乎不如其他模型。然而，对于更长的句子测试，它比其他人捕获了更多的聚类——14 个中的 9 个(其中 3 个是半正方形，因为分数计算的不对称性质)。此外，它似乎从暗示属于多个聚类的句子的对角线中捕获语义上接近的邻居。这一点在下面的长句子情况的附加注释部分进行了检查。

句子签名方法与其他三种模型相比有几个独特的方面

*   热图是不对称的，不像其他的。这只是前面描述的不对称分数计算的结果。
*   在远离对角线的地方有很多亮点，特别是在长句测试中——这在所有其他模型中都明显不存在。这部分是因为这些聚类有可能属于多个聚类的句子。还存在一定程度的错误匹配，部分原因是图 3 中捕捉上下文意义的术语的语义扩散。大的 **k** 会增加扩散*(除了影响矩阵大小增加的性能之外)*，而小的 **k** 可能不足以消除歧义——k 的选择是一种权衡。然而，与其他模型不同，我们可以根据对分数有贡献的主要描述符来检查这些浅色斑块*(在附加注释部分完成)*的原因。这是这种方法相对于结果很不透明的其他模型的一个明显优势。

在句子相似性任务的基准测试集上，模型的定量比较仍有待完成。

# 限制

一些限制是

*   对于短句，这种方法的表现不如其他模型。只有当句子长度增加时，它的表现才优于*(在定性测试中)*。
*   这种方法不适用于除句子相似性之外的任务，尽管个体标记的上下文敏感签名可以用于标记任务，如[无监督 NER](/unsupervised-ner-using-bert-2d7af5f90b8a) 。
*   这种方法就像任何其他模型一样容易出现假阳性，尽管它们可以根据上面提到的解释性描述符被剔除。

# 最后的想法

像 BERT 这样的基于转换器的模型的未开发的潜力之一是表示其词汇的学习向量的固定集合。虽然这些向量在本质上与 word2vec 等模型学习的单词向量没有什么不同，但这些模型有两个明显的优势

*   **固定大小而不是可变大小的词汇**。词汇表的大小是固定的，留给我们选择*(我们只需要用我们选择的词汇表预先训练模型)*使它能够作为一个固定的参考库——这是 word2vec 之类的模型所缺乏的。
*   **捕捉句子语境。**使用 MLM 中心模型将上下文相关向量映射回 BERT 词汇表中的向量，使我们能够根据单词出现的句子上下文来捕捉单词的上下文相关含义。

这两个事实使得即使是使用上下文敏感词来间接捕获序列信息的签名词包也能够在短句上表现得几乎一样好，甚至在长句上比其他模型更好。

*原型参考实现* [*可在 Github*](https://github.com/ajitrajasekharan/unsupervised_sentence_representations.git) *上获得。*

# 参考/相关工作

用于对当前方法进行定性基准测试的三个模型。这三者在 Github 上都有参考实现

*   [通用语句编码器，2018](https://arxiv.org/pdf/1803.11175.pdf)
*   [句子变压器，2019](https://arxiv.org/pdf/1908.10084.pdf)
*   [SBERT-WK，2020 年](https://arxiv.org/pdf/2002.06652.pdf)

[使用 word2vec 等模型评估句子嵌入的基线模型](https://openreview.net/pdf?id=SyK00v5xx) (2016)。这个简单模型在句子相似性任务中胜过序列模型 *(RNNS/LSTMs)* 。

# 附加注释

在长句测试中，导致浅色阴影单元格远离对角线的句子对(每句话约 51 个单词)将在下面进行检查。下图是图 10 的放大版，右侧热图。白色单元格是得分为 1 的句子对*(该得分是一个相对度量得分，与余弦距离度量不同，余弦距离度量通常只对完全相同的两个句子得分为 1)*

![](img/5fdd70d630d5295a6a77611e787398fb.png)

图 11。图 10 中的长句测试(约 51 个单词)的放大热图。距离对角线有 13 个高相似性得分。

远离对角线的白色方块对应的句子对如下所示。

![](img/0923394ed5c58445f2414a3676e90bd6.png)

图 12。十三对中的三对似乎是错误的相似性度量，这从句子对(由“|”符号分隔)中可以明显看出

来自句子签名的最高贡献对下面检查三个错误句子对。这些提供了为什么这些句子匹配的洞察力，并可以作为过滤句子对的手段。

句子签名中的第一个句子对及其最佳匹配描述符

![](img/fcfbae1b9c63d660cc74b66cc433163b.png)

句子签名中的第二个句子对及其最佳匹配描述符。这些句子接近的原因从描述符对中显而易见——蝴蝶和飞机常见的*翅膀*的概念通过几个微弱的成对交互作用叠加成一个信号发挥了主导作用。

![](img/e5225017d3a73740edb10bea3d2d354b.png)

在最后一个句子对中，除了一个事实，除了一个事实，即这些句子对没有太大的意义之外，这些句子对的解释力不如前一个句子。

![](img/380c74e12069806282d5aed403eaa104.png)

*本文由 Quora*[*【https://qr.ae/pNKmJ7】*手动导入](https://qr.ae/pNKmJ7)