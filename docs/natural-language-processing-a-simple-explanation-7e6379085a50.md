# 自然语言处理:简单解释

> 原文：<https://towardsdatascience.com/natural-language-processing-a-simple-explanation-7e6379085a50?source=collection_archive---------46----------------------->

## 自然语言处理(NLP)正在迅速发展，并在许多方面改善着我们的生活——下面是一个简单的介绍。

[![](img/9ac9bc7fa66f4e3dcb23ccc3dbb2c7d4.png)](https://highdemandskills.com/natural-language-processing-explained-simply/)

照片由[西德·瓦克斯](https://unsplash.com/@videmusart?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/books?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

# **什么是自然语言处理？**

自然语言处理，简称 NLP，是**专门分析人类语言**的 [**人工智能(AI)**](https://highdemandskills.com/what-is-artificial-intelligence/) **的一种。**

[](https://highdemandskills.com/what-is-artificial-intelligence/) [## 什么是人工智能？-高要求技能

### 人工智能(AI)是一个你可能听说过的术语——它对社会产生了巨大的影响，并且…

highdemandskills.com](https://highdemandskills.com/what-is-artificial-intelligence/) 

NLP 通过以下方式做到这一点:

*   阅读自然语言，这种语言是通过人类的自然使用进化而来的，我们每天都用它来相互交流
*   解释自然语言，通常通过基于概率的算法
*   分析自然语言并提供输出

你有没有用过苹果的 Siri，想知道它是如何理解(大部分)你说的话的？这是 NLP 在实践中的一个例子。

NLP 正在成为我们生活中必不可少的一部分，与机器学习和深度学习一起，产生的结果远远优于几年前可能实现的结果。

在本文中，我们将仔细研究 NLP，看看它是如何应用的，并了解它是如何工作的。

# **自然语言处理能做什么？**

如今，NLP 的使用方式多种多样。其中包括:

## 机器翻译

你上一次访问外国并用智能手机进行语言翻译是什么时候？或许你用过谷歌翻译？这是 NLP 机器翻译的一个例子。

机器翻译通过使用 NLP 将一种语言翻译成另一种语言来工作。历史上，简单的基于规则的方法已经被用来做这件事。但是今天的 NLP 技术是对已经存在多年的基于规则的方法的一个很大的改进。

为了让 NLP 在机器翻译方面表现出色，它采用了深度学习技术。这种形式的机器翻译有时被称为神经机器翻译(NMT)，因为它利用了神经网络。因此，NMT 解释语言的基础上，统计，尝试和错误的方法，可以处理语境和其他微妙的语言。

除了像 Google Translate 这样的应用程序，NMT 还用于一系列商业应用程序，例如:

*   翻译纯文本、网页或文件，如 Excel、Powerpoint 或 Word。Systran 是这样做的翻译服务公司的一个例子。
*   实时翻译社交内容，由专门从事公共部门语言服务的 [SDL 政府](https://www.sdl.com/industries/government/us/)提供。
*   在医疗情况下翻译语言，例如当一名讲英语的医生正在治疗一名讲西班牙语的病人时，由 [Canopy Speak](https://withcanopy.com/speak/) 提供。
*   翻译财务文件，如年度报告、投资评论和信息文件，由专门从事财务翻译的公司提供。

## 语音识别

前面我们提到 Siri 是 NLP 的一个例子。Siri 使用的 NLP 的一个特殊功能是语音识别。Alexa 和 Google Assistant(“ok Google”)是 NLP 语音识别的其他众所周知的例子。

语音识别并不是一门新科学，它已经存在了 50 多年。多亏了 NLP，直到最近它的易用性和准确性才有了显著的提高。

语音识别的核心是识别口语单词、解释它们并将其转换为文本的能力。然后可以采取一系列行动，如回答问题、执行指令或写电子邮件。

NLP 中使用的强大的深度学习方法使今天的语音识别应用程序比以往任何时候都更好地工作。

## 聊天机器人

聊天机器人是模拟人类自然对话的软件程序。它们被公司用来帮助客户服务、消费者查询和销售查询。

上次登录公司网站并使用在线帮助系统时，您可能已经与聊天机器人进行了互动。

虽然简单的聊天机器人使用基于规则的方法，但今天更有能力的聊天机器人使用 NLP 来理解客户在说什么以及如何回应。

聊天机器人的众所周知的例子包括:

*   世界卫生组织(世卫组织)[聊天机器人](https://www.who.int/news-room/feature-stories/detail/who-launches-a-chatbot-powered-facebook-messenger-to-combat-covid-19-misinformation)，建立在 WhatsApp 平台上，分享信息并回答关于新冠肺炎病毒传播的询问
*   《国家地理》的天才聊天机器人，说话像阿尔伯特·爱因斯坦，与用户互动以推广同名的《国家地理》节目
*   Kian 是韩国汽车制造商起亚在 FaceBook Messenger 上的聊天机器人，它回答关于起亚汽车的查询，并帮助销售查询
*   全食超市的[聊天机器人](https://venturebeat.com/2016/07/12/whole-foods-just-launched-a-messenger-chatbot-for-finding-recipes-with-emojis/)，帮助提供食谱信息、烹饪灵感和产品推荐

## 情感分析

情感分析使用 NLP 来解释和分类文本数据中包含的情感。例如，这用于根据正面或负面体验对在线客户关于产品或服务的反馈进行分类。

在最简单的形式中，情感分析可以通过根据传达情感的指定单词对文本进行分类来完成，如“爱”、“恨”、“快乐”、“悲伤”或“愤怒”。这种类型的情感分析已经存在了很长时间，但是由于其简单性，实际应用有限。

今天的情感分析使用 NLP 基于统计和深度学习方法对文本进行分类。结果是情感分析可以处理复杂和自然的声音文本。

如今，全世界的企业都对情感分析产生了浓厚的兴趣。它可以提供对客户偏好、满意度和意见反馈的宝贵见解，有助于营销活动和产品设计。

## 电子邮件分类

电子邮件超载是现代工作场所常见的挑战。NLP 可以帮助分析和分类收到的电子邮件，以便它们可以自动转发到正确的位置。

过去，简单的关键字匹配技术被用来对电子邮件进行分类。这有好有坏。NLP 允许更好的分类方法，因为它可以理解单个句子、段落和整个文本部分的上下文。

鉴于当今企业必须处理的电子邮件数量庞大，基于 NLP 的电子邮件分类可以极大地帮助提高工作场所的生产力。使用 NLP 进行分类有助于确保电子邮件不会被遗忘在负担过重的收件箱中，并被正确归档以供进一步处理。

# **自然语言处理是如何工作的？**

既然我们已经看到了 NLP 能做什么，让我们试着理解它是如何工作的。

本质上，NLP 的工作原理是将一组文本信息转换成指定的输出。

如果应用程序是机器翻译，那么输入的文本信息将是源语言(比如说英语)的文档，输出将是目标语言(比如说法语)的翻译文档。

如果应用是情感分析，那么输出将是输入文本到情感类别的分类。诸如此类。

## NLP 工作流

现代 NLP 是一门混合学科，它借鉴了语言学、计算机科学和机器学习。NLP 使用的流程或工作流有三个主要步骤:

步骤 1 —文本预处理

步骤 2 —文本表示

步骤 3 —分析和建模

每一步都可能使用一系列技术，这些技术随着不断的研究而不断发展。

## 步骤 1:文本预处理

第一步是准备输入文本，以便更容易分析。自然语言处理的这一部分已经很好地建立起来，并且利用了一系列传统的语言学方法。

此步骤中使用的一些关键方法有:

*   **记号化**，将文本分解成有用的单元(记号)。例如，用空格分隔单词，或者用句号分隔句子。标记化也识别经常在一起的单词，例如“纽约”或“机器学习”。例如，句子“客户服务好得不能再好了”的标记化将导致以下标记:“客户服务”、“可能”、“不是”、“是”和“更好”。
*   **规范化**使用像*词干*和*词汇化*这样的技术将单词转换成它们的基本形式。这样做是为了帮助减少“噪音”和简化分析。词干提取通过删除词尾来识别词干。例如，单词“studies”的词干是“studi”。词汇化同样会删除后缀，但如果需要的话也会删除前缀，从而产生自然语言中通常使用的单词。例如，单词“studies”的引理是“study”。在大多数应用中，词汇化比词干化更受欢迎，因为生成的单词在自然语言中有更多的含义。
*   **词性标注**利用了形态学，即研究单词之间的相互关系。单词(或记号)基于它们在句子中的功能被标记。这是通过使用从[文本语料库](https://en.wikipedia.org/wiki/Text_corpus)中建立的规则来识别语音中单词的目的，即。动词、名词、形容词等。
*   **解析**利用句法，或者对单词和句子如何组合的理解。这有助于理解句子的结构，是通过根据语法规则将句子分解成短语来完成的。一个短语可能包含一个名词和一个冠词，如“我的兔子”，或者一个动词，如“喜欢吃胡萝卜”。
*   **语义**确定句子中所用单词的预期含义。单词可以有一个以上的意思。例如，“通过”可以表示(I)实际交出某物，(ii)决定不参加某事，或(iii)衡量考试成功。通过查看单词前后出现的单词，可以更好地理解单词的意思。

## 步骤 2:文本表示

为了使用机器和深度学习方法分析文本，需要将其转换为数字。这就是文本表示的目的。

此步骤中使用的一些关键方法有:

## 一袋单词

单词包(Bag of words，简称 BoW)是一种表示文本的方法，它通过计算每个单词在输入文档中出现的次数，与已知的参考单词列表(词汇表)进行比较。

结果是一组向量，包含描述每个单词出现次数的数字。这些向量被称为“包”，因为它们不包含任何关于输入文档结构的信息。

为了说明 BoW 是如何工作的，考虑例句“猫坐在垫子上”。这包含单词“the”、“cat”、“sat”、“on”和“mat”。这些单词的出现频率可以用[2，1，1，1，1]形式的向量来表示。这里，单词“the”出现两次，其他单词出现一次。

当与大词汇量相比较时，向量将扩展到包括几个零。这是因为词汇表中所有不包含在例句中的单词都没有出现频率。得到的矢量可能包含大量的零，因此被称为“稀疏矢量”。

BoW 方法相当简单易懂。然而，当词汇表很大时，得到的稀疏向量可能非常大。这导致计算上具有挑战性的向量不包含太多信息(即大多为零)。

此外，BoW 会查看单个单词，因此不会捕获任何关于单词组合的信息。这导致后面分析的上下文丢失。

## 一袋 n-克

使用 BoW 减少上下文丢失的一种方法是创建成组单词的词汇表，而不是单个单词。这些分组的单词被称为“n 元语法”，其中“n”是分组大小。由此产生的方法被称为“n-grams 袋”(BNG)。

BNG 的优势在于，每个 n-gram 比单个单词捕捉到更多的上下文。

在前面的例句中，“sat on”和“the mat”是 2-gram 的例子，“on the mat”是 3-gram 的例子。

## TF-IDF

计算一个单词在文档中出现的次数的一个问题是，某些单词开始在计算中占主导地位。像“the”、“a”或“it”这样的词。这些词经常出现，但不包含太多信息。

处理这种情况的一种方法是将文档中频繁出现的单词与唯一出现的单词区别对待。频繁出现的单词往往是像“The”这样的低值单词。这些单词的计数可以被扣分以帮助降低它们的优势。

这种方法被称为“术语频率—逆文档频率”或 TF-IDF。术语频率查看一个词在给定文档中的频率，而逆文档频率查看该词在所有文档中的稀有程度。

TF-IDF 方法的作用是淡化频繁出现的单词，并突出具有有用信息的更独特的单词，如“cat”或“mat”。这可以带来更好的结果。

## 单词嵌入

一种更复杂的文本表示方法包括单词嵌入。这将每个单词映射到单独的向量，其中向量倾向于“密集”而不是“稀疏”(即。更小并且具有更少的零)。在映射过程中会考虑每个单词及其周围的单词。由此产生的密集向量允许更好地分析和比较单词及其上下文。

单词嵌入方法使用强大的机器学习和深度学习来执行映射。这是一个不断发展的领域，已经产生了一些出色的成果。目前使用的关键算法包括 Word2Vec、GloVe 和 FastText。

## 步骤 3:分析和建模

NLP 过程的最后一步是对通过步骤 1 和 2 生成的向量进行计算，以产生所需的结果。这里使用了机器学习和深度学习的方法。来自非 NLP 领域的许多相同的机器学习技术，如图像识别或欺诈检测，可用于此分析。

考虑情绪分析。这可以使用监督或无监督的机器学习来完成。有监督的机器学习需要预先标记的数据，而无监督的机器学习使用预先准备的精选单词(词典)数据库来帮助对情感进行分类。

使用机器学习，使用概率方法对输入文本向量进行分类。这是通过训练模型(监督机器学习)或通过与合适的词典进行比较(非监督机器学习)来完成的。

结果是基于通过机器学习过程生成的概率的情感分类。

# **结论**

NLP 发展迅速，对社会的影响越来越大。从语言翻译到语音识别，从聊天机器人到识别情感，NLP 正在提供有价值的见解，并使我们的生活更加富有成效。

现代 NLP 通过使用语言学、计算机科学和机器学习来工作。近年来，NLP 已经产生了远远超过我们过去所看到的结果。

自然语言处理的基本工作流程包括文本预处理、文本表示和分析。如今使用了多种技术，并且随着研究的进行，更多的技术正在开发中。

NLP 承诺将彻底改变工业和消费者实践的许多领域。它已经成为我们日常生活中熟悉的一部分。

有了 NLP，我们有了一种强大的方式，通过一种我们天生熟悉的媒介——我们通过自然语言交流的能力——来参与数字未来。

[](https://highdemandskills.com/blog/) [## 博客-高要求技能

### 阅读那些需求量很大的技能，这些技能可以让你更有生产力和效率，并且可以帮助你实现你的…

highdemandskills.com](https://highdemandskills.com/blog/)