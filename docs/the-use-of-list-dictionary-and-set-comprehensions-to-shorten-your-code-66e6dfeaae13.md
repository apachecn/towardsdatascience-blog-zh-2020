# 列表、字典和集合理解介绍

> 原文：<https://towardsdatascience.com/the-use-of-list-dictionary-and-set-comprehensions-to-shorten-your-code-66e6dfeaae13?source=collection_archive---------39----------------------->

## 将多行代码转换成单行代码

![](img/af6701c8a255b6e406d13923ae0542c6.png)

照片由 [Fotis Fotopoulos](https://unsplash.com/@ffstop?utm_source=medium&utm_medium=referral) 在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

在使用 Python 将近一年的时间里，我经常遇到“理解”这个词，但不一定理解它的确切含义或它涵盖的内容。直到最近，我才发现我已经在我的代码中使用它们来生成列表，并且我还没有完全理解它们能够将我的代码从多行缩短为一行的能力。此外，这种代码缩短方法不仅可以用于列表，也可以用于字典和集合。因此，本文试图解释它们对列表、字典和集合的适用性，以及它们如何减少日常编程中所需的代码量。

首先，理解是可以在一行中用来创建列表、字典和集合的代码片段。这取代了使用多行 for-loop，也减少了使用 map()、filter()和 reduce()函数的需要。它们由包含一个表达式的括号(根据您要创建的数据类型是方括号还是花括号)组成，后跟一个 for 子句，可能还有一个或多个 if 子句。表达式本身可以是任何东西，这意味着您可以将许多不同的对象放入列表中，只要它们是可迭代的。因此，从减少使用的行数和增加可读性的角度来看，探索这些对代码的影响是值得的。

## 列表

在 python 中可以简单地创建列表，方法是将项目放在方括号([])中，用逗号分隔，如下所示。

```
list1 = [1, 2, 3, "hello", 7.0, 52]
```

这些在编程中通常用于多种目的，但是用长格式写出或者用 for 循环编辑可能很麻烦。首先，就创建列表而言，小列表可能很容易以长格式输入，例如:

```
nums = [1, 2, 3, 4, 5, 6, 7, 8]
```

但是当它变得更长时，例如在 0-50 或更长的范围内，它们会变得难以使用。使用 range 函数通过 for 循环可以很容易地创建它们，如下所示:

```
nums = []for i in range(1, 51):
    nums.append(i)print(nums)# out: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50]
```

但是我们可以使用列表理解将它缩短为一行，并且不再需要 append()方法。

```
nums = [i for i in range(1,51)]print(nums)# out: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50]
```

本质上，for 循环放在一行中，列表同时被初始化，这样就不需要上面例子中的第一行和第二行代码了。

当我们开始为添加到列表中的数字添加条件时，这变得更加重要，比如只允许偶数并且希望这些数字是平方的。同样，这可以使用 for 循环产生，如下所示:

```
square_nums = []for x in range(1,26):
    if x % 2 == 0:
        square_nums.append(x**2)print(square_nums)# out: [4, 16, 36, 64, 100, 144, 196, 256, 324, 400, 484, 576]
```

但是同样可以使用 list comprehensions 将其缩短为一行，从而减少了循环遍历范围、创建条件并将结果追加到原始列表中所需的行。

```
square_nums = [x**2 for x in range(1,26) if x % 2 == 0]print(square_nums)#out: [4, 16, 36, 64, 100, 144, 196, 256, 324, 400, 484, 576]
```

这里，数字的转换在行首执行为`x**2`，for 循环在行中间执行为`for x in range(1,26)`，条件循环在末尾执行为`if x % 2 == 0`。这实质上使代码更具可读性，因为所有的操作都在一行中执行，并且减少了生成相同输出所需的代码量。

这还可以减少在创建新列表时对 append()、map()、filter()或 reduce()方法的需求，再次降低代码的复杂性并使其更具可读性。

类似的例子很容易找到，通过媒体上的其他文章可以很容易地获得更多的信息，例如这里的和这里的。然而，值得注意的是，这些理解也可以用在词典和集合上。

## 字典

字典是一个无序的数据集合，它是可变的、有索引的，用大括号通过键和值对编写。这里，键用于能够访问值，并且经常用于存储信息，对于这些信息，具有这样的对是有用的。下面提供了一个这样的例子，比如用于存储成绩。

```
Grades = {
    "Steven": 57,
    "Jessica": 82,
    "William": 42,
    "Hussein": 78,
    "Mary": 65,
    }print(Grades)# out: {'Steven': 57, 'Jessica': 82, 'William': 42, 'Hussein': 78, 'Mary': 65}
```

与列表类似，从基础开始硬编码有时会很耗时，因此可以使用 for 循环和条件来构造，但使用 comprehensions 可以更简单地构造。例如，对于我们上面创建的列表，我们不仅想知道数字的平方，而且还想存储原始数字，这样我们就可以使用它轻松地查找其平方值。然后，我们可以简单地创建一个包含键-值对的字典，其中键表示原始数字，值表示该数字的平方。使用 for 循环:

```
#initialising empty dict
even_squared_dict = {}for x in range(1,10):
    if x % 2 == 0:
        even_squared_dict[x] = x**2print(even_squared_dict)# out: {2: 4, 4: 16, 6: 36, 8: 64}
```

但是用字典理解:

```
even_sqaured_dict = {x: x**2 for x in range(1,10) if x % 2 ==0}print(even_squared_dict)# out: {2: 4, 4: 16, 6: 36, 8: 64}
```

本质上，这与列表理解之间的唯一区别是使用了花括号来包含理解，并在冒号前放置了 x 来表示这代表键。

这也可以用来基于一个已经存在的列表创建一个字典。例如下面，使用字典理解来创建字典，该字典具有三位国家代码的关键字和两位国家代码的值，其中两位代码与三位代码的前两位相同。

```
ThreeCharCodes = ["CAN", "FIN", "FRA", "GAB", "HKG", "IMN",
                  "MCO", "NPL"]cntryDict = {c: c[:2] for c in threeCharCodes}print(cntryDict)# out: {'CAN': 'CA', 'FIN': 'FI', 'FRA': 'FR', 'GAB': 'GA', 'HKG': 'HK', 'IMN': 'IM', 'MCO': 'MC', 'NPL': 'NP'}
```

## 设置

最后，理解也可以用于创建集合，集合是一种不同于列表或元组的数据类型，不能存储同一元素的多次出现。这样做时，它存储无序值，通过将一个列表传递到 set()或使用花括号包含由逗号分隔的值来初始化(尽管空花括号将初始化字典)。这方面的一个例子如下:

```
Fruits1 = set(["apple", "banana", "cherry", "apple"])
print(Fruits1)Fruits2 = {"orange", "pear", "grape", "pear"}
print(Fruits2)# out: {'apple', 'cherry', 'banana'}
       {'grape', 'pear', 'orange'}
```

这里可以清楚地看到，尽管将多个值`apple`或`pear`传递给了集合，但只产生了一个实例。同样，这些可以使用 for 循环生成，如下所示:

```
import randomnums = set([])for x in range(25):
    y = random.randint(10,20)
    nums.add(y)print(nums)# out: {10, 12, 14, 15, 16, 17, 18, 20}
```

其中虽然有 25 个 10–20 范围内的随机整数，但最终输出只包含 8 个唯一值，而不是列表中出现的 25 个值。同样，这可以用对集合的理解更简洁地写出来。

```
nums = {random.randint(10,20) for num in range(25)}print(nums)# out: {11, 12, 13, 14, 15, 16, 17, 19, 20}
```

因此，这种理解和列表理解的区别在于花括号的使用，而不是包含理解的方括号。

类似于列表和字典理解，这也可以用于现有的列表来生成集合。例如，如果我们想根据除以 1.6 的结果将公里数转换为英里数，则只需要唯一的值，并将其限制为小于 100 公里的值。

```
kms = [10, 12, 65, 40, 12, 75, 34, 65, 10, 10, 38, 100, 160, 200]miles = {d/1.6 for d in kms if d < 100}print(miles)# out: {0.625, 0.75, 2.5, 2.125, 4.0625, 4.6875, 2.375}
```

## 摘要

因此，理解可以很容易地用于创建新的列表、字典和集合。使用它们可以减少生成它们所需的行数，并增加可读性。它们可以替代 append()、map()、filter()或 reduce()函数。

很明显，这些方法可以扩展到执行更复杂的理解，比如使用 lambda 函数、嵌套列表理解或多重条件。然而，这样做值得注意的是，理解可能很快变得笨拙和难以理解，在这种情况下，当需要执行几个操作时，为了提高可读性，返回到创建函数或 for 循环是值得的。