# 机器学习中公平的反直觉性

> 原文：<https://towardsdatascience.com/the-counter-intuitiveness-of-fairness-in-machine-learning-6a27a6a53674?source=collection_archive---------48----------------------->

## 审查实现公平的统计框架

过去发生的事情可以作为未来的良好预测，这一想法是机器学习(ML)取得巨大成功背后的核心原则。然而，这种“过去作为前奏”的预测行为的方法正在受到越来越多的审查，因为它在偏见、歧视和公平方面被认为是失败的。例如，[苹果信用卡算法](https://www.washingtonpost.com/business/2019/11/11/apple-card-algorithm-sparks-gender-bias-allegations-against-goldman-sachs/)给女性的信用额度比男性少；指控一个广泛使用的评估再犯风险的软件是[歧视黑人被告](https://www.washingtonpost.com/news/monkey-cage/wp/2016/10/17/can-an-algorithm-be-racist-our-analysis-is-more-cautious-than-propublicas/)。这些报道不仅占据了新闻头条，还激怒了我们[与生俱来的公平感。](https://www.nature.com/articles/nature08785)

![](img/158b073fb225f897c0d7c038a37f2ea4.png)

由 [Unsplash](https://unsplash.com/@unseenhistories?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的[看不见的历史](https://unsplash.com/@unseenhistories?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)拍摄的照片

在刑事司法中，关于现有的反歧视法律是否足以监督预测算法，存在持续的争论。此外，有一个新兴的研究团体正在研究我们如何在这些法律下维护预测算法的公平性(例如 [Barocas & Selbst](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2477899) ， [Huq](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3144831) )。正如最近针对系统性歧视的骚乱和抗议所表明的那样，做错的后果是严重的。随着我们越来越多的生活变得自动化，我们迫切需要加快努力，让这项技术为整个社会所接受。

在这篇文章中，我将回顾一个关于如何给 ML 带来公平的想法。乍一看，这个想法似乎有悖常理，但正如几篇文章所阐明的，它有坚实的统计和法律基础。

这篇文章的目标读者是对 ML 有基本了解，并且对我们如何在 ML 中实现公平性感兴趣的人。

# 什么是公平？

公平是一种社会理想。正如一位学者所说，

> 只要人们同意，公平就是人们所说的一切。

在一个自由的社会里，这种理想既有争议又不断发展。因此，在马丁·路德·金的文献中，我们对公平有如此多的定义也就不足为奇了(例如[&维尔马【鲁宾】](https://dl.acm.org/doi/10.1145/3194770.3194776)，[纳拉扬](https://perma.cc/HE3CGXDU))。

尽管缺乏关于公平的明确协议，但美国有完善的法律保护个人的基本权利，尽管他们之间存在差异。最值得注意的是，种族、性别和宗教等差异代表了一组“[受保护的群体](https://en.wikipedia.org/wiki/Protected_group)”，使个人能够得到“公平”的对待，特别是在就业领域(1964 年《民权法案》第七章)和刑事司法领域(第十四修正案的[平等保护条款](https://en.wikipedia.org/wiki/Equal_Protection_Clause))。

# 实现公平的当前方法

由于这些法律和过去歧视的历史，使 ML 和一般预测算法公平的主流方法是消除使用来自受保护群体的数据。杨和 Dobbie 编制了一份刑事司法系统中最常用的八种商业工具的清单，并发现所有这些工具都没有将种族(一个受保护的群体)作为输入。

然而，消除作为输入的保护基团是不够的。正如许多学者指出的，我们仍然只剩下[相关变量，这相当于使用受保护变量](https://papers.nips.cc/paper/6228-man-is-to-computer-programmer-as-woman-is-to-homemaker-debiasing-word-embeddings.pdf)。例如，邮政编码可以代表种族。然而，对于这些是否也应排除在外，却没有一致意见。在同一个商业可用工具列表中，Yang 和 Dobbie 发现只有八分之三的工具不使用相关变量。换句话说，大部分最常用的预测算法，5/8 (62.5%)可以被认为违反了保护具有受保护属性的个人的既定法律。这些都是潜在的诉讼等待发生！

当前的方法可以总结如下。

基准(包括所有变量):

![](img/33e548ff0fc75a6ee5fc794bcdf729cc.png)

常见(不包括受保护组):

![](img/f4ad63525262c5f53338b52d800599c2.png)

限制性(排除保护组和相关变量):

![](img/f4e80641a261108792a93dc65ee2b050.png)

算法制定者的困惑是，根据变量与受保护群体的相关性进一步消除变量，最终将使算法变得几乎无用。例如，在 Yang 和 Dobbie 的研究中，他们发现*他们的所有*输入变量都与受保护变量相关。因此，遵循主流的消除受保护属性的方法的精神将会剥夺 ML 算法的任何输入！

我们的问题是:

> 我们如何将公平引入 ML，同时保持其效用？

# 实现公平的统计框架

Pope 和 Sydnor 引入了一个简单的统计框架来消除受保护变量及其替代变量的影响。杨和多比在审前预测中使用并进一步检验了这一框架。

它是这样工作的:假设我们正在做一个预测。例如，被告在受审前再次犯罪的可能性。根据这一预测，我们可以决定是否应该在审判前释放被告。

在这个框架中，我们用三种变量来表示被告的特征:

![](img/05e5acea52c4e2d4b4d74100af679403.png)

*   Protected (Xp):代表受保护组的变量。例如种族、性别、民族血统、宗教。

![](img/354b777949d6f684e5cb4ce5c497dda8.png)

*   相关(Xc):与受保护变量相关的变量。例如邮政编码或教育水平，这可以代表种族。

![](img/e8e26a91c76ac68954c19a64ad71cebd.png)

*   不相关(Xu):代表与受保护群体及其代理人不相关的数据的变量。

![](img/2125657e2983bd69bde6608b9a594186.png)

为简单起见，作者假设使用线性回归(普通最小二乘法)的预测模型:

![](img/7f397d0f51b79451db7558d1407efc39.png)

换句话说，预测等于常数(β-0)加上无保护变量、相关变量、受保护变量及其权重系数(β-1、β-2、β-3)之和，再加上误差项(E)。作者还讨论了如何在提出的框架下将该模型扩展到更复杂的非线性模型。

在此框架下进行预测的方法包括 2 个步骤:

步骤 1:训练预测模型并获得系数估计值。即上式中的β-0、β-1、β-2 和β-3。

![](img/7045e4960c83f7b24b8fa7402a1a910f.png)

第二步:使用第一步的系数估计值和受保护变量的平均值进行预测。

![](img/a0e2c1c8475902cdd96af815b13fb733.png)

这就是全部了！这种方法不仅看似简单，而且是反直觉的，因为我们使用受保护的变量及其代理作为算法的一部分来确保公平性！

# 为什么会这样？

让我们从第二步开始，因为这一步包含了主要的变化，实际上非常直观。

![](img/0e617e3041411045b2af816eea180827.png)

除了使用估计系数之外，这一步与第一步的唯一区别是，我们使用数据的平均值，而不是使用具有受保护特性的数据。

![](img/8d3c4a884a405dc133c2d5595f15fe83.png)

更准确地说，我们使用的是受保护群体的平均向量。这意味着仅在受保护特征方面不同的两个个体将不会收到不同的预测。例如，如果种族是一个受保护的变量，那么模型将不会知道个人的种族概况。据说它对受保护变量的影响“视而不见”。这正是我们想要从一个公平的 ML 算法中得到的。

但是相关项呢？也就是说，

![](img/00c746cb1cfaf8592d100668cb2de84f.png)

这难道不包括受保护变量的代理效应吗？答案是否定的，因为第一步。波普和西德诺是这样解释的:

首先，让我们看看对普遍接受的方法的估计:

㈠

![](img/54f6f1244cac90c0453a51531eac36f2.png)

即一个常数与不相关和相关变量及其相关系数之和；因为包含了相关变量，我们知道它包含了代理效应。

现在将其与基准方程的估计值进行比较:

㈡

![](img/603be15466699f5081c7a1069aea3408.png)

假设β-3 大于零，我们看到γ-2 不可能等于β-2。

![](img/068927a4d05c2b53340740de73e4f4ba.png)

这是因为在(ii)中，我们用受保护变量进行估计，而在(I)中，我们不使用受保护变量进行估计。我们的直觉告诉我们，系数γ-2 携带着代理的估计能力。换句话说，γ-2 携带了一个术语，允许 Xc 与 Xp 相关联。

让我们进一步打开包装。由于 Xc 与 Xp 相关，我们可以假设:

㈢

![](img/fb990898823cd85ef6a2bafb31e8b7d2.png)

使用经济学文献中的标准[省略变量偏差公式](https://en.wikipedia.org/wiki/Omitted-variable_bias#:~:text=In%20statistics%2C%20omitted%2Dvariable%20bias,to%20those%20that%20were%20included.)，我们可以用(iii)代替基准方程:

![](img/66d3f1a86b56503432144077fb4e6026.png)

将这与普遍接受的方法(I)相比较，

![](img/2cd30407bd208a647dfe1cc7c0e9101c.png)

忽略常数和误差项，我们现在看到γ-2 估计值接近β-2 加上β-3 乘以α-C，其中β-2 是不相关的权重系数(作者称之为正交系数)，α-C 是加权相关系数。也就是说，

![](img/e0741a09d3f71b74b1924a09943473c6.png)

通过在步骤 1 中包含受保护的变量 Xp，我们实际上使 Xc 的系数独立于 Xp。杨和杜比是这样说的:

> “估计该基准模型允许我们获得未被代理效应污染的相关特征的预测权重，这正是因为我们显式地包括了 X_protected。因此，这第一步估计确保我们从包含 X_correlated 中消除所有代理效应”(第 34 页)

因此，我们可以确信β-2 没有被相关物质“污染”。换句话说，它不包含受保护变量的代理效应。

# 这有多准确？

Pope 和 Sydnor 使用误差平方和作为度量，分析了统计框架的不同公式的预测准确性。结果表明，他们提出的框架是第三准确的，仅次于基准模型和通用模型，但比限制性模型更准确:

1.  基准模型
2.  通用模型
3.  **建议模型**
4.  限制性模型

正如预期的那样，基准模型和通用模型比提议的模型更准确，因为它们包括了受保护变量及其代理的使用。然而，由于这种做法的法律地位脆弱，算法制定者可能需要使用一个更具限制性的模型(前提是他们能够找到可以被认为与其他变量不相关的变量)。提议的模式提供了一种避免诉诸限制性方法的方式。

杨和多比将这些模型应用于纽约市 2008 年至 2013 年间的大型审前案件数据集。他们还煞费苦心地对照审前案件，看被告是否真的出庭。结果是大约 20 万名被告的数据语料库。

他们的发现证实了 Pope 和 Sydnor 的准确性发现。此外，虽然我们确实为了公平而牺牲了准确性，但 Yang 和 Sydnor 表明，不同算法之间的准确性差异非常小。例如，在 50%的释放率下，未出庭率为:

*   基准:8.35
*   普通:8.38
*   **建议:8.40**

在所检查的数据集下，所提出的模型只会导致 8 个额外的故障出现。

# 在法律上是否合理？

既然这个框架使用来自受保护群体的数据，它是否有可能违反法律？例如，第十四修正案的平等保护条款在种族方面强加了两项基本保护(见 [Huq](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3144831) ⁴):

1.  种族分类
2.  种族化的意图

那么如果在这个框架下使用种族，是否违反了歧视法？杨和杜比认为没有。尽管该框架使用了保护组，但它这样做是为了实现“种族中立的预测”。

法院对基于“受保护特征”的分类进行“严格审查”(即上述第 1 条)。然而，杨和多比认为，宪法“禁止所有种族分类，除非是作为对特定不法行为的补救措施”。他们认为这个框架

> “不应受到严格的审查，因为种族的使用/考虑并不意味着根据某一特定种族群体的成员资格来区别或区别对待个人，而是恰恰相反。”。(第 37 页)

即使它被标记出来，他们认为它也经得起任何法律审查，因为该程序的目的是“为了补救和纠正代理效应和历史偏见而定制的，这些效应和偏见可以‘嵌入’到算法中……”(即上文#2，见第 37 页)

然而，杨和多比承认，“对算法中直接效应和代理效应的潜在统计特性缺乏了解，可能会导致一个天真的观察者得出结论，认为这两个建议都是非法的，因为它们违反了广泛接受的禁止使用或考虑受保护特征的规定。”(第 36 页)我们----反洗钱联盟和相关团体----有责任以法院和广大公众容易理解的方式教育和宣传这一框架。

# 结论

人们常说人工智能，尤其是 ML，将会深刻地改变世界。然而，我们与这一新生技术建立了什么类型的关系，我们的生活将如何改变，仍有待确定。最近对预测算法的抵制，例如荷兰[禁止使用福利欺诈预测工具](https://www.loc.gov/law/foreign-news/article/netherlands-court-prohibits-governments-use-of-ai-software-to-detect-welfare-fraud/)、美国[禁止人脸识别软件](https://www.technologyreview.com/2020/06/26/1004500/a-new-us-bill-would-ban-the-police-use-of-facial-recognition/)以及英国[取消 A-levels 成绩预测](https://en.wikipedia.org/wiki/2020_UK_GCSE_and_A-Level_grading_controversy)，显示了我们作为一个自由社会为打造一个所有人都能接受的共生关系所做的努力。

我们不能在不了解我们的过去的情况下跌跌撞撞地走向未来，我们也不应该扼杀那些给我们带来前所未有的机会、让社会变得更好的技术。为了让 ML 走向成熟，我们需要学习、教育，并对这种技术应该具有什么样的理想特征做出明智的决定。

> “人只有在你让他看清自己是什么样的时候，才会变得更好。”安东·契诃夫

在这篇文章中，我强调了一个统计框架，旨在为 ML 带来公平性，同时保留算法的有用性。尽管乍一看有些违反直觉，但波普和西德诺尔的框架已经被证明在理论上和法律上都是合理的。与法律上有争议的模型相比，使用该框架创建的模型确实损失了一定程度的准确性；然而，它这样做是为了消除来自受保护变量及其代理的输入的影响。

这项工作也提出了一个重要的问题，即“准确性”在 ML 中意味着什么。例如，准确性是一个简单的算法做出正确预测的数量的问题吗？正如波普和西德诺尔所说，问题变成了:

> “是正确预测结果(“平均正确”)更重要，还是正确权衡不同的特征(“在边缘正确”)更重要？”

这样看的话，前面提到的很多算法公平性的激烈争论，本质上可以认为是侧重点的不同。这样的争论在哲学和伦理学中有很长的历史。毫无疑问，只要我们对我们赞同的理想有分歧，这些辩论就可能继续下去。因此，这里强调的工作值得更多关注。它提供了一个实用的解决方案，理论上满足法律的要求，而不会严重损害算法的预测能力。

# 参考

[1]许明，塞德里克·阿宁，史蒂文·r·石英.权利与善:公平与效率的分配正义和神经编码【https://science.sciencemag.org/content/320/5879/1092(2008 年)

[2] Crystal Yang & Will Dobbie，[算法下的平等保护:一个新的统计和法律框架](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3462379)，可得 3462379 (2019)

[3] Devin G. Pope 和 Justin R. Sydnor，[在统计特征模型中执行反歧视政策](https://www.aeaweb.org/articles?id=10.1257/pol.3.3.206)，3 AEJ:政策 206 (2011 年)

[4] Huq，Z，阿齐兹。算法刑事司法中的种族公平，[《杜克法律杂志》，第 68 卷，](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3144831#) (2019)

感谢马克·大卫、瑞安·理查兹和罗恩·埃斯佩思对早期草稿的评论。