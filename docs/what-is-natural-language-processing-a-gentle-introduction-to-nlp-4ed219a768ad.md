# 什么是自然语言处理？自然语言处理简介

> 原文：<https://towardsdatascience.com/what-is-natural-language-processing-a-gentle-introduction-to-nlp-4ed219a768ad?source=collection_archive---------33----------------------->

## 自然语言处理导论:它是什么，我们如何使用它，我们面临什么挑战，我们有什么工具。

*本文原载于* [*程序员背包博客*](https://programmerbackpack.com/what-is-natural-language-processing-a-gentle-introduction-to-nlp/) *。如果你想阅读更多这类的故事，一定要访问这个博客。*

*更感兴趣？在 Twitter 上关注我，地址是*[*@ b _ dmarius*](https://twitter.com/b_dmarius)*，我会在那里发布每一篇新文章。*

![](img/e6e567159ee1c45bd34d374f37ff55a6.png)

照片由[克里斯蒂安·威迪格](https://unsplash.com/@christianw?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

自然语言处理或 **NLP** 是人工智能研究的一个子领域，专注于开发基于自然语言的人类和计算机之间的交互模型和点。这包括文本，也包括基于语音的系统。

几十年来，计算机科学家和研究人员一直在研究这个话题，但直到最近它才再次成为热门话题，这种情况是由研究界最近的突破造成的。

话虽如此，但在本文结束时，你会学到以下内容。

*   自然语言处理如何工作的基本概述
*   谁使用自然语言处理，用于什么样的问题
*   在您的应用程序或业务中使用自然语言处理有哪些挑战
*   有哪些基本工具可以让你开始使用自然语言处理

# 自然语言处理是如何工作的

计算机科学中一个普遍接受的事实是，如果我们把复杂的问题分成更小的部分，每个复杂的问题都会变得更容易解决。在人工智能领域尤其如此。对于一个给定的问题，我们构建几个小型的、高度专门化的组件，它们擅长解决一个且仅一个问题。然后，我们将所有这些组件对齐，通过每个组件传递我们的输入，并在线的末端获得我们的输出。这就是我们所说的**管道**。

在自然语言处理的背景下，一个基本的问题是，对于一个给定的段落，计算机准确地理解它的意思，然后可能相应地采取行动。为此，我们需要经历几个步骤。

## 句子边界分割

对于给定的文本，我们需要正确地识别每一个句子，以便由此产生的每一个句子在接下来的步骤中都可以提取其含义。似乎从一篇文章的每一句话中提取意思，然后把它们放在一起，比试图确定整篇文章的意思更准确。毕竟，当我们说话(或写作)时，我们不一定只指一件事。我们经常倾向于将更多的想法传达给一个人，自然语言的美妙之处(以及对 NLP 的诅咒)在于我们确实可以做到。

一种简单的方法是只在文本块中搜索句点，并将其定义为句子的结尾。问题是句点也可以用于其他目的(例如缩写)，因此在实践中，机器学习模型已经被定义为正确识别用于结束句子的标点符号。

## 单词标记化

这一部分包括从上一步中提取一个句子，并将其分解为包含所有单词(和标点符号)的列表。这将在接下来的步骤中用于对每个单词进行分析。

## 词性标注

这一步包括从上一步中提取每个单词，并根据它所代表的词类进行分类。这是识别文本背后含义的重要一步。识别名词可以让我们弄清楚给定的文本是关于谁或什么的。然后动词和形容词让我们理解实体是做什么的，或者它们是如何被描述的，或者我们可以从文本中获得的任何其他含义。词性标注是一个困难的问题，但它已经得到了很大程度的解决，并且在大多数现代机器学习库和工具中都可以找到它的实现。

## 命名实体识别— NER

这项任务是指识别句子中的名称，并根据预定义的类别列表对其进行正确分类。这些类别可能包括:人员、组织、地点、时间、数量等。类别列表可能是为您自己的特定用例定制的，但是一般来说，几乎每个人都需要至少这些类别才能被正确识别。

这类问题有许多实现，最近建立的模型已经达到了接近人类的性能。基本上，这一步也分为两个子任务:正确识别句子中的名字，然后根据你的类别列表对每个名字进行分类。

当然，为了在现实世界的应用中使用，NLP 解决了许多其他任务，但是接下来的步骤是为每个用例以及每个业务需求量身定制的。综上所述，前面介绍的步骤是我们能想到的几乎所有用例的基本步骤。

# 如何使用自然语言处理

![](img/d0ce5f54f8cdbd0cbf4fb8ede3783bd3.png)

在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上由 [BENCE BOROS](https://unsplash.com/@benceboros?utm_source=medium&utm_medium=referral) 拍摄的照片

NLP 被用在各种软件中，各种用例已经被确定为可以通过部署 NLP 模型来解决。其中一些例子是:

*   **虚拟助理:**为了帮助用户完成任务，大多数现代的、强大的个人助理都采用了大量的自然语言处理技术。Siri、Google Assistant 和许多其他软件已经变得非常高效和熟练，通过使用 NLP 领域的最新突破来帮助他们的用户。这意味着他们背后的公司在开发完美虚拟助手的竞赛中投入大量资源进行进一步研究。虽然直到几年前，这些助手都是华而不实，但现在数百万用户正在使用它们，并能够利用它们的解决方案。
*   **机器翻译:**你有没有注意到，最近几年，谷歌翻译在为你翻译文本方面变得更加准确了？这要归功于该领域研究取得的最新进展，谷歌翻译为亿万用户提供了数百种语言的机器翻译。
*   在我们今天生活的快节奏的社会中，我们经常没有时间把我们讨论的所有事情都记录下来，无论是商务笔记、电话、演讲等等。现在有相当多的初创公司帮助我们解决这类问题，即把声音作为输入，并为我们提供文本，我们可以在此基础上继续并采取行动。

# 使用自然语言处理的挑战

当然，当使用 NLP 技术时，有相当多的挑战。最重要的是从文本中提取上下文。人类非常擅长理解一个句子的上下文，但计算机只使用统计模型来表示这些句子，所以他们很难理解我们的话到底是什么意思。

例如，当我们说“布什”时，我们可能会提到这种植物或美国前总统。对你来说，识别这种差异可能非常容易，但是计算机必须从流水线开始经历几个步骤，直到决定你使用的是哪一个意思。

NLP 的另一个挑战与第一个挑战有关，即寻找足够的数据来训练我们的模型。与任何其他机器学习模型一样，训练 NLP 模型需要大量数据和大量时间，这意味着只有少数足够大的公司有资源来构建涉及 NLP 的真正强大的应用程序。其他较小的公司采用高度专业化的机器学习模型，这意味着它们只解决所有 NLP 问题的一个子集，为此它们需要少得多的数据。

考虑了所有这些因素后，最终我们正确识别 NLP 模型给我们的业务或应用带来的价值是非常重要的。我们需要看看我们设法建立的模型是否能够真正帮助我们和我们的客户，或者它是否只是一个花哨的功能，以便我们可以说我们是一家机器学习公司。

# 自然语言处理工具

为了开始学习和开发 NLP 模型，有相当多的库可供开发者使用。好的一面是大多数都是开源的。

*   **NLTK —自然语言工具包**是一个主要用于研究和教育的 Python 库。它包括许多准备测试和使用模型的步骤。你可以在他们的[网站](https://www.nltk.org/)上开始使用。
*   **Stanford CoreNLP** 是另一个 Python 库，它为理解自然语言提供了广泛的工具。这里可以看到几个例子[。](https://stanfordnlp.github.io/CoreNLP/index.html)
*   spaCy 是另一个 Python 库，它利用机器学习和深度学习来帮助你实现许多强大的功能。他们的网站是[这里](https://spacy.io/)。

# 摘要

在本文中，我们对自然语言处理领域做了一个简单的介绍。我们已经讨论了构建 NLP 管道的一些基本步骤，然后我们看到了谁以及如何使用自然语言处理来增强他们的业务。然后，我们看了一下使用 NLP 的主要挑战，以及我们可以用来了解 NLP 并可能在我们的应用程序中使用它的一些最佳工具。

*更感兴趣？在 Twitter 上关注我，地址是*[*@ b _ dmarius*](https://twitter.com/b_dmarius)*，我会在那里发布每一篇新文章。*