# 作为数据科学家平衡理论和实践

> 原文：<https://towardsdatascience.com/balancing-theory-and-practice-as-a-data-scientist-f91ef0c4de14?source=collection_archive---------59----------------------->

## 推论和发现之间的权衡

![](img/ebc0ca3af9545132b45b774d1a724300.png)

照片致谢: [Unsplash](https://unsplash.com/photos/rBLTWS3WsQ8)

理论和实践在人类努力的地图上是一条双行道。许多发现和发明都是偶然和修补的结果，而不是根据基本原理进行的预测和设计。蒸汽机早于热力学定律，空气阻力和帆自古以来就为人所知，但对[空气动力学](https://en.wikipedia.org/wiki/History_of_aerodynamics)的正式描述出现得要晚得多。

另一个方向也有一些。T4 希格斯玻色子 T5 在被实验观测到之前就被预言了。在爱丁顿的远征之前，广义相对论在很长一段时间内仍然是一个理论。因此，重要的是要认识到这两种方法都是我们寻求知识的重要工具。

机器学习的快速发展归功于这两种方法，但它是 2017 年激烈辩论的主题，一个小组将这个主题比作炼金术，并很快被反驳说:

> “将太多精力从尖端技术转移到核心理解可能会减缓创新。
> 
> 这不是炼金术，这是工程学。工程很乱”

一方认为实践者“操之过急”，而理论家则被批评为“把婴儿和洗澡水一起泼出去”。

根据基本原则构建的领域具有“可解释的失败”的优势——这是生产逐渐可靠的系统所需的关键原则，也是每个工程领域努力的目标。

但是当我们评估不使用它的成本时，实用方法的重要性就凸显出来了。在某些情况下，如果人们坚持要有一个公理化的描述，整个研究领域就不会开始——现代飞机设计的关键贡献者[计算流体动力学](https://en.wikipedia.org/wiki/Navier%E2%80%93Stokes_equations)，为完全依赖尚未解决的[千年问题](https://en.wikipedia.org/wiki/Navier%E2%80%93Stokes_existence_and_smoothness)的一面提供了一个典型的例子。

机器学习的中间立场后来被[澄清](https://openreview.net/pdf?id=rJWF0Fywf)，并开始讨论更好的实践。特别强调了经验评估的标准，无论环境如何，都必须遵循这些标准。

作为一名数据科学家，在执行分析时，有哪些要点[1]需要牢记在心？

*   **分享您的调整方法** 应该对所有模型(包括基线和共享模型)执行所有关键超参数的调整(使用既定方法)。
*   **切片分析** 对完整测试集的准确性或曲线下面积(AUC)等性能测量可能会掩盖重要的影响，例如在一个区域质量提高，但在另一个区域质量下降。根据不同维度或不同类别的数据分解绩效指标是全面实证分析的关键部分。
*   **消融研究**
    测试模型架构中的每一个组件从之前的基线单独或组合变化。
*   **使用测试分布之外的数据** 对模型行为的理解应该由测试分布之外的数据提供信息。例如，对于来自不同人口分布的用户的数据，模型的表现如何？
*   **报告负面结果** 发现并报告新方法的表现不如先前基线的领域。会有这样一个地区是因为[没有免费的午餐。](https://en.wikipedia.org/wiki/No_free_lunch_in_search_and_optimization)

请注意，任何用于解决现实世界问题的机器学习框架，其核心都是“模型”——区分好的模型已经在这个[博客](https://medium.com/@gpavanb/the-trouble-with-predictions-66e215c995bc)中讨论过了。

非常感谢下面这篇文章开启了这个方向的对话

[1]d .斯卡利，Snoek，j .，Wiltschko，a .，& Rahimi，A. (2018)。赢家的诅咒？关于速度、进度和经验主义的严谨性。

此外，请务必查看以下关于此主题的视频

[2] [深度学习的认识论](https://www.youtube.com/watch?v=gG5NCkMerHU)

[3] [深度学习简介和“炼金术”之争](https://www.youtube.com/watch?v=kqhg-o-KEns)