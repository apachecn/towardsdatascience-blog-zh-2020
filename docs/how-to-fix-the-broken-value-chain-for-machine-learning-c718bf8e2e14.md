# 如何为机器学习修复断裂的价值链

> 原文：<https://towardsdatascience.com/how-to-fix-the-broken-value-chain-for-machine-learning-c718bf8e2e14?source=collection_archive---------74----------------------->

## 尽管数据科学家的平台取得了良好进展，但商业用户仍难以消费他们的机器学习模型。

欢迎光临！下面是您可以从这篇文章中期待的内容:

*   如果你是一名数据科学家，你会更好地理解为什么你的机器学习(ML)模型可能不被操作采用的一个原因
*   如果你站在商业的角度，你会更清楚为什么你可能难以消费和利用 ML 模型
*   如果你想投资机器学习和业务自动化平台，你会发现一个被忽视的集成点

机器学习的工具、库和平台在过去 10 年里取得了惊人的进步，也许令人惊讶的是，几乎完全是由开源工具和开放标准驱动的。在商业战略方面，机器学习[价值链](https://en.wikipedia.org/wiki/Value_chain)的前半部分是高度模块化的(见下图)。这里没有苹果或星巴克——没有垂直整合的玩家将几个步骤融合在一起作为专有解决方案的一部分。

这种模块化意味着在 ML 价值链的每一步(从数据到库再到部署)，很有可能自由选择前一步的组件。是的，有些库是针对 Python 的，有些在 Spark 中工作得最好，但是很大程度上可以根据手头问题的需要混合搭配 ML 库、管道、工具和平台。

![](img/d3f932f5344dc12c4cd3f120cfd4d344.png)

在机器学习价值链中，从数据科学到商业的移交是模块化未能为商业用户提供足够简单性的一步。

就专有平台而言(无论是来自亚马逊、IBM、谷歌还是微软)，它们倾向于将各种语言(例如 Python、R)、工具(例如笔记本、ide)和库(例如 scikit-learn、TensorFlow)打包为开源，并支持这些作为平台的一部分。

至关重要的是，这些供应商平台旨在扩展到模型部署、模型监控和模型服务，通常运行在 Kubernetes 上，并将 ML 模型作为 REST 端点公开。这部分链有时被称为“ML Ops”，类似于 DevOps 为软件开发和 IT 团队提供的东西。

因此，当 REST 端点可用时，大多数数据科学家、ML 工程师和 ML Ops 平台认为他们的任务已经完成。

然而，当业务和 IT 想要使用这些部署的 ML 模型，使它们成为业务操作的一部分时，这会导致在后续步骤中出现问题。

这些问题通常包括:

*   **模型发现**:有哪些 ML 模型可用，它们预测/分类什么，哪一个适合特定的业务需求？
*   **模型连接**:我如何调用一个 ML 模型，向它提供数据并处理输出(和异常)？
*   **模型管理**:有没有新的 ML 模型版本，有什么不同，我应该什么时候升级？

为了满足这些需求，关于可用的 ML 模型、它们的目的和状态，需要相当多的透明度。当前使用的方法(开放的基于 REST 的 API)技术性太强，没有携带足够的关于 ML 模型的元数据来满足业务消费者的需求。

这里所需要的实际上是 ML 服务和 ML 消费步骤之间更紧密的集成，即确保业务自动化平台对 ML 服务平台具有可见性，能够发现和反思可用的模型。您可以将此视为供应链中的合作伙伴协作，其中供应商向买方提供库存的可见性。

或者，业务自动化平台可以接管 ML 服务的任务，在操作上托管 ML 模型。在这个模型中，ML 模型的消费本质上是通过导入模型来完成的，而不是通过 REST 端点来引用和调用它们。虽然这在技术上可能是可行的，但它对谁来管理 ML 模型有影响，潜在地将 ML 工件的管理从 ML 工程师那里移走。

不管怎样，ML 和自动化平台之间的鸿沟需要被弥合。目前的情况是广泛采用机器学习的主要障碍。

我们从中得到了什么，哪些行动被认为是短期的？

*   如果你是数据科学家或 ML Ops 工程师，计划与那些使用你的模型的人密切合作。如果使用 REST APIs 的“黑盒”式集成是您采用的方法，那么您的业务同事将需要您的信息和支持，以了解您正在提供什么模型以及如何使用它们。
*   如果您所在的组织寻求在业务运营中利用机器学习，请寻找与数据科学家使用的机器学习平台紧密集成的业务自动化平台。评估它提供可发现性、模型消费和模型管理的能力。

最后，如果你是机器学习和业务自动化领域的软件开发人员或供应商，这里可能会有机会脱颖而出。想想克莱顿·M·克里斯坦森的*诱人利润守恒定律*(见他的书 [*【创新者的解决方案*](https://www.amazon.com/Innovators-Solution-n/dp/B001HYXNKW/) *):*

*“当* ***诱人的利润*** *因为产品商品化而在价值链的某一阶段消失时，用专有产品赚取* ***诱人利润*** *的机会通常会在相邻阶段出现”*

由于机器学习市场如此分散和模块化(接近商品化)，诱人的利润可能会提供给那些密切整合 ML 服务和 ML 消费的人，为商业用户利用机器学习提供了一种简单的体验。

注意:如果你喜欢这篇文章，你可能还想看看它的姊妹篇— [“解决机器学习的‘最后一英里问题’以进行运营决策”](/solving-machine-learnings-last-mile-problem-for-operational-decisions-65e9f44d82b)。

*格雷格在 IBM 工作，常驻法国。以上文章为个人观点，不代表 IBM 的立场、策略或观点。*