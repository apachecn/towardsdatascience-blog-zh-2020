# 构建一个 ML 产品——要避免的 4 个错误

> 原文：<https://towardsdatascience.com/build-an-ml-product-4-mistakes-to-avoid-bce30d98bd24?source=collection_archive---------20----------------------->

## [人工智能笔记](https://pedram-ataee.medium.com/list/notes-on-ai-for-executives-84e1081cf2dd)

## 这是我多年来学习的构建机器学习产品的综合课程。

![](img/64151052051a5733d4c0a8ea20b0d009.png)

由[彼得罗·郑](https://unsplash.com/@pietrozj?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

近年来，我在不同的角色和职责下与几个机器学习或 ML 初创公司合作，如工程师、团队领导、顾问和顾问。我发现了四个在工程师和高管中非常常见的错误。在这篇文章中，我描述了构建 ML 产品的 4 个常见错误，并给出了一些可穿戴技术公司的例子。

有一次，我在一家可穿戴技术公司领导机器智能团队。该公司制造了一种手势控制臂带，让用户使用手势控制他们的环境。我们开发了一个手势识别引擎，它将肌肉信号作为输入，并识别手势。

我们必须构建和评估大量的 ML 模型来构建行业级的 ML 产品。因此，我们建立了一个管道，适当地管理构建 ML 产品所需的所有开发步骤，包括数据收集、模型训练、模型评估或模型选择。

> 我们成功地将一款 ML 产品运送给了全球超过 10 万名用户。除非我们在 ML 产品的开发中实施了最佳实践，否则我们无法做到这一点。

[](https://www.amazon.ca/Artificial-Intelligence-Unorthodox-Innovative-Solutions/dp/B08D4Y5129/ref=tmm_pap_swatch_0?_encoding=UTF8&qid=&sr=) [## 人工智能:非正统的教训:如何获得洞察力和建立创新的解决方案

### 人工智能:非正统的教训:如何获得洞察力和建立创新的解决方案

www .亚马逊. ca](https://www.amazon.ca/Artificial-Intelligence-Unorthodox-Innovative-Solutions/dp/B08D4Y5129/ref=tmm_pap_swatch_0?_encoding=UTF8&qid=&sr=) 

在这里，我分享了构建 ML 产品的 4 个潜在错误，以及一些解决它们的建议。我发现这些错误在我后来工作过的许多其他团队中很常见。

## —单一端到端模型很棒，但可能不存在。

构建 ML 产品的一个常见错误是坚持构建一个单一的端到端模型来解决所有场景。一个 ML 产品几乎不能通过一个 ML 模型来运输。原因之一是用例比你通常预期的有更多的差异。

> 错误一——从早期开始，我坚持构建一个单一的端到端 ML 模型，并通过该模型处理所有用例。

在早期，我们的目标是为全世界 70 亿人建立一个手势识别模型。你可以猜猜。它不像我们计划的那样有效。因此，我们很快开始研究原始肌肉信号，以获得更好的见解。

我们发现，我们对每个手势的预期模式或特征在用户中并不一致。换句话说，我们发现个体之间的差异比我们早期认为的要多，单一的 ML 模型可能并不适用于所有人。例如，我们发现个人有不同的肌肉解剖，皮肤导电性，排汗率，前臂周长和手势风格。但是替代方案是什么呢？

例如，我们可以根据他们的前臂周长将他们分成相似的组，并为每个组建立一个特定的模型。这种方法可以显著提高模型性能。然而，它不能创造我们想要的用户体验。然后，我们采取了另一种方法。我们决定只为我们的用户创建两个选项:公司使用我们的训练数据集构建的“人口模型”和用户通过自己的数据构建的“个性化模型”。

## —盲目收集的测试数据集可能会非常误导人。

您必须在每次发布之前彻底评估 ML 模型的性能。因此，在流程中尽快收集有效的测试数据集非常重要。另一方面，有效的测试数据集必须是用户数据的真实表示。然而，你还不够了解你的用户；尤其是在早期。所以，你不知道你的产品如何被使用，在哪里被使用，或者被谁使用。因此，您必须始终怀疑您的测试数据集是否能够真正代表用户数据。

> 错误二——我没有时间仔细设计数据收集协议。我只会把时间花在训练一个复杂的模型上。

我们的分析表明，诸如“前臂周长”或“皮肤状况”等参数会显著影响模型的性能。我们可以测量个体的前臂周长，但是很难测量他们的皮肤状况。因此，我们充分收集了前臂周长的正态分布数据，但我们不能对皮肤状况进行同样的收集。请注意，我们使用电导率仪为一小部分用户测量皮肤状况以进行分析，仅此而已。

无论如何，我们不知道我们的用户前臂周长或皮肤状况的分布。如果我们有大量的用户，我们可以假设它一定是正态分布。但是，我们当时没有那么多用户。所以，我们确信分布绝对是偏斜的。这意味着我们可以猜测一个新版本如何影响用户体验。由于我们不能 100%确定发布的质量，我们必须有一个应急计划。

## —标准的性能指标并不总是足够的。

你可以简单地用准确度、精确度和召回率等标准指标来评估一个学术性的 2 类机器学习问题。然而，你不能那么容易地评估一个 ML 产品。例如，一个 ML 产品通常是一个具有特定问题配置的多类问题，每个配置都给评估框架带来一些复杂性。构建 ML 产品的一个常见错误是用标准的性能指标来评估 ML 产品。

> 错误三——我不需要特定于问题的指标。我可以使用标准指标来评估 ML 产品。

我们设计了一个 ML 模型来识别 5 种手势，即左、右、拳、展开和打响指。我们用 3 个标准参数，即准确度、精确度和召回率来评估每一类中 ML 模型的性能。因此，我们需要考虑 15 个(3×5)性能指标。这 15 个参数并不同等重要。例如，Fist 或 Snap 类中的误报对用例 a 中的用户体验有不同的后果。此外，用例也有它们自己的差异。简而言之，考虑到所有的复杂性，我们必须创建特定于问题的度量标准，以确保发布新的 ML 模型。

## —更多的数据并不能保证更好的结果。

“如果我们收集更多的数据，我们的模型会变得更好。对不对？”我相信你听过这句话很多次了。但事实是，模型性能并不一定会因为输入更多数据而提高。这就是为什么为了将来的目的，您必须将模型和它们的性能报告一起存档在一个库中。例如，您可能希望检索它们以进行比较分析或在生产中部署它们。

为了构建 ML 产品，您必须频繁地构建 ML 模型，而模型性能并不一定在每次构建中都得到持续的提高。因此，您必须将模型与其重要的元数据(如性能指标和超参数)一起存储。这有助于您在需要时对结果进行更深入的分析。您还必须将训练和测试数据存储在模型旁边，以确保在需要时可以重复前面的实验。

您可以在云存储解决方案(如亚马逊 S3)、通用工件管理解决方案(如 [JFrog](https://jfrog.com/) )或持续集成解决方案(如 [CircleCI](https://circleci.com/) )提供的隔间中构建这个模型库。最佳实践是使用工件管理解决方案，它创建了对存储的 ML 模型列表的更好的访问。请注意，您可能希望使用性能查询来搜索这个集合。如果模型存储在基于文件的存储中，比如亚马逊 S3，就不能这样做。

> 错误四——我不需要存档 ML 模型。如果我们收集更多的数据，我们的模型会变得更好。我为什么要花时间创建基础架构？

想象一下，你是一家公司机器智能主管。在过去的几个月里，你努力设计了一个包含一系列需求的 ML 模型。截止日期到了，出乎意料地，你被告知公司需要一个有不同要求的 ML 模型。你没有时间再次做所有的训练和测试。您必须做的是在模型库上运行一个查询，并提取一个与新需求性能最接近的模型。如果你没有准备好这个库，你能恰当地应对这种情况吗？

# 外卖食品

*   如果单一的 ML 模型不起作用，有一个替代策略
*   确保测试数据是用户数据的真实代表
*   使用特定于问题的指标来评估端到端性能
*   构建一个 ML 模型库，并用有用的元数据标记它们

# 感谢阅读！

如果你喜欢这个帖子，想支持我…

*   *跟我上* [*中*](https://medium.com/@pedram-ataee) *！*
*   *在* [*亚马逊*](https://www.amazon.com/Pedram-Ataee/e/B08D6J3WNW) *上查看我的书！*
*   *成为* [*中的一员*](https://pedram-ataee.medium.com/membership) *！*
*   *连接上*[*Linkedin*](https://www.linkedin.com/in/pedrama/)*！*
*   *关注我* [*推特*](https://twitter.com/pedram_ataee) *！*

[](https://pedram-ataee.medium.com/membership) [## 通过我的推荐链接加入 Medium—Pedram Ataee 博士

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

pedram-ataee.medium.com](https://pedram-ataee.medium.com/membership)