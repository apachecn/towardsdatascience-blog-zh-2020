# 发现自然语言处理模型中的编码语言知识

> 原文：<https://towardsdatascience.com/encoded-linguistic-knowledge-in-nlp-models-b9558ba90943?source=collection_archive---------31----------------------->

## 深度学习模型中发现编码语言知识的“探针”的背景、调查和分析

*本文作者为* [*凯于尔福尔杜*](https://medium.com/@keyurfaldu) *和* [*阿米特谢思*](https://www.linkedin.com/in/amitsheth/) *。本文详细阐述了更广泛的封面故事* [***“现代 NLP 的兴起和可解释性的需要！”***](/rise-of-modern-nlp-and-the-need-of-interpretability-97dd4a655ac3)**在 Embibe，我们在搭建 NLP 平台解决学术内容众多问题的同时，迫切需要开放性问题的答案。**

*现代 NLP 模型(伯特、GPT 等)通常以端到端的方式训练，精心制作的特征工程现在已经灭绝，这些 NLP 模型的复杂架构使其能够学习端到端的任务(例如，情感分类、问题回答等)。)而没有明确指定特性[2]。语言特征(如词性、共指等)在经典的自然语言处理中起着关键的作用。因此，理解现代 NLP 模型如何通过“**探究**”它们所学习的东西来做出决策是很重要的。这些模型会从未标记的数据中自动学习语言特征吗？我们如何解释现代 NLP 模型的能力？让**探测**。*

*![](img/10c66536df92ed5dcfbae948fb734f7f.png)*

