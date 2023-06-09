# 自然语言处理中的词干，是什么？

> 原文：<https://towardsdatascience.com/stemming-of-words-in-natural-language-processing-what-is-it-41a33e8996e2?source=collection_archive---------13----------------------->

![](img/f79551c0b66eeced553d007d996217f1.png)

词干提取是几乎所有自然语言处理(NLP)项目中最常见的数据预处理操作之一。如果你是这个领域的新手，即使你遇到过这个词，你也可能不知道这是什么。您可能还会混淆词干化和词汇化，这是两种类似的操作。在这篇文章中，我们将通过一些例子来看看词干到底是什么。我希望我能用简单的语言为你解释这个过程。

# 堵塞物

简单来说，词干化就是去掉一个词的一部分，或者说*把一个词简化为它的词干*或者词根的过程。这可能不一定意味着我们将一个单词减少到它的字典根。我们使用一些算法来决定如何砍掉一个单词。在很大程度上，这就是词干化与词干化的不同之处，词干化是将一个单词简化为它的词典词根，后者更复杂，需要非常高的语言知识水平。我们可能会在另一篇文章中讨论词汇化。在这篇文章中，我们将坚持使用词干并看几个例子。

假设我们有一组单词—发送、已发送和正在发送。这三个单词都是同一个词根*发*的不同时态。所以在我们词干之后，我们将只有一个词——*发送*。类似地，如果我们有单词——ask、ask 和 asked——我们可以应用词干算法来获得词根— *ask* 。词干就是这么简单。但是(总有但是)，很遗憾，没那么简单。我们有时会有并发症。而这些并发症被称为*过梗*和*欠梗*。让我们在接下来的章节中了解更多。

# 过度堵塞

过度词干化是一个过程，其中一个单词的大部分被砍掉，超过了所需的部分，这反过来导致两个或更多的单词被错误地缩减为同一个词根或词干，而它们本应被缩减为两个或更多的词干。比如*大学*和*宇宙*。一些词干算法可能会将两个单词都简化为词干 *univers* ，这意味着两个单词的意思相同，这显然是错误的。因此，当我们选择词干提取算法以及尝试优化模型时，我们必须小心谨慎。你可以想象，词干下是相反的。

# 底部堵塞

在词干提取中，两个或多个单词可能被错误地简化为多个词根，而实际上它们应该被简化为同一个词根。例如，考虑单词“数据”和“基准”有些算法可能会把这些词分别简化为 *dat* 和 *datu* ，这显然是错误的。这两者都必须简化为同一个词干 *dat* 。但是试图优化这样的模型可能会反过来导致词干过多。所以我们在处理堵塞时必须非常小心。

我希望这有助于理解什么是词干以及词干的两种不同的错误。如果对此还有任何困惑，请在下面的评论中告诉我，我会尽力消除你的任何疑问。

*原载于 2020 年 2 月 19 日我的* [*个人博客*](https://blog.contactsunny.com/data-science/stemming-of-words-in-natural-language-processing-what-is-it) *。*