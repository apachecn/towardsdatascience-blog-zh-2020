# 训练你的思维，用 5 个步骤进行递归思考

> 原文：<https://towardsdatascience.com/train-your-mind-to-think-recursively-in-5-steps-8f85c0e0eb81?source=collection_archive---------2----------------------->

## 如何轻松解决递归问题？

![](img/f368a53ef8a82fc74faae950ff45f063.png)

照片由[里德·祖拉](https://unsplash.com/@reidzura?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

在您的编程之旅中，有几个里程碑是您需要克服的。例如，熟悉类，理解指针，掌握代码函数化的艺术，等等。对于新手来说，最难学的编程概念之一是*递归*，对于已经编程一段时间的人来说，这是需要掌握的。

当我第一次开始编码的时候——大约十年前——我很难理解递归。虽然有些人可以自然地递归思考，但其他人——包括我自己——却不能。

***但是，***

递归思维是你可以训练你的大脑去做和掌握的事情，即使你天生没有这种能力。

回到 2012 年，我看到一本非常酷的书，叫做《像程序员一样思考》。这本书教会我开发一个思维过程，帮助我解决多年来的各种编程问题。它给了我一个程序员在职业生涯中取得成功所需的正确思维过程的基础。

这些年来，我扩展了书中提出的那些技术，以便熟悉各种编程概念。

在本文中，我将向您介绍我用来解决任何递归问题的不同步骤。虽然我将使用 Python 来演示这些步骤，但是这些步骤可以应用于任何编程语言。他们的逻辑不是特定于语言的。

让我们—让我们，让我们，让我们—开始吧！

# 训练你递归思考的步骤

为了演示这个过程，我们来看一个简单的问题。假设我们需要对任何给定数字的位数求和。例如，123 的和是 6，for 57190 是 22，以此类推。

所以，我需要写一个代码，用递归来解决这个问题。在你说之前，我知道有其他方法可以解决这个问题——可以说是更好更容易的递归方法。但是，为了这篇文章，让我们考虑递归解决方案。

# 1-首先使用 iterable 方法。

这一步对大多数人来说相对简单。我们有一个数字，想用循环对它的数字求和。基本上，我们需要知道如何计算数字中有多少位数，然后逐一求和。

一种方法是将包含数字的变量转换为 str，这样更容易迭代。

```
num = 123 #The variable containing the number we want to sum its digits
num = str(num) #Casting the number to a str
s = 0 #Initialize a varible to accumulate the sum
#Loop over the digits and add them up
for i in range(len(num)):
  s += int(num[i])
```

# 2-提取函数的参数。

使用循环解决问题将有助于我们理解答案，并找出它的所有非递归方面。现在我们有了答案，我们可以剖析它，提取我们需要继续前进的信息。

此时，我们需要问自己一个问题，*如果我把它写成一个函数形式，函数参数会是什么？*

这个问题的答案取决于你使用的编程语言。对于 Python，我们可以说只需要**一个**参数，就是变量`num`。

```
def sumOfDigitsIter(num):
    num = str(num)
    s = 0
    for i in range(len(num)):
        s += int(num[i])
    return s
```

# 3-扣除最小的问题实例。

一旦我们得到了函数参数，我们将对它们进行更深入的研究。在我们的例子中，我们只有一个参数 num。

我们现在需要做的是根据参数找到最小的问题实例。回想一下，我们的目的是对一个给定数字的位数求和。这个问题最简单的例子是如果数字只有一个数字。

例如，如果`num = 3`，那么答案将等于变量本身，因为没有更多的数字相加。

# 4-将解决方案添加到最小问题实例中。

让我们再来看看我们刚刚写的函数:

```
def sumOfDigitsIter(num):
    num = str(num)
    s = 0
    for i in range(len(num)):
        s += int(num[i])
    return s
```

按照这个函数的逻辑，如果参数 num 只有一个数字，那么仍然会执行循环。为了避免这种情况，我们可以添加一个条件语句，该语句只在输入数字的位数为 1 时执行。

```
def SumOfDigitsIter(num):
    num = str(num)
    if len(num) == 1:
      return num
    else:
      s = 0
      for i in range(len(num)):
          s += int(num[i])
      return s
```

# 5-扩展你的功能。

这是递归发生的步骤。到目前为止，我们并不太关心递归；我们在合乎逻辑地解决这个问题。这是从递归开始，从逻辑上考虑，然后转化为递归解决方案的最佳方法。

现在，让我们考虑一下函数的`else`部分。

```
else:
      s = 0
      for i in range(len(num)):
          s += int(num[i])
      return s
```

你可以把递归想象成展开一个问题实例，然后再次滚动它。我们可以从另一个角度来看这个问题，我们可以说 123 的和是 1+23 的和，23 的和是 2 +和 3——也就是 3。

因此，回滚到 123 = 1 +2 +3 =6。

让我们把它转换成代码。我们已经写好了最后一部分，它处理一位数。我们需要做的是将 num 个变量分解成一位数。

这就是递归。

```
def SumOfDigits2(num):
 num = str(num)
 if len(num) == 1:
   return num
 else:
   return num[0] + sumOfDigits(num[1:])
```

所以，每次，我都调用相同的函数，但是输入更少。一旦到了最后一位数，我最终会得到 1 + 2 + 3 这样的数，最终加起来就是 6。

瞧，我得到了一个递归函数。

# 另一个例子

让我们考虑另一个例子，假设我们想要得到两个相同长度的整数列表的绝对差的和。例如，如果我们有[15，-4，56，10，-23]和[14，-9，56，14，-23]，答案将是 10。

**第一步:用循环求解**

```
 assert len(arr1) == len(arr2)
    diffSum = 0
    for i in range(len(arr1)):
        diffSum += abs(arr1[i]-arr2[i]) 
```

**第二步:提取参数**

参数表= [arr1，arr2]。

**第三步:扣除最小实例**

这个问题的最小实例是当两个列表为空时；在这种情况下，没有区别，所以答案是 0。

**第四步:求解最小实例。**

```
if len(arr1) == 0:
  return 0
```

现在你可能会说，为什么不确保 len(arr2) == 0 呢？assert 语句已经确保了两个列表具有相同的长度，这意味着如果我想检查它们是否为空，我只需要检查其中一个的长度。

第五步:递归

就像 digits sum 示例一样，如果我想对两个列表之间的绝对差求和，我可以得到前两个元素之间的差，然后是第二个，然后是第三个，依此类推，直到我用完所有的元素。

```
def recDiff(arr1,arr2):
    assert len(arr1) == len(arr2)
    if len(arr1) == 0:
        return 0
    else: 
        return abs(arr1[0]-arr2[0]) + recDiff(arr1[1:],arr2[1:])
```

# 外卖食品

递归被认为是程序员在成为“优秀程序员”的过程中需要经历的高级技术之一然而，一开始把一个人的脑袋包起来是相当棘手的，许多人发现很难掌握。

遵循简单明了的五个步骤，你可以轻松解决任何递归问题:

1.  首先使用循环解决问题。
2.  从中提取可能的输入，如果你想把它变成一个函数的话。
3.  演绎问题最简单的版本。
4.  写一个函数来解决这个问题的最简单的例子。
5.  使用该函数编写一个新的递归函数。

虽然我提出了 5 个步骤，但是你不需要明确地经历所有的 5 个步骤，因为你会更加精确。随着时间的推移和练习，你将能够在头脑中执行这些步骤，而不用明确地写下来。

我把这个留给你，递归是一个需要掌握的具有挑战性的编程概念。所以，只要坚持下去，有耐心，多多练习；这是你真正掌握诀窍的唯一方法。