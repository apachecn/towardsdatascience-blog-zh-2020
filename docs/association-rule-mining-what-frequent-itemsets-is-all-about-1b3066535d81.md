# 关联规则挖掘:频繁项集是什么

> 原文：<https://towardsdatascience.com/association-rule-mining-what-frequent-itemsets-is-all-about-1b3066535d81?source=collection_archive---------50----------------------->

![](img/506d012873aa3b307cd122ad76809f0d.png)

凯利·西克玛在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 查找项目唯一组合的出现频率

要理解频繁项集，首先需要理解*频繁项集*和*频繁项集*。让我们先看看项目集是什么意思。简单地说，项目集是在一个事务或记录中一起出现的一组项目。组的大小可以小到 1，大到该事务或记录中所有项目的数量。甚至可以考虑大小为 0，但这不会产生任何有意义的结果。

# 项目集或幂集

让我们用一些关于项目集的代码更深入地研究一下。让我们从记录的一个例子开始。

这个记录只有三个项目:苹果、香蕉和牛奶。记录列表中总共有 2 个不同大小的集合，其中也包含一个空集。所以这个记录有 2 -1，7 个相关的集合。3 个项目可以创建总共 2 -1，7 个独特的集合。如果总共有 n 个可能的项目，它将产生 2^n-1 唯一集。

上面的代码显示了记录中的所有项目集。基本上显示了所有可能的 8 个唯一组，包括一个空集(通常不相关)。

# 如何计算项目集？

随着 n 变大，这些唯一项集会增长到一个非常大的数字。虽然有些可能永远不会一起出现。因为不是所有的项目组合都会出现在记录中。例如，如果记录相当于商店中的一笔交易，则不是每个项目都会以某种组合与所有其他项目一起出现。

> 记录中的项目集:
> 
> {('苹果'，'牛奶'，('香蕉'，'牛奶'，('苹果'，'香蕉'，'牛奶'，('鸡蛋'，'香蕉'，)，('牛奶'，)，('苹果'，'鸡蛋'，)，('鸡蛋'，)，('苹果'，'鸡蛋'，)，('面包'，)，('苹果'，'面包'，)，('苹果'，'面包'，)，('苹果'，)，('苹果'，'香蕉'，('鸡蛋'，'牛奶'))
> 
> 来自项目
> [()，('苹果'，)，('香蕉'，)，('牛奶'，)，('鸡蛋'，)，('面包'，)，('苹果'，'牛奶'，('苹果'，'鸡蛋')，('苹果'，'面包'，('香蕉'，'牛奶')，('香蕉'，'鸡蛋'，('香蕉'，'面包'，('牛奶'，'鸡蛋'，'面包')，('苹果'，'香蕉'，'牛奶'，'牛奶'，'牛奶')的项目集

上面的代码显示了一些记录和所有独特的项目。通过唯一项和少数记录计算的项集不匹配。使用记录的项集少于通过唯一项计算的项集。因此，不是从所有可能的唯一项中创建唯一项集，而是使用记录数据库来高效地计算可能的项集。

# 频率

频率是多少？它只是某一事件的发生次数与某一观察周期内所有事件的发生次数之比。那么它在项目集的情况下是如何工作的呢？让我们来分解一下。

> 某一事件的**发生次数与某一**观察周期**内所有事件**的**发生次数之比**

> 项目集出现的频率:
> ('苹果'，)，0.67
> ('香蕉'，)，0.33
> ('牛奶'，)，0.67
> ('苹果'，'香蕉')，0.33
> ('苹果'，'牛奶')，0.33
> ('香蕉'，'牛奶')，0.33
> ('苹果'，'香蕉'，'牛奶')，0.33
> ('鸡蛋'，)，0.67

例如，苹果出现在三分之二的记录中，所以它的频率是 2/3=0.67(四舍五入到两位小数)

支持度是关联规则挖掘中频率的另一个术语。在这种情况下，会使用某个阈值，并且只有高于该阈值的项目集才会被考虑用于规则挖掘。

# 结论

希望这篇文章能澄清什么是频繁项集。我想指出两点:

1.  为了提高效率，如何从记录数据库中计算唯一项集而不是唯一项是很重要的。
2.  一旦我们有了唯一的项目集，频率的计算方法是找出这个组合出现的所有记录，除以记录总数。

我想接下来写一下[信心](https://en.wikipedia.org/wiki/Association_rule_learning#Confidence)、[提升](https://en.wikipedia.org/wiki/Association_rule_learning#Lift)、[信念](https://en.wikipedia.org/wiki/Association_rule_learning#Conviction)，然后在规则挖掘上来个满圈。