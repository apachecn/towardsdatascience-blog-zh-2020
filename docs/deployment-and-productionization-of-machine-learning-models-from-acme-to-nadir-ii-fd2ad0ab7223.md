# 机器学习模型的部署和生产—从顶点到最低点— II

> 原文：<https://towardsdatascience.com/deployment-and-productionization-of-machine-learning-models-from-acme-to-nadir-ii-fd2ad0ab7223?source=collection_archive---------51----------------------->

## **建造机器学习家园的砖块和混凝土:系统和架构**。

机器学习系统是一个包括整个基础设施(包括从 RAM 到正常平台构建设备的所有硬件的基础设施)的实体，然后它包括一个操作系统，该操作系统为我们的机器学习任务提供动力，并通过提供一个强大的背景使它变得更简单。它还包括所有的应用程序、软件和工具。它渗透到所有的配置方面，如兼容性，以及数据和一点一点地记录工作流程等部分。

机器基础设施包含了机器学习工作流程的几乎每个阶段。为了训练、测试和部署机器学习模型，您需要来自数据科学家、数据工程师、软件编程工程师和 DevOps 工程师的服务。该基础设施允许来自所有这些领域的人员进行协作，并使他们能够为项目的端到端执行进行关联。

工具和平台的一些例子是 AWS(亚马逊网络服务，谷歌云，微软 Azure 机器学习工作室，kube flow:Kubernetes 的机器学习工具包。

架构处理这些组件的安排(上面讨论过的事情),并且还处理它们必须如何与它们交互。可以把它想象成建造一个机器学习之家，砖块、混凝土、铁是基础设施、应用程序等不可或缺的组成部分。建筑通过使用这些材料来塑造我们的家。类似地，这里的架构提供了这些组件之间的交互。

**版本化和再现性**:“IT”IT 术语

我们先来了解一下什么是版本化和可复制性。

**版本控制**:

这是常见的软件和 It 实践，您创建和管理一个产品的多个版本，所有这些版本具有相同的一般功能，但是经过改进、升级或定制。

在机器学习中，为给定的数据建立不同的模型，我们通过版本控制工具如 **DVC** 和 **Git 来跟踪。版本控制将跟踪在每个阶段对模型所做的变更，并保留一个存储库。**

**再现性**:

在研究阶段，我们建立机器学习模型的阶段。一旦模型被测试，然后才被部署。部署后，该模型被假定用于构建该模型的相同数据，并预期给出相同的结果。我们部署整个模型管道，而不仅仅是算法。可再现性确保了复制模型的能力，使得给定相同的原始数据作为输入，两个模型返回相同的输出(相同的数据意味着相同的特征等)。

让我来解释一下是什么影响了再现性，这样可以帮助你更好地理解。假设你之前建立的模型给出了 20%的误差。假设您的数据库已经更改，并且当您尝试再次构建模型时，您不知道数据库正在向模型中注入额外的定型数据，因此导致了额外的错误。

有很多因素会影响再现性。因此，这种版本化和版本控制有助于我们跟踪它。大多数情况下，它是在模型改进过程中出现的。

从再现性到配置问题到数据问题，还有各种其他系统挑战。在体系结构中，有一些关键点，如可再现性、可伸缩性:模型为许多人服务的能力，以及其他必须牢记在心的点。

因此，撰写本文主要是为了让您深入了解部署中使用的基本术语。我希望你喜欢这篇文章。