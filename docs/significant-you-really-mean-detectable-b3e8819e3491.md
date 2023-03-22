# 意义重大？你真的是说可辨别的

> 原文：<https://towardsdatascience.com/significant-you-really-mean-detectable-b3e8819e3491?source=collection_archive---------39----------------------->

## 关于统计显著性的两个常见错误短语

![](img/04c29bad786a31f54e64d46cde5031d7.png)

伊恩·帕内洛在[的照片 https://www . pexels . com/photo/放大镜教科书-4494644/](https://www.pexels.com/photo/magnifying-glass-on-textbook-4494644/)

*(注:2020 年 10 月 13 日，我将“检测”改为“辨别”，以避免与信号检测或异常检测等领域相关的分析混淆。)*

> 统计学意义从来都不意味着科学上的重要性。…总之，“统计显著性”——不要说也不要用。( [Wasserstein 等人，2019 年，在美国统计协会的出版物《美国统计学家》](https://www.tandfonline.com/doi/full/10.1080/00031305.2019.1583913))

> 每当我听到一位讲师、主持人或研究人员说“显著的”，而他们的意思显然是“统计上显著的”，你可能会看到我抽搐(“T8”)，这实际上与“临床上显著”或“科学上显著”没有任何关系。参见[瓦瑟斯坦等人，2019](https://www.tandfonline.com/doi/full/10.1080/00031305.2019.1583913) ，以及[瓦瑟斯坦和耶戈，2016](https://www.tandfonline.com/doi/full/10.1080/00031305.2016.1154108) 。这些认知上的打嗝把我从他们原本谨慎的科学叙述中拉了出来——让我担心他们可能从根本上误解了他们的分析结果。

这肯定不是你想从你的统计同事那里听到的！因此，这里是我的简短尝试，以帮助纠正关于研究结果的两个常见短语。它们是错误的，因为它们通常被误解。

我将分享每个错误的短语，它的解释，和一个更好的短语。如果你感兴趣，我在最后提供了错误短语 1 的详细推理。(作为练习，你应该试着对错误的短语 2 应用类似的推理。)

(如果你想通过一个带有代码和一些数学的 R 中的工作示例来深入了解细节，请参见我之前的帖子: [**混淆 P 值与临床影响:显著性谬误**](/the-significance-fallacy-confusion-about-p-values-d7b5e530d0c?sk=87cfd2bfdebe3800776905fd916505d2) **)**

# 错误短语 1:减少/增加

> 结果显示 D 显著降低。

![](img/4846bc80ae9b1dc159abecf29661e7e1.png)

照片由 [Anthony](https://www.pexels.com/@inspiredimages) 在[拍摄 https://www . pexels . com/photo/animals-avian-beaks-birds-133615/](https://www.pexels.com/photo/animals-avian-beaks-birds-133615/)

## 解释

*   **常见误解:**结果中出现了具有科学或临床意义的、重要的、有意义的或有用的 D 减少。
*   **正确的解释*:** 有显著的统计证据表明，平均结果存在真实的未知变化(即减少/增加)，且不为零(例如非零)。如果这项研究设计和执行得当，那么这一证据表明，我们从样本中计算出的 D 的减少是对真实的未知的 c 变化的一个很好的估计。

相关的统计测试结果说[绝对没有关于 C 在科学上或临床上是否显著、重要、有意义或有用的内容](/the-significance-fallacy-confusion-about-p-values-d7b5e530d0c?source=friends_link&sk=87cfd2bfdebe3800776905fd916505d2) ( [Wasserstein et al，2019](https://www.tandfonline.com/doi/full/10.1080/00031305.2019.1583913)；[瓦瑟斯坦和耶戈，2016](https://www.tandfonline.com/doi/full/10.1080/00031305.2016.1154108) 。它只是告诉我们，有足够的统计证据(随着样本量的增加而增加)来*辨别*C 可能不为空，因为我们的估计值 D(我们假设它是 C 的一个很好的估计值)表明 C 减少了。

## 一个更好的短语

> *结果中 D 的*减少*。*

具体来说，在结果样本平均值中有一个统计学上可辨别的 D(我们假设是 C 的一个很好的估计)的减少。

# 错误短语 2:联想

> 变量 X 和 y 之间没有显著的联系。

![](img/9f46b95e0db26924ee60270cd2b1f0b6.png)

照片由 [Nextvoyage](https://www.pexels.com/@nextvoyage) 在[https://www . pexels . com/photo/white-boat-sailing-near-islands-during-golden-hour-1481096/](https://www.pexels.com/photo/white-boat-sailing-near-islands-during-golden-hour-1481096/)

## 解释

*   **常见误解:**变量 X 和 y 之间没有科学或临床上显著、重要、有意义或有用的关系。
*   **正确解释:**没有显著的统计证据表明变量 X 和 Y 之间真实的、未知的统计关联不是空的(例如，零相关，线性关联)。如果这项研究设计和执行得当，那么这个证据表明我们从样本中计算出的关联 Z(基本上是零关联)，是对真实的未知关联 a 的一个很好的估计。

相关的统计测试结果说[绝对没有关于 A 在科学上或临床上是否显著、重要、有意义或有用的内容](/the-significance-fallacy-confusion-about-p-values-d7b5e530d0c?source=friends_link&sk=87cfd2bfdebe3800776905fd916505d2) ( [Wasserstein et al，2019](https://www.tandfonline.com/doi/full/10.1080/00031305.2019.1583913)；[沃瑟斯坦和耶戈，2016 年](https://www.tandfonline.com/doi/full/10.1080/00031305.2016.1154108)。它只是告诉我们，没有足够的统计证据(随着样本量的增加而增加)来*辨别*A 可能不为空，因为我们的估计值 Z，我们假设它是 A 的一个很好的估计值，表明基本上是零关联。

## 一个更好的短语

> *变量 X 和 Y *之间没有*可识别的 ***表*** *关联。**

具体来说，变量 X 和 y 之间没有统计上可辨别的联系，用 Z 来衡量(我们假设这是对 A 的一个很好的估计)

# 详细推理:错误短语 1

最初的短语调用了三个关键量:

1.  平均结果中 C 的真实变化是未知的。如果我们有目标人群的所有相关数据，这就是我们简单计算的结果。
2.  相反，我们必须从目标人群中抽取样本来估算这个数量。我们的特殊估计 D 可能接近也可能不接近 c。
3.  非零(例如非零)C 的**统计证据量**定义为“矛盾证明”,如下所示。如果 C 真的为零(即，如果平均结果真的没有任何变化)，观察到我们的估计值 D 或更极端值的概率是多少？这个概率被称为一个 **p 值**，通常是使用你的样本近似得到的*。*

对于像 D 这样的给定估计，这个 p 值随着样本量的增加而减小；即零假设的“矛盾”越来越大。“统计显著性”被宽泛地定义为这个 p 值的一些倒数:p 值越低，统计显著性越高。也就是说，如果我们从一个更大的样本中计算出相同的精确值 D，D 将会更有统计学意义。如果我们从一个更小的样本中计算出同样精确的 D 值，D 的统计意义会更小。

相关统计假设检验:

*   确实回答:“我们有多少证据证明非空 C 的存在呢？”换句话说，“我们有足够的证据来**辨别**一个非空的 C 吗？”
*   没有回答:“我们有多少证据证明 C 在科学或临床上是重要的、重要的、有意义的或有用的？”再次提醒，请记住[的统计显著性与](/the-significance-fallacy-confusion-about-p-values-d7b5e530d0c?source=friends_link&sk=87cfd2bfdebe3800776905fd916505d2)的科学/临床显著性完全不同。特别是， [C 不可能*永远*具有统计显著性](/the-significance-fallacy-confusion-about-p-values-d7b5e530d0c?source=friends_link&sk=87cfd2bfdebe3800776905fd916505d2)，因为真实数量是固定值，通常与用于估计它们的样本大小无关。
*   不回答:“D 近似 C 吗？”这是估计量(如样本平均值、MLE 估计量)和研究设计的一个属性。

这是对最后一点的一些粗略的直觉。

1.  将你的评估者应用于你的整个目标人群(没有任何变化)。这只是计算某个固定的(即非随机的)量 t。
2.  好的估计量对于 T 是统计一致的(即，对于样本量较大的 T 越来越无偏)。
3.  但是你的估算者总会估算出一些东西！在统计机器学习中，如果你告诉它一个模式存在，你的聚类或预测算法总是会找到一个模式——即使没有模式。(感谢[Daniela Witten](https://twitter.com/daniela_witten)教授在[最近的一次演讲](https://events.linuxfoundation.org/r-medicine/program/schedule/)中清晰地展示了这一点，以及一些精彩的解决方案。)
4.  确保 T=C 取决于你如何设计和执行你的研究:你如何制定你的科学假设，收集数据，并进行所有的分析。

所以通常的解释是错误的，原因有二:

1.  它混淆了 D(已知样本量)和 C(未知总体量)。
2.  它错误地声称你的样本提供了证据，证明 C 在科学或临床上是重要的、重要的、有意义的或有用的。

# *注:错误短语 1

## 解释

*   **另一个正确的解释:**“有重要的统计证据表明，结果中存在真实的、未知的非空(例如，非零)均值变化(即，减少/增加)。”

这是一个微妙但重要的区别，从早期的解释，并可以暗示不同的估计方差。例如，在前后或成对设计中，如果结果对相互关联，则先取平均值然后取差值的估计量比先相减然后取平均值的估计量更易变。

实际正确的解释将取决于研究设计和统计假设。

# 关于作者

Daza 博士是一名生物统计学家和健康数据科学家，他为个人(n-of-1)数字健康开发因果推断方法。| ericjdaza.com[🇺🇸🇵🇭](https://www.ericjdaza.com/)@ ericjdazalinkedin.com/in/ericjdaza|[statsof1.org](https://statsof1.org/)[@ stat sof 1](https://twitter.com/statsof1)[@ fsbiostats](https://twitter.com/fsbiostats)