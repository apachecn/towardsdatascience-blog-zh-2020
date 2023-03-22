# 提升数据科学项目的 4 种软件开发技术

> 原文：<https://towardsdatascience.com/4-software-development-techniques-to-level-up-your-data-science-project-59a44498ca3f?source=collection_archive---------27----------------------->

## 让您的项目更清晰、更高效、更专业

![](img/beb16c50b78d5e4a2807c3aac1569624.png)

照片由[负空间](https://www.pexels.com/@negativespace)发自[像素](https://www.pexels.com/photo/dark-computer-green-software-225769/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

软件开发是开发人员和程序员设计、编写、记录和测试代码的过程。无论您使用什么编程语言，或者您的目标应用领域是什么，遵循良好软件开发的特定指导方针对于构建高质量、可维护的项目是必不可少的。

数据科学项目——可能比其他类型的软件项目更多——应该以可维护性的心态来构建。这是因为，在大多数数据科学项目中，数据不是恒定的，而是频繁更新的。此外，任何数据科学项目都期望它具有*可扩展性*和*抗崩溃性*。它应该不受数据中任何错误的影响。

因为在数据科学项目中，代码的每一个部分都是为适应特定的数据形式而构建的，所以如果给代码一个特定的数据，它就可能会崩溃。当然，无论输入什么数据，您都不希望代码出错。因此，在设计和构建代码时，要记住一些事情，以使您的代码更具弹性。

要设计和编写好的、稳定的代码，有许多准则可以遵循。然而，在本文中，我们将重点关注我认为的构建可靠的数据科学项目所需的 5 个最重要的*规则或技能。*

所以，让我们开门见山吧…

[](/level-up-your-code-e1424fff031d) [## 提升你的代码

### 编写干净、高质量代码的 5 个简单步骤

towardsdatascience.com](/level-up-your-code-e1424fff031d) 

# 文件编制

不提到文档，就谈不上好的软件。现在，有两个步骤来保持代码的整洁和良好的文档记录。第一步是*注释*你的代码。注释对于阅读你的代码的人来说是至关重要的，更重要的是，通过你写代码时的思考过程，对于你未来的自我来说也是至关重要的。

评论需要简单，不超过两句，开门见山。无论何时定义一个类或函数，或者创建自己的模块，都不要忘记编写一个描述性的 docstring。写评论时，请始终记住:

> 注释不是用来向人们解释代码的；代码是用来向计算机解释注释的。

一旦你的代码和注释完成了——好吧，暂时因为代码永远不会完成——你需要为你的代码建立足够的*文档*。文档通常是用简单的英语编写的代码的外部解释。文档通常使用文档处理工具创建，例如 [Sphinx](http://sphinx.pocoo.org/) 和 [DocUtils](http://docutils.sourceforge.net/ reStructuredText) 。文档通常是项目网站的一部分。

说到最佳实践，在开始编码之前开始编写文档是一个好主意。它将作为需要做什么的指南。不幸的是，我们大多数人——包括我自己——都不遵守这条规则。然而，我们都需要开始实践它。

# 测试

我们写代码的时候，往往是基于一些变量和数据集来写的。然而，很常见的是，您的代码可能包含一些只会在某些特定情况下或特定数据集上出现的错误。因此，在部署应用程序之前对其进行测试至关重要。

但是，测试可能会变得非常复杂，尤其是当涉及到数据科学项目时。通常，数据科学项目使用其他数据科学家的评论进行测试，因为大多数众所周知的测试方法很难应用于数据科学项目。

这是因为数据的简单变化可能会导致代码性能的显著变化。多年来，研究人员和开发人员一直在寻找测试数据科学项目的最佳方式。他们发现测试数据科学应用程序的最佳方式是通过单元测试。

**单元测试**是一种测试类型，用于检测可能中断程序流程的变化。他们帮助维护和更改代码。有许多 Python 测试库可以用来执行单元测试。

1.  [**Unittest**](https://docs.python.org/3/library/unittest.html) 是 Python 中的内置库，用于执行单元测试。Unittest 通常被称为 PyUnit，这是一种创建单元测试程序的简单方法。
2.  Pytest 是一个完整的测试工具——这是我最喜欢的。Pytest 有一个简单直接的方法来构建和使用单元测试。
3.  [**假设**](http://hypothesis.readthedocs.io/en/latest/index.html) 是一个单元测试生成工具。开发假设的目标是帮助开发人员创建和使用单元测试来处理代码的边缘情况。

# 数据管理

具体到数据科学项目，在处理数据时，我们需要注意的一件事是管理我们的数据。我们需要考虑很多事情，比如你的数据是怎么创建的？它有多大？是每次都加载还是存储在内存里？

当处理数据时，我们需要非常小心内存管理以及代码如何与数据交互。需要考虑的一点是 Python 函数调用如何影响代码的内存使用。有时候，函数调用占用的内存比你意识到的要多。

克服这个问题的一个方法是使用 Python 的自动内存管理功能。下面是 Python 处理函数调用的方式:

1.  每次你调用一个函数和对象时，就用一个计数器计算创建的位数；使用此功能。
2.  每当我们使用或引用这个函数时，计数器就增加 1。
3.  当代码引用离开函数对象时，计数器递减 1，直到达到 0。一旦完成，内存将被释放。

[](/what-to-do-when-your-data-is-too-big-for-your-memory-65c84c600585) [## 当你的数据对于你的内存来说太大了怎么办？

### 使用 Panda 处理大数据

towardsdatascience.com](/what-to-do-when-your-data-is-too-big-for-your-memory-65c84c600585) 

如果您想知道如何编写使用这种自动内存管理的代码，请不要再想了。 [Itamar Turner](https://pythonspeed.com/about/) 提出了 [3 种不同的](https://pythonspeed.com/articles/function-calls-prevent-garbage-collection/)方法，可以让你的功能更有内存效率:

1.  尽量减少局部变量的使用。
2.  如果不能，那么重用变量，而不是定义新的变量。
3.  转移占用大量内存的函数的对象所有权。

# 使用特定领域的工具

最后但同样重要的是，为了帮助您构建弹性项目，请使用专门为数据科学构建的工具。当然还有大家熟知的工具，比如 IPython，Pandas，Numpy，Matplotlib。

但是，让我来介绍两个不太为人所知的工具:

1.  [**graph lab Create**](https://pypi.org/project/GraphLab-Create/)**:**是一个用于快速构建大规模、高性能数据产品的 Python 库。您可以使用 GraphLab Create 来应用最先进的机器学习算法，如深度学习、提升树和因式分解。您可以通过可视化执行数据探索，并且可以使用预测服务快速部署项目。
2.  [**Fil:**](https://github.com/pythonspeed/filprofiler) 是用于数据科学的 Python 内存管理工具。您可以使用 Fil 来测量 Jupyter 笔记本中的内存使用峰值。以及测量普通(非基于 Jupyter 的)Python 脚本的内存使用峰值，并调试代码中的内存不足崩溃。此外，Fil 有助于显著减少内存使用。

# 外卖食品

如今，建立一个好的数据科学项目并不足以让你脱颖而出。你需要你的项目具有抗崩溃性和内存效率。这就是为什么使用一些软件开发技巧；你可以让你的数据科学项目更上一层楼，让它脱颖而出。

我们在本文中讨论的软件开发技能是:

1.  高效的记录和评论。
2.  测试，测试，然后更多的测试。
3.  明智的数据和内存管理。
4.  可以简化您的工作并提高项目效率的特殊工具。

然而，我们没有谈到的是任何开发人员都必须获得的最重要的技能，即始终致力于改进您的技能和知识库，以及跟上最新技术和工具的能力。