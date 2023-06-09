# 揭秘二分搜索法

> 原文：<https://towardsdatascience.com/demystifying-binary-search-bed0274e27e7?source=collection_archive---------67----------------------->

## 搜索算法指南

## 升级你的搜索游戏！

在之前的文章中，我们一直在讲[线性搜索](/demystifying-linear-search-cf0373020af8)。如果你没看过，建议你先浏览一下。现在你已经理解了线性搜索的概念，是时候让你知道一个更强大的搜索方法，那就是二分搜索法。

![](img/d65c2b851962aa0cf2ea2e91f743e01a.png)

图片由 [Unsplash](http://unsplash.com) 上的 [Annie Theby](https://unsplash.com/@annietheby) 拍摄

在编程中，你会遇到很多需要在一个有序数组中找到一个元素的确切位置/索引的情况。大多数时候，二分搜索法将是正确的方法。这就是为什么二分搜索法是程序员工具箱中必不可少的工具。

# 什么是二分搜索法？

二分搜索法是一种有效的搜索技术。唯一的缺点是它只能在有序列表上运行。二分搜索法也称为对数搜索、二分法或半区间搜索。

通过从数组的中间开始，该算法可以通过确定所需的关键字是放在前半部分还是后半部分来有效地将搜索空间减半。

# 它是如何工作的？

这些是在二分搜索法完成的步骤:

1.  从中间元素开始，将该元素与所需的键进行比较。
2.  如果键匹配中间的元素，则返回中间的位置。
3.  如果键小于中间的元素，那么键只能位于左半部分的子数组中。我们只将焦点移到左半部分的子阵列。
4.  否则，我们只关注右半部分的子阵列。
5.  重复步骤 1、2、3 和 4，直到找到所需的键或检查完每个子阵列。
6.  如果数组中没有匹配项，则返回-1

# 二分搜索法的例子

在这里，我将为您提供一个二分搜索法算法的伪代码。阅读伪代码将帮助你更好地理解算法中到底发生了什么。

> 二分搜索法伪码

我还将提供 3 种不同编程语言的示例代码，Python、C 和 JavaScript。

> Python 中的二分搜索法代码

> C 语言中的二分搜索法码

> JavaScript 中的二分搜索法代码

# 二分搜索法的时间复杂性

二分搜索法的最佳情况发生在所需密钥位于数组中间的时候，在这种情况下，时间复杂度为 O(1)。而对于最坏的情况，我们将需要进行 log2(n)比较，因为在每次迭代中，数组的长度变成一半。

例如，我们有一个长度为 8 的数组。在最坏的情况下，我们需要经历 3 次迭代。

1.  在第一次迭代之后，我们关心的子阵列的长度是 8/2 = 4
2.  在第二次迭代时，剩余子阵列的长度是 4/2 = 2
3.  这是最后一次迭代，因为在这一步之后，子数组是一个单元素数组。

我们知道 log2(8)等于 3，这就是为什么二分搜索法的时间复杂度是 O(log n)。对于一般情况，所做的比较次数与最差情况大致相同。因此，平均情况下的时间复杂度也是 O(log n)。

# 最后的话

尽管二分搜索法很实用，但我们应该始终记住它有一些局限性:

1.  必须对列表进行排序。
2.  我们必须能直接接触到中间元素。

学习二分搜索法对每个想发展编程技能的人来说都是必不可少的。二分搜索法是一个伟大的工具，它将帮助你克服你在成为一名专业程序员的道路上所面临的许多问题。

> "一步一个脚印是让你达到目标的唯一办法."
> 
> —艾米莉·狄金森

永远不要说以后再往前走一步！

问候，

**弧度克里斯诺**