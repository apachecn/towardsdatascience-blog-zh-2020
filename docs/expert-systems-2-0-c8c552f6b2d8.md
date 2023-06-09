# 专家系统 2.0

> 原文：<https://towardsdatascience.com/expert-systems-2-0-c8c552f6b2d8?source=collection_archive---------32----------------------->

## 神经网络如何使程序知识大众化

![](img/0ed3a27757527f34bd41b5089bf2ca65.png)

在 [Unsplash](https://unsplash.com/s/photos/ai-music?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上由 [Franck V.](https://unsplash.com/@franckinjapan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄的照片

神经网络和深度学习是最终打开人工智能之路的钥匙吗，还是我们正处于另一个 [AI Winter](https://en.wikipedia.org/wiki/AI_winter) 的边缘？

如果你是企业家，那么答案是:**没关系**。你的资助并不依赖于资助者对你的研究议程——制造一个会说话的机器人——感到兴奋。这取决于为真实的人提供真实的价值。

事实是，尽管人工智能的发展到目前为止还没有制造出可以与我们自己的智能相媲美的机器，但沿着这条道路发展起来的技术都非常有用，并且充满了潜在价值。虽然看起来神经网络*本身*不足以构建最智能的系统，但它们丰富我们生活的全部潜力尚未得到充分挖掘。

今天，我想提醒我们所有人一项来自人工智能前一个时代的有用且相关的技术:[专家系统](https://en.wikipedia.org/wiki/Expert_system)。虽然不再是一个迷人的研究海报的孩子，这项技术已经对社会产生了持久的影响。即使没有强化学习、培训课程和其他前沿创新，神经网络也准备做同样的事情。

正如我们将看到的，正如专家系统基于描述性知识自动进行推理一样，神经网络也可以对程序性知识做同样的事情。与商业专家系统不同，商业专家系统在很大程度上掌握在企业手中，我们随时准备让所有人都可以使用神经网络系统。

## 专家系统:综述

专家系统至少需要两个组件才能运行:

1.  知识库
2.  推理机

知识库存储命题——这些命题是经过编码的信息——而推理机使用[推理规则](https://iep.utm.edu/prop-log/#H5)来推导新的命题。

显然，建立专家系统的一个主要挑战是建立知识库所需的知识获取。领域专家通常需求量很大，而他们自己通常缺乏整理自己知识的能力。这意味着构建知识库是程序员和专家之间耗时的协作。

然而，这种专业知识的缺乏也是专家系统有价值的原因。一旦编码，知识库很容易转移，并且不会过期。它可以被无休止地复制，并在许多应用程序中使用。专家系统将困难的技术推理和知识查找自动化，以换取前期投入的时间和精力。

毫不奇怪，专家系统通常出现在医学、法律和其他需要对事实和程序有明确的专业知识的领域。

由于它们是一项成熟的技术，与其学习技术细节，不如对它们的*目的*、*需求*和*相关性*有一个整体的了解，这会更好地为您服务。当讨论神经网络时，我们将回到这三个因素，所以请记住它们。

我们已经介绍了目的和要求…

**目的:**专家系统利用明确的事实和推理规则自动推理。

**需求:**构建或更新专家系统需要领域专家的时间和知识，以及用代码表示这些知识的能力。

那么，专家系统还有意义吗？当然可以。

虽然现在很少能找到明确称为“专家系统”的软件，但知识表示和推理的思想和实现仍在大量使用。例如， [ROSS](https://www.ibm.com/blogs/watson/2016/01/ross-and-watson-tackle-the-law/) ，一个由 [IBM Watson](https://www.ibm.com/watson) 支持的法律系统，结合了一个巨大的知识库和更现代的从自然语言处理领域过滤相关信息的方法。

此外，许多[语音接口](https://en.wikipedia.org/wiki/Voice_user_interface)，将声音输入映射到意图，但有一个固定的[意图](https://cloud.google.com/dialogflow/docs/intents-overview)和响应规则库，类似于旧的专家系统。这些新系统不是自动化需要专业知识的高度专业化的任务，而是自动化更日常的事情，如检查账户余额，同时被打包在一个被认为更智能的接口中(但通常也是硬编码的)。

总之…

**相关性**:虽然专家系统背后的思想很少作为独立产品出现，但它们对软件产生了持久的影响，并且一直沿用至今。

## 描述性知识与程序性知识

在继续讨论神经网络之前，我想快速了解一下我们人类可以拥有的知识类型的区别:描述性知识和程序性知识之间的区别。

[描述性](https://en.wikipedia.org/wiki/Descriptive_knowledge)(也称*显性*或*陈述性*)知识，采取事实和规则的形式。它通常可以用文字或符号来表示，并使用逻辑或其他演算来操作。

[程序性](https://en.wikipedia.org/wiki/Procedural_knowledge)(也叫*隐性*或*表现性*)知识，更多的是关于[知道](https://plato.stanford.edu/entries/knowledge-how/)*如何去做事。它通常与直觉、肌肉记忆和实践等概念联系在一起。*

*想想骑自行车需要什么。当然，你知道你坐下来，把你的脚放在踏板上，这个动作会保持自行车直立。但是更重要的是知道如何骑自行车，这需要练习。这样，骑自行车就有了更多的程序成分。*

*另一方面，考虑找出三角形的缺角，给定一些长度和角度。在这里，得到解的过程要清楚得多，可能涉及到三角恒等式之类的东西。如果需要，每一步都可以写在纸上。这个问题需要更多的描述性知识。*

*当然，许多复杂的任务需要知识类型的混合，这种区分比它必然地指示一个深层的机械真理更方便。然而，我们会看到，在考虑神经网络的潜在应用时，记住这一区别是有用的。*

## *神经网络和软件 2.0*

> *事实证明，现实世界中的大部分问题都有这样一个特性，即收集数据(或者更一般地说，确定一个理想的行为)比显式地编写程序要容易得多安德烈·卡帕西，[软件 2.0](https://medium.com/@karpathy/software-2-0-a64152b37c35)*

*你可能已经注意到上面的*描述性知识*是构成专家系统的*知识库*和*推理规则*的那种东西。*

*如何为程序性知识建立一个知识库？嗯，这将是非常困难的，尤其是因为即使是这些领域的专家也很难准确地表达他们自己的专业知识。*

*也就是说，使用传统的编程方法是非常困难的。*

*机器学习模型将范式从程序员必须提供规则和输入以获得结果的范式转变为程序员可以提供输入和结果以导出规则的范式。那就是:*

***软件 1.0:** 输入+规则→结果*

***软件 2.0:** 输入+结果→规则*

*软件 1.0 的成分非常类似于专家系统所需的知识库和推理机。软件 2.0 的承诺是，任何人使用该软件都可以将学到的规则应用到许多新的输入中，而不需要他们自己拥有得出结果所需的专业知识。*

*我们可以看到这是如何暗示由神经网络和深度学习驱动的新一代专家系统的，其目的、要求和相关性如下。*

***目的:**专家系统 2.0 将通常需要专业培训和实践的决策和感知自动化，在该领域，专业知识更多的是程序性的，而不是描述性的。*

***需求:**要建立这样的系统，需要建立一个数据集，让专家运用他们的知识做出判断(例如，作者给创造性写作打分)。更新这样的系统只需要更新数据集。*

***相关性:**专家系统 2.0 已经准备好将过程专家民主化，几乎不需要进一步的技术创新。*

*正如旧的专家系统一样，知识获取仍然需要领域专家的时间和注意力。然而，建立一个机器学习数据集仅仅需要他们*练习*他们的手艺，而不是解构它。此外，对于工程师来说，在数据集中表示这些知识比想出编码和操作符号知识的方法要容易得多。最后，随着数据集随着时间的推移而增长和发展，更新和改进模型可以更顺利地完成。*

## *识别专家系统 2.0 的机会*

*如果一项任务需要程序多样性的专业知识，那么使用深度学习实现自动化的时机已经成熟。许多创造性学科符合这一描述——音乐、舞蹈、艺术等。*

*2018 年，谷歌艺术与文化实验室(Google Arts & Culture Lab)制作了 [Living Archive](https://www.youtube.com/watch?v=qshkvUOc35A&feature=emb_logo) ，这是一个经过训练可以预测韦恩·麦格雷戈(Wayne McGregor)舞蹈动作的模型，因此可以用来建议舞蹈编排。*

*在技术方面，*评估*的表演和作品要比*合成*新的表演和作品容易得多。像 [SmartMusic](https://www.smartmusic.com/) 这样的软件能够对音频录音的语调和节奏等方面进行评分。然而，这些事情可以使用硬编码的规则来检测和分析。在音乐等领域，真正的价值来自于模特为诸如 dynamics 和 rubato 等更微妙、更具解释性的元素配乐。*

*如果人类专家可以在几秒钟内做出决定，然后有时间解释他们到底是如何做出决定的，那么捕捉数百万个这样的决定将使我们走向一台可以做同样事情的机器。*

*正如人工智能技术的理想一样，专家系统 2.0 将扩大和民主化人类智能，而不是使其过时。人们仍然应该每周去上小提琴或舞蹈课，但他们也可以即时获得有效的反馈，即使他们的老师不在他们面前。缩短反馈的距离将大大加快学习。*

*现在，为什么我说基于深度学习的系统将*民主化*专业知识，而这对于旧的专家系统来说并不是真的？这里有几个因素在起作用:*

*   *旧的专家系统通常被设计在错误代价很高的领域——法律、药物设计、医学诊断——因此民主化的价值较低。*
*   *自从有了互联网，我们的文化已经转向重视信息的公开获取。*
*   *与上述相关，[获得技术](https://www.pewresearch.org/internet/fact-sheet/mobile/)的机会比以往任何时候都多。*

*神经网络和深度学习可能只是通往人工智能的垫脚石，但这并不意味着它们没有直接的价值。*

*通过以专家系统自动化描述知识的方式自动化和民主化程序知识，神经网络可以改善我们对专业知识的获取，并永远增强我们的学习方式。他们的价值才刚刚开始被意识到。*