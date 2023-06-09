# 如何解决人工智能偏见

> 原文：<https://towardsdatascience.com/how-to-tackle-ai-bias-ec39313ccacf?source=collection_archive---------27----------------------->

## 拥有一个有道德的人工智能对于拥有一个成功的人工智能是至关重要的。以下是如何确保你的人工智能不会导致偏见和歧视

![](img/b1109231a9480d025a532e93e9f59c50.png)

由 [Pixabay](https://pixabay.com/vectors/a-i-ai-anatomy-2729782/) 提供

近年来，我们都看到机器学习(ML)和人工智能中的偏见的例子占据了头条，例如[亚马逊的招聘算法](https://www.reuters.com/article/us-amazon-com-jobs-automation-insight/amazon-scraps-secret-ai-recruiting-tool-that-showed-bias-against-women-idUSKCN1MK08G)【1】偏向男性，[脸书在定向广告中指控住房歧视](https://www.theguardian.com/technology/2019/mar/28/facebook-ads-housing-discrimination-charges-us-government-hud)【2】，或者这个突出的[医疗算法](https://science.sciencemag.org/content/366/6464/447)【3】表现出明显的种族偏见。在这里，我将向数据科学家概述数据中可能的偏差来源，如何识别和测量偏差，以及减轻偏差的方法。

# 偏见的来源

算法本身没有任何固有的偏见，但当出现不适当的数据时，可以学会表现出歧视性行为。以下是一些导致偏差的数据质量问题:

*   数据不足:在您的培训数据中，整体或特定少数群体的示例太少。模型准确性和强大的洞察力是非常小的数据集中的主要挑战，特别是在涉及直接影响个人的用例时，应该小心谨慎。这就是为什么[面部识别算法](https://www.nytimes.com/2018/02/09/technology/facial-recognition-race-artificial-intelligence.html)【4】在某些人群中表现良好，而在其他人群中表现不佳。
*   数据收集实践:通过数据收集实践得到的更大的数据集在特征(列)级别上对于某些组可能没有足够的数据。您可能会发现某些组中的选择要素缺少过多的值，从而导致这些组在数据集中的表示不完整。ML 技术不太可能很好地预测代表性不足的群体，并且可能进一步加剧数据中存在的对他们的歧视。从不同来源提取数据有助于创建更加异构的数据集，因此模型的准确性更高，偏差更小。
*   历史偏见:不同群体目标分布的显著差异可能是由于数据中潜在的人类偏见。一些众所周知的例子是雇用中的歧视、贷款歧视做法或司法判决中的偏见。

仅仅因为数据中不存在受保护的或敏感的属性，并不意味着您对偏见免疫。为了评估偏倚，数据科学家应调查可能代表受保护和敏感属性的特征的使用情况。常见的、众所周知的例子包括邮政编码、体育活动、大学联系、文本文档中的某些单词(例如简历中的“执行”)、病历中的激素水平等。以上任何一项都可以用作暗示个人的种族、性别或其他受保护/敏感属性的代理。要检查代理特性，一种方法是将目标更改为受保护的属性，并相应地训练模型。精确度明显高于随机模型的模型表示泄露受保护属性信息的要素。通过检查要素的重要性，您可以直接识别数据特有的代理要素。

# 检测偏差

有许多不同的方法来检测关于受保护或敏感属性的偏见的存在。学术界的研究人员已经对公平和偏见提出了不同的定义，Arvind Narayanan 的这篇教程解释了每一个定义。根据使用案例，数据科学家可以选择最合适或优先的公平性定义，并检测模型预测中的偏差。以下是数据科学家在评估数据和模型偏差时应该采取的几个步骤:

*   比较不同组中某些要素缺失值的频率
*   评估数据中不同组的目标分布
*   使用教程中提到的不同测试，识别数据或模型预测中的偏差示例

# 偏差缓解

在 ML 流水线中有三个不同阶段的偏倚减少干预:预处理、处理中和后处理。

*   预处理技术旨在训练模型之前减少原始数据中的偏差。几个例子是[用于防止歧视的优化预处理](https://krvarshney.github.io/pubs/CalmonWVRV_nips2017.pdf)【6】，[用于无歧视分类的数据预处理技术](https://core.ac.uk/download/pdf/81728147.pdf)【7】和[证明和消除不同的影响](http://sorelle.friedler.net/papers/kdd_disparate_impact.pdf)【8】。
*   处理中方法解决模型训练中的偏差。[具有公平性约束的分类:具有可证明保证的元算法](https://arxiv.org/pdf/1806.06055.pdf) [9]在优化过程中实施公平性约束，并且[具有偏见消除器正则化器的公平感知分类器](http://www.kamishima.net/archive/2012-p-ecmlpkdd-print.pdf) [10]使用正则化作为减少偏见的手段。
*   后处理算法通过修改模型预测来减少偏差。[关于公平和校准](https://arxiv.org/pdf/1709.02012.pdf)【11】和[监督学习中的机会均等](https://arxiv.org/pdf/1610.02413.pdf)【12】改变模型预测以满足特定的公平定义。另一方面，[区分感知分类的决策理论](https://mine.kaust.edu.sa/Documents/papers/ICDM_2012.pdf)【13】假设大多数区分发生在决策边界附近，因此利用分类器的低置信度区域来减少区分。

访问受保护的或敏感的属性可能具有挑战性。它可能限于 ML 流水线中的某些阶段。如果这些特性在培训阶段是可用的，那么上面的任何缓解步骤都可能是有用的。但是，如果这些属性只对最终用户可用，例如对人力资源部门的招聘人员，后处理技术仍然可以用于模型预测。在无法访问受保护或敏感属性的情况下，数据科学家仍然可以利用缓解技术，通过识别代理特征来减少偏差。

# 参考资料:

[1]“亚马逊废弃了显示偏见的秘密人工智能招聘工具……”2018 年 10 月 9 日。[https://www . Reuters . com/article/us-Amazon-com-jobs-automation-insight/Amazon-scraps-secret-ai-recruiting-tool-that-show-bias-against-women-iduskcn 1 MK 08g](https://www.reuters.com/article/us-amazon-com-jobs-automation-insight/amazon-scraps-secret-ai-recruiting-tool-that-showed-bias-against-women-idUSKCN1MK08G)。

[2]“脸书被控在定向广告中进行住房歧视……”[https://www . the guardian . com/technology/2019/mar/28/Facebook-ads-住房-歧视-收费-美国-政府-hud](https://www.theguardian.com/technology/2019/mar/28/facebook-ads-housing-discrimination-charges-us-government-hud) 。

[3]“剖析用于管理……的算法中的种族偏见”。[https://science.sciencemag.org/content/366/6464/447](https://science.sciencemag.org/content/366/6464/447)。

[4]“面部识别是准确的，如果你是一个白人——”2018 年 2 月 9 日，[https://www . nytimes . com/2018/02/09/technology/face-recognition-race-artificial-intelligence . html](https://www.nytimes.com/2018/02/09/technology/facial-recognition-race-artificial-intelligence.html)。

[5]“阿尔温德·纳拉亚南——YouTube。”【https://www.youtube.com/watch?v=jIXIuYdnyyk 

[6] Calmon，f .，Wei，d .，Vinzamuri，b .，Ramamurthy，K. N .，和 Varshney，K. R.《防止歧视的优化预处理》。神经信息处理系统进展 30，2017。

[7]卡米兰，费萨尔和考尔德斯，图恩。无区别分类的数据预处理技术。知识与信息系统，33(1):1–33，2012

[8] M. Feldman、S. A. Friedler、J. Moeller、C. Scheidegger 和 S. Venkatasubramanian。验证和消除不同的影响。2015 年在 KDD。

[9] L. Elisa Celis，Huang，Vijay Keswani 和 Nisheeth K. Vishnoi。具有公平性约束的分类:一种具有可证明保证的元算法。《公平、问责和透明会议论文集》，FAT* '19，2019 年。

[10] T. Kamishima、S. Akaho、H. Asoh 和 j .佐久法史带有偏见消除器正则化器的公平感知分类器。数据库中的机器学习和知识发现，第 35–50 页，2012。

[11] Pleiss，g .，Raghavan，m .，Wu，f .，Kleinberg，j .，和 Weinberger，K. Q. (2017 年)。论公平与校准。神经信息处理系统进展，5680-5689 页。

12 莫里茨·哈特、埃里克·普莱斯和纳蒂·斯雷布罗。监督学习中的机会均等。神经信息处理系统进展，2016 年。

[13]卡米兰，f .，卡里姆，a .，张，X. 2012 年。区分感知分类的决策理论。在*IEEE 数据挖掘国际会议论文集(ICDM 2012)* 中，Zaki M. J .、Siebes A .、Yu J. X .、Webb G. I. & Wu X .(编辑)。IEEE 计算机学会，924–929