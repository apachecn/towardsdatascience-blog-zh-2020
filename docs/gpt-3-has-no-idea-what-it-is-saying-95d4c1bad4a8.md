# GPT 3 号不知道自己在说什么

> 原文：<https://towardsdatascience.com/gpt-3-has-no-idea-what-it-is-saying-95d4c1bad4a8?source=collection_archive---------59----------------------->

## OpenAI 的大规模 GPT-3 语言模型产生了令人印象深刻的文本，但仔细分析表明，它的事实都是错误的。

![](img/977679f9c2bf0d24e76fb1a406bfd541.png)

照片:Bakalavar/Dreamstime

想象一下，我们将一艘机器人控制的宇宙飞船发射到银河系的遥远地方，与其他生命形式联系。在船上，我们在互联网上放了一份过去三年所有文本的副本，这样聪明的外星种族就能了解我们的一些情况。在航行了 12 光年之后，飞船进入了卢伊滕星周围的太阳系，在那里外星人登上了飞船。路易坦尼人检索互联网文本的副本，并试图理解它。

他们请顶级语言学家解释这些奇怪的符号，但进展甚微。吕特尼人的地位与十八世纪考古学家相同，他们不断发现带有古埃及象形文字的石头。最后，在 1799 年，考古学家发现了罗塞塔石碑，上面既有埃及象形文字，也有古希腊文字。因为他们有两种语言的同一个法令，他们最终能够理解象形文字的意思。

但我们的吕特尼就没这么幸运了。互联网文本包含英语、法语、俄语和其他语言，但当然没有吕特尼语文本。

他们最多只能分析文本中符号的统计模式。通过这种分析，他们能够生成具有相似统计模式的新文本。例如，他们生成了这段文字:

据《华盛顿邮报》报道，经过两天的激烈辩论，联合卫理公会已经同意进行历史性的分裂——预计最终将产生一个新教派，一个“在神学和社会上保守”的教派。参加 5 月份教会年度大会的大多数代表投票加强了对 LGBTQ 神职人员的任命禁令，并制定了新的规则，将“约束”主持同性婚礼的神职人员。但是那些反对这些措施的人有了一个新计划:他们说他们将在 2020 年前成立一个独立的教派，称他们的教堂为基督教卫理公会教派。《华盛顿邮报》指出，该教派声称有 1250 万成员，在 20 世纪初是“美国最大的新教教派”，但近几十年来一直在萎缩。新的分裂将是教会历史上的第二次。第一次发生在 1968 年，当时大约 10%的教派离开，成立了福音联合弟兄会。《华盛顿邮报》指出，拟议的分裂“发生在教会的关键时刻，教会多年来一直在失去成员，”教会“被推到了 LGBTQ 人士在教会中的角色分裂的边缘。”同性婚姻并不是教会分裂的唯一问题。2016 年，该教派在跨性别神职人员的任命问题上出现分歧，北太平洋地区会议投票禁止他们担任神职人员，南太平洋地区会议投票允许他们担任神职人员。

吕特尼人不知道这种产生的文字是什么意思，他们想知道这对创造这种文字的种族是否有意义。

