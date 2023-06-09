# 面向对象编程已经死了。等等，真的吗？

> 原文：<https://towardsdatascience.com/object-oriented-programming-is-dead-wait-really-db1f1f05cc44?source=collection_archive---------0----------------------->

## 函数式编程的鼓吹者们，你们把枪口对准了错误的敌人

![](img/0f42321de0e996a323bbc4ea2b985a27.png)

如果这么多人讨厌面向对象编程，为什么它仍然占主导地位？Vale Zmeykov 在 [Unsplash](https://unsplash.com/s/photos/geometry-human?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

20 世纪 60 年代的编程有一个很大的问题:计算机还没有那么强大，它们需要在数据结构和过程之间进行[分割。](https://medium.com/javascript-scene/the-forgotten-history-of-oop-88d71b9b2d9f)

这意味着，如果你有一大堆数据，如果不把计算机推到极限，你就不能做那么多。另一方面，如果你需要做很多事情，你不能使用太多的数据，否则计算机会永远运行不完。

然后，艾伦·凯在 1966 年或 1967 年提出理论，认为人们可以使用封装的微型计算机，这些计算机不共享数据，而是通过消息传递进行通信。通过这种方式，可以更加经济地使用计算资源。

尽管这个想法很巧妙，但直到 1981 年，面向对象编程才成为主流。然而，从那时起，它就没有停止吸引新的和经验丰富的软件开发人员。面向对象程序员的市场和以前一样繁忙。

但是最近几年，这种有十年历史的模式受到了越来越多的批评。有没有可能，在面向对象编程风靡大众四十年后，技术正在超越这种范式？

[](/why-developers-are-falling-in-love-with-functional-programming-13514df4048e) [## 为什么开发人员会爱上函数式编程

### 从 Python 到 Haskell，这种趋势不会很快消失

towardsdatascience.com](/why-developers-are-falling-in-love-with-functional-programming-13514df4048e) 

# 函数和数据耦合有那么蠢吗？

面向对象编程背后的主要思想非常简单:你试图把一个程序分解成和整体一样强大的部分。接下来，您将数据片段和那些只在相关数据上使用的函数结合起来。

请注意，这仅包括封装的概念，也就是说，位于对象内部的数据和函数对外部是不可见的。人们只能通过消息与对象的内容进行交互，通常称为 getter 和 setter 函数。

最初的想法中没有包含的，但被认为是今天面向对象编程所必需的，是继承和多态。继承基本上意味着开发人员可以定义拥有其父类所有属性的子类。直到 1976 年，在它的概念提出十年之后，它才被引入面向对象编程。

多态性在另一个十年后来到了面向对象编程。基本上，这意味着一个方法或一个对象可以作为其他方法或对象的模板。从某种意义上说，这是继承的一般化，因为并不是原始方法或对象的所有属性都需要传递给新实体；相反，您可以选择覆盖属性。

多态的特别之处在于，即使两个实体在源代码中相互依赖，被调用的实体更像是一个插件。这使得开发人员的生活更加轻松，因为他们不必担心运行时的依赖性。

值得一提的是，继承和多态并不是面向对象编程所独有的。真正的区别在于封装了数据片段和属于它们的方法。在计算资源比今天稀缺得多时候，这是一个天才的想法。

![](img/7044d37c8d2274084efb3fddff5e2166.png)

面向对象编程不是一个愚蠢的想法。这使得编码变得容易多了。由 [Unsplash](https://unsplash.com/collections/9691452/business?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的[窗口](https://unsplash.com/@windows?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)拍摄的照片

# 面向对象编程中的五大问题

一旦面向对象编程风靡大众，它就改变了开发人员看待代码的方式。20 世纪 80 年代以前流行的过程编程是非常面向机器的。开发人员需要对计算机如何工作有相当多的了解，才能写出好的代码。

通过封装数据和方法，面向对象编程使得软件开发更加以人为中心。方法`drive()`属于数据组`car`，但不属于数据组`teddybear`，这符合人的直觉。

当遗传出现时，那也是直觉。很有意义的是，`Hyundai`是`car`的子群并且共享相同的属性，但是`PooTheBear`不是。

这听起来像是一台强大的机器。然而问题是，只懂面向对象代码的程序员会把这种思维方式强加到他们做的每一件事情上。这就像人们看到到处都是钉子，因为他们只有一把锤子。正如我们将在下面看到的，当你的工具箱里只有一把锤子时，这会导致致命的问题。

## 香蕉大猩猩丛林问题

想象你正在建立一个新的程序，你正在考虑设计一个新的类。然后，您回想起您为另一个项目创建的一个整洁的小类，您意识到它非常适合您当前正在尝试做的事情。

没问题！您可以在新项目中重用旧项目中的类。

除了这个类实际上可能是另一个类的子类，所以现在你也需要包含父类。然后，您意识到父类也依赖于其他类，您最终会包含大量代码。

二郎的创造者，乔·阿姆斯特朗，著名的[宣称](https://www.defprogramming.com/quotes-by/joe-armstrong/):

> 面向对象语言的问题是，它们拥有所有这些隐含的环境。你想要一个香蕉，但你得到的是一只大猩猩拿着香蕉和整个丛林。

这几乎说明了一切。重用类没问题；事实上，这可能是面向对象编程的一个主要优点。

但是不要走极端。有时你最好写一个新的类，而不是为了枯燥而包含大量的依赖项(不要重复)。

![](img/51d7c153ea9c1e7ad6ce8734c5caf8f4.png)

要聪明，不要像宗教一样遵循一种范式。[车窗](https://unsplash.com/@windows?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在[挡泥板](https://unsplash.com/collections/9691452/business?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)上拍照

## 脆弱的基础类问题

假设您已经成功地为新代码重用了另一个项目中的一个类。如果基类改变了会怎样？

它会破坏您的整个代码。你可能都没碰过它。但是某一天你的项目运行得很好，第二天就不行了，因为有人改变了基类中的一个小细节，而这个小细节对你的项目来说是至关重要的。

使用继承越多，可能需要做的维护就越多。因此，即使重用代码在短期内看起来非常有效，但从长远来看，它可能会变得非常昂贵。

## 钻石问题

继承是一个可爱的小东西，我们可以把一个类的属性转移给其他类。但是如果你想混合两个不同类的属性呢？

你做不到。至少不是以优雅的方式。以类`Copier`为例。(我从 Charles Scalfani 的[病毒故事](https://medium.com/@cscalfani/goodbye-object-oriented-programming-a59cda4c0e53) *再见，面向对象编程*中借用了这个例子，以及关于这里提出的问题的一些信息。)复印机扫描文件内容，然后打印在一张空白纸上。那么它应该是`Scanner`的子类，还是`Printer`的子类呢？

根本没有好的答案。尽管这个问题不会破坏您的代码，但它经常出现，足以令人沮丧。

## 等级问题

在钻石问题中，问题是哪个类`Copier`是。但是我骗了你——有一个简单的解决方案。让`Copier`作为父类，`Scanner`和`Printer`作为子类，它们只继承属性的一个子集。问题已解决！

很好。但是如果你的`Copier`只是黑白的，而你的`Printer`也能处理彩色的，那该怎么办呢？这个意义上的`Printer`不就是`Copier`的一个概括吗？如果`Printer`连接了 WiFi，而`Copier`没有呢？

在一个类上堆积的属性越多，建立适当的层次结构就越困难。实际上，您正在处理属性集群，其中`Copier`共享`Printer`的一些属性，但不是所有属性，反之亦然。如果你试图把它固定在层级结构中，并且你有一个大的复杂项目，这可能会把你引向一场混乱的灾难。

![](img/ab13407e34f6c090b196ae3baba9825e.png)

不要混淆层次结构，否则你可能会陷入混乱。艾玛·道在 [Unsplash](https://unsplash.com/collections/9691452/business?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

## 参考问题

你可能会说，好吧，那我们就只做没有层次结构的面向对象编程。相反，我们可以使用属性集群，并根据需要继承、扩展或覆盖属性。当然，这可能有点乱，但这将是手头问题的准确表示。

只有一个问题。封装的全部目的是保护数据块之间的安全，从而提高计算效率。没有严格的等级制度，这是行不通的。

考虑如果一个对象`A`通过与另一个对象`B`交互来覆盖层次结构会发生什么。`A`和`B`有什么关系并不重要，只不过`B`不是直接的父类。那么`A`必须包含一个对`B`的私有引用，因为否则，它不能交互。

但是如果`A`包含了`B`的孩子也拥有的信息，那么这个信息可以在多个地方被修改。因此，关于`B`的信息不再安全，封装被破坏。

尽管许多面向对象的程序员用这种架构来构建程序，但这不是面向对象编程。就是一团乱。

# 单一范式的危险

这五个问题的共同点是，它们在不是最佳解决方案的地方实现了继承。因为继承甚至没有包含在面向对象编程的原始形式中，所以我不认为这些问题是面向对象所固有的。它们只是教条走得太远的例子。

然而，不仅仅是面向对象编程可能会过头。在纯粹的[函数式编程](/want-to-get-started-in-functional-programming-enter-scala-ea71e5cfe5f8)中，处理用户输入或在屏幕上打印消息极其困难。面向对象或过程式编程更适合这些目的。

尽管如此，仍有一些开发人员试图将这些东西作为纯函数来实现，并将他们的代码扩充到几十行，没有人能够理解。使用另一种范式，他们可以很容易地将代码减少到几行可读的代码。

范式有点像宗教。他们善于中庸——可以说，耶稣、穆罕默德和佛陀说了一些很酷的东西。但是如果你遵循它们到最后的小细节，你可能会让你自己和你周围的人的生活变得非常痛苦。

编程范例也是如此。毫无疑问，函数式编程正在获得越来越多的关注，而面向对象编程在过去几年中已经受到了一些严厉的批评。

了解新的编程范例并在适当的时候使用它们是有意义的。如果说面向对象编程是让开发者走到哪里都看到钉子的锤子，那这是把锤子扔出窗外的理由吗？不。你在工具箱里放一把螺丝刀，也许一把小刀或一把剪刀，然后根据手头的问题选择工具。

函数式和面向对象的程序员都一样，不要把你的范例当成宗教。它们是工具，在某个地方都有用途。你用什么应该只取决于你在解决什么问题。

[](https://medium.com/madhash/what-is-better-functional-programming-or-object-oriented-9a116c704420) [## 函数式编程和面向对象哪个更好？

### 你可能问错了问题

medium.com](https://medium.com/madhash/what-is-better-functional-programming-or-object-oriented-9a116c704420) 

# 最大的问题是:我们正处于一场新革命的风口浪尖吗？

最终，函数式编程与面向对象编程之间的争论——诚然相当激烈——可以归结为:我们是否正在走向面向对象编程时代的终结？

越来越多的问题出现了，而函数式编程通常是更有效的选择。想想数据分析、机器学习和并行编程。你越深入这些领域，你就会越喜欢函数式编程。

但是如果你看看现状，有十几个面向对象的程序员和一个函数式程序员。这并不意味着如果你更喜欢后者，你就找不到工作；如今功能性开发人员仍然非常缺乏。

最有可能的情况是，面向对象编程将在未来十年左右继续存在。当然，前卫是实用的，但这并不意味着你应该抛弃面向对象。在你的节目中有这样的表演还是非常好的。

所以在未来几年内，不要把面向对象编程扔出你的工具箱。但是要确保这不是你唯一的工具。