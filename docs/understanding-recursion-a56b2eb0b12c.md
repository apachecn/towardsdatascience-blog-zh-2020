# 理解递归

> 原文：<https://towardsdatascience.com/understanding-recursion-a56b2eb0b12c?source=collection_archive---------12----------------------->

![](img/40201648516282963c3ac1cfeef2bdab.png)

安德里亚·费拉里奥在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

## 了解如何利用这一基本但令人困惑的编程概念

每次我有一段时间不用它的时候，我发现自己都要重新学习这个概念。我大体上记得它是什么，以及我们为什么需要它，但是在长期搁置之后，递归编程总是一场斗争。

现在它又一次让我记忆犹新，让我来记录一下我们为什么以及如何使用递归。如果你想下载这篇文章中用到的代码，你可以在我的 GitHub 上找到它。

学过递归的人可能都记得计算斐波那契数的经典例子:

```
# Function that returns the nth number in the Fibonacci sequence
# For example, if n=3 the 3rd number in the sequence is returneddef fib(n):
    if n==0:
        return 1
    elif n==1:
        return 1
    else:
        return fib(n-1) + fib(n-2)
```

在我们进入一个更实际的例子之前，让我们用它来理解递归是如何工作的。

**递归是函数调用自身。我把递归比作 do-while 循环，遗憾的是这在 Python 中并不存在。与 for 循环不同，do-while 循环会在满足终止条件之前一直运行，而 for 循环会预先指定要运行的次数。do-while 循环的美妙之处在于**它会一直运行到任务完成**——您不需要提前知道需要运行多少次。**

**递归很棒，因为它是 do-while 循环的有价值的替代品。它还会一直运行，直到任务完成。但是递归不是一个循环，而是像电影《盗梦空间》。在《盗梦空间》中，莱昂纳多·迪卡普里奥和他那群快乐的盗梦贼冒险进入了一个人的梦的更复杂的层面——每一层都是梦中的梦。只要他们能找到回去的路，他们能走多深是没有限制的。**

每次我们的递归函数调用自己时，它实际上是更深入一层(当前梦中的另一个梦)。但就像《盗梦空间》中的角色一样，深入是达到目的的一种手段。让我们看看我们的斐波纳契代码，特别是最后一行:

```
return **fib(n-1) + fib(n-2)**
```

这里，该函数调用自身两次，并将结果相加，但是，尽管最初的函数是用 **n** 作为输入调用的，但这两次调用是用修改后的输入进行的: **n-1** 和 **n-2** 。所以基本上梦里的每一个梦都从最初的输入 **n** (通过从中减去)逐渐减少，直到它到达终点。让我们展开 **fib(5)** 来看看这是如何工作的:

```
 fib(5)= fib(4) + fib(3)= fib(3) + fib(2) + fib(2) + fib(1)= fib(2) + fib(1) + fib(1) + fib(0) + fib(1) + fib(0) + 1= fib(1) + fib(0) + 1 + 1 + 1 + 1 + 1 + 1= 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1= **8**
```

请注意，该函数一直持续到到达 **fib(1)** 或 **fib(0)** 为止，这些都是终止情况。比如 **fib(3)** 变成 **fib(2) + fib(1)** ，就变成 **fib(1) + fib(0) + fib(1)** 。这种自我传播，直到达到一个终止的情况，这就是函数如何越来越深(进入梦中的梦)，直到它到达一个出口点。

我们可以通过对照我们的函数来验证 8 是否是正确答案:

```
In:  fib(5)Out: 8In:# For fun, print first 10 values of the Fibonacci Sequence
for i in range(10):
    print(fib(i))Out:1
1
2
3
5
8
13
21
34
55
```

## 结束

让我们花点时间来谈谈终止案例。**这些都很关键，因为如果没有这些情况，函数就会无限期地调用自己，陷入死循环。**所以编写任何递归函数的第一步是指定它可以退出(终止)的条件。

在斐波那契数列的例子中，我们知道序列中的前两个值是 1 和 1。即 **fib(0) = 1** 和 **fib(1) = 1** 。所以任何时候我们得到一个 0 或 1 的输入，我们就可以返回一个 1，然后就结束了。如果我们的输入大于 1，那么我们需要像上面那样，通过一系列递归函数调用，朝着终止情况(0 或 1)前进。

# 更实际的用例

打印斐波那契数列是一个巧妙的聚会把戏，但是现在让我们来看一个更实际的用例——遍历树。树木的问题在于我们不知道它们有多深。你可以有一个这样的:

```
root
|  \
|   \
b1   b2
```

或者像这样稍微深一点的:

```
root ____________
|           \     \
|            \     \
b1 ____       b2    b3
|  \   \      |  \
l1  l2  l3    l1  l2
```

让我们编写一个足够通用的函数，它可以处理这两种树(甚至更复杂的树)。首先，让我们使用 Python 字典构建上面描述的两棵树:

