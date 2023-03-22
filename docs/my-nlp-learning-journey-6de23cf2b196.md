# 我的 NLP 学习之旅

> 原文：<https://towardsdatascience.com/my-nlp-learning-journey-6de23cf2b196?source=collection_archive---------19----------------------->

## 开始用文本数据处理项目的指南。

![](img/e275e8690fc03b829012cedd2b007988.png)

当你阅读标题时，我将与你分享我惊人的学习之旅，它始于一年前我在 NLP 领域做毕业设计的时候。在开始这个项目之前，我对自然语言处理(NLP)领域的了解还不够多。

> “永远不要后悔你的过去。
> 更确切地说，像老师一样接受它。”——**罗宾·夏尔马。**

# 介绍

通常在执行分析时，许多数据是数字的，例如销售数字、物理测量、可量化的类别。计算机非常擅长处理直接的数字信息。然而，我们如何处理文本数据呢？

作为人类，我们可以看出文本文档中有过多的信息。但是计算机需要专门的处理技术来理解原始文本数据。我们知道，文本数据是高度非结构化的，可以使用多种语言！

这就是为什么 NLP 试图使用各种技术来创建文本数据的结构。

在这篇文章中，我想概述一下在学习 NLP 技术时我必须知道的一些主题。我注意到许多其他帖子都涉及到同样的事情，但是写下我的学习之旅帮助我组织我所知道的事情。

# 目录

1.  工业中的自然语言处理
2.  文本预处理
3.  计算语言学和单词嵌入
4.  深度学习的基础
5.  面向自然语言处理的深度学习

# 工业中的自然语言处理

我们可以注意到文本数据无处不在。这就是为什么自然语言处理负责大量的应用。
在这一部分，我列出了其中一些应用:

*   NLP 启用了一些有用的功能，如自动更正、语法和拼写检查，以及自动完成。
*   提取和总结信息:NLP 可以从各种文本源中提取和综合信息。
*   情感分析(电影、书籍和产品评论)。
*   聊天机器人:是使用自然语言处理的算法，能够理解你的查询，并充分、自动和实时地回答你的问题。
*   自动翻译是 NLP 的一个巨大应用，它使我们能够克服与来自世界各地的个人交流的障碍，并理解用外语编写的技术手册。

