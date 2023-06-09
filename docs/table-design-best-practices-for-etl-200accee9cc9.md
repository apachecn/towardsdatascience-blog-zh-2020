# 表 ETL 的设计最佳实践

> 原文：<https://towardsdatascience.com/table-design-best-practices-for-etl-200accee9cc9?source=collection_archive---------33----------------------->

![](img/9d620be7d258efe67ae34f5488f43b94.png)

[田宽](https://unsplash.com/@realaxer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/pipeline?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍照

## 如何为 ETL 管道设计源系统表

不久以前，在源系统(应用程序数据库)中设计表的方法曾经是——我们不关心 ETL。弄清楚后，我们将专注于构建应用程序。过去几年是 ETL 方法发展的大好时光，许多开源工具来自一些大型科技公司，如 Airbnb、LinkedIn、Google、脸书等等。随着云成为主流，Azure、谷歌和微软等提供商已经确保他们构建并支持数据工程领域的所有开源技术。

我参与过许多 ETL 项目，其中一些失败得很惨，其余的都成功了。ETL 项目出错的方式有很多。我们今天将讨论最重要的一个方面——源系统中的表设计。

> ETL 管道和构建它们的源系统一样好。

不管在 ETL 管道的 T 层做了多少努力，这个说法都是完全正确的。转换层通常被误解为修复应用程序和应用程序生成的数据的所有错误的层。这绝对不是真的。不多说了，让我们看看在设计将要被 ETL 到目标系统的表时，您应该考虑的最低要求——

# **强制唯一性**

这一点应该不说，但我看到系统也没有强制执行(作为设计的一部分)。唯一键本质上是单列还是组合并不重要。但是，可能会要求用户在没有惟一键的情况下对表进行满负荷，并在每次满负荷后推断出变化。这个解决方案实际上比听起来更糟糕。

# **启用增量 ETL**

使数据工程师能够通过访问`created_timestamp`和`updated_timestamp`等简单字段来识别新的和更新的记录。确保这两个字段都是由数据库而不是应用程序填充的。如果要从应用程序中填充日期时间或时间戳字段，应该有一个单独的日期时间或时间戳字段。这些应该被定义为—

```
1\. created_timestamp TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
2\. updated_timestamp TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
```

只追加主键总是递增的表可以正常工作。您不需要为这些设置审计时间戳列。

# **定义&记录关系**

在大多数情况下，我们将关系数据库作为源系统来处理。因此，理解源系统中的数据流和沿袭是非常重要的。在大多数情况下，负载的目标系统中的数据流和沿袭保持不变，尽管这不是强制性的。这里有两件事会有帮助——来自产生数据的应用程序的服务架构图和源数据库的 ER 图。

# 那又怎样？

所有这些问题都可以被完全或部分解决，即使这些点在源系统中没有被注意到，但是没有一个解决方案是可持续的。是的，这就是开始构建一个整洁的 ETL 管道所需要的一切。

作为一个规则，ETL 系统的任务应该仅仅是通过一个通用的转换层将数据从一个地方移动到另一个地方(这个层不处理 bug，特殊的一次性情况)。记住垃圾进垃圾出的普遍原则——如果源系统中有错误的数据，那么目标系统也会有错误的数据。

我在很多地方看到的一个实践是，数据团队试图修补有问题的数据，并暂时处理它。它通常会一直工作到冲刺阶段结束，而同样的问题总是会回来困扰你。抵制诱惑，不要养成像这样解决问题的习惯。正确的做法是报告问题，修复源系统中的数据，并在有问题的时间段内进行干净的重新加载。与显示在应用程序 UI 和 data BI 仪表板上的不同数据相比，重新加载更容易证明。

# **参考文献**

[](https://medium.com/@rchang/a-beginners-guide-to-data-engineering-part-ii-47c4e7cbda71) [## 数据工程初学者指南—第二部分

### 数据建模、数据分区、流程和 ETL 最佳实践

medium.com](https://medium.com/@rchang/a-beginners-guide-to-data-engineering-part-ii-47c4e7cbda71) [](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/) [## 设计数据密集型应用程序

### 数据是当今系统设计中许多挑战的核心。困难的问题需要解决，例如…

www.oreilly.com](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/) [](https://www.timmitchell.net/post/2017/01/10/why-data-warehouse-projects-fail/) [## 为什么数据仓库项目会失败

### 数据仓库项目是组织可以采取的最明显和最昂贵的计划之一。可悲的是，他们…

www.timmitchell.net](https://www.timmitchell.net/post/2017/01/10/why-data-warehouse-projects-fail/)