```
my_dict0 = {'root': {'b1': [1],
                     'b2': [2]}
           }my_dict1 = {'root': {'b1': {'leaf1': [1,2,3],
                            'leaf2': [4],
                            'leaf3': [5,6]
                           },
                     'b2': {'leaf1': [7,8],
                            'leaf2': [9,10,11]
                           },
                     'b3': 12
                    }
           }
```

现在让我们考虑如何通过递归来遍历这些树。首先让我们定义终止的情况。由于我们构造字典的方式，**终止的情况非常简单:如果我们看到一个列表(或单个值),我们可以只追加内容并继续前进**。注意，我将结果存储在一个名为 **result** 的扩展列表中( **result** 是函数运行完成后返回的结果)。另外，请注意，虽然我称之为终止案例，但我们还没有返回任何内容。相反，我们只是将结束节点的值附加到**结果**中，并继续我们的 for 循环，因为我们知道我们已经完成了树的当前子部分。

```
def parse_dict(my_dict, result):
    for key, val in my_dict.items():
        **if type(val) == list:
            for i in val:
                result.append(i)**
```

如果我们看不到名单呢？然后，我们需要通过递归(Inception)更深入地研究。我们这样做的方法是通过再次调用我们的函数，但是在修改的输入上(如果我们每次调用都不改变我们的输入，我们将陷入无限循环)。因此，我们现在只给函数当前正在检查的树的一部分( **my_dict** )，而不是给函数原始输入。例如，一个对 **parse_dict** 的递归调用可能只处理 **b1** 分支(它有 3 个叶子: **leaf1** 、 **leaf2** 和 **leaf3** )，而另一个调用可能只处理 **b3** 分支(它只有值 **12** )。

```
def parse_dict(my_dict, result):
    for key, val in my_dict.items():
        if type(val) == list:
            for i in val:
                result.append(i)
        **elif type(val) == dict:
            parse_dict(val, result)**
```

最后要添加的是一个终止案例，它检查分支何时没有叶子或列表，并且只包含一个数值(比如 **b3** )。在这种情况下，我们可以直接将 **val** 中的值追加到**结果**中:

```
def parse_dict(my_dict, result):
    for key, val in my_dict.items():
        if type(val) == list:
            for i in val:
                result.append(i)
        elif type(val) == dict:
            parse_dict(val, result)
        **else:
            result.append(val)**
    return result
```

如果我们在简单的树上运行函数， **my_dict0** ，我们得到:

```
In:  parse_dict(my_dict0, [])Out: [1, 2]
```

如果我们在 **my_dict1** 上运行它，我们会得到:

```
In:  parse_dict(my_dict1, [])Out: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
```

酷，我们已经遍历了我们的树，挖掘了存储在每个端节点中的值。不管树是简单的还是更复杂、更深入的，我们的函数都能工作。

需要记住的一点是，如果你有一棵非常复杂的树，有很多层和很多分支，那么递归遍历它可能需要很长时间。如果您正在处理非常复杂的树结构，那么投入一些时间和思想来构建一个更加优化的解决方案是有意义的。

# 额外收获:获得每个值的路径

我们可能还想知道到达每个最终值所经过的路径(或者到达特定最终值的路径)。下面的函数产生一个包含每个结束值的路径的列表(与 **parse_dict 的**输出共享相同的顺序)。它的工作方式与 **parse_dict** 类似，所以我就不赘述了(但是代码中有一些注释)。

```
def get_path(my_dict, result, path):
    for key, val in my_dict.items():
        # If it's a dict, go one level deeper and update path
        # to include the current key (node name)
        if type(val) == dict:
            get_path(val, result, path+[key])

        # If it's not a dict, then append the key and don't
        # go down another level (since no need to)
        elif type(val) == list:
            for i in val:
                result.append(path+[key])
        else:
            result.append(path+[key])
    return result
```

下面是一些输出示例。注意，我们需要提供两个输入——返回的**结果**和**路径**，后者是附加到**结果**的中间输出(但在函数结束时不返回)。

```
In:  get_path(my_dict1, [], [])Out: [['root', 'b1', 'leaf1'],
 ['root', 'b1', 'leaf1'],
 ['root', 'b1', 'leaf1'],
 ['root', 'b1', 'leaf2'],
 ['root', 'b1', 'leaf3'],
 ['root', 'b1', 'leaf3'],
 ['root', 'b2', 'leaf1'],
 ['root', 'b2', 'leaf1'],
 ['root', 'b2', 'leaf2'],
 ['root', 'b2', 'leaf2'],
 ['root', 'b2', 'leaf2'],
 ['root', 'b3']]
```

希望这对你有帮助。干杯！

***更多数据科学相关帖子由我:***

[*理解交叉验证*](/understanding-cross-validation-419dbd47e9bd)

[*QQ 剧情到底是什么？*](/what-in-the-world-are-qq-plots-20d0e41dece1)

[*了解正态分布*](/understanding-the-normal-distribution-with-python-e70bb855b027)

[*熊猫加入 vs 合并*](/pandas-join-vs-merge-c365fd4fbf49)

[*理解贝叶斯定理*](/understanding-bayes-theorem-7e31b8434d4b)