可以查看我之前的文章 [***这里***](https://medium.com/@amalmenzli7) 我在哪里做过 NLP 相关的项目。

# 文本预处理

这一节是关于熟悉和熟悉基本的文本预处理技术。

## 从多个来源加载文本数据:

在这一部分，我将向你展示如何打开不同来源的文本文件，如 CSV 文件，PDF 文件等。

## 正则表达式:

正则表达式(有时称为 regex)允许用户使用几乎任何类型的规则搜索字符串。例如，在字符串中查找所有大写字母，或者在文档中查找电话号码。正则表达式必须能够过滤出任何你能想到的字符串模式。使用 Python 的内置`**re**`库来处理它们。更多信息见[文档](https://docs.python.org/3/library/re.html)。

大多数行业仍然使用正则表达式来解决问题，因此我们不能忽视它的重要性。它们通常是数据清理的默认方式。知道了它们的适用性，了解它们并恰当地使用它们是有意义的。

让我们看一些使用`**re**`的代码示例

## Spacy vs NLTK:

我将稍微介绍一下`**nltk**`和`**spacy**`，它们都是 NLP 中最先进的图书馆，以及它们之间的区别。

[**Spacy**](https://spacy.io/)**:**是一个开源的 Python 库，可以解析并“理解”大量文本。针对特定语言(英语、法语、德语等)提供不同的型号。).旨在通过最有效地实现常用算法来处理 NLP 任务。

[**NLTK**](https://www.nltk.org/)**:**自然语言工具包是一个非常流行的开源。最初发布于 2001 年，比 Spacy(2015 年发布)要老很多。它也提供了许多功能，但实现效率较低。

→对于许多常见的 NLP 任务，Spacy 更快、更有效，代价是用户不能选择算法实现。然而，Spacy 并不包括一些应用程序的预创建模型，比如情感分析，这通常更容易用 NLTK 来执行。

**空间安装和设置:**安装分为两步。首先，使用`**conda**`或`**pip**`安装 SpaCy。接下来，根据语言下载您想要的特定型号。更多详情，请访问此 [***链接***](https://spacy.io/usage/) 。

从命令行或终端:

```
conda install -c conda-forge spacy
or
pip install -U spacy
```

接下来，`**python -m spacy download en_core_web_sm**`

## 符号化:

处理文本的第一步是将所有的部分(单词和标点)分割成“记号”。这些标记在 Doc 对象内部进行了注释，以包含描述性信息。与句子分割一样，标点符号也很有挑战性。作为一个例子，英国应该被认为是一个令牌，而“我们”应该被分成两个令牌:“我们”和“'的”。对我们来说幸运的是，SpaCy 将隔离那些不构成单词组成部分的*标点符号。句子末尾的引号、逗号和标点符号将被分配给它们的标记。但是，作为电子邮件地址、网站或数值的一部分存在的标点符号将作为令牌的一部分保留。这里有一个例子，你可以运行它，看看结果。*

## 命名实体:

*超越了令牌，命名实体*增加了另一层上下文。语言模型认为某些单词是组织名称，而其他单词是位置，还有一些组合与金钱、日期等有关。命名实体可以通过`ents`访问。

## 词干:

词干提取是对相关单词进行编目的一种粗略方法；它基本上是从末尾直到词干截断字母。这在大多数情况下工作得相当好，但不幸的是，英语有许多需要更复杂过程的例外。SpaCy 没有包含词干分析器，而是选择完全依赖于词汇化。我们将在下一部分讨论*引理化*的优点。相反，我们将使用另一个名为`**nltk**` **的 NLP 库。**

## 词汇化:

与词干化相反，词汇化不仅仅是减少单词，而是考虑一种语言的全部词汇，对单词进行词法分析。“was”的引理是“be”，“mice”的引理是“mouse”。此外,“meeting”的引理可能是“meet”或“meeting ”,这取决于它在句子中的用法。

变元化比简单的词干化提供了更多的信息，这就是 Spacy 选择变元化而不是词干化的原因。我们应该指出，尽管词汇化查看周围的文本来确定给定单词的词性，但它并不对短语进行分类。

```
import spacy
nlp = spacy.load('en_core_web_sm')text = nlp(u"I am a runner always love running because I like to run since I ran everyday back to my childhood")for token in text:
    print(token.text, '\t', token.pos_, '\t', token.lemma, '\t', token.lemma_)

#### ----> In the above sentence, running, run and ran all point to the same lemma run. ####
```

## 停止单词:

停用词是指像“a”和“the”这样出现频率很高的词，它们不像名词、动词和修饰语那样需要彻底标记。SpaCy 拥有一个大约 305 个英语停用词的内置列表。

之后，我们可以将所有这些技术结合在一起，如果我们需要纠正拼写，删除多余的空格或标点符号等，我们可以添加更多的技术。建立一个文本规范化和预处理我们的文本数据。

> **“数据清理和准备是数据科学过程的关键步骤”**

![](img/ef3a3c25cc06227cc16ab1207d540f70.png)

图片:[来源](https://www.cleanpng.com/png-cleaning-cartoon-cleaner-housekeeping-clip-art-cle-556406/)

# 计算语言学和单词嵌入

在这一部分，我将讨论几个主题，例如:

1.  提取语言特征
2.  向量空间中的文本表示
3.  主题建模

## 提取语言特征

*   **使用空间进行词性标注:**

有些看起来完全不同的词，意思却几乎一样。相同的单词以不同的顺序排列可以表达完全不同的意思。然而，我们需要看这个词的词性，而不仅仅是这个词。这正是 Spacy 的设计目的:你放入原始文本并得到一个 Doc 对象，它带有各种注释。

名词、动词、形容词等词性标签，以及复数名词、过去式动词、最高级形容词等细粒度标签。

回想一下，您可以通过索引位置获得特定的标记。

*   使用`token.pos_`查看粗略位置标签
*   使用`token.tag_`查看细粒度标签
*   使用`spacy.explain(tag)`查看任一类型标签的描述

注意‘token . pos’和‘token . tag’返回整数散列值；通过添加下划线，我们得到了等价的文本。更多详情和信息，可以查看 [*这里*](https://spacy.io/api/annotation#pos-tagging) 。

结果是:

![](img/a7a9d6971dbe929f540f74073354d8c7.png)

Visualizing POS: SpaCy 提供了一个出色的可视化工具，名为`displaCy`。

```
#Import the displaCy library
from spacy import displacy#Render the dependency parse immediately inside Jupyter:
displacy.render(doc, style='dep', jupyter=True, options={'distance': 110})
```

![](img/551ac436d97807a5d3ecd2e7831bcb9c.png)

POS 文档可视化

*   **NER 使用空间:**

命名实体识别(NER):寻找非结构化文本中的命名实体并将其分类到预定义的类别中，如人名、组织、位置、医疗代码、时间表达式、数量、货币值、百分比等。Spacy 有一个“ner”管道组件，它标识符合一组预定命名实体的令牌跨度。

结果:

```
Spain - GPE-Countries, cities, states next April - DATE-Absolute or relative dates or periods the Alhambra Palace - FAC-Buildings, airports, highways, bridges, etc.
```

欲了解更多关于**命名实体识别**请访问此 [***链接***](https://spacy.io/usage/linguistic-features#101) 。

## 向量空间中的文本表示

*   **单词的离散表示:**

假设我们有一门拥有 10 个单词的语言。

```
V = {cat*, car, ship, city, man, laptop, word, woman, door, computer*}
```

我将“笔记本电脑”和“汽车”这两个词表示如下:

![](img/512d0935c1d72fcff911674a8b2d0432.png)

我们可以看到，所有的条目都是*“0”*，除了单词*“laptop”*= 1 的索引，单词*“car”*也是如此。我们称那些向量为 10 个单词的***【one-hot】***表示。

离散表示的问题是，它可能无法捕获特定于领域的语义。换句话说，我们无法捕捉表示中的语义相似性和关联性。例如，家和住所是相似的，所以应该彼此靠近。但在按字母顺序组织的英语词典中，它们却相距甚远。

*   **作为分布式表示的神经单词嵌入:**

一个单词将由其相邻单词的平均值来表示。为每个单词构建一个 ***密集向量*** 。例子:`hello=[0.398, -0.678, 0.112, 0.825, -0.566]`。我们称这些*单词嵌入为*或*单词表示。*

**Word2vec 模型**是一个处理文本的两层神经网络。它的输入是一个文本语料库，输出是一组向量。Word2vec 的目的和用途是将向量空间中相似词的向量分组。给定足够的数据、用法和上下文，Word2vec 可以根据过去的表现对单词的意思做出高度准确的猜测。这些猜测可以用来建立一个单词与其他单词的关联(例如，“男人”对“男孩”，“女人”对“女孩”)。给定一个中心词，它可以预测周围的词，反之亦然。

它以两种方式中的任何一种来实现，使用上下文来预测目标单词(这种方法被称为连续单词包，或 **CBOW** )或使用单词来预测目标上下文，这被称为 **skip-gram** 。

## 主题建模:

主题建模允许我们通过将文档聚集成主题来分析大量文本。我们将从检查*潜在的狄利克雷分配*如何尝试为文档集发现主题开始。

*   ***【潜在狄利克雷分配法】* :**

LDA 早在 2003 年[就被引入，以解决文本语料库和离散数据集合的建模问题。我将基于示例解释 LDA。LDA 是一种自动发现这些句子包含的主题的方法。假设你有以下一组句子:
——“糖不好吃。我妹妹喜欢吃糖，但我父亲不喜欢。”
——“健康专家说糖对你的生活方式没有好处。”
——“我父亲花很多时间开车带我妹妹去练习舞蹈。”
——“我爸爸总是开车送我妹妹去学校。”
——“医生提示开车可能导致压力和血压升高。”LDA 是一种自动发现这些句子包含的主题的方法。例如，给定这些句子并要求 2 个主题，LDA 可能会产生如下内容:
句子 1 和 2: 100%主题 A
句子 3 和 4: 100%主题 B
句子 5: 20%主题 A，80%主题 B
主题 A:我们可以将主题 A 解释为关于糖病)。
话题 B:我们可以把话题 B 解读为关于开车)。](http://ai.stanford.edu/~ang/papers/jair03-lda.pdf)

# 深度学习的基础

深度学习是 NLP 最近发展的核心。从谷歌的 BERT 到 OpenAI 的 GPT-2，每个 NLP 爱好者都应该至少对深度学习如何为这些最先进的 NLP 框架提供动力有一个基本的了解。

在我们直接进入神经网络之前，我们需要首先了解单个组件，例如单个“神经元”。
人工神经网络有生物学基础！让我们看看如何用一种被称为感知器的人工神经元来模仿生物神经元。

![](img/514897f8d7e1805663fb858add942342.png)

人工神经元也有输入和输出！这个简单的模型被称为感知器。
输入将是特征值，它们乘以一个权重。这些权重最初是随机生成的。
然后这些结果被传递给一个激活函数(有许多激活函数可供选择，我们将在后面详细介绍)。现在，我们的激活函数将非常简单…如果输入的和是正回报，1 如果和是负输出 0。
因此，有一个可能的问题。如果原始输入从零开始会怎样？
那么任何权重乘以输入仍然会得到零！我们可以通过添加一个偏置项来解决这个问题，在这种情况下，我们选择 1。

**神经网络简介:**

我们已经看到了单个感知器的行为，现在让我们将这个概念扩展到神经网络的想法！！
我们来看看如何连接多个感知机。

![](img/8877d9a0ec989904c6a990a19ca8e595.png)

图片:[来源](/build-up-a-neural-network-with-python-7faea4561b31)

多重感知器网络:
-输入层(来自数据的真实值)。
- 2 个隐藏层(输入和输出之间的层(3 层或更多层是“深度网络”)】
- 1 个输出层(输出的最终估计)
关于之前的激活函数:这是一个非常戏剧性的函数，因为微小的变化没有反映出来。所以，如果能有一个更动态的函数就好了。
让我们再讨论几个激活功能:

![](img/d771c75b34a80e9c5c933f7b0c0220c0.png)

[不同的激活函数及其图形](https://medium.com/@shrutijadon10104776/survey-on-activation-functions-for-deep-learning-9689331ba092)

ReLu 因其简单性和前向与后向计算容易，在许多情况下具有最佳性能。但是，在某些情况下，其他激活函数会给我们带来更好的结果，例如当我们希望我们的输出在[0，1]
之间压缩时，会在最后一层使用**Sigmoid**。DL 库为我们内置了这些函数，因此我们不必担心必须手动实现它们！！
现在我们已经了解了神经网络理论的基础，我们可以进入更高级的话题了。

# 面向自然语言处理的深度学习

在我们看到深度学习基础知识的简要概述后，是时候将事情提升一个档次了。深入了解高级深度学习概念，如递归神经网络(RNNs)、长短期记忆(LSTM)等。这些将帮助我们掌握行业级的 NLP 用例。
**递归神经网络:**专门设计用于处理序列数据。让我们想象一个序列`[1,2,3,4,5,6]`，你可以问的问题是:你能预测一个类似的序列移动一步到未来吗？？像那个`[1,2,3,4,5,6,7]`。

最终，有了 RNN，我们可以做到这一点。

![](img/e23c4ea0ddc600db67ebb7170a64442d.png)

[FFN vs RNN](https://www.oreilly.com/ideas/build-a-recurrent-neural-network-using-apache-mxnet)

**RNN 直觉:**

*   ***序列到序列* :** 是关于训练模型将序列从一个领域(例如英语中的句子)转换到另一个领域中的序列(例如翻译成法语的相同句子)。我们可以用它来进行机器翻译或问答任务。
*   **序列到向量:**情绪得分你可以输入一个单词序列，可能是一段电影评论，然后请求返回一个向量，指示它是否是积极的情绪，例如他们是否喜欢这部电影。
*   **Vector to sequence:** 可能只是为一个单词提供一个种子，然后得到一个完整的高概率序列短语序列。(exp: word=Hello，为你生成的序列= How are you)。

![](img/16ab533d8e6e86169c6099efb4144c56.png)

RNN 建筑

现在我们已经了解了基本的 RNNs，我们将继续了解一种称为 LSTM(长短期记忆单位)的特殊细胞结构。生成有意义的文本是必要的，因为我们希望网络不仅知道最近的文本，还知道它看到的文本的整个历史。

**长短期记忆(LSTM):**
RNN 面临的一个问题是，过一段时间后，网络将开始“忘记”最初的输入，因为信息在通过 RNN 的每一步都会丢失。因此，我们的网络需要某种“长期记忆”。
LSTM 分部帮助解决这些 RNN 问题。
让我们来看看 LSTM 细胞是如何工作的！记住，这里会有很多数学！查看资源链接获得完整的分解！

![](img/d4cfe1e6e7f0d6454eace7f6c9a2786a.png)

[LSTM 电池](https://www.researchgate.net/figure/Structure-of-the-LSTM-cell-and-equations-that-describe-the-gates-of-an-LSTM-cell_fig5_329362532)

在这里，我们可以看到整个 LSTM 细胞似乎如此复杂，当我们看到它的格式。然而，当你把它分解成几个部分时，它就没那么糟糕了。

在此图中，每条线都承载一个完整的向量，从一个节点的输出到其他节点的输入。粉色圆圈代表逐点操作，如向量加法，而黄色方框是学习过的神经网络层。行合并表示连接，而行分叉表示其内容被复制，并且副本被移动到不同的位置。
lst ms 的关键是单元格状态，即贯穿图表顶部的水平线。

GRU:LSTM 的另一个变种。这是最近在 2014 年左右推出的，它最终通过将遗忘门和输入门合并为一个名为更新门的门来简化事情。此外，它合并了单元格状态和隐藏状态，并做了一些其他更改。

# 下一步是什么？

在本文中，我想从零开始，只介绍 NLP 中的基本技术和一些高级技术。但是，我不能跳过基本概念就跳到更高级的话题。下一次，我们将探索现代 NLP 技术，如迁移学习，NLP 快速进步的原因。敬请关注！！！

# 结论

> "让你做的每一件事都像有所不同一样."威廉·詹姆斯

如果你正在读这篇文章，这是我的一篇较长的文章；我想为你陪我到最后而热烈鼓掌。本文通过一些例子介绍了我在 NLP 领域的学习历程，我相信这些例子会给你一个关于如何开始处理文本文档语料库的好主意。正如我所说的，我将在以后的文章中介绍迁移学习技巧。同时，请随时使用下面的评论部分让我知道你的想法，或者问你对这篇文章的任何问题。

***快乐阅读，快乐学习，快乐编码。***

# 在你离开之前:

你可以在这里找到我之前与 NLP 领域[相关的项目。](https://github.com/AmalM7)

# 参考资料:

[1] Sainbayar Sukhbaatar，Arthur Szlam，Jason Weston，Rob Fergus。[端到端存储网络。](https://arxiv.org/pdf/1503.08895.pdf) 2015 年。

[2] D. Bahdanau、K. Cho 和 Y. Bengio。[通过联合学习对齐和翻译的神经机器翻译。](https://arxiv.org/pdf/1409.0473.pdf) 2016。

[3] I.Sutskever、O.Vinyals 和 Q.Le (2014 年)。[用神经网络进行序列对序列学习。](https://arxiv.org/pdf/1409.3215.pdf)神经信息处理系统进展(NIPS 2014)。

[4]米科洛夫，托马斯；等人[向量空间中单词表示的有效估计](https://arxiv.org/pdf/1301.3781.pdf)。2013.

[5]利维，奥默；戈德堡，Yoav 达甘，伊多。 [*利用从单词嵌入中吸取的经验教训提高分布相似度*](http://www.aclweb.org/anthology/Q15-1016) *。* 2015 年。