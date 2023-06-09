# 机器学习操作基础设施的观点

> 原文：<https://towardsdatascience.com/a-view-on-machine-learning-operations-infrastructure-e2bbc7cf0bdc?source=collection_archive---------46----------------------->

## 笔记本之后的现实:如何开发一个健壮的框架来确保对机器学习操作的控制

生成一个工作的(产生价值的)机器学习模型不是一件容易的事情。它通常涉及先进的建模技术和技能稀缺的团队。然而，这只是更复杂任务的第一步:将模型部署到产品中并防止其退化。

即使通过云转移得到缓解，至少三分之二的 IT 支出仍然集中在维护模式任务上。关于 ML 相关项目的这种划分是否成立的研究仍然很少，但我认为这一比例甚至会显著增加，因为 ML 工作负载有更多的“流动”输入和更少的控制杠杆，如下所示:

![](img/ec94389726ca9c0215a12dfc0a3a4d22.png)

**图 1**—ML 工作负载维护中可变性和控制的影响

本质上，维护主要是由我们对系统中不同组件的可变性和控制水平驱动的。如图所示，有理由得出这样的结论:机器学习工作负载更倾向于维护任务。更糟糕的是，数据和代码(业务角色)的演进路径不一定需要一致。这在[机器学习系统中隐藏的技术债务](https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf)中有很深入的解释

> 有理由得出结论，机器学习工作负载更倾向于维护任务

因此，绝对有必要开发一个健壮的框架，以确保一旦我们的模型被部署到生产中，就能控制机器学习操作，同时确保模型的质量及其发展不受损害。

