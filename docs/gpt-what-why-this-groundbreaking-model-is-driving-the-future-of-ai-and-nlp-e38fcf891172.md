# GPT-怎么了？OpenAI 开创性的新 NLP 模型的非技术性指南

> 原文：<https://towardsdatascience.com/gpt-what-why-this-groundbreaking-model-is-driving-the-future-of-ai-and-nlp-e38fcf891172?source=collection_archive---------33----------------------->

![](img/5f16f15d8d1dc7f6921aebb43d11ee74.png)

图片由 Unsplash.com 提供

## 周末期间，推特上对 GPT 3 号的炒作达到了历史新高，许多人将这一技术发展称为未来人工智能研究的突破性拐点。在这篇文章中，我探索了什么是 GPT，它对人工智能发展意味着什么，以及我们可能从这里走向何方。

OpenAI 的 GPT-3 语言模型上周获得了极大的关注，让许多人相信这项新技术代表了自然语言处理(NLP)工具发展的一个重要转折点。那些通过 OpenAI 的测试程序获得早期 API 的人去 Twitter 展示了使用 GPT-3 技术构建的令人印象深刻的早期工具:

对于非工程师来说，这可能看起来像魔术，但这里有很多东西需要解开。在这篇文章中，我将提供一个 GPT 和它可以用来做什么的简要概述。

**什么是 OpenAI 和 GPT-3？**

OpenAI 是一个人工智能研究实验室，由埃隆·马斯克、萨姆·奥特曼等人于 2015 年创立，其使命是创造造福全人类的人工智能。该公司最近在 2019 年获得了微软 10 亿美元的额外资金，被认为是人工智能研发的领导者。

