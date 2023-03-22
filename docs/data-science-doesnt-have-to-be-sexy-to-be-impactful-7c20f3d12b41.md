# 数据科学不一定要性感才能有影响力

> 原文：<https://towardsdatascience.com/data-science-doesnt-have-to-be-sexy-to-be-impactful-7c20f3d12b41?source=collection_archive---------44----------------------->

![](img/df1525666dd736bc1c4065c92c4564c7.png)

数据科学不仅仅是机器人和人工智能助手。Unsplash 上 [Photos 爱好的照片](https://unsplash.com/@photoshobby)。

## 2020 年格蕾丝·赫柏庆典

今年 9 月 29 日至 10 月 3 日，来自 115 个国家的 30，000 名技术人员聚集在一起参加[格蕾丝·赫柏庆典](https://ghc.anitab.org/)，这是一个女性学习、交流和庆祝其技术成就的年度会议。我很幸运地成为与会者之一，我从那里的大量讲座中学到了很多东西——从如何评估创业想法，到下一代人工智能硬件如何工作，到打击刻板印象威胁和冒名顶替综合症，到使用一种特殊的基于时间的神经网络来教机器人自动驾驶，我已经在之前的帖子中[写过这些。](/learning-about-spiking-neural-networks-for-time-based-data-at-the-grace-hopper-celebration-2020-68ba58fac5bb)

## 在数据科学的未开发领域建立伟大的职业生涯

有一件事是我没有预料到的，那就是我最喜欢的演讲之一来自并不令人兴奋的会计软件领域。但我想写的是我参加的 Intuit 两位高级数据科学家的演讲，因为这是我见过的最好的例子之一，说明了一个最初看起来很平凡的任务实际上可以成为一个非常迷人和复杂的数据科学项目。

> 尝试在目前“热门”的领域寻找数据科学角色确实很有诱惑力…但令人惊叹的职业生涯可以超越目前被认为是数据科学中性感或迷人的话题。

我们都听说过“数据科学家是 21 世纪最性感的工作”这句恶名昭彰的话，这句话出自 2012 年《哈佛商业评论》一篇文章的标题。即使在这个“性感”的工作中，机器学习的“性感”部分也往往会得到所有的关注，就像我上面提到的自主机器人。但在不那么迷人的部分(包括会计软件)，也有一些真正伟大的工作正在进行，这些工作可能以各种意想不到的方式引人入胜并具有挑战性。

我认为，对于正在开始数据科学职业生涯的读者来说，这是特别重要的一点。尝试在媒体目前“热门”的领域寻找数据科学角色可能真的很有诱惑力，比如[自动驾驶汽车](https://www.embedded.com/the-role-of-artificial-intelligence-in-autonomous-vehicles/)、[语言](https://openai.com/blog/openai-api/)和[图像](https://github.com/NVlabs/stylegan)生成模型、[人工智能助手](https://voicebot.ai/2019/10/05/what-are-virtual-assistants/)，或者任何工作描述中大量掺杂“前沿”一词的领域。

但是，惊人的职业生涯可以超越目前被认为是数据科学中性感或迷人的话题。一些最有影响力的工作发生在传统行业或数据科学领域相对较新的行业，如法律、房地产或会计。

这些都是巨大的行业，有巨大的需求和现有的用户群，以及数据科学和机器学习应用的巨大潜力。因此，绿地项目有大量的机会，即使很小的改进和效率也可以产生真正有影响力的结果，并增加巨大的价值。

最重要的是，像这样的项目也很有趣。我自己也做过一些，但是我想在这里讨论的是一个更清晰的例子。表面上看起来相对简单的分类模型实际上是一项大数据科学事业，涉及一系列复杂的数据处理、多种不同的机器学习模型和定制的评估技术。

# Chi-chat:一个度量驱动的最佳频道推荐用户协同框架

*本次演讲由 Intuit 高级数据科学经理范和高级数据科学家文瑶主讲*

## 看似复杂的数据科学项目

这个例子来自为个人和企业制作会计和其他财务软件的 Intuit。当客户联系客户服务时，他们有三种与他人通话的方式可供选择——拨打电话、实时聊天或预定回拨。不同的方法适合不同类型的问题。例如，实时聊天很受欢迎，适合简单的标准问题，但如果你有一个更复杂的问题，就不那么好了。

因此，当客户有问题时，任务就是推荐他们应该使用三个渠道中的哪一个。总体目标是将用户行为导向最有助于他们的渠道，以提高客户满意度并缩短处理时间。这听起来相当简单——这只是一个分类任务，对吗？不对。事实上，这个看似简单的问题原来是一个复杂而有趣的数据科学项目，涉及多个不同的机器学习模型和一堆其他考虑因素。

> 在进行有影响力的工作方面(这应该是每个数据科学家的最终目标)，该项目将帮助数百万客户以最适合他们的方式获得他们需要的帮助。

## 项目步骤

首先，你有杂乱的训练数据，以成千上万个客户问题的形式发给客户服务。每个客户及其需求都是独一无二的，不同代理的反应也各不相同。在**步骤 1** 中，数据科学家必须使用自然语言处理进行文本预处理来准备这个问题数据。除了删除停用词等标准内容，这还包括映射首字母缩写词、自定义拼写检查模块(包括与 Covid 相关的关键字，如“刺激支票”和特定于税务软件的术语，如“TurboTax ”),以及标准化税务表单名称的格式(事实证明这非常复杂)。

接下来，在**步骤 2** 中，他们使用了一个名为 sent2vec 的模型，将问题表示为句子嵌入的集合。这是基于一个奇妙的单词嵌入模型，叫做[word 2 vec](https://radimrehurek.com/gensim/models/word2vec.html)——如果你还不熟悉这个，我强烈推荐你去看看。Word2vec 可以用于将大量的单词缩减为少量的特征，这些特征基本上代表了单词的共享上下文。语料库中的每个单词然后可以以向量(也称为单词嵌入)的形式来表示，该向量对于这些共享特征中的每一个都具有值。Sent2vec 通过取句子中单词嵌入的平均值，将这些单词嵌入转换成句子嵌入。这将创建一个向量，它表示您创建的 n 维空间中的句子，其中 n 是嵌入特征的数量。

然后，在**步骤 3** 中，他们使用 k-means 聚类来基于这些句子嵌入以及一些给出用户上下文的特征(包括他们的操作系统、平台和语言)对问题进行聚类。在**第 4 步**中，他们通过使用这些上下文特征进行客户合作，对此进行了补充。

接下来，在**步骤 5** 中，他们进行了度量驱动的集群标记，以确定要使用的正确通道，这也涉及统计显著性测试(姑且称之为**步骤 5.5** )。这被证明是一个重大的技术挑战，因为他们有多个指标需要优化—客户满意度、效率、案例解决率和客户偏好。让事情变得更加复杂的是，一些指标相互冲突。例如，在案例解决时间上得分很低的更长的电话通常会导致更高的客户满意度。

![](img/dda3d02211e980c162ea7a506de4cdca.png)

最高优先级的指标是客户满意度。图片来自[维基媒体](https://commons.wikimedia.org/wiki/File:Customer_Satisfaction.png)。

为了给正确的频道分配标签，他们使用了一种非常有趣的基于指标优先级的分级顺序方法。例如，客户满意度是他们最重要的衡量标准。因此，他们首先进行了一个双样本 t 检验，以确定净推销商得分(一个常用的客户满意度指标)。如果结果是显著的(即，如果一个通道在这种情况下明显更好)，他们会推荐具有更好指标的通道。如果没有，他们会转到下一个指标，如案件处理时间，并重复这一过程，以此类推每个指标。

这些示例将提供基于指标的建议。如果这些指标都不重要，但用户偏好率很重要，那么他们会给出基于偏好的建议，例如，如果客户倾向于为特定类型的问题安排回电。如果结果在任何指标上都不显著，他们会默认为实时聊天，因为这是最受欢迎的渠道。

最后，在**步骤 6** 中，他们根据满意度、联系解决方案和通话效率进行了 A/B 测试，以确定该模型是否比当前情况有所改进(用户可以选择自己的沟通方式，无需推荐)。在这种情况下，A 中的频道是随机排序的，而 B 中的频道是由机器学习模型推荐的。基于 ML 的推荐在所有指标上都表现得更好。他们还输出模型推荐的强度，以指定它是强推荐还是弱推荐，并发现当模型有信心时，客户体验改善得更多。

> 科学或主题听起来有多性感或前沿并不重要。重要的是增加价值，产生影响，并建立帮助人们和解决问题的东西——你可以在任何领域工作。

## 有影响力的数据科学

总之，尽管一开始看起来像是一个相对简单的项目，但这项任务涉及复杂的数据预处理、单词和句子嵌入的 NLP 模型、聚类模型、客户协同分类、统计显著性测试、基于度量层级的标签的复杂解决方案以及 A/B 测试。在进行有影响力的工作方面(这应该是每个数据科学家的最终目标)，该项目将帮助数百万客户以最适合他们的方式获得他们需要的帮助。还不错。

因此，下次你发现自己在阅读数据科学工作清单，或者被要求从事一个听起来不像是世界上最迷人的数据科学主题的项目时，请记住，无论科学或主题听起来多么性感或前沿。重要的是增加价值，产生影响，并建立帮助人们和解决问题的东西——你可以在任何领域工作。