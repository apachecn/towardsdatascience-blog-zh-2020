# 产品经理机器学习指南:平衡计分卡

> 原文：<https://towardsdatascience.com/a-product-managers-guide-to-machine-learning-balanced-scorecard-344cd37ab4a7?source=collection_archive---------28----------------------->

## 研究表明，只有一小部分机器学习(“ML”)项目会产生商业影响。在这篇文章中，我将探索和分享我自己的经验建立记分卡，以最大限度地提高 ML 项目的成功。

![](img/ebf158d967f60b3c9d9bf205108e7e53.png)

由[安德烈斯·达利蒙提](https://unsplash.com/@dallimonti?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/cockpit?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

在亚马逊从事顶线/底线战略时，我的一个重点是获得设计和构建 ML 模型的工作知识。例如，我学会了使用神经网络来建立图像分类。构建 ML 模型并观察其结果对我来说绝对是一件令人着迷的事情。不管 ML 有多吸引人，或者将会变得多么吸引人，我目前还没有转变成数据科学家或应用科学家的计划。产品管理是我的热情所在，但我总是发现自己被数学和 ML 的应用所吸引！当我在亚马逊找到一个具有领先 ML 特性的角色时，我欣喜若狂。我喜欢产品管理和 ML 之间的最佳平衡点。

## “我们 ML 这个东西吧！”

分享我在亚马逊担任 ML 产品经理期间学到的五条经验:

1.*角色* —第一个也是最明显的教训是，知道如何建立一个 ML 模型与领导一个 ML 产品是不同的。

2. *ML 项目与软件相关项目* —领导一个传统的软件相关项目与领导 ML 项目是不同的。科学方法(即观察、假设、测试、学习等。)仍然适用于传统软件和 ML 项目。然而，与传统的软件模型相反，ML 完全依赖于与业务问题相关的数据的质量和数量。一旦克服了数据的局限性，就有了损失、优化和评估的复杂性。我提到评估业务价值来源和客户价值主张的模糊性了吗？

3.*复杂程度*——“你只需要在这个产品中启动 ML 特性”并不像听起来那么简单。理解并尊重这些年来因为 ML 而需要重新调整的技术架构。你挖得越多，发现的骨骼就越多。

4.*业务影响*——计算一个 ML 模型的业务影响是极其模糊的。企业需要“展示资金”作为产品经理，你要拿出量化的价值。识别、理解和评估正确的假设起着关键作用。当然，这需要与更广泛的组织保持一致。

5.*客户影响* —使用 ML 验证客户影响可以在没有 ML 的情况下完成。我了解到，我们可以验证一个 ML 模型的有效性和影响，而无需构建一个 ML 模型。向后工作！构建模拟(各种格式)来测试这些假设。拥有一些验证数据可以增强组织的信心，并帮助其他人团结在事业周围。

## 冰山一角

![](img/4dc6f84bb5682161ff29a059ec6f24f0.png)

由[亚历山大·哈弗曼](https://unsplash.com/@mlenny?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/iceberg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

总结一下我学到的经验:ML 给商业利益相关者增加了大量的不确定性。推出 ML 产品时出现的问题是:它能给企业带来好处吗？存在什么证据？假设是什么？有哪些财务风险？谁受它的影响最大？实现有多复杂？用于训练 ML 模型的数据是否真正代表生产？我们有足够的标签吗？这些只是冰山一角。在推出 ML 产品的整个过程中，还会出现更多类似的问题。

## 构建记分卡

如你所见，在领导一个 ML 产品时，需要在任何给定的时间同时理解和管理几个领域。在读 MBA 期间，我读过一个案例研究和一篇关于构建平衡计分卡概念的文章。大约 30 年前，罗伯特·S·卡普兰和大卫·P·诺顿为管理商业的各个方面提供了这个解决方案。他们建议使用平衡计分卡从四个重要的角度来看待业务:

*   客户如何看待我们？
*   我们必须擅长什么？
*   我们能持续改进并创造价值吗？
*   我们如何看待股东？

> “把平衡计分卡想象成飞机驾驶舱里的刻度盘和指示器。对于导航和驾驶飞机的复杂任务，飞行员需要关于飞行许多方面的详细信息。他们需要有关燃油、空速、高度、方位、目的地以及总结当前和预测环境的其他指标的信息。”

我们能否采用平衡记分卡的概念并对其进行定制，以管理机器学习产品？以下是我从自己的经历中总结出的记分卡:

## **1。数据，数据，数据**

是啊！夏洛克！我同意没有粘土就不能砌砖。没有正确的数据，我们无法构建 ML 解决方案。所以，让我们从数据开始，数据，数据。理解和积累适合您项目的数据是无可替代的。根据您在项目中所处的位置，与您的应用科学家坐下来了解他们对数据的限制。认真对待这些问题，并召集你的团队来解决这些问题。制定一个计划，逐步建立数据。这是一个说明我的数据记分卡的表格。

## **2。给我钱**

ML 工作与业务单位的顶层指标紧密相关。将 ML 输出链接到 topline 对于项目的持续成功至关重要。当利益相关者表达对潜在影响的担忧时，理解被质疑的假设，并制定计划来确认这些假设。收集证据，向风险承担者展示模型的影响。结合莫斯科项目框架，以避免范围蔓延，即使在计算影响时也是如此。

## 3.内部记分卡

通过清晰的沟通流程减少跨职能部门的歧义。每个人都投入了大量精力来沟通项目中各个里程碑的状态。

## 4.顾客

客户为你的项目制造了一个很好的共鸣板，尽早让他们参与进来，然后逆向工作。这对于任何一个产品经理来说都应该是显而易见的一步，我就不拿这个来烦你了。

## 邀请您:

仅仅专注于推出 ML 解决方案而没有一个平衡的方法会让你走上一条循环的道路。利用上述平衡计分卡提高推出正确解决方案的几率。问题列表和记分卡的类型越来越多。请随意在你的项目中使用这些记分卡。我邀请您分享其他对您有帮助的记分卡或相关问题。祝你一切顺利！

**引文**:

[1]:弗莱明、雷蒂卡和菲尔·费施特。“如何避免你隐约出现的机器学习危机。”HFS 研究，2018 年 7 月。[https://1 PCL 3 wzgyqw 5 KF 62 erficswwpengine . net DNA-SSL . com/WP-content/uploads/2018/07/RS _ 1807 _ HfS-POV-machine learning-crisis . pdf .](https://1pcll3wzgyqw5kf62erficswwpengine.netdna-ssl.com/wp-content/uploads/2018/07/RS_1807_HfS-POV-MachineLearning-Crisis.pdf.)

[2]:卡普兰&诺顿。(1992).平衡计分卡——推动绩效的衡量标准。《哈佛商业评论》，71–79 页。检索自[https://HBR . org/1992/01/the-balanced-score card-measures-the-drive-performance-2](https://hbr.org/1992/01/the-balanced-scorecard-measures-that-drive-performance-2)