# 如何构建让你作为数据科学家感到自豪的代码

> 原文：<https://towardsdatascience.com/how-to-build-code-you-can-be-proud-of-as-a-data-scientist-19c4101752fc?source=collection_archive---------21----------------------->

## [入门](https://towardsdatascience.com/tagged/getting-started)

## 让你在竞争中脱颖而出

![](img/7340680bd025547b55dbb21e037369af.png)

照片由[在](https://unsplash.com/@thisisengineering?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) [Unsplash](https://unsplash.com/s/photos/coding-proud?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

人们普遍认为数据科学家无法写出清晰易懂的代码。你不一定要这样。通过学习一些如何正确编写代码的原则，你可以将这种模式化运用到你的优势中，让你在竞争中脱颖而出。

为了找到最佳实践，我们应该只看软件工程的可靠实践。以下是一些软件工程原则，可以让你像数据科学家一样编写干净、易读、易操作的代码:

# 阅读文档

当谈到使用新技术时，我看到数据科学家犯的最大错误之一是忽略文档。工具或库的文档只是为了帮助用户更容易地将工具应用到他们的工作中。

当用户没有查阅文档时，开发阶段可能会花费太长时间，或者库可能没有被充分利用。

因此，当您准备使用一个从未使用过的工具时，请务必阅读并理解文档。这会让你的生活更轻松。 **‍**

# 编写文档

既然说到这个话题，我也必须强调写文档的重要性。您可能没有开发出将被成千上万人使用的最先进的代码，但是简单地记下您的代码中的所有内容就足够了。

这对那些在你之后使用你的代码的人，对你的队友，对你几年后回头看你写的东西的时候都是有用的。

你的文档不必看起来超级专业。只要一个 word 文档描述这段代码做什么，输入是什么，输出是什么就足够了。 **‍**

# 评论评论评论

类似于创建文档，对代码本身进行注释是一个救命稻草。养成一个习惯，在你写的每个函数的开头加上一两句话，解释这个函数做什么，预期的输入和输出是什么。如果函数中有一些复杂的逻辑，记下一些行做了什么。例如:“这行计算每列的平均值”，“这行删除平均值小于 10 的”，等等。 **‍**

# 编码前设计

这不是颜色/布局设计。在设计中，您决定项目的总体流程。在我的脑海中，我将代码设计分为两类:

*   **知道你的输入和输出需要什么**:对于你写的任何东西，都会有一个输入和输出。决定什么将被输入到你的代码中。这可能是您的业务利益相关者的需求，或者是您可以在网上找到的 JSON 类型。例如“我将从互联网上下载一个 CSV 文件”或“我将发送到数据库的 json 格式的查询答案”等。
*   **有目的地编写代码**:当你开发代码时，在每一步，花些时间想想接下来会发生什么。你知道你更大的目标，但短期目标是什么？在项目的这个阶段，你想达到什么目的？在[掌握数据科学方法](https://www.soyouwanttobeadatascientist.com/mdsm)上，规划步骤以内置任务的形式出现。在开始实现之前，您需要回答几个问题。以下是一名学生对这些作业的评价:

我发现，如果我不写下我的目标、假设或我想如何想象某件事的大纲……那么我的大脑很容易在设置这件事的过程中迷失或靠边站。这真的很容易忘记时间，甚至忘记我正在努力实现的具体具体的小步骤。喜欢这些有用的辅导问题！”—内森·埃克尔 **‍**

[点击此处了解课程的更多信息](https://www.soyouwanttobeadatascientist.com/mdsm)

# 清理您的代码

当然，说你需要清理你的代码有点抽象。我在这里的意思是，当你完成代码时，不要在代码中添加任何不必要的东西。这对数据科学家来说尤其是个问题。在 Jupyter 笔记本上，很可能尝试几行代码只是为了看看结果会是什么，然后忘记删除它，或者忘记跟踪哪些单元格是程序的一部分，哪些不再使用。

我所做的就是打开一个草稿本和一个最终本。我从在草稿本上编码开始。我在草稿笔记本上尝试了所有我想尝试的东西，并一步一步地实现了这些功能。而且每次我完成项目的一个阶段(比如数据探索)，我都会审核并把代码转移到最终的笔记本上。这样，我总是保持我的代码有条理，在最终的笔记本上没有不必要的代码行。这也有助于将错误降到最低，因为我会在每个阶段结束时检查我的代码。 **‍**

# 遵循命名惯例并清楚地命名

遵循严格的命名准则是软件工程中的一件大事。例如，根据您使用的语言或您工作的团队，这些可能是:

*   变量名应该以小写字母开头，变量名的第一个字母应该大写(soLikeThis)或
*   函数名应该以大写字母开头(FunctionNameXyZ)。

我不知道数据科学社区有严格的命名政策，老实说，我不认为强制执行这一政策是可行的。尽管如此，我认为与你自己的命名保持一致是个好主意。

只要决定你的风格是什么。在命名变量、类和函数时，有两种选择:大写字母(NewVariable)或无大写字母(newVariable)、下划线(new_variable)或无下划线(newVariable)。为每一种选择一种风格，并坚持下去。这将使你的代码更容易理解。

不过有一件事我很严格，那就是明确命名。你应该根据它们的角色来命名你的变量、函数和类，而不是随机的。数据帧 1 不可接受。尤其是当数据框在您的代码中起着关键作用时。这并不意味着您应该将其命名为 data frame _ where _ location _ and _ time _ is _ merged _ for _ model _ training。保持简短，让阅读你的代码的人能够理解。但是话说回来，当你获得一些经验时，命名会变得更容易，所以不要为了让它尽善尽美而给自己太大压力。 **‍**

# 保持一个整洁的文件结构

根据我的观察，数据科学家倾向于下载数据，启动笔记本，编写代码片段，并把它们放在桌面上，只有在真正需要的时候，他们才会把所有东西放在一个文件夹中。这不仅看起来不专业，也是生产力的杀手。当他们知道他们需要首先在上周随机创建的 10 个笔记本中找到他们需要工作的笔记本时，他们想要开始工作。

将所有项目文件保存在一个地方。为你的数据准备一个文件夹，并清楚地给你的笔记本命名，这样你就知道哪一个是你需要处理的。仅此而已。没什么特别的。只要在项目开始的时候就开始这个结构，这样你就不用花几个小时去整合所有的东西。 **‍**

# 使用版本控制

版本控制，或者换句话说，把你的代码保存在 GitHub 上会帮助你自信地做出改变，而不用害怕破坏一切。它将帮助你跟踪什么改变了，它将使你的代码在某个地方的服务器上保持愉快和舒适，这样它就不会仅仅因为有人离开你的公司而被删除。

我所说的“使用版本控制”不仅仅意味着你应该设置它。你也应该在你的项目中积极地使用它。每当你完成项目的一个新的部分时，把你的改变推送到 Git。让上传你的改变和工作成为一种日常习惯。这样，一切都保持良好和有组织的状态，对于新加入你的团队的人来说，继续工作是微不足道的。最重要的是，当某些东西崩溃时，恢复到最新的工作版本是很容易的。 **‍**

# 有效地使用调试

调试是在代码中出现问题时找出问题所在的能力。如果没有编码背景，这是新数据科学家最常见的技能之一。但这没问题，因为就像其他事情一样，这只是一项你需要学习的技能。

调试不仅仅是盯着你的屏幕试图找出问题所在。您需要知道如何与您的代码交流，以及如何理解它在抱怨什么。这可能包括:改变变量值，注释掉行，打印变量值，看看是否一切如你所愿。如果没有，这意味着有问题，你应该解决它。

如果我能告诉你一件关于调试的事情，那应该是:调试时一次只改变一件事。当你考虑它的时候，它是科学的。如果你想知道为什么有些事情不工作，你有 5 个不同的变量，你需要一个一个地改变它们，看看哪一个影响结果。如果你同时改变两个，并看到结果的变化，你不能推断哪个是导致变化的原因。听起来很简单，但许多新数据科学家犯了一个错误，他们太急于修复错误，反过来让他们的调试持续更长时间。

总而言之，说到编码，没有人是完美的。但是如果你遵循软件工程师使用的一些简单规则，你将会改进你的编码。一旦你开始把每天编码作为你工作的一部分，你的习惯将会是最重要的，还有什么更好的方法来获得更好的习惯，然后从今天开始适应最佳实践！

🐼*想更多地了解熊猫吗？* [*获取我的免费熊猫小抄。*](https://www.soyouwanttobeadatascientist.com/pandas-cheat-sheet)