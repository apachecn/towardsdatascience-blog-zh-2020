# 如何选择范围最广的软件包？

> 原文：<https://towardsdatascience.com/how-to-choose-the-software-package-with-the-widest-scope-a8851f29d8b7?source=collection_archive---------44----------------------->

## 从数据科学的角度来看。

**TL；博士:**

*你对软件工具最大的愿望是什么？疯狂一下，问问自己如果我想拿这个拿那个，然后以最小的努力把它们组合/比较/组合在一起？最有可能的是，某个领域专家已经想出了解决这个问题的好办法。他们可能需要将它包装在花哨的软件结构下，这种结构从一开始就不直观，而且有自己的行话。是否值得学习它，并利用您将来可能会发现的大范围解决方案？大范围包还有什么特征？*

![](img/257c9bbcd13ccd50ae397e3f1ac531aa.png)

[图片来源](https://unsplash.com/photos/ipmwlGIXzcw)

**ML 示例:**您运行一个机器学习预测分析，比如简单的线性回归，然后您希望将其与另一个模型进行比较，比如正则化回归(如 ridge，lasso)。你如何为此整合你的代码？最简单的方法可能是“复制- >粘贴”您的回归模型代码，更改模型部分，用唯一的名称保存输出，与以前的输出集成(假设您以统一的方式保存了列名和其他结构)，并进行比较。但是有趣的事情仅仅从这里开始…如果您想要添加更多的模型，其中一些模型也需要调整(通过一些优化过程选择参数的最佳值)，或者您想要尝试一些由多个模型组成的集成技术(打包、提升、堆叠)，该怎么办？你还打算从头开始做所有的事情吗，复制粘贴，编织各种函数/包的结果，每个函数/包都有自己的名字和结构？希望不是…有人已经找到了这个挑战的解决方案，并编写了一个[包来统一这个繁琐的过程](/meta-machine-learning-packages-in-r-c3e869b53ed6)，并将您最疯狂的愿望列表聚合到一个单一的、全面的生态系统中，这将为您完成这项脏工作。

**时间序列示例:**

你运行一个预测模型，比如说 ARIMA。你也希望将它与 ETS 进行比较。同上，在完全相同的假设、随机种子和其他约定下，通过简单地指定两次独立运行的输出名称来创建它们的系综有多容易？然后…您对数据集中的总体观察值运行它，但是您也希望对数据中的每个分层子组再次运行它。您可以在循环中执行此操作，但是如果工具的范围已经允许您指示嵌套组，并且在您对分析进行分层/重新折叠时也会考虑到它，该怎么办呢？

**‘去过那里……做过那件事’**

在这两个例子中，目标是识别已经完成这项工作的包，而不需要重新发明轮子，也不需要在争论、统一和其他您可以避免的繁琐工作上投入宝贵的时间。因为…其他人，一个领域专家，已经找到了更好的解决方法。是什么让他们成为领域专家？嗯，在花了很长时间处理这些挑战，并且对当前的解决方案不满意(当时)之后，激励他们写自己的最先进的解决方案。他们玩这些工具的时间已经够长了，这促使他们设计一种更好的方式来无缝地组合软件的各种组件。

**如何识别具有你所需要的范围级别的包？我们来贪一下…如何识别范围最广的包？**

当你学习一个新的领域(机器学习、时间序列……)时，除了你自己的任务之外，你可能不知道这个领域中存在的丰富工具，或者这个领域处理的常见问题。但是随着你了解的越来越多，你可能会遇到一些很酷的解决问题的方法，这些方法可能会在以后遇到。

对我来说，这就像…“你为什么不提前告诉我这是我们以后要做的…如果我以前知道，我可能会以不同的方式开始构建我的工具，这样我就可以添加这个新的功能/解决方案，而不必改变我的工具的设计(范围)”。

所以诀窍是…想象你想问/分析的下一步是什么。在上面的例子中，它是 ML 的集合，以及时间序列的[加权分层/组分层。的确，您可能不需要这些花哨的解决方案来解决您当前的问题，但是通常来说，一个被设计来处理更高层次问题的包，对于简单的、核心的步骤/组件，也会有一个好的解决方案。](https://otexts.com/fpp2/hierarchical.html)

**重点在哪里？没有免费的午餐**

当然，这是有代价的。以一种内聚的方式识别和设计软件(方法)的核心模块并不简单。适应这些块的无缝组合通常需要一些更高层次的框架，这些框架有自己的学习曲线。它可以是由[原子和非原子](https://medium.com/@drorberel/bioconductor-s4-classes-for-high-throughput-omic-data-fd6c304d569b)结构组成的对象结构(如面向对象的类、嵌套表/模型等)。他们通常会有自己独特的行话，你不熟悉，因为…嗯，他们必须发明它。毕竟这是个新事物。这些可能一开始并不直观，但通过设计被精心构造以满足独特的需求*。*

**取舍:**

根据我的经验，值得花时间学习如此复杂的结构，并利用大范围的解决方案，而不是在以后面临类似挑战时重新发明一个次优的解决方案(是的，你会的！).

大范围包的典型特征是丰富的*文档*，以及对稳定的生态环境(包)的依赖，这将确保您的代码在扩展到新的极限时不会“中断”。

大范围的软件包也以作者自身经历的*血统*为特征，在艰难、多风的学习曲线中。说我迄今为止开发的工具有一个 [*范围蔓延*](https://medium.com/free-code-camp/scope-creep-and-other-software-design-lessons-learned-the-hard-way-edacf021965b) 需要一些勇气，所以我将放弃它，并从零开始[重新设计它](https://medium.com/analytics-vidhya/meta-machine-learning-aggregator-packages-in-r-round-ii-71ee1ff68642)，所以它更好地适合我当前的范围(这在回顾中可能再次受到限制，从现在起 5 年后，当该领域扩展到更广的范围时)。

当软件包文档中有一个比较不同竞争软件包特性的表格，明显地强调了它自己的优势时，问问你自己:这是我需要的范围吗？包范围的限制是什么？它依赖于哪些其他的生态环境，并且可以很容易地与它们整合？它能让我根据自己的需要扩展它，并为它添加新的特性吗？

**警告:避免单一功能的疯狂包装包**

如果一个包试图实现一个大范围功能，但它是一个带有太多参数的单一函数，将其他嵌套步骤包装在里面，那么它可能不是您的最佳选择。这个“包装器”功能与上面描述的大范围包的区别在于它的结构。疯狂包装器功能可能缺乏其组件的独立设计，以及它们的内聚结构。Crazy-wrapper 函数不能扩展到其他用途，并且只限于预定义的参数值。另一方面，宽范围函数由于其结构的复杂性而避免了这种陷井，这使它能够以与其他组件很好地集成的方式存储各种数据类型和参数值。

**结论:**

通过利用其他领域专家工具，让自己成为领域专家。当你问自己为什么他们要创造这个奇怪的复杂物体，并用一个新的词来命名它时，一定有一个很好的理由。要有耐心，学习它，并享受未来的花式技巧的成果。

查看我的其他[博客文章](https://medium.com/@drorberel)和我的 [GitHub 页面](https://drorberel.github.io/)获得更多有趣的阅读。[领英](https://www.linkedin.com/in/dror-berel-1848496/)。