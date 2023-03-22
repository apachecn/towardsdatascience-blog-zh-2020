# DevSecOps vs DataOps vs MLOps

> 原文：<https://towardsdatascience.com/devsecops-vs-dataops-vs-mlops-93b49f0282b8?source=collection_archive---------23----------------------->

## 为您的项目选择正确的工作流程

![](img/3233a5ba709a0adff9d888fa6e26da62.png)

马文·迈耶在 [Unsplash](https://unsplash.com/s/photos/technology?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

自从敏捷宣言在 [2001](https://agilemanifesto.org/history.html) 开始，许多软件开发方法出现了，每一种都试图改进过程。虽然基本的敏捷宣言仍然指导着工作流，但是今天主要的努力已经扩展到打破广泛领域的孤岛。这是通过将孤立的部门统一到协作团队中来实现的。

起初，开发和运营团队被统一到 DevOps 团队中。今天，越来越清楚的是，DevOps 是不够的。安全性也是一个关键的方面，需要在整个过程中解决，而不是在最后解决。因此，DevSecOps 应运而生，它为开发周期增加了安全性。为了确保数据库操作和机器学习操作顺利运行，还创建了 DataOps 和 MLOps。

本文研究了这四种主要方法——devo PS、DevSecOps、DataOps 和 MLOps——为何时以及如何使用每个工作流提供了指导原则。

# 什么是 DevSecOps？

DevSecOps 是 DevOps 与安全团队的结合。它旨在确保在开发和操作任务中分担安全责任，并实现“安全即代码”的管理。实现 [DevSecOps](https://resources.whitesourcesoftware.com/blog-whitesource/devsecops) 通常由已经习惯使用 DevOps 策略的团队承担。

DevSecOps 团队使安全成员能够在开发和部署操作与安全问题之间架起一座桥梁。通过打破团队之间的孤岛，他们可以帮助将安全实践集成到现有的工作流中，减少摩擦，并从一开始就确保产品更加安全。

DevSecOps 与 DevOps 的不同之处在于工具和思维方式。这些实现将测试转移到开发过程的左侧，并专注于教授安全性最佳实践。这个想法是从一开始就防止漏洞进入项目。

例如，DevSecOps 团队经常在集成开发环境(ide)中集成静态应用程序安全测试(SAST)工具。这意味着安全审计和测试甚至在提交代码进行传统测试之前就开始了。同样，团队的关注点可能包括云安全状态管理(CSPM)或环境部署步骤中的合规性审计工具。这有助于在环境上线之前发现错误配置。

# 数据运营:利用 DevSecOps 原则进行安全数据分析

随着 DevSecOps 从 DevOps 发展而来，其他业务单位也开始结合 DevOps 原则，从战略中分支出来并不断发展。一个例子是 DataOps，它有一个数据分析的基础。

DataOps 采用 DevOps 的实践和价值观，并将其扩展到数据分析工作流和目标。它将重点放在协作和分担责任上，并将其转移到收集、存储、分析、保护和交付数据的工程师和管理员身上。

DataOps 旨在简化现有的大数据流程，同时提高工作负载价值和安全性。它通过将安全性集成到数据的编码、保留和交付中来实现这一点，同时牢记分析和存储工作流之间的依赖关系。这有助于确保更可靠的访问，并且可以[提高价值实现时间](https://www.forbes.com/sites/forbestechcouncil/2020/05/15/bringing-time-to-value-to-the-customers-doorstep/#5adb599210a2)。

# 数据运营基础设施

实施数据运营需要的不仅仅是心态或工作流程的改变；它还需要基础设施的改造。例如，关注敏捷反馈循环和自动化的新架构模式。

DataOps 还经常要求团队实施专为分析和存储设计的下一代技术。例如，团队通常需要采用冗余的、基于集群的存储来确保数据处理管道的高可用性和可伸缩性。可能还需要配置和部署环境，以确保隔离和遵守数据隐私法规。对于生产和测试或开发环境都是如此。

DataOps 团队可能需要解决的另一个变化是所支持的工作负载的多样性。为了让管道提供敏捷性，解决方案需要集成到单个基础设施中，而不是由任务或团队来分发。这意味着整合大数据分析工具，如 [Spark 和 Hadoop](/big-data-analytics-apache-spark-vs-apache-hadoop-7cb77a7a9424) ，日志聚合器，如 Sumo Logic 和 Splunk，以及监督工具，如 Prometheus 和吉拉。

# DevOps 与 MLOps

MLOps 是 DevOps 的另一个分支。在其中，DevOps 原理和工作流被应用于机器学习操作，例如模型训练和部署。它实现了流水线和自动化，使训练操作和完成的模型集成到软件产品中的流程更加顺畅。

在许多方面，MLOps 也与 DataOps 重叠，因为它也需要数据集的处理、维护和安全性。然而，机器学习工作负载的某些方面需要不同的关注点或实现。这些差异包括:

*   **团队技能** —在 MLOps 中，团队需要吸收 ML 研究人员和数据科学家，他们通常不是经验丰富的软件工程师。这些成员专注于实验、模型开发和数据分析，可能不具备执行应用程序开发、操作或安全任务所需的技能。
*   **开发**——与传统的更加线性的开发不同，ML 通常是高度实验性的。团队需要能够操作参数和特性，并经常重新训练模型。这需要更复杂的反馈回路。此外，团队需要能够在不妨碍工作流可重用性的情况下跟踪操作的可重复性。
*   **测试** —在 MLOps 中测试需要在 DevOps 或 DevSecOps 中通常完成的方法之上的额外方法。例如，MLOps 需要测试数据验证、模型验证和模型质量测试。
*   **部署** —根据您正在部署的 [ML 模型](/the-beginners-guide-to-selecting-machine-learning-predictive-models-in-python-f2eb594e4ddc)的类型，您可能需要为正在进行的数据处理和培训建立管道。这需要多步流水线，可以处理再训练步骤以及验证和重新部署过程。没有 MLOps，这是手动完成的，但有了它，这些步骤应该是自动化的。
*   **生产** —生产中的模型可能会面临标准应用程序部署不会面临的挑战，例如与不断发展的数据配置文件相关的问题。这可能导致模型衰退，可靠性降低。MLOps 实现需要包含持续的监控和审计，以确认模型是可用的和准确的。如果精度下降，模型需要被召回并修正。

MLOps 与 DevOps 不同的另一个重要领域是如何构建持续集成/持续开发(CI/CD)管道。在 MLOps 中，CI 组件需要扩展到测试和验证数据模式、数据和模型。CD 组件需要支持培训管道以及最终模型预测服务或应用程序的部署。此外，还有另一个组件，持续测试(CT ),它需要被考虑以实现自动的模型再训练和改进。

# 结论

DevSecOps 将开发、安全和操作角色统一到一个统一的团队中。工作流程通常是自动化的，反馈循环应该是连续的。这确保团队成员将时间花在关键任务上，并不断改进和保护代码。

DataOps 工作流将协作和自动化等 DevOps 原则用于数据管理工作流。此工作流有助于消除源自数据级别的孤岛。MLOps 工作流也利用了 DevOps 原则，但这里的应用是在机器学习操作中。

选择工作流程是一个关键的组成部分，它需要所有相关方的合作。在实现工作流之前，您应该确保所有团队成员都具备必要的技能，工作流适合您的项目，并且您拥有用于测试、部署和生产的所有必要工具。