开发模型的科学(艺术)是一个被充分研究的领域，甚至有模型开发的行业参考框架，如 [CRISP-D](https://en.wikipedia.org/wiki/Cross-industry_standard_process_for_data_mining) M，特定的 [EdA 方法](https://en.wikipedia.org/wiki/Exploratory_data_analysis)，所以在本文的其余部分，我们将假设我们已经有了一个具有可接受性能的经过训练的模型。

*大规模运行机器学习，我们需要什么基础设施？*

简而言之，我们需要设计三个大平台，当然除了构建初始模型、运行实验等的开发平台，还有另一个跨功能平台，如代码库、容器注册表、调度程序或监控系统。下图描述了这些平台:

![](img/a849a9cf023c4b90aa3407cd771acc5f.png)

**图 2 —** 基础 ML 平台组件

**特色店内**

本质上，特征库将特征工程过程与其使用分离。这对于输入数据受制于复杂的特征转换逻辑或一个特征被多个模型使用的情况尤其有用，在这些情况下，特征存储是一个很好的工程组件，因为它隐藏了复杂性并提高了可重用性。但是，在某些情况下，我们可以跳过此组件，例如，用于训练模型的数据处于其自然状态，或者模型本身包含特征生成器(例如，卷积、双向或嵌入层)。

![](img/a14dc867316fccf21787cf7289354714.png)

**图 3 —** 功能商店内的组件

特征库由许多元素组成:

*   *摄取:*该组件负责将原始数据加载到特性存储存储中。应该支持批处理和在线摄取路径。
*   *特征转换:*该组件负责实际计算特征，同样应支持批处理和在线处理。设计该组件时，计算时间性能至关重要。
*   *特征服务层*:实际为下游处理提供特征的组件。同样，可以在线或批量检索特征。

**训练平台内**

训练装备的目标是找到并产生最佳模型(在特定时间点),给定:(I)初始模型架构，(ii)一组可调超参数，以及(iii)历史标记特征集。

下图突出了我认为应该存在的主要组件，以确保顺利和有效的培训操作。

![](img/a5a9a3b76771a165066d0e83c3a04cf7.png)

**图 4 —** 训练设备内部的组件

训练平台的输出是我所谓的*“黄金模型”*，换句话说，就是将在推理平台中部署的架构、权重和签名。为了产生这些资产，几个组件必须介入。

*   *重新训练检查器*:该组件任务是检测何时需要重新训练当前黄金模型，有许多情况下必须引发重新训练事件。我建议部署一些评估人员来检查再培训条件。一些例子可以是特征的改变(添加或删除)、训练集中的统计差异(数据漂移)、或者训练数据和服务数据之间的差异(偏斜)、或者只是准确性度量的下降。生成的模型应该被传递给 promoter 组件，该组件将拥有将它部署到生产环境以及如何部署的最终决定权。
*   *黄金模型循环*:这可能是最关键的一步，它实际上执行了训练。因此，在设计系统时，应考虑性能因素(例如，分布式基础设施和对硬件 asics 的访问)。另一个职责是生成模型签名，明确定义输入和输出接口以及任何初始化任务(如变量加载器)。
*   *下一个黄金模型循环*:该组件旨在通过不断优化(或试图优化)当前黄金模型来发现潜在的新模型。有两个子循环，一个用于优化超参数(例如学习率、优化器..)和另一个用于启动对新模型架构(例如层数)的搜索。虽然有两个独立的循环，但是新的模型架构候选可以在超参数循环上进一步细化。该组件可能是资源密集型的，特别是如果搜索空间很大并且优化算法(例如网格搜索、hyperband)是贪婪的。从工程角度来看，应该考虑可恢复操作的检查点和作业优先级机制等技术。在采取任何额外措施之前，应进一步评估该组件的输出。
*   *模型发起人*:该组件负责发布准备投入生产工作的模型，因此这一步需要进行大量的测试。在任何情况下，正如我们将在推理装备中检查的，没有新的模型将被公开部署到他们所有的潜在用户群。
*   *元数据存储*:这个组件集中了所有与训练阶段相关的元数据(模型库，参数，实验..)

**预测装置内部**

预测平台的主要目标是执行推理。下图展示了实现这一目标的一组组件。

![](img/15b224ed87453709ae2e7be0f6ff921e.png)

**图 5 —** 预测试验台内部的组件

推理阶段有几个组件:

*   *特性转换器:*即使已经有了一个特性存储库来将特性从数据生产系统中分离出来，我认为特性转换器仍然可以在推理时将低级的特定操作应用到潜在的可重用和更抽象的特性中。对于在线系统，延迟要求至关重要。
*   *调度程序:*调度程序的目标是将请求路由到特定的预测端点。我相信每一个请求都应该经过试验，这就是为什么调度员应该能够将呼叫重定向到一个特定的或许多现场试验，黄金模型或两者。每一个未经实验的请求都是一个改进机会的丧失。
*   *预测主干:*预测装备的马力取决于该组件，因此从工程的角度来看，针对传统的非功能性需求(如性能、可伸缩性或容错)进行设计至关重要。
*   *缓存层:*低延迟键值存储，快速响应重入查询。它必须实现经典的缓存机制(失效、基于特征散列的密钥计算、LRU 队列..)
*   *黄金推广者/去推广者:*随着 A/B 测试的进行，我们可能会达到这样一个点，其中一个真实实验实际上比当前的黄金模型更具性能，该组件任务是分析元数据，特别是特征存储中的基础事实数据，以建议用一个实验替换黄金模型。
*   *型号预热器:*当冷启动情况发生时，确保缓存和内存预热的组件(例如，新型号升级)
*   *解释器:*实现模型可解释性逻辑的组件(如锚点、CEM..)并为给定的请求返回它
*   *元数据存储:*该组件集中了与预测阶段相关的所有元数据(实时实验性能、预测数据统计…)

**平台支持的一些用户旅程**

这种架构可以表达几个旅程，我的目标不是提及所有旅程，但我想强调几个有趣的旅程:

*在特征生成时*

*   合成一个复杂的要素并实时提供
*   编写一个踢 LRO 的复杂特征，并在许多模型中一致使用
*   在不影响转换和服务逻辑的情况下更改/更新特征信息生产者

*训练时*

*   启动重新训练(分布式)作业，由训练集中包含的新功能触发
*   基于数据(要素)依赖性的模型评估器
*   为当前的 DNN 模型发现一种新的、更高性能的架构
*   优化已部署模型的学习速度

*在预测时间*

*   逐步推广新的黄金模式，将其覆盖范围扩大到所有人群
*   查询预测及其黑盒解释

*可管理性*

*   检查模型、特征、签名版本

**可用于部署的技术**

我们可以使用大量开源软件来构建一个包含上述所有组件的平台，但在考虑独立设计每个组件之前，我们可以用一种标准和统一的方式来解决非功能性需求，如可扩展性、安全性或可移植性，这不是很好吗？

幸运的是，我们可以依赖 kubernetes 作为部署组件的主要平台。下图显示了一份提案，其中包含开源产品/项目*的组件映射。

![](img/d27f30d50f59c85bdb39968d7885d485.png)

**图 6 —** ML 平台开源实例化

*FEAST 和 kubeflow 集成目前正在[进行中](https://github.com/kubeflow/kubeflow/issues/2141)

为了让事情变得更简单， [kubeflow](https://www.kubeflow.org/) 已经以一种很好的方式打包了所有的组件，所以大部分的集成已经完成。

**结论**

甚至有人会认为，运行机器学习操作与传统操作有根本的不同，大多数软件工程原则实际上都成立，它们只是在不同的上下文中应用。在本文中，我们展示了一个逻辑高级架构，可以使用开源组件(如 kubeflow)轻松部署。

我在这里发布了一些关于这个主题的组件和示例笔记本[。](https://github.com/velascoluis)