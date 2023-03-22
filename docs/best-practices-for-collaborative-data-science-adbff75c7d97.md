# 协作数据科学的最佳实践

> 原文：<https://towardsdatascience.com/best-practices-for-collaborative-data-science-adbff75c7d97?source=collection_archive---------26----------------------->

## [办公时间](https://towardsdatascience.com/tagged/office-hours)

## *帮助确保项目交付真正商业价值的五种方法*

![](img/2016888e38714e0b13ff6caac0e711d2.png)

照片由[米利安·杰西耶](https://unsplash.com/@mjessier?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

考虑到所需技能的多样性，数据科学项目是协作技术工作的完美原型。然而，总体而言，随着世界在全球疫情中航行，大多数人在可预见的未来继续在家工作，协作变得更加困难。对移民和 H-1B 签证越来越多的限制加剧了这一问题，阻止了公司从美国以外雇佣技术工人

网络网络是远程协作数据科学可能会在这里停留。那么企业如何适应这种新常态呢？以下是在数据科学项目中实现远程协作的五种最佳实践。

**为成功做好准备**

建立模型需要大量的时间和精力。数据科学家可能会花费数周时间试图找到、捕获数据并将其转换为模型的适当特征，更不用说许多周期的训练、调整和调整模型以确保它们能够工作。然而，尽管如此，很少有模型能够投入生产。根据 VentureBeat AI 的数据，[只有 13%的数据科学项目进入生产](https://venturebeat.com/2019/07/19/why-do-87-of-data-science-projects-never-make-it-into-production/)，而在为企业交付价值方面， [Gartner 预测只有 20%的分析项目将交付提高绩效的业务成果](https://blogs.gartner.com/andrew_white/2019/01/03/our-top-data-and-analytics-predicts-for-2019/)。为什么失败率这么高？

因为，在最高层面上，数据科学和业务根本没有联系。为了确保更高的成功几率，数据科学家可以通过回答三个关键问题来启动每个新项目:

1.  我们有一个清晰的价值路径的业务问题吗？
2.  这个问题对我们来说可行吗？
3.  企业能否根据数据科学见解做出必要的改变？

提高数据科学项目的成功率需要数据科学团队和决策者之间的合作伙伴关系，以确保模型是适当的并且可以被采用。通过在开发开始前对这些问题进行标准化，数据科学团队可以构建一种可重复的方法来识别潜在业务问题的价值驱动因素，在模型开发期间获得业务支持，并与业务部门合作以增加其模型结果被采用的机会。

**设计并记录合作项目**

执行一个成功的数据科学项目需要广泛的技能和工作角色。数据科学经理、数据科学团队、数据工程师、部署和验证工程师、IT 管理员、数据对业务联络人和业务客户只是其中的一部分角色。考虑一下，你现在不仅仅是在与人合作:你还在与未来的人合作。

数据科学不像软件工程；它是概率性的，更基于研究，这意味着不是每个数据科学都会成功。然而，每个项目都代表了从现在起六个月内的一个项目的经验教训或灵感。

所有这些的一个关键是文档。不仅记录业务环境、可交付成果和代码，还记录过程、中间目标和关口、关键人物和关键见解。

此外，跨异构团队建立一套最佳实践允许那些团队协作，即使他们可能正在进行完全不同的项目。这些最佳实践包括在每个项目中有一套通用的定义明确的项目阶段和通用目录文件夹，以及更周到的要求，例如在开始项目之前必须执行的通用飞行前清单。

最后，慢下来。数据科学家和数据科学领导者经常疯狂地经营他们的组织以获得最终产品，但他们忘记了在这个过程中建立智力和组织知识。我想说的一件事是，数据科学需要更像生命科学研究实验室一样运作:例如，如果你试图为新冠肺炎创造一种疫苗，你失败了五次，你不会把你学到的东西扔进垃圾桶，对吗？那是黄金信息。你知道什么是行不通的，这可以引导你以更简化的方式去做什么。

**规范知识共享**

那么我们刚刚谈到的那五次失败？这就是所谓的“现有技术”，它是创新中最有价值的资产之一，尤其是在数据科学中。如果无法确保公司中的每个人都可以访问这些信息，您的数据科学家将会重新发明很多轮子。不同的团队会无意中复制相同的模型，而看不到其他人正在生成的工作。

提供一种跨业务单元和其他小环境共享知识(代码、文件、项目和模型)的简单方法消除了潜在的冗余，也促进了学习。例如，如果我需要构建一个预测心脏病的应用程序，我应该能够在我的组织的内部知识库中搜索“心脏病”，并且能够查看公司中其他任何人以前就心脏病做过的每个数据科学项目。此外，我应该能够看到他们使用的数据源，他们尝试的建模方法，他们考虑的交付形式因素，他们使用的软件环境版本，他们在此过程中产生的见解，等等。即使这些项目和我的不完全一样，我也能从中学到很多。

**创建可复制的工作单元**

有多少次你想，“我想运行我六个月前创建的那个项目，并将其集成到我现在正在做的事情中”，而你却找不到它？或者当您找到它时，由于包版本的变化或操作系统的升级，代码块不再运行的频率是多少？可能多得数不过来。这就是为什么您需要确保创建可重复的工作单元——尤其是在四个领域:代码、文件、环境和计算。Kubernetes 和 Docker 是使这种可复制性成为可能的基石。在一个精心编排的数据科学平台的手中，实验和模型都有完整的出处，可以很容易地复制。

**采用清晰的验证和部署框架**

您已经创建了您的模型，并准备投入使用，但是还有最后一个障碍:代码审查。简单地确保代码评审被清晰地定义和实现是一个好的开始。除此之外，实现简洁的性能测试管道可能看起来像(而且确实是)相当多的工作，但是在前端投入这种努力将会在客户满意度方面得到显著的回报。这与通过进行用户验收测试来确保项目满足服务水平协议密切相关。

最后，监控您的模型以确保它们实际工作是非常重要的。很多时候，模型在生产中遭受“数据漂移”:您已经获得了创建模型所依据的隐式数据，但是在生产中，您的模型会看到新的数据源。这些输入会改变结果吗？使用实时监控和警报可以帮助您跟踪数据漂移，并在模型漂移太远之前纠正模型。

很明显，远程协作将会一直存在，随着世界的不断快速发展，为什么不将您的数据科学实践与它一起带来呢？协作不仅仅是数据科学家在一个项目上一起工作；它包括与业务部门合作，正确记录代码和流程，建立现有技术库，确保可再现性，以及构建协作验证管道。使用本文中概述的最佳实践可以帮助您走向数据科学的成功。