这段文字实际上是由有史以来最大的机器学习系统 [GPT-3](https://arxiv.org/pdf/2005.14165.pdf) 创建的。GPT-3 由 [OpenAI](https://openai.com/) 开发，该公司已获得数十亿美元的资金，用于创建人工通用智能(AGI)系统，该系统可以获取常识性的世界知识和常识性的推理规则。GPT-3 有 1750 亿个参数，据报道[花费](https://www.digitaltrends.com/features/openai-gpt-3-text-generation-ai/#:~:text=It%20reportedly%20cost%20around%20%2412%20million%20to%20train.)1200 万美元来训练。

# GPT-3

OpenAI 团队使用 GPT-3 生成了 80 条如上图所示的文本，并将这些文本与人们生成的新闻文本混合在一起。他们做了一项研究，要求使用亚马逊的机械土耳其人招募的工人确定每篇文章是由人还是计算机生成的。GPT-3 生成的文章被识别为机器生成的概率为 52%，比随机生成的概率仅高 2%。从本质上讲，这些被雇佣的工人无法区分人类生成的文本和 GPT-3 生成的文本。事实上，上面显示的新闻文章被 88%的员工认为是人为的。

像 GPT-3 这样的文本统计模型被称为 [**语言模型**](https://www.aiperspectives.com/lm) 。GPT 3 是一系列日益强大的语言模型中的最新一个。2018 年发布的[首款 GPT 车型](https://cdn.openai.com/research-covers/language-unsupervised/language_understanding_paper.pdf)，拥有约 1.5 亿个参数。2019 年发布的 GPT-2 拥有 15 亿个参数，比最初的 GPT 多一个数量级，但比 GPT-3 少两个数量级。

一些研究人员提出，语言模型以某种方式神奇地学习关于世界的常识，并基于这些常识学习推理。他们认为语言模型可以利用这些常识和推理来生成文本。更重要的是，这种常识性的知识可以作为发展 AGI 能力的基础。

# 事实核查

然而，尽管 GPT-3 生成的文章听起来似乎有理，但如果你试图验证 GPT-3 生成的上述文本中的事实，你会很快意识到大多数重要事实都是错误的。真正发生的是 2020 年 1 月的一个新闻故事，被许多新闻媒体报道，包括[华盛顿邮报](https://www.washingtonpost.com/religion/2020/01/03/united-methodist-church-is-expected-split-over-gay-marriage-disagreement-fracturing-nations-third-largest-denomination/)。这个故事是，联合卫理公会的官员提议将教会拆分，将在 2020 年 5 月的大会上投票表决。

《GPT 协议 3》的文章可能从这些新闻文章中获得了大部分的单词模式。然而，GPT-3 将这些单词模式合并成了大部分事实都是错误的句子:

*   大会每四年举行一次，而不是每年一次。
*   培训时，大会投票定于 2020 年 5 月。这还没有发生。
*   约束神职人员的新规则还没有被投票表决。然而，之前提出的一系列规则引发了分歧讨论。
*   1968 年的分裂从未发生过。事实上，1968 年的事件是合并，而不是分裂。
*   教会不会将会员大会(或任何我能找到的关于会员大会的信息)分成北太平洋和南太平洋两个分别投票的会议。

我无法访问 GPT-3，但每个人都可以在 https://talktotransformer.com/的站点访问它的前任 GPT-2。您可以键入起始文本，GPT-2 将创建后续文本。

例如，当我输入“*康涅狄格的交通……”，* GPT-2 产生了这样的文本:

***康涅狄格州*** *和纽约州的交通大致处于满负荷运行状态，许多长岛高速公路和长岛铁路公路交汇处都在收取通行费。这可能会影响今年剩下的时间，因为司机们试图弄清楚他们的旅行是否会一切顺利。在新泽西州，司机预计将首次支付超过 1000 美元，使用港务局新的横跨哈德逊河的免费桥梁。*

第一句话开头很好，但随后它开始谈论长岛铁路交汇处的通行费。然而，这违背了我们的常识，因为我们知道火车不会因为收费而停下来。第二句还好，虽然很难确定它的意思。第三句话是哪里出轨了。纽约和新泽西的通行费很高，但还不到 1000 美元。

为什么 GPT-3 和其他语言模型得到的事实是错误的？因为 GPT-3 就像虚构的吕特尼人一样，对其输入文本或生成文本的含义没有常识性的理解。这只是一个统计模型。

NYU 教授 Gary Marcus 写了许多论文并做了许多演讲，批评 GPT-2 获得常识性知识和推理规则的解释。正如他所说:“……仔细检查后，很明显[系统不知道它在说什么](https://thegradient.pub/gpt2-and-the-nature-of-intelligence/)……”。另见这篇 [*《纽约客》杂志*文章](https://www.newyorker.com/magazine/2019/10/14/can-a-machine-learn-to-write-for-the-new-yorker)，它描述了 GPT-2 在杂志的大量档案中接受训练后产生的故事。

# 结论

GPT-3 正在[学习关于单词共现的统计特性](https://www.aiperspectives.com/lm)。在它得到正确事实的时候，GPT-2 可能只是反刍一些记忆的句子片段。当它得到错误的事实时，那是因为它只是根据一个单词跟随另一个单词的统计可能性将单词串在一起。

缺乏常识性的推理并不会使语言模型变得无用。相反，它们可能非常有用。谷歌在其 Gmail 系统的智能撰写功能中使用了语言模型。Smart Compose 预测用户将要键入的下一个单词，用户可以通过按 TAB 键来接受它们。

然而，GPT-3 似乎没有学习常识，也没有学习根据这些知识进行推理。因此，它无法启动 AGI 系统的发展，这些系统像人类一样将常识推理应用于他们对世界的知识。

*随意访问* [*人工智能视角*](https://www.aiperspectives.com/introduction) *在那里你可以找到免费的在线人工智能手册，有 15 章，400 页，3000 篇参考文献，没有高等数学。*

*原载于 2020 年 7 月 6 日 https://www.aiperspectives.com*[](https://www.aiperspectives.com/gpt-3-does-not-understand-what-it-is-saying/)**。**