从历史上看，获得大量的标记数据来训练模型一直是 NLP 开发(以及一般人工智能开发)的主要障碍。通常，这可能非常耗时且昂贵。为了解决这个问题，科学家们使用了一种叫做[迁移学习](https://heartbeat.fritz.ai/pre-trained-machine-learning-models-vs-models-trained-from-scratch-63e079ed648f#f3f6)的方法:使用在先前训练的模型中学习到的现有表示/信息作为起点，为不同的任务微调和训练新的模型。

例如，假设你想学习一门新的语言——德语。最初，你仍然会用英语思考你的句子，然后翻译和重新排列单词，得出德语的对等词。事实是，即使实际的单词和语法是不同的，你仍然在间接地应用从以前的语言中学到的句子结构、语言和交流。这就是为什么如果你已经知道另一种语言，学习新的语言通常会更容易。

将这种策略应用于 AI 意味着我们可以使用预训练的模型，用更少的训练数据更快地创建新模型。在这个[伟大的演练](https://blog.keras.io/building-powerful-image-classification-models-using-very-little-data.html)中，Francois Chollet 比较了从零开始训练的人工智能模型和从预训练模型构建的模型的有效性。他的结果显示，在用相同数量的训练数据训练两者后，后者的预测准确性提高了 15%。

2018 年，OpenAI 提交了[令人信服的研究](https://openai.com/blog/language-unsupervised/)，显示这种策略(将监督学习与无监督预训练配对)在 NLP 任务中特别有效。他们首先使用“未标记文本的多样化语料库”(即来自各种流派的超过 7000 本独特的未出版书籍)产生了一个生成性预训练模型(“GPT”)，本质上创建了一个“理解”英语和语言的模型。接下来，这个预训练的模型可以进一步微调和训练，以使用监督学习来执行特定的任务。打个比方，这就像教某人英语，然后训练他或她阅读和分类可接受和不可接受的求职者的简历。

GPT-3 是 GPT 模型的最新版本，于 2020 年 5 月在[首次描述。它包含 175 *亿*个参数，相比之下 GPT-2 中有 15 亿个参数(增加了 117 倍),训练它消耗了](https://arxiv.org/abs/2005.14165)[几千万亿次/秒-天](https://www.theregister.com/2020/06/01/ai_roundup_290520/)的计算能力。与 GPT-2 相比，GPT-3 提供了更多的数据，调整了更多的参数，因此，到目前为止，它已经产生了一些惊人的 NLP 能力。所需的大量数据和计算资源使得许多组织不可能重现这一点，但幸运的是他们不必如此，因为 OpenAI 计划在未来通过 [API](https://openai.com/blog/openai-api/) 发布访问。

**关键接待**

诚然，GPT-3 并没有得到太多的关注，直到上周沙里夫·沙米姆和其他人的病毒推文(见上图)。他们展示了 GPT-3 可以用来创建基于简单英语指令的网站，设想了一个无代码技术的新时代，人们可以通过简单的文字描述来创建应用程序。早期采用者凯文·拉克尔[用图灵测试测试了模型](http://lacker.io/ai/2020/07/06/giving-gpt-3-a-turing-test.html)，看到了惊人的结果。GPT-3 在最初的 Q & A 中表现异常出色，展示了人工智能系统传统上与之斗争的“常识”的许多方面。

然而，该模型远非完美。Max Woolf 执行了一项[批判性分析](https://minimaxir.com/2020/07/gpt3-expectations/)，指出了几个问题，如模型延迟、实施问题以及需要重新考虑的数据偏差。一些用户也在 Twitter 上报告了这些问题:

OpenAI 的博客讨论了该模型的一些关键[缺陷](https://openai.com/blog/language-unsupervised/)，最值得注意的是 GPT 对世界的全部理解都是基于它接受训练的文本。例证:它是在 2019 年 10 月接受训练的，因此不了解新冠肺炎。不清楚这些文本是如何选择的，以及在这一过程中进行了(或要求)什么样的监督。

此外，生产和维护这些模型所需的巨大计算资源引发了关于人工智能技术对环境影响的严重问题。虽然经常被忽视，但硬件和软件的使用都极大地导致了能源资源的枯竭、过多的废物产生以及稀土矿物的过度开采，从而对人类健康产生了相关的负面影响。

为了平息人们的担忧，OpenAI 一再声明其使命是为了人类的利益开发人工智能，并打算在发现滥用时停止访问其 API。即使在测试版中，它也要求候选人描述他们对该技术的意图以及对社会的好处和风险。

我们将何去何从？

毫无疑问，GPT-3 仍然代表着人工智能发展的一个重要里程碑。许多早期用户已经建立了令人印象深刻的应用程序，这些应用程序可以准确地处理自然语言并产生惊人的结果。总而言之:

1.  GPT 3 号是对 GPT 2 号的重大改进，具有更高的精确度和更好的使用情况。这是人工智能发展向前迈出的重要一步，仅用了两年时间就令人印象深刻地完成了
2.  建立在 GPT-3 上的早期工具显示了商业可用性的巨大前景，例如:允许你通过描述来构建应用的无代码平台；使用简单英语的高级搜索平台；以及更好的数据分析工具，使数据收集和处理速度更快
3.  OpenAI 宣布计划发布一个[商业 API](https://openai.com/blog/openai-api/) ，这将使组织能够大规模构建由 GPT-3 驱动的产品。然而，关于如何具体实施仍存在许多问题，如定价、SLA、模型延迟等。
4.  用户指出了在广泛商业使用之前需要解决的几个问题。模型中固有的偏见，围绕公平和道德的问题，以及对滥用(假新闻、机器人等)的担忧。)需要深思熟虑，监督可能是必要的
5.  OpenAI 公开[承诺](https://openai.com/about/)为了人类的利益创造人工智能，但是，大规模监控滥用将很难实现。这引发了一个更广泛的问题，即政府参与保护个人权利的必要性(T4)

总之，我非常兴奋地看到哪些新技术建立在 GPT 3 号上，以及 OpenAI 如何继续改进其模型。对 NLP 和 GPT-3 越来越多的关注和资助可能足以抵御许多批评家的恐惧，他们担心一个[人工智能的冬天可能会到来](https://mindmatters.ai/2020/01/so-is-an-ai-winter-really-coming-this-time/)(包括我自己)。尽管该模型存在不足，但我希望每个人都能对未来持乐观态度，在未来，人类和机器将以统一的语言相互交流，数十亿人将能够使用技术创造工具。