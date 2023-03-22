# 用 P 值认识这些问题

> 原文：<https://towardsdatascience.com/youre-probably-misusing-the-p-value-fef44d665955?source=collection_archive---------31----------------------->

## 以及为什么 P 值小于 0.05 并不重要

![](img/064462bd2b2bc7f34f51501ce6e60acc.png)

塞巴斯蒂安·赫尔曼在 [Unsplash](https://unsplash.com/s/photos/frustration?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

# **简介**

p 值是频数统计中的一个重要概念，通常在统计学导论课程中讲授。

不幸的是，这些课程要么在解释 p 值可以(和不可以)做什么方面做得不好*，要么公然宣传与 p 值在因果推理中的作用有关的虚假宣传。*

这导致了很多本科生，甚至是应该更了解的学者，在研究中做出不正确的主张，都是因为发现 p 值小于 0.05。

本文的目标是澄清围绕 p 值的神话，并希望鼓励数据科学家在他们自己的项目中超越 p 值。

# P 值是多少？

对 p 值的任何准确解释都必须首先讨论零假设显著性检验(NHST)。

NHST 是一个统计程序，研究者通过它陈述两个假设:一个**零假设**和一个**替代假设。**

零假设表明给定的处理对目标变量没有影响。另一个假设陈述了相反的情况；也就是说，给定的处理*不会影响目标变量。*

例如，假设我们想确定最低工资法是否会导致更高的失业率。

无效假设和替代假设可能如下:

**零假设:**最低工资法不影响失业率。

**替代假设**:最低工资法增加了失业率。

通常，研究人员想要拒绝零假设。(拒绝零假设会增加替代假设的可信度)。

然而，我们应该如何拒绝零假设呢？

这就是 p 值的来源。

> p 值是一个介于 0 和 1 之间的数字，它告诉研究人员在假设零假设为真的情况下观察到某个值的概率。

假设我们想检验我们的最低工资假说。我们收集了美国城市的随机样本——有些城市有最低工资法，有些没有——发现有最低工资法的城市的失业率平均比没有最低工资法的城市高半个百分点。

这是自由市场资本主义的胜利吗？我们应该废除全世界的最低工资法吗？

不完全是。

> 在标准的学术研究中，大于 0.05 的 p 值通常不被认为是*统计显著的——*一个用来掩盖任意分界点的花哨短语。

假设我们得到 p 值为 0.78。也就是说，如果我们假设零假设是真的，**那么有 78%的可能性，我们会看到有最低工资法的美国城市和没有最低工资法的美国城市之间有半个百分点的差异。**

如果我们试图将这些结果提交给学术期刊，那么期刊的编辑可能会嘲笑我们回到 Medium(当然是开玩笑，因为阅读 Medium 的人比阅读*美国政治科学杂志—* 的人多，但我离题了)。

在标准的学术研究中，大于 0.05 的 p 值通常被认为不具有统计显著性*—*一个用来掩盖任意分界点的花哨短语。

所以，p 值是 0.78。太糟糕了。我们如此努力的研究被证明是毫无意义的。

![](img/fde5d20b25e43d8f4f81dbc9b8e64ad7.png)

马科斯·保罗·普拉多在 [Unsplash](https://unsplash.com/s/photos/crying?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

**但是，等等！**

也许任意截止点的一个优点是它防止虚假研究进入著名的学术期刊。

是吗？我们会回来的。

# P 值的(许多)问题

## 1) P 黑客

我们刚刚被我们最喜欢的学术期刊拒绝，因为我们的 p 值太高了。

然而，我们对我们的结果有把握。我们是在弗里德曼、格林斯潘和伯南克的教导下长大的。我们知道最低工资法会对劳动力市场造成巨大破坏。

所以，我们回到我们的研究，看看我们是否可以降低我们的 p 值。首先，我们将更多的城市纳入研究:来自加拿大、中国、巴西、欧洲和俄罗斯的城市。因为 p 值与样本量成负相关，所以增加样本量会降低我们的 p 值。

其次，我们决定改变我们的模式。我们控制了可能对城市失业率产生影响的特征——人口规模、地理位置、税率等。还有一些与失业率有着更难以解释的关系的特征，比如城市中星巴克的数量。一般来说，增加模型的复杂性可以降低 p 值，因为我们的模型可以解释样本中更多的随机性。

现在我们的 p 值是 0.1。**好一点，但还是没出息。**

最后，我们改变我们的测试统计。也许我们使用了学生的 t 检验，但现在我们决定使用卡方检验和…

*p 值= 0.049。*

**完美的**。我们的结果现在具有统计学意义。学术期刊决定发表我们的研究。

上述程序被统计学家亲切地称为“p hacking ”,是一种操纵数据分析过程的形式，其程度之深，掩盖了比它提供的更多的信息。

作为一名研究人员，您不能:

1.  报告称，只有当您将非美国城市包括在内时，您的测试才变得“具有统计学意义”
2.  探索您使用的其他模型(这些模型在统计上不显著)
3.  报告你的结果只有卡方检验有统计学意义；学生的 t 检验产生了无统计学意义的结果

不幸的是，p hacking 在学术研究中普遍存在，它通常会导致难以重现的结论。(如果一篇研究文章报告 p 值为 0.049，你可以合理地确定该研究人员进行了一些 p 黑客攻击)。

## 2) P 值不能说明事实

反正你的 p 值现在是 0.049。

*万岁！*

如果零假设是真的，那么我们有 4.9%的机会观察到有最低工资法的城市和没有最低工资法的城市之间的失业率差异 0.5 个百分点。

据应用研究人员称，这意味着我们现在可以安全地 ***拒绝*** 的无效假设。也就是说，我们已经证明最低工资法对失业率没有影响。

这是许多应用研究人员出错的地方。

低 p 值本身并不能说明零假设(或替代假设)的真假。

不相信我？

以下是美国统计协会(ASA)对这个话题的看法:

> p 值不衡量所研究的假设为真的概率，也不衡量数据仅由随机机会产生的概率。

如果零假设*为真，观察结果将出现的 4.9%的概率不*转化为零假设*为*真的 4.9%的概率。

根据 p 值的定义，这个结论应该是显而易见的:

> p 值是一个介于 0 和 1 之间的数字，它告诉研究人员在假设零假设为真的情况下观察到某个值的概率。

我们测量的是观察某个值的概率，而不是假设为真的概率。

我们已经看到操纵 p 值是多么容易:

1.  增加样本量
2.  使我们的模型复杂化
3.  使用不同的测试统计

然而，p 值作出了许多其他假设，这些假设可能不适用于当前的研究。

例如，p 值假设我们正在比较相似的组。也就是说，美国城市和中国城市相似。这是一个不太可能的假设，即使我们的模型过于复杂。首先，中国城市的政治体系与美国城市截然不同。我们的模型无法量化这种差异。

同样，p 值假设待遇(最低工资)是随机应用的。

当然，这不是真的。一个美国城市有最低工资而另一个没有，这一事实与随机性关系不大，更多的是与政治和经济差异有关。

## 3)低 p 值并不意味着强烈的影响

假设我们再次篡改了我们的模型。现在，我们得到 p 值为 0.004。如果我们假设零假设是真的，那么现在只有 0.4%的可能性，我们会观察到有最低工资法的城市和没有最低工资法的城市之间有 0.5 个百分点的差异。

暂时，让我们忽略 p 值的所有其他问题，让我们假设我们的结果代表地面真理。

谁在乎呢。

我们是否应该阻止数百万人获得生活工资，因为这可能会使失业率上升半个百分点？

通常，低 p 值掩盖了预测的因果影响微不足道的事实。美国广告标准局写道:

> 科学结论和商业或政策决策不应仅仅基于 p 值是否超过特定阈值

不幸的是，许多应用研究人员忽略了因果影响，并使用小 p 值来提出政策建议。

回到我们的最低工资的例子，仅仅考虑 p 值来决定一项政策是不正确的。我们必须采取更全面的方法。

# 所以，p 值很烂。我们做什么呢

我们已经展示了 p 值是如何误导人的。如果不是因为它几乎被普遍接受为因果关系的充分指标，这不会是一个大问题。毕竟，许多统计数据本身可能会产生误导。

因此，这就引出了一个问题:*我们应该停止报告 p 值吗？*

2015 年，*基础和应用社会心理学*【BASP】*期刊禁止论文报道 p 值——在我看来，这是一个激烈的举措。*

*我认为解决办法是教育人们使用(和误用)p 值。*

*p 值从来没有打算成为统计研究的存在理由。相反，当罗纳德·费雪——频率主义统计学的教父——在 20 世纪 20 年代开发 p 值时，他打算把它作为因果分析中的一个步骤。*

*尽管许多人对它有误解，p 值仍然提供了一些有趣的信息。它必须与其他统计数据、领域知识和(一点)常识结合使用。*

# *笔记*

1.  *最低工资法例子的另一个假设也可以写成“最低工资法影响失业率”；然而，正如我在文章中所写的，劳动经济学家通常对另一种假设感兴趣。*

# *文献学*

*[1]努佐·里贾纳(2014)《统计误差》 *Nature* Vol. 506。*

*[2] Head ML，Holman L，Lanfear R，Kahn AT，Jennions MD (2015)《科学中 P-Hacking 的程度和后果》。PLoS Biol 13(3): e1002106。【https://doi.org/10.1371/journal.pbio.1002106 号*

*[3] Cumming，Geof(2015)《p 黑客入门》。*方法空间*。[https://www.methodspace.com/primer-p-hacking/](https://www.methodspace.com/primer-p-hacking/)*

*[4]罗纳德·l·瓦瑟斯坦和妮可·a·耶戈(2016)“美国统计学会关于 p 值的声明:背景、过程和目的”，*《美国统计学家》*，70:2，129–133，DOI:10.1080/00003035486*

*[5]卡尔彭，塞缪尔·C(2017)“P 值问题”，*美国药学教育杂志，* 81:9，93*