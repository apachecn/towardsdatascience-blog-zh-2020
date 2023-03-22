# 如何建立我们都可以信任的机器学习算法？

> 原文：<https://towardsdatascience.com/how-to-build-machine-learning-algorithms-that-we-can-all-trust-cb00f1c055e1?source=collection_archive---------30----------------------->

## 内部人工智能

## 在几分钟内解释任何机器学习模型-充满信心和信任。

当哈姆雷特在莎士比亚著名的悲剧中说出这句话时，“生存还是毁灭”成了哲学领域中思想和自我反省的口头禅。在今天的商业世界中，在人工智能所做决策的驱动下，这句口头禅已经变成了“要么信任，要么不信任”。

![](img/73250b5993d66c0ab13f4892452ff9f9.png)

[https://imgs.xkcd.com/comics/machine_learning.png](https://imgs.xkcd.com/comics/machine_learning.png)(消息来源 1)

随着最近人工智能的崩溃成为新闻，人工智能模型中缺乏透明度和越来越多的偏见的问题已经暴露出来。在最近的例子中，人工智能系统声称高度污染的空气可以安全呼吸，而在现实中，这是非常危险的；或者人工智能系统声称某个病人没有癌症，但事实上该病人确实患有癌症并已死亡；或者人工智能系统将某项交易识别为欺诈，而这是一项完全合法的交易，给客户带来了不必要的麻烦，这显然是有问题的。随着人工智能的广泛使用，这些崩溃每天都在增加，这是由我们盲目信任这些人工智能系统造成的，但现在是采取行动的时候了！

![](img/16d7541b668f9b2e64b506dd61092d7d.png)

https://imgflip.com/i/2yc1nf

当谈到实施和信任这些人工智能系统时，当前的商业前景仍然非常怀疑。许多公司已经启动了这一过程，但尚未意识到其价值。这主要是由于数据科学团队和业务利益相关者之间的理解差距。在过去的几个月里，我们与许多商业利益相关者进行了交谈，他们是这些预测的接受者，我们发现数据科学家无法解释人工智能系统预测背后的原因和方式，这是对数据科学计划不信任和怀疑的最大因素。数据科学团队中的人技术含量很高，他们擅长用复杂性来表示他们的技能范围。然而，业务涉众有时是完全相反的:他们不关心使用的技术，而是模型生成的结果如何与他们的业务目标和 KPI 联系起来。

除非数据科学家能够回答这些基本问题，否则这是不可能实现的:

> 1.我为什么要相信模型生成的结果？
> 
> 2.模型产生结果的基本原理是什么？
> 
> 3.在生产中使用该模型的好处和坏处是什么？
> 
> 4.结果是否符合业务逻辑？

只有回答了这些问题，数据科学家才能向业务用户提出建议，并期望取得一些进展。

为了解决这个问题，数据科学家有两个选择:

> 1.通过在黑盒模型之上构建一个可解释的模型来解释黑盒模型。这是莱姆 SHAP 公司背后的逻辑。SHAP 得到了更广泛的应用，因为它保证了每个变量的公平分配，并有大量的图表。遗憾的是，这种方法需要大量迭代，缺乏交互性，并且不可扩展，尤其是在处理敏感数据集和决策时。更重要的是，可视化没有吸引力和互动性。它们的静态性质在数据科学家和业务利益相关者之间造成了更大的分歧。缺乏动态和互动的图表使得从 SHAP 或莱姆产生价值变得极其困难，因此需要一种更好的方法来使用这些技术。
> 
> 2.使用可解释的模型:数据科学家可以尝试优化逻辑回归或决策树等更简单的模型来进行预测，而不是使用深度神经网络等黑盒模型。在准确性和可解释性之间会有一个权衡，但是数据科学家需要决定什么是产生价值的重要因素，并且需要关注两种模型之间的边际收益。如果精确度之间的边际增加不显著，那么更理想的是实现更简单的模型，并将预测直接与业务 KPI 联系起来。可悲的是，随着我们今天收集的数据越来越复杂，简单的模型表现不佳。

## 所以问题来了:**在我们的机器学习模型中，有没有更好的建立信任的方法？**

[mltrons 的 xAI 实验室](https://xai-0a52ca.webflow.io/)正在研究一个 **xAI 模块**，旨在通过交互创新为 ML/DL 黑盒模型带来可解释性和透明性。目的是理解为什么决策是由人工智能系统做出的，并确保人工智能预测是公正的，准确的，没有任何逻辑矛盾。

该模块充当即插即用系统，适合任何 Jupyter 笔记本电脑——凭借自动化可视化和高度交互性，数据科学家将能够与业务利益相关者坐在一起，建立对人工智能系统的信任，并做出完全知情的决策。

![](img/567178f49251cf5823500fed706f5920.png)

图 1.1—m trons 模块示例工作流程。

这意味着数据科学家现在可以将他们的 Jupiter 笔记本、数据源(亚马逊、MySQL、HDFS 和使用 XGBoost、CatBoost、PyTorch、Tensorflow、SageMaker 的定制模型)引入 m trons 引擎，mltrons xAI 模块将接收输入，并将作为一个附加层，提供关于这些算法如何工作、思考和输出结果的可解释性。然后，数据科学家将能够通过交互式可视化、报告和可共享的仪表板，用简单的业务友好语言解释结果，任何人都可以很好地理解。

如果您对该技术有任何疑问，请通过以下表格联系我们:

[https://raheelahmad453253.typeform.com/to/qa8QRB](https://raheelahmad453253.typeform.com/to/qa8QRB)

关于作者: [Raheel Ahmad](https://www.linkedin.com/in/raheelahmad12/) 是 NYU·坦登可视化成像和数据分析(VIDA)中心的客座研究员，专注于 ML 模型的可解释性。他也是 mltrons 的联合创始人。