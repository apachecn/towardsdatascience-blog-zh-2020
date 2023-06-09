# 理解推荐系统的矩阵分解

> 原文：<https://towardsdatascience.com/understanding-matrix-factorization-for-recommender-systems-4d3c5e67f2c9?source=collection_archive---------9----------------------->

## 了解如何实现 Google 在实现协作过滤模型时使用的矩阵分解算法

![](img/393f10c6c7fda76db7fd03f995c82c10.png)

# 介绍

矩阵成了面试问题中必不可少的话题，不管你是开发人员还是数据工程师。作为一名数据工程师，操作和转换矩阵索引是一项非凡的能力。这个想法是在它下面学习数学。当你理解了算法，你需要做的就是玩指数来得到答案。

在这篇文章中，我将一步一步地分享实现矩阵分解函数的算法。代码片段应该在 R 中；但是，您可以用您喜欢的任何语言生成代码。

# 矩阵分解的现实应用是什么？

矩阵分解在许多应用中是一种重要的方法。有超级计算机可以进行矩阵分解。例如，跟踪航班的雷达利用一种叫做卡尔曼滤波的策略。卡尔曼滤波的核心是矩阵分解活动。当卡尔曼滤波器利用雷达跟踪你的飞行时，它们照亮了条件的直接框架。另一个很好的例子是 Google，它应用矩阵分解来开发一个协作过滤模型。

# 理解数学

矩阵分解算法的工作原理是将原始矩阵分解成两个矩阵，一个是上面的三角形(U ),另一个是下面的三角形(L)。在本教程中，我将坚持将方阵 A 因式分解为 LU，如下所示。

> 请注意:为了简单起见，我们不用担心 A 的置换行，可以假设 A 小于 5x5。最后，矩阵入口点(中枢)不等于零。本教程的目标是理解数学，并将其转化为代码。更复杂的版本将很快在另一篇文章中发布。

![](img/393f10c6c7fda76db7fd03f995c82c10.png)

矩阵 A 是一个 I 乘 j 的正方形矩阵，分解成 L 和 U 矩阵。目标是在矩阵的右上角获得零— (L)，在矩阵的左下角获得零— (U)。

# U 矩阵

![](img/3ea662a6bb24f84d8f803f9eccdabf44.png)

在这种情况下，我们需要找到一种方法来将提到的值降为零。重要的是要明白，我们必须在不交换行的情况下分解矩阵，我们需要保持行的顺序。在这种情况下，我们将使用线性代数中的行缩减方法。

为了更好的理解，我们来举个例子，假设我们有一个维数为 3×3 的方阵，如下图。

![](img/621f0c2059b9143d32d4a8db5ebef83e.png)

为了得到这个矩阵左下角的零，我们要做如下的事情:

![](img/9782e51f4d575775cb7c1e477218c798.png)

我在这里做的是将 4 除以 2——这被称为乘数，然后用它乘以第一行。之后从第二排减去第一排。最后，将结果放在第二行。

![](img/7197858d5eafc262bfdb60b3af6bf710.png)

对第三行重复这些步骤。注意，第一行应该保持不变。

![](img/d1089d6bc687f2bcac3f1842993407ac.png)

现在，我们需要将 6 化为 0。我们可以通过实现以下内容来实现这一点:

![](img/dc3d7b4ad504d74da9d66d895777fd29.png)

请注意，我用 R2 而不是 R1，因为我不想失去我在第三行得到的零分。因此，我将该等式交替应用于第二行。

![](img/2983a3afbace4476a14832b505c18038.png)

U 的最终形式

# L 矩阵

![](img/500873c3a137c22b651da0d7fda92927.png)

L 矩阵是直接和简单的。这是一个梯队对角矩阵——对角线上是 1，右上角是 0。剩余值将是我们通过行缩减得到的乘数，其中 U 矩阵位于相同的索引中。

因此，L 矩阵的最终值将如下所示:

![](img/6df005807a2498f54b5872d6ebde51ef.png)

# 计算机算法

理解了数学之后，是时候构建一个通用的计算机程序来分解任何维数相对较大的矩阵了。

![](img/7a01b921c6fd8898cbcc3844736e123c.png)

基本的算法思想

基本思想是遍历矩阵的列，然后遍历每一行来得到乘数。我们从 2 开始 j，因为我们需要保持第一行不变。我们设置了一个条件，只在行比列高的时候执行，因为我们想对角移动。我们一直想保留归约得到的零。

下面是用 R 语言实现的算法。您可以使用您喜欢的任何语言来实现相同的功能。

由于执行了两个嵌套的 for 循环— [引用](http://pages.cs.wisc.edu/~vernon/cs367/notes/3.COMPLEXITY.html)，该算法的时间复杂度为 O(n2)。

# 结束语

试着继续解决矩阵挑战，学习数学技巧来战胜这类面试问题。一旦你发现问题，你就能抓住算法模式，这是很有帮助的。这样做会帮助你赢得面试，给面试官留下好印象。

最后，我希望这篇文章能让面试过程中的其他人受益。如果你能用不同的语言或使用不同的算法自己解决这个问题，我将不胜感激。感谢您的阅读，祝您求职顺利。