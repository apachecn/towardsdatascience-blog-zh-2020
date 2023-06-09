# 车床 0.1.2 有什么新功能？

> 原文：<https://towardsdatascience.com/whats-new-in-lathe-0-1-2-b3d9bc96dff4?source=collection_archive---------74----------------------->

## 车床 0.1.2 中一些最激动人心的特性的回顾。

![](img/deb1a77bbbef7babf3bb0b148fa79fc1.png)

L 距离 0 . 1 . 2“butter ball”被合并到 master 并取代之前的车床 0.1.1 只有几个提交之遥。在车床 0.1.2 中已经呈现了许多令人兴奋和有趣的东西，并且有许多有趣的新东西需要实验——既有已实现的，也有计划中的。所以事不宜迟，我们来看看车床 0.1.2 有什么新功能！

# 宏指令

![](img/931e31083b94b8dc18465ac5fb70e840.png)

车床现在有一系列易于访问和利用的宏，用于车床内部的最基本操作。这还附带了一系列非常酷的实验性宏，你可能没有想到它们会被实现，这很可能会使机器学习在车床上变得更加容易。

首先，stats.jl 已经获得了执行统计测试的宏。正如您所预料的，这可以使统计测试更快。新宏的一些示例包括:

```
@t -> Independent T-test
@f -> F-test
@- -> Signs test
```

以及一些为方便起见而添加的基本统计宏:

```
@mu -> Mean
@r -> Correlation Coefficient
@sigma -> Standard Deviation
```

除此之外，还有一个非常酷的新精度宏，叫做@acc。这在某种程度上是未来努力的模板，但是@acc 宏的目标是能够在同一个函数中保持连续和绝对的准确性。不要再问 r2、广义分类准确度或平均绝对误差，很快一个机器学习模型就会为你做这些！在未来，我很乐意进一步扩展它，以包含一个更强大的模型和更受欢迎的验证方法，比如混淆矩阵。

# Powerlogging —有进一步实施的计划

Powerlogging 是一个非常酷的概念，已经在 STATA 软件中使用了一段时间。它允许统计学家用数学方法计算模型功效的适当样本量。如果您想了解更多关于 powerlogging 本身的知识，我已经写了另一篇文章，深入讨论了它是如何工作的，它做了什么，以及如何从头开始编写代码。

[](/power-analysis-the-coolest-thing-that-youve-never-heard-of-476d35c18161) [## 电源分析——你从未听说过的最酷的东西。

### 将权力投入到您的物流决策中。

towardsdatascience.com](/power-analysis-the-coolest-thing-that-youve-never-heard-of-476d35c18161) 

虽然这本身很酷，但我有很多想法，谁可以将它进一步实现到模型中，甚至可能是预处理。这可以通过使用不同的训练样本大小来实现，也可以通过同时测试不同的样本来获得更准确的结果。所有这些都可能等同于更高的后勤准确性，这绝对是非常酷的！

# 分割

我最终得到的印象是车床包装太大了。因此，它们被分开并包含在内。虽然这不会对最终用户产生影响，但对于贡献者来说，这无疑是一个显著的增加。这将使在车床上操作特定组件比以前容易得多，并允许像宏、模型和公式这样的东西驻留在它们自己的位置上。

# 证明文件

虽然 http://lathe.ai 服务器目前正在进行维护，但 lathe 终于有了一个自动更新文档的网站！这当然会使使用文本文件时使用车床比使用 REPL 更容易。在这个新的文档站点发布之前，关于车床的文档只能通过 Julia？()方法。虽然我当然认为在大多数情况下这仍然是处理文档的一个更好的方法，但是我当然能够理解能够滚动浏览网站的吸引力。此外，能够在谷歌上找到你的答案总是一件很棒的事情！

在新网站的顶部，车床的文档已被修改，以包括更多的信息，并彻底解释如何在车床类型使用。当然，由于车床仍然处于开发的早期，这只会随着开发的深入而改进，这是令人兴奋的！

# 结论

这一次，车床增加了一些令人兴奋的新功能，但是这个软件的未来肯定是非常光明的。未来的车床更新将提出进一步的统计库，增加更多的模型，并增加更多的预处理功能。虽然有很多工作要做，但我仍然对车床自诞生以来的发展感到高兴。