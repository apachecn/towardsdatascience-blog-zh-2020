# 具有复杂和嵌套数据类型的大数据转换

> 原文：<https://towardsdatascience.com/big-data-transformations-with-complex-and-nested-data-types-c1b9c45ca792?source=collection_archive---------22----------------------->

## Apache Spark 编程技巧和诀窍

![](img/8d4bef324763be62c0f624781bd8fe4c.png)

劳拉·奥克尔在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

# 介绍

***Apache Spark*** 是一个分布式计算大数据分析框架，旨在跨机器集群转换、设计和处理海量数据(想想万亿字节和千兆字节)。经常使用不同的数据集，您会遇到复杂的数据类型和格式，需要昂贵的计算和转换(想想*物联网*设备)。极其复杂和专业，在扩展大数据工程工作方面， ***Apache Spark*** 是其工艺的大师。在这篇博客中，我将使用原生的 *Scala* API 向你展示 1。)如何用嵌套 schema ( *array* 和 *struct* )对半结构化 *JSON* 数据进行扁平化和规范化，2。)如何透视数据，以及 3 .)如何将数据作为*拼花*模式保存到存储中，以便进行下游分析。注意，同样的练习可以使用 *Python* API 和 *Spark SQL* 来完成。

# 步骤 1:规范化半结构化嵌套模式

1a。)让我们来看看我们漂亮的多行 *JSON* schema(来自我最喜欢的视频游戏的虚拟数据)。

1b。)接下来，为了提高性能，我将把我们的模式映射并构造为新的`StructType()`，以避免在读取 *JSON* 数据时触发不必要的 ***Spark*** 作业。

1c。)现在，我们可以打印我们的模式并检查数据，您可以看到，由于涉及到的数据类型，这是一件令人欣喜的事情。该数据集中总共有 12 行 5 列，但是我们在本机模式中看到 2 行 2 列。

1d。)是时候使用内置的***Spark****data frame*API 函数(包括`explode`)将`array`数据类型中的元素转换为单独的行和点`*`，这些函数解包`struct`数据类型中的子字段。由于*子类*和*超级*列具有一对一的元素对映射，slick `arrays_zip`函数也将与点选择一起使用，以避免在分解期间创建额外的行组合。

1e。)是时候检查转换后的数据集及其模式了。正如所料，它返回 12 行 5 列。

# 第 2 步:转换和重塑数据

2a。)下一个练习将采用我们的展平数据集并应用`pivot`函数，这将触发大范围转换，将特定列的不同值转置到各个列中。可以在聚合或不聚合的情况下执行透视。对于使用许多列*也称为*功能作为学习算法输入的数据科学用例，无聚合通常是必需的模式。一个有效的性能提示是在`pivot`函数输入中指定您的唯一值，这样 ***Spark*** 就不必触发额外的作业。

# 第三步:写入拼花格式

3a。)最后一个练习将简单地把我们的数据写到存储器中。*将使用 Parquet* 格式，因为它是一种可拆分的文件格式，经过高度压缩以提高空间效率，并针对列存储进行了优化，因此非常适合下游大数据分析。

# 结论

这些练习只是触及了 ***Apache Spark*** 对于大数据工程和高级分析用例的皮毛。感谢你阅读这篇博客。