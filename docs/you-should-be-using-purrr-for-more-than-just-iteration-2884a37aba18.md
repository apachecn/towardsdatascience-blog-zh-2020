# 你不应该仅仅在迭代中使用 purrr

> 原文：<https://towardsdatascience.com/you-should-be-using-purrr-for-more-than-just-iteration-2884a37aba18?source=collection_archive---------33----------------------->

## Tidyverse 包中的 3 个函数改进了 R

![](img/19cb236ed94b8c65578ab98ee9c09ff1.png)

照片由[凯瑟琳·希斯](https://unsplash.com/@catherineheath?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/cat-computer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍摄

[purrr 包](https://purrr.tidyverse.org/)是 [Tidyverse](https://www.tidyverse.org/packages/) 的主要支柱之一，在实用性和通用性方面与 [dplyr](https://dplyr.tidyverse.org/) 和管道操作器不相上下。其主要目的之一是将循环的*意图*与其*语法*对齐。在编写 for 循环时，不涉及一堆乏味的样板文件——它很少告诉读者循环做了什么——purrr map 可以像简单的英语一样阅读，并且可以整齐地放入管道连接的操作组中。

但这并不是 purrr 所能提供的全部。最长的一段时间，我只用了`map`、`walk`，以及它们的变体。从那以后，我发现了这个包的其他实用程序，它们使处理列表变得轻而易举。

因为这些函数一点也不隐藏，就在文档页面中的显眼位置，我觉得没有早点使用它们有点愚蠢。但是对于程序员来说，太容易陷入相同的例行程序，无意识地遵循“如果它没有坏”的思维模式。因此，为了激起您对 purrr 提供的鲜为人知的工具的兴趣，我选择了几个我最喜欢的工具来分享。我希望这样做会改进您的工作流，让您更加好奇这个 R 包还能提供什么。

## 避免用“set_names”反斜杠或替换函数

现在，一个实际上是从 [rlang 包](https://rlang.r-lib.org/reference/set_names.html)重新导出的函数，它本身在 base R 中有一个对应的可用版本，这看起来似乎是一个奇怪的起点。但是`set_names`非常符合 purrr 的基本理念，我认为它是合适的。

在 R 中，从语法上来说，有四种类型的函数。分别是**前缀**(**`do_something(argument)`)**中缀** ( `+`、`-`、`%>%`)**替换**(`setter(x) <- “eggs"`)**特殊**(类似`if`的关键词)。**

**事实是，大多数阅读代码的人都非常熟悉前缀和中缀形式，尤其是来自其他语言的形式。虽然任何函数都可以通过使用反斜线以前缀形式编写，但这是 R 的另一个怪癖，在使代码更具可读性方面并没有起到很好的作用。**

**假设我们有一个字符向量，我们需要它们的字符长度。为了举例，我将使用像这样的简单操作，可能不需要使用列表和 purrr——如果这让您感到困扰，那么想象一下我们正在做一些输出异构数据类型的更复杂的任务。**

**如果我们希望输出列表的名称是原始字符，我们可以这样做:**

**注意这个函数是如何很好地适应管道的。这里我利用了这样一个事实，即`set_names`将默认给一个向量它自己的参数值作为名称。比手工创建一个命名的向量要快得多，也比在单独的一行上使用`names(animal_nchars) <- animals`漂亮得多。**

## **用“cross”避免嵌套循环**

**假设我们有两个不同长度的字符向量，我们希望将它们中的元素粘贴到一起，作为另一个字符向量返回。我们可以这样使用嵌套地图:**

**请注意，这种方法很难阅读，并且需要一些额外的工作来获得一个字符向量。虽然像 [map2 和 pmap](https://purrr.tidyverse.org/reference/map2.html) 这样的工具可以很好地处理相同长度的输入，但是在条件不太整洁的情况下它们就不起作用了。此外，内循环返回长度大于 1 的向量的事实阻止了我们在外循环中使用`map_chr`。**

**请考虑这种方法:**

**好多了，你不觉得吗？对于更复杂的函数，如果使用公式的话，我喜欢手动解包`.`或`.x`,只是为了让内容更具可读性。在决定是利用特定语言的速记来节省自己的时间，还是使用更冗长的速记来方便其他人时，总会有一点权衡。**

## **使用“保持”和“压缩”进行过滤**

**在我的工作场所，我处理大量的空间数据。当跨地理区域迭代时，过程经常因为简单的数据覆盖原因而失败。我发现 [compact](https://purrr.tidyverse.org/reference/keep.html) 函数对于在探索阶段过滤掉这些故障非常有用。**

**对于更持久的代码，最好明确要丢弃哪些元素，因此使用`keep`可能是更好的选择，因为它让您指定一个谓词。**

**r 有多个[内置数据集](https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/00Index.html)。假设我们想要列出它们的列名，但前提是它们必须以 dataframes 的形式存储。这是可以做到的:**

**由于内置数据集是 base R 的一个怪癖，以编程方式访问它们有点奇怪，因此使用了`get`。关于上面的片段，需要注意一些事情:**

*   **因为不是所有列出的数据集都被成功检索，所以我使用`possibly`和`compact`来过滤掉这些失败。**
*   **“仅当它们作为数据帧存储时”部分由管道的第 4 行中的`keep`完成。**
*   **注意`set_names`是如何再次派上用场的，这样在过滤完成后，我们就知道每组列名与哪个数据集相关联。**

**我在这里仅仅触及了表面，我的例子不可否认地有点做作，但是我希望我至少已经说服了你自己去探究除了使迭代更可读之外，purrr 还能为你做些什么。**

**当然，伴随着所有伟大的锤子而来的是责任，不要把一切都看成钉子。R 中的列表通常不是保存数据的最佳数据结构选择。如果您可以将事情存储在数据帧中，并使用 dplyr 而不是 purrr 来实现您的目的，那么您应该这样做！**

**但是对于处理列表的时候，purrr 是一个很好的工具，但是经常没有被充分利用。祝你好运！**