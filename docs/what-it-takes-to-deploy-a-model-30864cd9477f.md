# 部署一个模型需要什么

> 原文：<https://towardsdatascience.com/what-it-takes-to-deploy-a-model-30864cd9477f?source=collection_archive---------24----------------------->

## 将机器学习模型投入生产时的基本步骤和最佳实践

![](img/40f4d4db5b9f7bb40b2b3ed75a4f0b9f.png)

图片由 [Pixabay](https://pixabay.com/) 的 [Mudassar Iqbal](https://pixabay.com/users/kreatikar-8562930/) 提供

所以你(或你的团队)花了几个月的时间在笔记本上摆弄代码。您已经失眠了，不知道是否应该使用 Word2Vec 或 BERT 来矢量化您的文本输入。你已经在几十个(不，几百个？真的，几千？)连续几天，你终于达到了你想要的那种甜美的准确度。这种满足感就是你从事数据科学工作的原因。你手里拿着宝贵的 model.pickle 文件。你知道你的公司会通过使用它获得大量的金钱，但是你可能没有意识到这是最容易失败的时刻。不幸的是，许多模型无法投入生产。例如，2009 年 4 月，网飞组织了一场奖金为 100 万美元的 Kaggle 竞赛，但获胜的模型从未投入生产！[1].所有这些工作和准确性只有在一天结束时有人能够真正使用该模型时才会有回报——稳定、可靠、快速和大规模地产生价值。

那么，实际部署一个模型需要什么呢？下面是一个部署路径的一些基本步骤和注意事项，当您的模型从研发转换到生产时，请记住这些步骤和注意事项。

# 1.将您的模型包装在 Web 服务器中

当然，许多人使用手动部署选项。每当需要做出新的预测时，您的队友可以手动运行该模型。但是这种方法很可能无法满足您的业务需求。作为自动化的第一步，您可以创建一个简短的脚本来加载您的模型并对新数据进行评分，但是每次您需要预测时，您都会浪费时间来加载和重新加载您的模型，这可能不是一个微不足道的损失。

这个挑战的一个解决方案是用一个简单的 web 服务器来包装您的模型。web 服务器会将您的模型加载到内存中，并能够以较低的延迟立即提供预测。对于大多数语言来说，有很多关于如何编写 web 服务器的教程。

想得更远一些，您还应该问自己:这个服务器会一直只托管一个模型吗？或者以后，您需要一起托管多个模型吗？

# 2.改进您的 Web 服务器

现在你有了一个 web 服务器，你必须问自己如果它崩溃了会发生什么？您的模型有望为高影响力的业务流程提供动力，并且为不同事件建立应急计划至关重要。可能会发生运行时异常。您可能在某个地方有内存泄漏，这导致您的预测评分过程最终在内存耗尽时被终止。您不希望晚上在紧急情况下醒来重新启动它，所以最好提前考虑并围绕您部署的单独运行的模型开发流程管理。它将处理自动重启，并提供报告机制来传达服务的实时状态。

# 3.托管您的 Web 服务器

既然您已经有了本地运行的模型，并且运行稳定，那么您需要向世界公开它。您的公司是在裸机上托管软件，还是依赖某个云提供商？在任何情况下，您都需要将您的服务器托管在某个地方。您关于托管的决定应该取决于模型的公共可用性。您的模型是公开提供给客户，还是仅在您的内部网络中提供？如果模型是公开可用的，您需要为 web 服务器建立一个授权机制，以限制恶意用户的访问。

任何软件都需要更新，所以一旦你的网络服务器被托管在某个地方，你需要一些更新它的过程。当更改完成后，您需要测试服务是否继续工作。为了实现这一点并确保您团队的生产力，您应该建立某种形式的持续集成/持续交付管道。

# 4.高可用性服务

**高可用性** ( **HA** )是衡量系统运行性能水平的一个特征。它通常以正常运行时间的百分比来衡量。“两个 9”或 99%的正常运行时间意味着您的服务在一年中有 88 小时不可用。问问你自己:如果你的模型宕机 88 小时，会对你的业务造成多大影响？

大多数 web 服务在 HA 上提供服务级别协议。但是，即使达到三个 9(99.9%)的正常运行时间也非常困难。您的 web 服务器的主机可能会关闭。托管它的数据中心可能会停电。高可用性的基础之一是消除单点故障[2]。要做到这一点，您需要拥有模型的多个副本，并在它们之间保持平衡。请记住，在地理上分散它们将减少失败的数量。为了能够适应不断变化的负载并优化托管成本，能够扩大和减少副本的数量非常重要。

# 5.监视

即使采取了前面所有的步骤，仍有可能出错。也许您的服务器的所有节点都关闭了，或者您的测试管道没有发现一个 bug。为了能够对这种紧急情况做出反应，您需要对您的服务进行监控和警报。收集服务日志将有助于在此类问题发生后发现其根本原因。

为了使您的服务更新建立在科学决策的基础上，您需要收集关于您的服务当前如何运行的数据。你不应该说你的模式“慢”；相反，您应该精确，并根据响应时间的中间值或其他重要的百分位数进行操作。你不应该说你的服务“太失败了”；相反，您应该有准确的失败请求百分比作为基准。

# 6.更多监控？！

但是仅仅监控服务对于我们的用例来说是不够的。一旦你将一个模型投入生产，它就开始退化。大多数情况下，这与您的模型预测的数据漂移有关。为了在一段时间内提供准确的预测，您需要监控模型的性能。最流行的技术包括监控模型的输入变量、预测和准确性。想象一个使用美元价格作为输入的模型，假设由于一个错误，发送了乌克兰格里夫纳的价格。该模型将照常处理请求，因为它仍然是一个数字特性，但是您的预测将非常不同，因为该数字现在大了 30 倍。

您需要设置明确的阈值，以确定模型何时发生漂移，并在模型预测准确度较低时发出警报。这些通知与关于服务健康的通知一样重要。

# 7.再训练

一旦您清楚地知道您的模型预测不佳，您就需要用更多的最新数据来更新您的模型。我们之前提到的 CI/CD 管道可以方便地持续更新您的模型。为了重新训练模型，您将需要更新的、最近的**标记的**数据，因此您还需要一个过程来收集新的标记数据。小心不要注入过多的历史数据，因为如果最近的数据与历史数据相差太大，模型的效果可能会更差。您可以将最近的数据优先于历史数据。

另一个有趣的方面是，对于全新的数据，不同的 ML 算法可能会执行得更好。你应该不时地考虑不只是重新训练相同的算法，而是用其他算法进行实验。或者你可以更进一步，每次更新时，试着自动适应不同的型号并选择最好的型号。

现在，我们已经从一种模式转变为一种可持续的服务。虽然这并没有涵盖所有内容，但我希望它能为您提供基本需求和最佳实践的全面概述。

参考资料:

[1]迈克·马斯尼克(Mike Masnick)，为什么网飞从未实现赢得网飞 100 万美元挑战赛(2012)的算法，tech dirt:[https://www . tech dirt . com/articles/2012 04 09/03412518422/Why-网飞-Never-Implemented-Algorithm-That-Won-网飞-100 万-challenge.shtml](https://www.techdirt.com/articles/20120409/03412518422/why-netflix-never-implemented-algorithm-that-won-netflix-1-million-challenge.shtml)

[2]布雷克·索恩(Blake Thorne)，四个九及更高:高可用性基础设施指南(2018)，Atlassian 博客:【https://www.atlassian.com/blog/statuspage/high-availability 

[3] Alexandre Gonfalonieri，为什么机器学习模型在生产中退化(2019)，走向数据科学:

[https://towards data science . com/why-machine-learning-models-degrade-in-production-d0f 2108 e 9214](/why-machine-learning-models-degrade-in-production-d0f2108e9214)