# PEP 8 风格指南概述

> 原文：<https://towardsdatascience.com/an-overview-of-the-pep-8-style-guide-5672459c7682?source=collection_archive---------18----------------------->

![](img/9baf1081a97c2e81a6fbd65b682aef82.png)

照片由[克里斯里德](https://unsplash.com/@cdr6934?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

## 让您的 Python 代码具有风格。

ython Enhancement Proposal 8 或 PEP 8 是一个全面的 Python 代码样式指南。PEP 8 的目标是将所有 Python 集合在一个样式指南下。这增加了 Python 代码的可读性和整体理解。PEP 8 并不意味着在任何情况下都要遵循。你会遇到不适用的代码，如果是这样，你可能需要暂时脱离风格指南。关键是尽可能使用风格指南。它将帮助你和其他所有看到你的代码的人阅读和处理它。我会涵盖我认为最重要的领域。我不会讨论一些领域和其他领域，我可能只是略读一下。我真的推荐完整阅读 PEP 8，因为这个指南更像是一个快速概览。为了真正理解并获得更深入的解释，以及我选择不包含在本文中的部分。PEP 8 中我将复习的部分如下:

*   代码布局
*   用线串
*   空白
*   尾随逗号
*   评论
*   命名规格
*   推荐

PEP 8 可在此处找到:

[](https://www.python.org/dev/peps/pep-0008/) [## PEP 8 风格的 Python 代码指南

### Python 编程语言的官方主页

www.python.org](https://www.python.org/dev/peps/pep-0008/) 

# 代码布局

## 缩进:

*   4 个空格，虽然这取决于你的延续行，只要有某种形式的缩进。
*   您可以垂直排列括号中的换行元素，或者使用悬挂缩进。

```
# 4 space indent
def hello(var):
    print(var)# vertical alignmentexample2 = function(first_var, second_var,
                    third_Var, fourth_var)# hanging indentexample3 = function(
    first_var, second_var,
    third_var, fourth_var)
```

1.  您可以对太长或希望成为延续行的条件使用类似的工作流。您可以在两个字符的关键字后使用括号，这将允许在转到新行时自动缩进。这对于长条件语句很有用，比如一个`if`语句。对于嵌套语句，您可以选择没有额外的缩进，注释您的缩进细节，或者添加额外的缩进。
2.  您可以将结束标点(大括号、中括号或圆括号)与最后一行的第一个字符或非空白的多行表达式的第一个字符对齐。

```
# last line, first character
new_list = [
    'one', 'two', 'three',
    'four', 'five', 'six'
    ]# first line, first character
new_list = [
    'one', 'two', 'three',
    'four', 'five', 'six'
]
```

## 制表符和空格

1.  建议缩进时使用空格，而使用制表符是为了与使用制表符缩进的代码保持一致。
2.  Python 不允许在同一个代码中同时使用这两者。如果您正在转换混合了两者的 Python 2，请使用空格重做。

## 最大线路长度

1.  最大的行长度应该是 79 个字符，虽然我发现这有时是限制性的，在那些情况下必须更长。在这种情况下，最多可以输入 99 个字符。
2.  对于注释和文档字符串，应该使用 72 个字符，不能增加。
3.  这有助于阅读 Python 代码并将其保存在编辑器、检查和调试工具中。
4.  为了帮助你坚持下去，Python 有一个助手。您可以用括号将行括起来，从第一个关键字之后的所有内容开始，到下一个关键字之前结束。这是 PEP 8 建议的，它会根据正确的 Python 行样式格式自动换行。
5.  也可以使用反斜杠，仅当圆括号换行不适用时，例如`assert`语句。

## 使用二元运算符换行

1.  为了更好的可读性，你应该在二进制操作符之前换行，尽管在过去这是相反的，如果它们是一致的，这两者都是可以接受的。

## 空白行

1.  在类定义之前和之后应该有两个空行。
2.  方法定义前后都应该有一个空行。
3.  您应该在代码中保守地使用空行来分隔函数组。
4.  如果不同行之间只有一行代码相互独立，则不必包含空行。
5.  Python 使用 control-L (^L)换行符来表示空白。

## 源文件编码

1.  代码应该使用核心 Python 3 发行版的 UTF-8(Python 2 的 ASCII ),并且不应该有声明。
2.  除此之外的编码只应用于测试目的。
3.  跳转到 [PEP 3131](https://www.python.org/dev/peps/pep-3131/) 了解更多关于这项政策的信息。
4.  标识符应该只使用 ASCII，如果可能的话，应该使用英文单词。

## 进口

1.  导入通常没有空行分隔。
2.  导入通常应该在不同的行上分开，除非使用`from`关键字。
3.  导入属于代码的顶部，在注释和文档字符串之后，在全局变量和常量之前。
4.  进口应该是这个顺序。

*   标准程序库
*   第三方
*   特定于本地/库。

5.推荐绝对导入，但是显式相对导入也很好。以不太冗长的为准。

6.从单独的类模块导入类。

7.除非必要，否则不应使用通配符(`*`)。

8.模块级“dunders”是带有两个尾随下划线的名称。这些名称应该放在注释和文档字符串之后，但在导入之前。

9.`from __future__`导入必须在除注释和文档字符串之外的任何代码之前。

# 用线串

1.  字符串两边的单引号或双引号意思相同。你可以选择你更喜欢哪一个，但是要坚持，这样你就可以用你没有选择的替代来代替反斜杠。
2.  三重引号应该使用双引号字符。检查一下 [PEP 257](https://www.python.org/dev/peps/pep-0257/) 。

# 空白

避免尾随空白。

1.  不要在你的表达式和语句中使用过多的空格。如果逗号、冒号和分号不在中括号、大括号或圆括号后面，则应该在逗号、冒号和分号后面有空格。
2.  对于任何运算符，您都应该在运算符的两边使用空格。用于切片的冒号被视为二元运算符，它们之间不应该有任何空格。
3.  当调用函数`function()`时，函数旁边应该有不带空格的括号。
4.  索引或切片时，括号应直接紧挨着集合，没有空格`collection[‘index’]`。
5.  不建议使用空格来排列变量值。
6.  当可选选项可用时，请确保与您选择的格式一致。

# 尾随逗号

1.  唯一需要尾随逗号的时候是在创建单个元素元组的时候。
2.  如果您使用尾随逗号，请用括号将它们括起来。
3.  尾部逗号经常在版本控制中使用，用来详细说明以后将要扩展的区域。

# 评论

1.  确保您的注释有意义，并且对阅读代码有用。适得其反的注释可能会损害代码的可读性。
2.  更新代码时，请确保更新您的注释。
3.  确保你的评论对其他 Python 程序员来说容易理解。
4.  块注释是一段或多段单行注释，以每行的结束标点结束。他们应该以`#`开头，然后是空格。同样，块注释的缩进量应该与它们将要进入的代码的缩进量相同。用一行没有任何内容的注释来分隔段落。
5.  在多行注释中，在句尾使用两个空格，除了在最后一句后只使用一个空格。
6.  行内注释是跟在同一行代码后面的注释。保守地使用行内注释。在您的代码后面，它们应该至少由两个空格分隔。只有在必要时才使用它们。
7.  文档字符串或文档字符串确实如其所述。它们为模块、函数、类和方法提供文档。对于以下所有内容，您都应该有 Docstrings。通过在文档串的开头和结尾使用三个`“””`引号来创建文档串。要了解更多关于文档字符串的信息，请看 [PEP 257](https://www.python.org/dev/peps/pep-0257/) 。

# 命名规格

**尽管 Python 库中的命名约定与 Python 有些不一致，但仍然建议使用当前的命名约定，除非您正在使用的已经有了不同的约定，然后使用该格式。**

最重要的原则是你应该为你的 API 的公共方面反映用法而不是实现。

**有多种命名方式可供选择。记得要有描述性。您也可以使用前缀将名称组合在一起。**

```
b  
B  
lowercase  
lower_case_underscore
UPPERCASE
UPPER_CASE_UNDERSCORE
CamelCase
mixedCase
Cap_words_Underscore # not recommended 
```

## 4.规范的命名约定

*   单前导下划线:弱，除非内部使用，否则不推荐使用。
*   单结尾下划线:用于避免 Python 关键字的问题。
*   双前导下划线:用于命名类属性。
*   双前导和尾随下划线是用户名称空间中的“神奇”对象或属性。

**要避免的名字:**

```
# try not to use.
l  # lowercase L
O  # uppercase o
I  # uppercase i
```

**ASCII 兼容性:**

*   标准库要求标识符与 ASCII 兼容。

**包和模块名称:**

*   如果可能的话，包和模块应该有小写和简短的名字。
*   模块可以有下划线。
*   包不应有下划线。
*   如果一个模块在 C 或 C++中，并且与一个 Python 模块相关联，那么它会创建一个更高的接口，并且可以用一个前导下划线来命名。

**类名:**

*   使用大写单词的惯例`WordExample`。
*   如果函数有很好的文档记录，并且主要用于可调用，那么您可以使用函数命名约定。
*   内置名称通常是一个单词或两个单词长。他们也只对异常和内置常量使用大写单词约定。

**类型变量名称:**

*   类型变量应该使用大写字母约定和简称。
*   后缀`_co`用于具有协变行为的变量。
*   后缀`_contra`用于具有逆变行为的变量。

**异常名称:**

*   使用类命名约定。
*   后缀`Error`用于出错的异常名。

**全局变量名称:**

*   遵循函数命名约定。
*   `__all__`机制应该用来防止由`from M import *`引起的全局变量或者像前缀`globals`一样使用。

**功能&变量名:**

*   函数和变量应该是带下划线的小写字母。
*   如果已经在使用混合案例风格，您可以使用它。

**函数&方法参数:**

*   包含`self`作为即时方法的第一个参数。
*   包含`cls`或类方法的第一个参数。
*   如果需要，最好使用尾随下划线，而不是缩写。

**方法名&实例变量:**

*   使用函数命名约定。
*   对非公共方法和实例变量使用前导下划线。
*   如有必要，您可以使用两个前导下划线，以使用 Python 的名称 mangling。

**常量:**

*   带下划线的大写命名约定。

**继承:**

*   确保您的类的属性是公共的或非公共的。
*   非公共属性不是为第三方设计的。
*   “私有”是 Python 中使用的一个术语。
*   “子类 API”(又名。“受保护”)。旨在继承。基类。
*   公共属性=没有前导下划线，除非关键字冲突。
*   只公开公共数据属性的属性名。
*   子类化的类可以用双前导下划线来命名，使用 Python 的名称转换器。

## 5.公共和内部接口

*   用户应该能够区分公共接口和内部接口。
*   如果一个接口被文档化，它就被认为是公共的，除非文档中另有说明。
*   未记录的接口是内部接口。
*   模块应该使用`__all__`来声明公共 API。如果`__all__`设置为空列表，表示没有公共 API。
*   内部接口的单前导下划线。
*   如果任何名称空间是内部的，那么接口也是内部的。
*   导入是一个实现细节。

# 推荐

1.  编写代码，以免对 Python 的其他实现产生负面影响。
2.  `is`或`is not`来比较单件。
3.  `is not`而不是`not is`。
4.  将 lambda 表达式绑定到标识符时，使用`def`而不是赋值。
5.  对于例外情况，使用`Exception`代替`BaseException`。
6.  确保您的异常链接被正确使用。
7.  尽可能具体说明例外情况。
8.  使用显式名称绑定语法。
9.  对操作系统错误使用显式异常层次结构。
10.  当使用`try`和`except`时，在需要包装在`try`块中的区域周围保持代码紧凑。
11.  在本地资源上使用`with`语句。
12.  确保正确使用`return`语句。要么有`return`表情，要么没有。
13.  与字符串模块相对的字符串方法。
14.  使用方法`.startswith()`和`.endswith()`进行字符串前缀和后缀切片。
15.  使用`isinstance(<item>, <item>)`而不是`if type(<item>) is type(<item>)`。
16.  空序列被视为`False`。
17.  不要用`==`来做`True` `False`的比较。
18.  流控制语句应该在`finally`代码块中。

## 函数注释

*   功能注释见 [PEP 484](https://www.python.org/dev/peps/pep-0484/) 。

## 可变注释

*   变量注释见 [PEP 526](https://www.python.org/dev/peps/pep-0526/) 。

# 结论

对于任何 Python 程序员来说，PEP 8 都是一个不可思议的资源。如果使用正确，它将保持你的代码可读性和 PEP 8 的风格参数。同样，这只是对 PEP 8 的一个简要概述，如果你想真正了解这个令人惊叹的样式指南，我鼓励你在 Python 网站或 GitHub 上阅读整个内容。我希望你喜欢阅读和快乐编码！

[](https://www.python.org/dev/peps/pep-0008/) [## PEP 8 风格的 Python 代码指南

### Python 编程语言的官方主页

www.python.org](https://www.python.org/dev/peps/pep-0008/) [](https://github.com/python/peps/blob/master/pep-0008.txt) [## python/peps

### 标题:Python 代码版本风格指南:$Revision$ Last-Modified: $Date$作者:吉多·范·罗苏姆，巴里华沙…

github.com](https://github.com/python/peps/blob/master/pep-0008.txt)