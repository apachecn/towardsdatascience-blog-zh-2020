# 句子向量表征中作文评价综述

> 原文：<https://towardsdatascience.com/a-summary-of-assessing-composition-in-sentence-vector-representations-4dce904220cd?source=collection_archive---------56----------------------->

## 自然语言处理领域著名研究论文综述

![](img/838b9f8b20ed56886e97e3c2daa422f3.png)

照片由来自 [Unsplash](https://unsplash.com/photos/Oaqk7qqNh_c) 的 [Patrick](https://unsplash.com/@impatrickt) 拍摄

来源:[https://www.aclweb.org/anthology/C18-1152.pdf](https://www.aclweb.org/anthology/C18-1152.pdf)(艾丁格等人，2018)

**背景:**为了理解什么是句子嵌入，有必要理解单词嵌入。单词嵌入已经变得非常著名，因为它们能够以可以普遍使用的向量的形式来表示单词。著名的嵌入有 word2vec、Glove 等。
单词嵌入的相同概念可以扩展到句子，使得每个句子用向量表示。诸如“发现两个堆栈溢出问题是否重复”之类的任务需要使用句子嵌入。

**引言:**为了理解语言，理解句子的意思和组成是必不可少的。今天的大部分神经网络模型本质上都是黑盒。因此，很难理解句子嵌入作为最终产生它们的训练的一部分正在捕捉什么。

本文讨论了专门用来测试句子嵌入是否抓住了句子的组成和意义的特定任务。本文基于另一篇论文(Adi 等人。al，2016)，其中，(Adi 等人。al，2016)使用弓模型和自动编码器进行类似的实验。然而，由于数据集中的非预期偏差，他们的结果非常可疑。例如，他们表明，在单词顺序任务中，BOW 模型实现了 70%的性能，即使这种模型在逻辑上不可能保留与单词顺序相关的信息。因此，这篇论文的作者认为，BOW 模型的这种表现是一个偶然事件，因为数据集中存在偏差。

本文提出消除/减少这种偏见，并测试其他深度学习模型。它们还引入了额外的任务，这些任务将在下面详细讨论。本文的贡献包括一个句子生成集，一个已证实的模型来测试组成和意义是否确实被嵌入，生成系统和用于分类的数据集作为开源提供给其他人进行进一步的探索和分析。

**研究问题:**本文试图回答的研究问题有:

1.当前的神经句子嵌入模块在它们的句子嵌入中捕获句子的含义和组成的情况如何？

2.我们能提出一种方法和框架来评估句子嵌入和它们的模型在多大程度上捕捉了句子的意义和组成吗？

**意义和构成:**构成句子的元素向读者传递意义。它通常包含一个代理、一个患者和一个事件。构图是元素排列的一种方式，有助于传达意义。一个句子的不同部分可以结合起来达到它的意思。

**数据集准备:**作者提出了一种新的句子生成系统，减少了数据集中的偏差。例如，它根据英语的句法、语义和词汇规则生成多样化的、完全带注释的句子。它由三部分组成。

**事件/句子表征:**这些是句子的部分表征，接受诸如施事、受事、及物、不及物动词以及关系从句的存在与否等参数。这些表示作为输入提供给事件生成系统。例如，考虑如下所示的句子。

**事件填充:**系统从句子表示系统获取输入，并用给定的信息填充事件。它使用副词和 17 个词汇。字数受到限制，以保持对生成句子的控制。它循环通过副词和名词来生成句子。

**句法实现:**它使用基于规则的技术对生成的句子中的单词进行词形变化，以遵循词法。他们使用(Bird 等人，2009)中提到的 NLTK 框架，屈折从 XTAG 形态学数据库中提取(Doran 等人，1994)。

**分类任务:**设计不同的任务来测试句子嵌入是否保持句子的组成和意义。大致可分为两种类型，**肯定**和**否定**。SemRole 任务旨在测试句子嵌入是否抓住了意思。要回答的问题是，给定一个名词(n)，一个动词(v)和一个句子嵌入(s)，n 是 v 在 s 中的施事吗？

否定任务是测试句子嵌入是否捕捉到动词的否定。即给定一个动词(v)和一个句子嵌入(s)，v 是否在 s 中被否定？生成的句子在动词和否定之间填充副词，使得动词在否定之后不明显，并且该模式易于模型学习和检测。

其他三项任务与单词内容和顺序有关。第一个任务， **Content1Probe** 被设计为测试句子嵌入是否包含输入句子中存在的动词。 **Content2Probe** 类似于 Content1Probe，它测试句子嵌入是否同时包含名词和动词，假设两者在句子嵌入生成之前都作为输入出现。

**排序任务**旨在测试合成句子嵌入是否捕捉到句子中单词顺序的信息。给定一个既包含动词(v)又包含名词(n)的句子嵌入(s ),那么名词(n)出现在动词(v)之前吗？

**分类实验:**作者建立了一个神经网络/多层感知器模型，其输入大小等于句子嵌入的大小。ReLU 用作神经元的激活函数。上述分类任务本质上是二元的。因此，对于生成的句子，每个任务的标签(是或否)被分配。生成 5000 个这样的句子，其中 4000 个具有适当标签的句子被用作训练集，其余 1000 个句子(具有适当标签)被用作测试集。不需要超参数调谐，因为网络规格在(Adi et。al，2016)。作者不执行任何训练来生成句子嵌入。他们也没有设计一个句子嵌入算法。他们使用嵌入算法，这些算法已经可以作为他们自己的语料库上的预训练模型。这些模型用于为生成的 5000 个句子产生句子嵌入。句子的嵌入和它们各自的任务标签形成了神经网络模型的数据集。该模型用训练集进行训练，并用测试集进行测试。

**句子嵌入模型:**下面描述所使用的不同句子嵌入模型:

**BOW:**BOW 模型是一个简单的模型，它使用一个向量来表示句子中的每个单词。它对这些嵌入进行平均，并将其用作句子嵌入。

**顺序去噪自动编码器:**它是一种无监督学习技术，使用基于 LSTM 的自动编码器。

**跳过思想嵌入:**他们利用 GRUs 生成句子嵌入。有两种可用的变体，uni-skip (ST-UNI)和 bi-skip (ST-BI)。Uni-skip 编码器在正向传递时进行回复，而 bi-skip 在神经网络中同时使用正向和反向传递。

**InferSent:** InferSent 是最先进的模型，它使用多层双向 LSTM 来生成句子嵌入。

**结果:**

![](img/5f054aeea2702f4ce8c8f31abd89734f.png)

**表。1(摘自** [**来源**](https://www.aclweb.org/anthology/C18-1152.pdf) **论文)**

各种任务的模型结果如上表所示。它摘自 Ettinger 等人(2018 年)。

单词袋(BOW)模型在基于内容的任务上表现良好。这说明弓模型完美地编码了单词的意思。人们期望它在顺序、语义角色和否定任务中表现糟糕，它确实如此。这用作对数据集的检查，并且它满足该标准。这也可能是由于数据生成模块中使用的 17 个单词的词汇集非常有限。

在否定任务中，除了 ST-BI，所有模型都表现良好。这可能是因为在向前传递时，它首先遇到否定，然后是动词，但在向后传递时，这个顺序是相反的。因此，信息可能没有被很好地捕获。其他模型做得很好，即使很难捕捉到否定和动词之间的关系，即使很难做到这一点。这也可能是由于嵌入的维数从 1200 减少到 300。

对于语义角色(SemRole)任务，InferSent 表现随机，其他模型也表现不佳。正如本文作者(Ettinger 等人，2018 年)所述，**句子嵌入模型没有提供有力的证据表明它们充分捕捉了语义角色。**

还可以推断出，当通过它们的嵌入进行评估时，具有不同设计架构和目标的不同句子嵌入模型未能对句子的含义和组成产生任何显著影响。所有的模型在其嵌入中捕获几乎相同水平的意义和组成。

实验结果也证明了所提出的方法是可靠的，可以检测句子嵌入捕获了多少或是否捕获了句子的意义和成分。可以定义更多的任务来更好地理解句子嵌入中捕获的信息。

作者计划通过显式嵌入 e 中提到的句法结构来测试其他模型(Bowman 等人，2016；戴尔等人，2016；Socher 等人，2013 年)在他们未来的工作。

**参考文献**

Ettinger，a .，Elgohary，a .，Phillips，c .，& Resnik，P. (2018)。评估句子向量表示中的成分。arXiv:1809.03992。

约西·阿迪、埃纳特·克尔马尼、约纳坦·贝林科夫、奥弗·狮式战斗机和约夫·戈德堡。2016.使用辅助预测任务对句子嵌入进行细粒度分析。arXiv 预印本 arXiv:1608.04207。

史蒂文·伯德、伊万·克莱恩和爱德华·洛珀。2009.用 Python 进行自然语言处理:用自然语言工具包分析文本。奥赖利媒体公司。

克里斯蒂·多兰、达尼亚·埃杰迪、贝丝·安·霍基、班加罗尔·斯里尼瓦斯和马丁·扎伊德尔。1994.XTAG 系统:覆盖面广的英语语法。《第 15 届计算语言学会议论文集》第 2 卷，第 922-928 页。计算语言学协会。

塞缪尔·R·鲍曼、加博·安格利、克里斯托弗·波茨和克里斯托弗·D·曼宁。2015.用于学习自然语言推理的大型标注语料库。在 EMNLP。

克里斯·戴尔、阿迪古纳·昆科罗、米盖尔·巴列斯特罗斯和诺亚·史密斯。2016.递归神经网络语法。纳克。

理查德·索彻、亚历克斯·佩雷金、让·吴、贾森·庄、克里斯托弗·曼宁、和克里斯托弗·波茨。2013.情感树库语义合成的递归深度模型。2013 年自然语言处理经验方法会议论文集，第 1631-1642 页。