# 开始使用:Python I/O

> 原文：<https://towardsdatascience.com/getting-start-with-python-i-o-9a28ce635ba4?source=collection_archive---------48----------------------->

## Python I/O 概述

## Python 如何与 I/O 交互的快速演示

![](img/810058a93097118f26c91f8ceef0146f.png)

照片由[克里斯蒂娜·莫里尔](https://www.pexels.com/pt-br/@divinetechygirl)在 [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral) 拍摄

> 有几种方法可以显示程序的输出；数据可以以人类可读的形式打印出来，或者写入文件以备将来使用。
> 
> Python 3 文档。

在开始时，ASCII 由 128 个字节表示；这些人物是在考虑使用英语的情况下创造出来的；因此，如果你死在一个像中国这样的国家，那里你的语言基础是特殊字符，这是不可能的，因为那时新的编码类型被创造出来了。例如，ISO-8859–1 编码(也称为 Latin_1)考虑的是西欧，如法国、西班牙、葡萄牙，但问题仍然存在，如果日本开发人员试图读取我们的文件怎么办？然后，一种新的编码类型 utf-8 诞生了，它支持超过 100 万个字符，包括阿拉伯语、汉语、俄语字符以及特殊字符。我们硬盘上的文件是以字节写的，所以我们可以知道读取这些字节的正确方式，编码提供了这一点，所以我们可以找出解码这些字节的正确方式。

# 开文件

首先，要知道我们文件的内容，我们需要打开它。

`>>> f = open(‘workfile’ ,’r’, encoding='utf-8')`

函数 open return 是我们文件的一个表示，或者你也可以理解为一个文件对象。函数 open 的第二个参数是我们的文件将被打开的模式，在这个例子中我们使用模式 r。

# 读取文件

现在，我们将看到读取文件的三种可能方式。

```
>>> f = open(‘workfile’ ,’r’)>>> f.readline()
>>> f.readlines()
>>> f.read()
```

**方法 readline:** 从文件中读取一行。

**方法 readlines:** 返回一个列表，其中每一项都是文件中的一行。因此，您可以迭代内容变量，以显示文件中的所有行。

**方法 read:** 以字符串格式返回文件的所有内容。

# **写文件**

我们已经知道如何打开一个现有的文件，现在我们将了解如何写入一个文件。

```
>>> f = open(‘workfile’ ,’w’)>>> f = open(‘workfile’ ,’w’)>>> new_content = 'someContent'
>>> f.write(new_content)
```

在这个例子中，我将写入一个现有的文件。当我使用 W(录制)模式时，如果你打开文件，你会看到旧的内容已经被删除，现在只有我们添加的内容在文件中。这就是录音模式的工作原理。
另一种保存文件的方式是使用 A()模式，这种模式不替换文件的内容，相反，新的内容被添加在文件内容的末尾。

# 关闭方法

你可能会问自己:我为什么要关闭我的文件？当我完成我的任务时，一切都将从记忆中清除，一切都很好。

嗯，你没有错。当你写一个文件时，Python 只在我们的应用程序完全完成时才释放我们的文件，也就是说，如果你有一个正在运行的进程或一个需要很长时间才能完成的大任务，如果你将信息写入一个文件，你将无法访问这些内容，直到你的应用程序完全完成，close 方法来帮助我们解决这个问题。

```
>>> f = open(‘workfile’ ,’w’)>>> new_content = 'someContent'
>>> f.write(new_content)
>>> f.close()
```

# **冲洗方法**

考虑上面的相同场景，您有一个需要在文件中插入一些数据的长任务，并且有几个例程将被执行，直到您的应用程序完成。但是，您需要向该文件添加更多信息。关闭并打开文件不是最佳解决方案。

你可以刷新，基本上，强迫 Python 插入文件中已经存在的东西，这样，如果你在应用程序完全完成之前打开它，数据将已经保存在文件中。

```
>>> f = open(‘workfile’ ,’w’)>>> new_content = 'someContent'
>>> f.write(new_content)
>>> f.flush()
.
.
.
```

# **求法**

这个方法将内存指针指向作为参数传递的数值位置，这个函数没有返回值，所以您需要使用它，然后使用一个读取方法在您指定的位置准确地显示它的内容。

```
>>> f = open(‘workfile’ ,’w’)>>> new_content = 'someContent'
>>> f.write(new_content)
>>> f.seek(0)
>>> line = f.readline()
>> print line
someContent
```

# 结论

使用 Python 文件很容易，这种语言的工作方式和给我们的反馈令人印象深刻。使用这些示例性的方法，您将能够在某些情况下有效地工作，但是如果您想迈出更大的一步，您必须理解，存在文件竞争的环境是一个更复杂的情况，但是更现实的是，这里展示的是以简单和正确的方式处理文件的基础。