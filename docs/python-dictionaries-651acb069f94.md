# Python 词典

> 原文：<https://towardsdatascience.com/python-dictionaries-651acb069f94?source=collection_archive---------9----------------------->

## 像专家一样使用 Python 字典

![](img/194941276cc01a044fcecd1c4e9d2c15.png)

[自由股票](https://unsplash.com/@freestocks?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

**Python** 编程语言在数据科学项目中被开发者广泛使用。要完成这样的项目，理解数据结构起着重要的作用。Python 有几个内置的数据结构，如**列表**、**集合、元组**和**字典**，以支持开发者使用现成的数据结构。

在这篇文章中，我将尝试解释为什么以及何时使用 **Python 字典**，同时给你一些关于正确使用字典方法的提示。

让我们通过一步一步的解释和例子来详细理解 Python 字典。

## 什么是 Python 字典？

简而言之，一个**字典**可以被定义为存储在**键/值**对中的数据集合。**键**必须是不可变的数据类型(如字符串、整数或元组)，而字典中的**值**可以是任何 Python 数据类型。

不允许出现重复的**键**。如果同一个**键**在同一个字典中使用了两次，那么最后一次出现的将覆盖第一次出现的。

存储在字典中的数据可以被修改，所以它们被称为可变对象。它们是无序的，这意味着我们没有保持指定项目的顺序。(从 3.7 版本开始订购)

因为它们是动态的，它们可以在需要的时候收缩。

## 什么时候使用 Python 字典？

既然您现在已经知道了什么是 Python 字典，那么是时候探索何时在您的代码中使用它们了。

这里有一个帮助你理解何时使用 Python 字典的列表。

*   当数据具有可以与值相关联的唯一引用时。
*   当快速访问数据项很重要时。字典被设计成让我们立即找到一个值，而不需要搜索整个集合。
*   当数据顺序不重要时。
*   因为字典是可变的，所以使用字典来存储不应该被修改的数据并不是一个好主意。
*   当内存考虑不是应用程序的重要因素时。与列表和元组相比，字典占用更多的内存空间。

## 如何创建 Python 字典？

有许多创建和初始化字典的方法。如下面的代码片段所示，创建字典最简单的方法是直接使用**花括号**或 **dict()** 方法；

如果你有两个可迭代的对象(例如列表对象)，你可以使用 **zip()** 函数来创建一个字典。参见下面的例子；

fromkeys() 方法是另一种创建字典的方法。它接受一个 iterable 对象并创建一个具有指定值的字典，如下面的代码片段所示；

## 什么是 Python 词典释义？

Python **字典理解**提供了一种创建字典的优雅方式。它们使你的代码更容易阅读，更有 Pythonic 风格。它们缩短了字典初始化所需的代码，并可用于用**代替**循环。

字典理解的一般语法是:

```
dictionary = {key:value for (key, value) in iterable}
```

## 将条件句添加到词典理解中

你可以用**条件语句**扩展字典理解的使用。你可以在下面看到多个**‘if’**条件句、**‘else-if’**条件句在字典理解中的用法；

## **字典操作的时间复杂度**

**获取**、**设置**和**删除**字典中的一个条目具有 **O(1)** 的时间复杂度，这意味着无论你的字典有多大，访问一个条目所花费的时间都是恒定的。

**在一个字典上迭代**具有 **O(n)** 的时间复杂度意味着执行这个任务所花费的时间与字典中包含的条目数量成线性比例。

## 如何访问字典中的值

如果你试图用一个字典中不存在的**键**访问一个元素，你会得到一个 **KeyError** 。了解访问字典中元素的正确方法对于在运行时不出现 **KeyErrors** 非常重要。

为了避免 **KeyError，**用 **get()** 方法访问字典的元素。或者，您可以使用'关键字中的' T45 '来检查该键是否存在。

## 如何将一个条目插入词典？

没有`add()`、`insert()`或`append()`方法可以用来将条目添加到字典中。相反，您必须创建一个新的键来存储字典中的值。如果字典中已经存在该键，则该值将被覆盖。

下面的代码片段展示了许多向字典中添加条目的例子；

## 字典方法有哪些？

Python 字典中包含许多**方法**，帮助您在字典对象上执行不同的任务。我在下面列出了它们的简短定义；

*   **popitem()** :从字典中删除最后一项
*   **pop( *key，defaultvalue* )** :从字典中移除并返回给定键的元素
*   keys(): 返回键
*   **values():** 返回数值
*   **items():** 返回字典的键值对
*   **get( *key[，value]* ):** 如果指定键在字典中，则返回该键的值
*   **fromkeys( *keys，value* ):** 返回具有指定键和指定值的字典
*   **setdefault( *key，value* )** :返回具有指定键的项目的值。如果键不存在，则插入具有指定值的键
*   **update(*iterable*)**:如果关键字不在字典中，则将指定的项目插入字典，否则更新值
*   **copy():** 返回字典的浅层副本
*   **clear():** 从字典中删除所有项目

## 如何从字典中删除一个条目？

要从 dictionary 对象中删除一个条目，可以使用 **'del'** 关键字或 **pop()** 方法。此外，您可以使用**字典理解**删除字典中的条目。请查看下面的代码片段，了解这些方法的实现示例；

## 如何抄字典？

您可以使用 **copy()** 方法获得一个现有字典的**浅层副本**。**浅拷贝**意味着一个新的字典将用对现有字典中对象的引用来填充。

要创建深层副本，应使用 **'copy.deepcopy(dict)'** 方法。它用原始字典的所有元素创建一个完全独立的副本。

参见下文，了解如何在字典对象上实现**浅拷贝**和**深拷贝**方法；

## 如何合并字典？

您可以使用包含 **dict.copy()** 和 **dict.update()** 方法的自定义函数来合并字典。

在 Python 3.5 及更高版本中，您可以使用' ****'** 操作符通过解包来合并字典。

合并字典最简单、最容易的方法是使用 Python 3.9+中可用的合并操作符 **'|'**

下面的代码片段通过示例展示了上述所有方法的实现；

## 如何对字典中的条目进行排序？

Python 字典在 3.7 版之前是无序的，所以即使对(键，值)对进行排序，也不能通过保留顺序将它们存储在字典中。为了保持排序，我们可以将排序后的字典存储在一个`[OrderedDict](http://docs.python.org/library/collections.html#collections.OrderedDict)`中

参见下文，了解如何通过**键**和**值对字典进行排序；**

## 如何在字典中循环？

Python 字典方法； **values()、keys()、**和 **items()** 提供了对字典中包含的元素的访问。您可以在 **for 循环**中使用它们来遍历字典。

另外，**字典理解**也可以用于迭代，如下所示；

# 结论和关键要点

因为数据结构是我们程序的基础部分，所以对 Python 字典有一个坚实的理解对于创建高效的程序是非常重要的。

我解释了为什么以及什么时候使用字典，下面列出了一些要点；

*   当数据具有可以与**值**关联的**唯一引用**时，可以使用 Python 字典。
*   由于**字典**是**可变的**，使用字典来存储那些一开始就不应该被修改的数据并不是一个好主意。
*   Python 字典在 3.7 版本之前是无序的，所以即使你对(键，值)对进行了排序，你也不能通过保留顺序来将它们存储在字典中。
*   Python **字典理解**提供了一种创建字典的优雅方式。它们使你的代码更容易阅读，更有 Pythonic 风格。

感谢您的阅读！