# 现在，每两个皮达尼斯人中就有一个应该学习戈朗语

> 原文：<https://towardsdatascience.com/one-in-two-pythonistas-should-learn-golang-now-ba8dacaf06e8?source=collection_archive---------3----------------------->

## 意见

## 为什么 Google 的语言在 web 开发、系统编程等方面击败了 Python

![](img/fad7768bc4149c00189d5ce6f35e91cb.png)

谷歌地鼠在工作。图片来自 [Golang 网站](https://golang.org/doc/gopher/)。

![Y](img/1864a05fd5673a0b1702a1fd713d09c8.png)  Y 我们一般的软件工程师还在爱着 Python。甚至结婚了。

但谷歌、优步、Dropbox、Soundcloud、Slack 和 Medium 的员工却没有。顶级公司的程序员早已爱上了这种有着可爱吉祥物的语言。

这并不是说 Python 不好。太棒了！

但是，无论是 API、web 服务还是数据处理——尽管大多数开发人员仍在使用 Python，但表现出色的人正在越来越多地采用 Golang，或 Go。因为它很棒。

# 由先驱者创造

围棋是由谷歌的全明星三人组发明的:罗伯特·格里斯默是谷歌 V8 JavaScript 机器的负责人之一，也是谷歌发明的另一种语言 Sawzall 的主要开发者。Rob Pike 共同开发了 Unix 环境，并共同创建了 Limbo 编程语言。有了 Ken Thompson，这个团队就有了 Unix 的发明者和 B 语言——C 语言的前身——的创造者。

Google 最初是用 Python 编写的[——是的，Python 仍然很酷——但是在 2007 年左右，工程师们在寻找一种更好的语言来执行 Google 的典型任务。根据 Rob Pike 在 2012 年的一次演讲，他们遇到了这样的问题:](http://infolab.stanford.edu/~backrub/google.html)

*   **缓慢的构建:**产生新代码要花很长时间。听起来很熟悉！
*   **不受控制的依赖关系:**你有没有试过安装一个软件包，却发现你必须安装至少五个其他的依赖关系和无数的子依赖关系才能让它工作？事实证明，即使是谷歌员工也有这个问题。
*   **每个程序员使用不同的语言子集:**在 Python 中，一个开发人员可能使用 numpy 包，另一个更喜欢 scipy，以此类推。当程序员想要将他们的代码混合到一个包中时，事情就变得混乱了。
*   糟糕的程序理解:那些说他们在阅读代码的那一刻就理解了代码的人是在撒谎。至少如果它不是一个非常简单的“Hello World”程序的话。并且代码的文档通常没有帮助——在大多数情况下，它甚至不存在，或者写得很差。
*   **重复工作:**你有没有从程序的一部分复制一段代码，只是为了把它复制到别的地方？不好的做法。但是大多数编程语言都很容易做到。
*   **更新的成本:**面对上述的混乱局面，更新软件需要花费大量的时间和脑力，你真的会感到惊讶吗？不酷。
*   版本偏差:重复代码到处都是，工程师可能只更新原始代码片段的一个版本，而忘记了其他版本。所以你最终会得到一个包含新旧代码的版本。听起来很混乱？确实是。
*   **编写自动化工具的难度:**编写自己编写代码的程序是可能的——事实上，大多数程序在某个阶段都会这样做。但是用现代编程语言，这仍然很难实现。
*   **跨语言构建:**你知道问题所在——Python 非常适合中小型脚本，C++非常适合复杂的程序，Java 非常适合 web 开发，Haskell 非常适合懒惰但健壮的代码。结果是一个程序经常包含许多不同语言的代码片段。但是为了编译、调试和简洁起见，用一种语言编写程序要好得多。

因此，三人组着手设计一种干净、简单、易读的语言。这种语言将会消除或者至少减轻软件工程中这些太常见的问题。

[](https://medium.com/@kevalpatel2106/why-should-you-learn-go-f607681fad65) [## 为什么要学围棋？

### " Go 将成为未来的服务器语言."Tobias Lütke，Shopify

medium.com](https://medium.com/@kevalpatel2106/why-should-you-learn-go-f607681fad65) 

# 精益语言…

这些常见问题的根源是现代语言的复杂性。想想 Python 或 C——你有没有尝试过阅读完整的文档？祝你好运。

相比之下，围棋最大的特点就是简单。这并不意味着你不能用它来构建复杂的代码。但是 Go 是非常谨慎的，不要有带来更多复杂性而不解决问题的特性。

例如，Go [不像其他面向对象语言那样有类](https://medium.com/@simplyianm/why-gos-structs-are-superior-to-class-based-inheritance-b661ba897c67)。作为其他语言的一个常用特性，类对于让一个对象继承另一个对象的属性非常有用。问题是，如果你试图改变一个对象的结构而不改变其他对象的结构，你会破坏代码。Go 有一个替代方法，叫做 struct，它更倾向于组合而不是继承。

![](img/4a8c43fc5125abd374d7da012ba3a345.png)

谷歌应用引擎的地鼠。图片来自 [Golang 网站](https://golang.org/doc/gopher/)。

Go 的其他主要功能包括:

*   **类型安全:**在 C 中，你可以使用指针做任何事情——包括让程序崩溃。围棋不会让你这样乱来的。
*   **可读性:**和 Python 一样，Go 把可读性放在第一位。这使得它比大多数语言对初学者更友好，也使得代码更容易维护。
*   文档:特别是初级开发人员发现写一些关于你的代码的简介让其他人可以使用是很乏味的。有了 Godoc，这个过程比大多数语言自动化得多——开发者不必浪费宝贵的时间写下他们一直在做的事情。
*   **正交性:**这意味着如果你改变了代码中的一个对象，其他对象不会因此而改变。从这个意义上说，[收音机是正交的](https://stackoverflow.com/questions/1527393/what-is-orthogonality)，因为如果你换台，音量不会改变。例如，与 C 语言非常不同——如果你改变了一件事，那么其他人可以依赖于它而改变。Go 是正交的，因为它使事情变得更简单。
*   在 Go 中，编写一段代码只有一种方法。与 Python 相比，你有无数种方法来编写一个东西！
*   实用性:重要的东西应该易于编码——即使这意味着其他事情在 Go 中是不可能完成的。这里的逻辑是，您希望通过使重复任务变得快速和简单来提高开发人员的生产率。如果有更复杂的问题——这种情况很少发生——他们总是可以用另一种语言来写。

所有这些听起来可能很无聊，没有创意。从某种意义上来说，这是真的——这是一种没有可以用来给别人留下深刻印象的时髦特征的语言，解决问题的过多方法，没有没有限制的自由。Go 不是一种可以用来探索和研究的语言。

但是当你试图建造一些有用的东西时，这是很神奇的。当你在一个团队中，有很多来自不同背景的不同的人在编写相同的代码。当你厌倦了其他语言带来的混乱时。

![](img/a0d97ff55745abdd282150728602da29.png)

如何 gopher？图片来自 [Golang 网站](https://golang.org/doc/gopher/)。

# …一个繁荣的社区

由于其简单性，Go 是当今最具协作性的语言之一。程序员过去常常坐在他们的小隔间里，从不与他人见面的时代已经过去了。

现在，我们有了 StackExchange 来解决我们所有的编码问题。我们有 Slack、Zoom、Google Meet 等工具来与我们的团队保持联系。但是现代语言仍然是为小隔间里的小书呆子量身定做的。

Go 改变了这一切。尽管比 Python 年轻 20 年，但它有一个充满活力的社区。

所以毫不奇怪，他们把尊重、开放和友好放在他们行为准则的首位。虽然其他语言，如 Python 或 C，也有类似的社区声明，但对这些基本价值的强调较少。

因此，社区在年度 Go 调查中扮演明确的角色就不足为奇了——不像在许多其他语言中。

![](img/99c0753e4baf822f918f1f2c93a9859b.png)

关于社区和领导力的问题，来自 [2019 Go 开发者调查](https://blog.golang.org/survey2019-results)。

# 数据不言自明

根据 [2019 Go 调查](https://blog.golang.org/survey2019-results)，谷歌的语言最常用于 web 开发、网络和系统编程。Python 的前景看起来非常相似:

![](img/5e8b0cd84c28684230fdcdd8366063f5.png)

Python 的使用，来自 2019 [Python 开发者调查](https://www.jetbrains.com/lp/devecosystem-2019/python/)。

唯一显著的区别是 Python 用于数据分析和机器学习的程度。在这些领域，其他热门的新语言正在出现。

除此之外，你可以看到 Python 的许多用法可以被 Go 取代。其中包括 46%的网页开发，37%的系统管理和开发，19%的网络编程。即使你假设许多开发人员做所有这三项工作，你也可以有把握地假设一半的 Pythonistas 正在做他们在 Go 中可以做的事情。

事实上，开发人员意识到了 Go 提供的巨大潜力。根据 Hackerrank 的数据，2019 年大约有三分之一的程序员想要学习围棋。

![](img/e145cc4a42363b9e948716191a080f79.png)

根据[黑客排名](https://info.hackerrank.com/rs/487-WAY-049/images/HackerRank_2019-2018_Developer-Skills-Report.pdf)，接下来最热门的语言。

这种趋势是真实的——由于围棋非常容易学习，我们应该会在未来几年看到从 Python 到围棋的转变。对于大多数公司来说——尤其是那些没有 Dropbox 或 Medium 那么大和资金充足的公司——重写他们所有的代码将会非常昂贵。但是对于新项目，你至少应该尝试一下。

在最大的公司里，开发人员已经在用 Go 建立他们的成功。你什么时候会？