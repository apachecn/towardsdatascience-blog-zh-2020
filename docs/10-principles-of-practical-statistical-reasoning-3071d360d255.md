# 实用统计推理的 10 个原则

> 原文：<https://towardsdatascience.com/10-principles-of-practical-statistical-reasoning-3071d360d255?source=collection_archive---------33----------------------->

![](img/21b9e984ac93527d84b887750f1999a3.png)

安德烈亚斯·布吕克尔在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

卓有成效地应用统计学(数据科学)有两个核心方面:

1.  领域知识。
2.  统计方法。

由于这一领域的高度特殊性，任何一本书或文章都很难对两者之间的相互作用进行详细而准确的描述。一般来说，人们可以阅读两种类型的材料:

1.  关于统计方法的广泛信息，带有概括但不具体的结论。
2.  详细的统计方法，其结论只在特定领域有用。

在我自己的数据科学项目上工作了 3 年，在交易大厅操纵数据 3 年半之后，我学到了另外一类知识。它基本上和上面一样有用，我把它们带到了**的每个**项目/兼职/咨询工作中…

**实用统计推理**

我创造了这个术语，因为我真的不知道该如何称呼这个类别。但是，它涵盖了:

*   应用统计学/数据科学的性质和目标。
*   所有应用的通用原则
*   获得更好结论的实用步骤/问题

如果你有应用统计方法的经验，我鼓励你用你的经验来阐明和批评下面的原则。如果您从未尝试过实现统计模型，请尝试一下，然后再回来。不要把下面的内容看成是需要记忆的清单。如果你能联系自己的经历，你会得到信息的最高综合。

以下原则帮助我提高了分析的效率，并使我的结论更加清晰。我希望你也能从中发现价值。

## **1 —数据质量问题**

通过更精细的分析可以纠正差的数据质量的程度是有限的。值得完成的实际检查有:

*   *对逻辑上不一致或与每个变量可能产生的范围的先验信息相冲突的值进行视觉/自动检查。例如极值、变量类型。*
*   *分布频率。*
*   *两两散点图用于共线性的低水平检验。*
*   *缺失观察值(0，99，无，NaN 值)。*
*   *质疑由不一致(如观察者之间的差异)引入的偏倚的收集方法。*

## **2 —批评变异**

在几乎所有的问题中，你都将面对**不受控制的变化**。对于这种变化的态度应该是不同的，这取决于这种可变性是被研究系统的固有部分还是代表实验误差。在这两种情况下，我们考虑变异的分布，但动机不同:

*   **内在变异:**我们对分布形式的细节感兴趣。
*   **误差变化:**我们感兴趣的是，如果误差被消除，会观察到什么。

## **3 —选择合理的分析深度**

尝试独立于可用的数据量或可用的技术来考虑深度。仅仅因为收集数据容易/便宜，并不意味着数据是相关的。这同样适用于方法和技术。精心选择的分析深度支持清晰的结论，而清晰的结论支持更好的决策。

## **4 —理解数据结构**

**数据量**涉及个体数量和每个个体的变量数量。**数据结构=数据量+个体分组。**大多数数据集具有以下形式:

*   有很多人。
*   在每个个体上，观察到许多变量。
*   个人被认为是相互独立的。

鉴于这种形式，回答下面的问题将缩短有意义的结论解释的路径。

*   *什么才算是个体？*
*   *个人是否以必须纳入分析的方式分组/关联？*
*   *对每个人测量哪些变量？*
*   是否有任何观测数据丢失？可以做些什么来替换/估计这些值？

注意:小数据集允许容易地检查数据结构，而大数据集可能只允许结构的小部分分析。把这个因素考虑到你的分析中，需要多长时间就多长时间。

## **统计分析的 5 — 4 个阶段**

1.  **初始数据操作。** 意图=对数据质量、结构和数量进行检查，并以表格形式汇总数据进行详细分析。
2.  **初步分析。意图=阐明数据的形式，并建议最终分析的方向(图、表)。**
3.  **权威分析**。意图=为结论提供依据。
4.  **结论陈述。**意图=准确、简洁、清晰的结论和领域解释。