*到**探头**就是调查。由[马库斯·温克勒](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片*

# *语言学:背景*

*语言知识是自然语言处理的一个重要方面。我们可以从以下几个方面来考虑，*

*   ***句法**:分析句子的结构和单词的连接方式。*
*   *形态学:研究单个单词的内部结构，以及新单词是如何由这些基本单词的变体形成的。*
*   ***音系学**:对构成语言基本成分的语音系统的研究。*
*   ***语义**:处理单个单词和整个文本的意思。*

*![](img/95a93fe5bfb4fb631b7c3b2afca6badb.png)*

**图一。一份来自克什米尔的十七世纪* [*桦树皮手稿*](https://en.wikipedia.org/wiki/Birch_bark_manuscript)*pāṇini's 语法论著(图片来源:*[*https://en.wikipedia.org/wiki/Panini*](https://en.wikipedia.org/wiki/P%C4%81%E1%B9%87ini)*)**

*在统计方法和经典机器学习中，解决任何与自然语言处理相关的问题都涉及推导上述语言知识。因此，研究界关注了许多与语言知识相关的任务。我们可以看到如下几个例子:*

*![](img/b5b62f12520d13bda0c00f96d401b520.png)*

**图 2:一句话中的语言学知识举例。(图片来自* [*其他文章*](/rise-of-modern-nlp-and-the-need-of-interpretability-97dd4a655ac3) *)**

*   ***词性**:词的句法范畴，即名词、动词、形容词、代词等。*
*   ***成分树**(或短语结构语法):短语结构规则考虑到句子结构是以成分为基础的，一棵解析树将这些成分排列成具有成分关系的树形结构。*
*   ***依存树**(或称依存文法):依存文法规则认为句子结构是以依存为基础的，依存解析树将单词排列成有依存关系的树形结构。*
*   ***共指**:两个词或短语与共同所指物之间的关系。*
*   ***引理化**:使用形态分析去除前缀或后缀后，导出基本引理词。*

*以上是几个与语言学知识相关的重要任务的例子，其中词性主要处理句法知识，依存树，共指对进一步理解语义很重要，词条化是形态学的例子。*

*许多其他任务进一步分析句子的语言属性，如语义角色、语义原型角色、关系分类(词汇和语义)、主语名词、主要助动词、主谓一致等。*

# *现代自然语言处理模型*

*现代 NLP 模型要么基于 LSTM，要么基于变压器。ELMO 和乌尔菲特是基于 LSTM 架构的语言模型的例子。相反，伯特[1]和 GPT 是基于语言模型的变形金刚架构的例子。对于研究的其余部分，让我们以“BERT”为例作为参考。*

*   *BERT 模型以屏蔽词预测和对大量未标记数据的下一句预测为目标进行预训练。*
*   *预训练的 BERT 模型通过使用特定于任务的层对其进行扩展来进行微调，这些特定于任务的层用于具有有限标记数据的任务，如“情感分析”、“文本分类”或“问题回答”。*

*由预训练的 BERT 模型产生的表示对相关信息进行编码，这使得能够利用非常有限的标记数据进行特定于任务的微调。问题是，*

# *BERT 中编码了哪些语言学知识？*

*因此，一系列研究试图了解神经网络中捕捉的是哪种语言信息。不同方法中最常见的主题可以分为**“探针**”(或探测分类器、诊断分类器、辅助预测任务)，它探测神经网络的内部机制如何分类(或执行)辅助语言任务(或探测任务，或辅助任务)。*

*![](img/382e8d14fbee32d3f98a9deff0fe8109.png)*

**图三。伯特模型上探针的示意图。它展示了如何使用注意机制将输入令牌置于连续的层中。显示了两种类型的探针，(1)基于表征的，和(2)基于注意力的。注意，这个图是为了更广泛的说明，所以没有显示像 CLS 和 SEP 这样的特殊标记。**

# *“探针”是如何工作的？*

*   ***探针**是浅层神经网络(通常是一个分类器层)，插在为主要任务训练的神经网络的中间层或注意力头的顶部。探针有助于调查不同的层或注意力头捕捉到了什么信息。使用辅助任务来训练和验证探测器，以发现是否捕获了这种辅助信息。*
*   *图 3 示出了如何将探测分类器插入不同层或注意力头的顶部，以发现与不同层和注意力头的辅助任务相关的编码信息。*
*   *比方说，我们想要调查来自 BERT 模型的编码表示是否捕获语言信息，如“如果一个动词是助动词”或“如果一个短语是主语名词”。助动词是助动词，主语名词是充当主语的名词短语。这些任务可以被框定为探头的“辅助任务”。例如，在句子*“孩子们整天在玩板球”——**是*“是助动词，”*玩*是主动词，“*孩子们*是主语名词，“*板球*是宾语名词。*
*   *如果探测分类器不能很好地完成语言信息的辅助任务，这意味着这种信息没有被编码在模型的内部表示中，这也是可能的，因为它可能不需要解决模型的主要目标。*

# *“探索”与微调或多任务学习有什么不同？*

*![](img/7bc7a4d2f1a09c4e451299faa4209e00.png)*

*表 1。探针 vs 微调 vs 多任务学习*

*   *“探针”是 ***而不是*** 与对下游任务的微调有关，无论是在目标上还是在方法上。*
*   *表 1 显示了对比情况。*
*   *“探针”是为了发现编码的语言知识，而微调和多任务学习在一个或多个主要任务上训练模型。*

*![](img/3cbbe535dd4176c73ef42604d4d54a3c.png)*

*图 4。多任务学习与探究*

*   *如图 4 所示，“探针”可以访问模型内部但不能更新模型参数，另一方面，微调和多任务学习不访问模型内部，但它们可以更新模型参数。*
*   *就复杂性而言，“探针”应该是浅层的(即模型顶部的单层分类器)，而微调和多任务学习可以根据下游任务的复杂性堆积深层[7][8]。*

# *什么是不同类型的“探针”？*

*这些探测分类器可以基于它们利用什么样的神经网络机制来探测语言知识而被分类。这些主要是*

*   ***内部表示:**在来自不同层的内部表示之上构建一个小型探测分类器，以分析不同层编码了什么语言信息。*
*   ***注意力权重:**探测分类器建立在注意力权重之上，以发现注意力权重模式中是否存在潜在的语言现象。*

# *(A)基于“探测”的内部表示:*

*相当多的技术正在探索在像 BERT 这样的模型的不同层次上，有多少语言知识被编码在内部表示中。让我们来看几个例子。*

***(A.1)边缘探测:**Tenney 等人[4][5]提出的框架旨在探测编码在模型的上下文化表示中的语言知识。*

*   *对于词性、成分、依存关系、实体、语义角色标记、语义原型角色和共指消解等辅助任务，它比较了伯特、GPT、ELMO 和科夫等模型的上下文化表示的性能。*
*   *边缘探测将结构化预测任务分解成一种通用格式，其中探测分类器从句子中接收一个文本区间(或两个区间),并且必须预测诸如成分或关系类型等标签。从那些目标区间内的令牌的每令牌嵌入中。*
*   *BERT-Large 模型的辅助任务总体性能的宏观平均值为 **87.3，**，而使用非情境化表示的基线探测器达到了 **75.2** 。因此，大约 20%的额外语言知识作为语境化的一部分被注入。*

***(A.2) BERT 重新发现经典的 NLP 管道** : Tenny 等人【3】【9】进一步分析了语言学知识从何而来。*

*   ***重心:**重心反映了参与计算不同层的内部表示的标量混合(加权池)的平均层。对于每一项任务，直观地说，我们可以解释为更高的重心意味着该任务所需的信息被更高层所捕获。*
*   ***期望层:**用不同层的内部表示的标量混合来训练探针分类器。层 I 的贡献(或差异分数)通过取用层 0 至层 I 训练的探测器的“*性能*”与用层 0 至层 i-1 训练的探测器的“*性能*”之差来计算。期望层是对每一层的差异分数的期望。*

*![](img/22090a5ac4bc24384aee1dd0e619de65.png)*

**图 5:探头性能，以及图层对辅助任务的贡献(图片来源，* [*Tenney 等人*](https://arxiv.org/abs/1905.05950)*【5】)**

*   *在图 5 中，行标签是探测语言知识的辅助任务。每个任务的探测分类器的 F1 分数在前两列中提到，其中 l=0 表示辅助任务在非上下文表示上的表现，l=24 表示通过混合来自 BERT 模型的所有 24 层的上下文表示的辅助任务表现。预期层以紫色显示(重心以深蓝色显示)。*
*   *预期层是最大的额外语言知识的来源。可以看出，关于句法任务的语言知识是在最初几层获得的，而关于语义任务的语言知识是在后来几层获得的。*

# *(B)基于注意力权重的“探针”:*

*“伯特在看什么？对 BERT 注意力的分析”，Clark 等人[2]探讨了 BERT 中语言知识的注意力权重。有趣的是，我们注意到特定的注意头是如何表达语言现象的，而注意头的组合可以预测语言任务，如与艺术表现水平相当的依存语法。*

***(B.1)具体注意事项***

*   *从图 6 中可以看出，BERT 中的特定注意力中心表达特定的语言现象，其中一个标记根据注意力中心表达的语言关系参与其他标记。*

*![](img/5a8585f33e34263ec41ac4d5dacc10ce.png)*

**图 BERT 中特定注意头表达的语言现象。(图片来源:* [*克拉克等人*](https://arxiv.org/pdf/1906.04341.pdf)*【3】)**

*   *上面显示了六种不同注意力的可视化效果。BERT 基本模型有 12 层，每层有 12 个注意头。图 5 中左上的图表示第 8 层中的第 10 个注意头。客体关注其名词的模式是显而易见的。同样，在第 8 层的第 11 个注意头中，名词修饰语(限定词等。)正在关注他们的名词。同样，我们可以注意到其他情节中的注意头是如何表达语言知识的。*

*![](img/0f754e4da9846e34220ca8bfabf6f668.png)*

**表 2:特定注意头的依存关系分类精度。克拉克等人【3】**

*   *注意到注意力头作为现成的探测分类器的表现真是令人惊讶。*

*如表 2 所示，对于每个依存关系，特定注意头如何实现预测依存标记的分类性能。对于行列式(det)、直接宾语(dobj)、所有格词(poss)、被动助词(auxpass)等情况，与基线模型(预测最佳固定偏移量处的令牌)相比，性能增益是巨大的 **(~100%)** 。*

***(B.2)注意力头部组合***

*![](img/7b9dc7dfc4c2a1c5ef5adf03e01e6044.png)*

**表 3:不同基线和探测技术的性能。UAS 是用于依存首部令牌预测的未标记附件分数。克拉克等人【3】**

*   *在直接采用注意力权重的线性组合以及具有非上下文嵌入(如 GloVe)的注意力权重上训练的探测分类器，给出了与依赖于内部上下文表示的相对复杂的模型相当的性能，用于依存性解析任务。*
*   *同样，关于共指、消解任务的实验也显示了类似的潜力。也就是说，我们可以得出结论，BERT 中的注意机制也编码和表达语言现象。*

# *探索“探针”*

*既然我们已经了解了基于表征的探针和基于注意力权重的探针，以使用辅助任务来发现编码的语言知识，那么询问更深层次的问题将会很有趣:*

*   **模型越大，对语言知识的编码越好吗？**
*   **如何检查模型对语言知识编码的泛化能力？**
*   **我们能否解码语言学知识，而不是依赖浅层探针分类器标签？**
*   **探针有哪些局限性，如何得出结论？**
*   *我们能注入语言学知识吗？*
*   **编码语言知识能捕捉意义吗？**
*   ****编码的语言学知识对于自然语言理解来说足够好吗？****

*让我们在下一篇文章**“超越**分析 NLP 模型的编码语言能力&中进一步阐述上述问题。(即将推出)*

***参考文献**:*

1.  *Devlin 等人《BERT:用于语言理解的深度双向转换器的预训练》。NAACL 2019。*
2.  *Belinkov 等人[“神经语言处理中的分析方法:调查”](https://www.mitpressjournals.org/doi/pdfplus/10.1162/tacl_a_00254)，ACL 2019*
3.  *凯文·克拉克，乌尔瓦什·汉德尔瓦尔，奥默·利维，克里斯多佛·d·曼宁，[“伯特在看什么？伯特注意力分析”](https://arxiv.org/pdf/1906.04341.pdf)，2019*
4.  *伊恩·坦尼，迪潘詹·达斯，艾莉·帕夫利克，[《伯特重新发现经典 NLP 流水线》](https://arxiv.org/abs/1905.05950)，2019*
5.  *Tenney 等人[“你从上下文中学到了什么？语境化词语表征中的句子结构探索”](https://arxiv.org/pdf/1905.06316.pdf)，ICLR 2019*
6.  *阿迪等[“使用辅助预测任务对句子嵌入的细粒度分析”](https://arxiv.org/pdf/1608.04207.pdf)，ICLR 2017*
7.  *Stickland 等人[“BERT 和 PALs:多任务学习中高效适应的投射注意层”](https://arxiv.org/pdf/1902.02671.pdf)，ICML 2019*
8.  *周等[《极限-BERT:语言学告知多任务 BERT》](https://arxiv.org/pdf/1910.14296.pdf)，2019*