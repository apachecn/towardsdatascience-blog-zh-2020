# 人工智能中的系统偏差

> 原文：<https://towardsdatascience.com/systematic-bias-in-artificial-intelligence-8698ffa20d57?source=collection_archive---------42----------------------->

## 照亮了明天最大的问题之一

![](img/0caa3141cefc25befc38b8991ddb998c.png)

数据真的有更好的想法吗？鸣谢:弗兰基·查马基

最近，詹妮弗·林肯医生做了一个[抖音](https://www.tiktok.com/@drjenniferlincoln/video/6835696093255322886?lang=en)强调了非裔美国人在医疗保健中面临歧视的多种方式，例如接受较少的止痛药和在急诊室等待更长时间。该视频基于发表在《国家科学院院刊》( PNAS)上的[研究](https://www.pnas.org/content/early/2016/03/30/1516047113.abstract),已在抖音获得 40 万次点击量，在推特上获得近 800 万次点击量。如果人工智能模型根据医疗记录进行训练，以预测患者的止痛药剂量，它可能会建议非裔美国人患者使用更低的剂量，因为它是在非裔美国人患者接受更低剂量的数据集上训练的。显然，这将变得非常成问题，因为这种人工智能的假设用例将进一步使种族主义制度化。

# 偏见的后果

随着人工智能日益融入当前系统，系统偏差是一个不容忽视的重要风险。当模型输入的数据存在对某个种族或性别的偏见时，它们就不能有效地达到预期目的。根据准确性、利润等指标评估的模型将试图最大化所述指标，而不考虑其形成的偏差。如果不采取措施解决这个问题，更重要的是，人类或监管机构可能会对人工智能失去信心，阻止我们释放这项技术的潜力。为了理解这个问题的严重性，这里有两个更可怕的人工智能偏见的例子。

*   正如论文“[仇恨言论检测中种族偏见的风险](https://homes.cs.washington.edu/~msap/pdfs/sap2019risk.pdf)”中所概述的那样，华盛顿大学的研究人员在超过 500 万条推文中测试了谷歌的人工智能仇恨言论检测器，发现来自非洲裔美国人的推文比其他种族的人更容易被归类为有毒言论。
*   COMPAS(替代制裁的矫正罪犯管理概况)是一种算法，由纽约、加利福尼亚和其他州用于预测获释囚犯再次犯罪的风险。在研究文章“[预测累犯的准确性、公平性和局限性](https://advances.sciencemag.org/content/4/1/eaao5580)”中，达特茅斯大学的研究人员得出结论，“没有累犯的黑人被告被错误地预测为重新犯罪的比例为 44.9%，是白人被告 23.5%的近两倍；而曾经再犯的白人被告被错误地预测为不会再犯的比例为 47.7%，几乎是黑人被告(28.0%)的两倍。考虑到 COMPAS 分数会影响被告的刑期，这是非常麻烦的。

# 战斗偏见

许多人工智能批评者表达的一个担忧是人工神经网络的“黑盒”性质:机器学习模型可以为我们提出的问题提供答案，但由于涉及的计算非常复杂，我们无法理解该模型如何得出答案。这种不透明性让偏见悄悄潜入。即使抛开偏见，消费者/企业也有兴趣了解人工智能是如何得出结论的。

解释人工智能如何做出高风险决策的一个潜在解决方案是可解释的机器学习。顾名思义，可解释机器学习涉及创建模型，其决策过程比黑盒模型更容易理解。为了变得可解释，这些模型被设计成具有诸如附加约束和领域专家的输入等因素。例如，防止贷款申请中的偏见的另一个约束是合规性:该模型必须遵守公平贷款法，不得歧视某一种族的消费者。

虽然可解释的机器学习模型由于其复杂性的增加而更加耗时和昂贵，但对于自动驾驶汽车、医疗保健或刑事司法等错误会产生严重影响的应用来说，可解释性层绝对是值得的。人性使社会抵制变化，但更透明的模型可以开始使公众/政府更容易接受人工智能的广泛采用。

其他潜在的解决方案关注模型使用的数据，而不是模型如何使用数据。一种提议的方法涉及获取通常保持机密的大型数据集(例如医疗数据)并在删除个人身份信息后向公众发布。这个想法是偏见将在这些匿名数据集中被过滤掉。然而，这种策略有其自身的风险，因为黑客可以交叉引用数据，使其通过匿名层。与此同时，有意识地纳入代表性不足的人群将支持缺乏多样性的数据集。最后，在设计这些算法的工程师中培养多样性应该有助于对抗偏见。

随着人工智能的快速发展，主动打击偏见仍然是当务之急。

# 参考

[1] Cynthia Rudin，[停止解释高风险决策的黑盒机器学习模型，转而使用可解释的模型](https://www.nature.com/articles/s42256-019-0048-x#Sec8)，《自然》

[2]克里斯托夫·莫尔纳尔，[可解释机器学习](https://christophm.github.io/interpretable-ml-book/)，Github

[3]朱丽亚·德雷塞尔，[《预测累犯的准确性、公平性和限度》](https://advances.sciencemag.org/content/4/1/eaao5580)，科学进展

感谢阅读！

我是 Roshan，16 岁，对人工智能的应用充满热情。如果你对人工智能更感兴趣，可以看看我关于人工智能在医疗保健中的应用的文章。

在 Linkedin 上联系我:[https://www.linkedin.com/in/roshan-adusumilli/](https://www.linkedin.com/in/roshan-adusumilli/)