…但是这些阶段有一些注意事项:

*   阶段划分是有用的，但并不严格。初步分析可能会得出明确的结论，而最终分析可能会揭示出人意料的差异，需要重新考虑整个分析基础。
*   当给定一个干净的数据集时，跳过 1。
*   在有大量现有分析的字段中跳过第 2 步。

## 产量是多少？

记住，统计分析只是更大的决策过程中的一个步骤。**向决策者展示结论**对于任何分析的有效性至关重要:

*   结论风格要看受众。
*   以一种对批判性的非技术读者来说合理的形式解释广泛的分析策略。
*   包括结论和数据之间的直接联系。
*   用简单的方式展示复杂的分析是值得的。然而，要知道简单是主观的，与熟悉程度相关。

## **7 —合适的分析风格**

从技术角度来看，**分析风格**指的是如何对感兴趣的底层系统进行建模:

*   **概率/推理:**得出不确定的结论，通常是数字。
*   **描述性:**试图总结数据，通常是图形。

适当的分析风格有助于保持重点。尽早考虑它，这将减少返回到耗时的数据处理步骤的需要。

## **8 —计算方面的考虑**有时只是一个问题

技术的选择渗透到应用统计分析的各个方面，包括:

*   原始数据的组织和存储。
*   结论的排列。
*   主要分析的实施。

但是这应该在什么时候引起注意呢？

*   **大规模调查+大数据** =如果通过现有工具无法实现灵活性和性能，则值得投入资源来定制程序/库。
*   **大规模调查+小数据** =计算考虑不重要。
*   **小规模调查+大数据** =定制程序不可行，灵活通用程序/库的可用性至关重要。
*   **小规模调查+小数据** =计算考虑不重要。

## **9 —设计调查井**

同时一系列的统计方法可以用于一系列的调查类型。结果的解释将根据**调查设计**而有所不同；

*   **实验** =研究中的系统由研究者建立和控制。明显的差异可以理直气壮地归因于变量。
*   **观察性研究** =除了监测数据质量之外，研究者无法控制数据收集。真正的解释变量可能会丢失，很难有把握地得出结论。
*   **抽样调查** =在研究者的控制下，通过方法(随机)从人群中抽取样本。尽管解释变量如上所述受到影响，但仍可对人口的描述性特征得出有把握的结论。
*   **受控前瞻性研究** =研究者选择的样本，测量并随时间推移跟踪的解释变量。实验有一些优点，但在现实中，不可能测量所有的解释变量。
*   **受控回顾性研究** =对解释变量进行适当处理的现有数据集。

注:调查设计的一个重要方面是区分响应和解释变量。

## **10 —调查目的**

显然调查的目的很重要。但是你应该如何考虑目的呢？

第一，目标的一般质量区别:

*   **说明:**增加理解。在合身的模特中任意挑选是危险的。
*   **预测:**初级实际使用。易于在合身的模型中任意挑选。

调查的具体目的可能表明，分析应该集中在所研究系统的某个特定方面。它还影响到要寻求的结论的种类和结论的表述方式。

目的可能决定结论的失效日期。如果观察到变量之间相互关系的变化，任何完全基于经验的模型都是有风险的。

# 一锤定音

生活中几乎所有的任务都可以从框架中考虑:

输入->系统->输出

接下来的工作就是定义框架的每个方面。

实用的统计推理针对的是“系统”。系统的某些部分不能脱离上下文来确定。有些部分可以。实用的统计推理实际上就是简单而胜任地定义你的“系统”的能力。那种能力绝对不局限于这些原则。

*如果你想看编程/数据科学方面的构建，请查看我的* [*YouTube 频道*](https://www.youtube.com/watch?v=s4cQMryKwqA&t=324s) *，我在那里发布了 python 的完整构建。*

*我们的目标是激励和合作，所以伸出援手吧！*