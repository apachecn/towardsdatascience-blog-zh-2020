# 假阳性或假阴性:哪个更糟？

> 原文：<https://towardsdatascience.com/false-positives-vs-false-negatives-4184c2ff941a?source=collection_archive---------18----------------------->

## 数据科学概念

## 解释第一类和第二类错误

![](img/3d2fc3c275299d42cee61731b54b25d8.png)

[腾雅特](https://unsplash.com/@tengyart?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

在统计学和数据科学中，有一种叫做“*假阳性*或“*假阴性”的东西。“现在，你很可能在日常生活中遇到过这些术语。它们实际上被广泛使用，但是你有没有想过它们到底是什么意思？*

对于统计学家和数据科学家来说，这些术语正式称为第一类和第二类错误。在您探索数据科学和统计学时，您会遇到这些术语，因此了解这两者之间的区别非常重要。在对这些术语有了更多的了解之后，你会在日常生活中注意到第一类和第二类错误。

> [在这里注册一个中级会员，可以无限制地访问和支持像我这样的内容！在你的支持下，我赚了一小部分会费。谢谢！](https://marco-santos.medium.com/membership)

# 第一类和第二类错误从何而来？

像其他统计术语一样，第一类和第二类错误来自统计假设检验。通常在这些测试中，我们能够得出某种结论。这一结论并不总是正确的，当结论错误时，会导致错误，即*类型的*错误。根据我们得出的结果和我们犯下的错误，这个错误可以是 I 类错误，也可以是 II 类错误。

更具体地说，当我们拒绝了事实上为真的零假设时，我们犯了第一类错误。当我们接受零假设时，第二类错误发生了，事实上，它是假的。

# 假阳性还是假阴性？

![](img/a14baf4aa51f896b8490a40e8995a60d.png)

巴勃罗·加西亚·萨尔达尼亚在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄的照片

你可能想知道哪个错误是假阳性和假阴性。这就是:

> 假阳性= I 型错误
> 
> 假阴性=第二类错误

将这些错误称为假阴性或阳性似乎更容易。你可以称这些错误为假阳性或假阴性，没有人会被它困扰，但你应该记住它们的正式名称类型 I 和类型 II 错误。

# 这些错误意味着什么？

既然我们已经了解了哪个是哪个，我们可以继续解释它们的确切含义。为了更好地理解这些术语，我们将举例说明。

![](img/afd808f7776688fa9583f9ea98379d9e.png)

[自由股票](https://unsplash.com/@freestocks?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

## 第一类错误(假阳性)

I 型错误或假阳性的一个常见但有效的例子通常是妊娠试验。假阳性是告诉某人他们怀孕了，而事实上他们没有，就像告诉一个男人他们怀孕了。

## 第二类错误(假阴性)

继续以怀孕为例，第二类错误或假阴性会告诉孕妇她们没有怀孕。

所有这些错误在犯下时都有不同的后果。这些错误的结果可能是可怕的，但确定哪一个更糟完全取决于问题。

# 犯错误和后果的例子

假设你正在做一个实验，试图对一个物体是不是蛋进行分类。你会得到几十个真正的鸡蛋和几十个蛋形的石头。现在这里的问题是，你只能在视觉上对它们进行分类，而不能触摸它们。

因此，让我们快速浏览这个实验，到达您创建了一个可以以大约 90%的准确率对鸡蛋进行分类的机器的部分。这就是错误可能出现的地方。与每个错误相关的后果取决于问题。

![](img/7fcaf806a8f24bc03d91fcff11f278d9.png)

照片由[娜塔莉·瑞亚·里格斯](https://unsplash.com/@natalie_rhea?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

## 向房子里扔鸡蛋

例如，如果我们的机器将一个蛋形岩石分类为一个鸡蛋，就会出现 I 类错误或假阳性。从几个方面来看，这可能比第二类错误更糟糕。如果我们是一群想往房子里扔鸡蛋的孩子，结果我们扔了块石头打破了窗户。一些原本需要花费时间和水来清洁的东西现在可能会伤害到某人，并演变成严重的破坏行为。

在这种情况下，如果我们的机器将一个鸡蛋分类为*而不是*一个鸡蛋，就会出现假阴性的第二类错误。在我们的例子中，这不是一个大问题，因为我们不会选择这个*非*蛋。现在，作为一群孩子，我们不会使用这种非鸡蛋，因为我们想在不破坏任何东西的情况下给房子下鸡蛋。

## 哪个更糟？

在这个例子中，我们可以看到第一类错误比第二类错误代价更大，后果更严重。在这里，一类错误比二类错误更糟糕。我们希望不要因为我们使用这些蛋的目的而把一个蛋形的岩石误归类为蛋。

现在，如果我们改变了这些鸡蛋的用途，那么我们可能犯的更严重的错误也会改变。第二类错误怎么会比第一类错误更糟糕？

## 金蛋

![](img/056c5454a11d29d4758d59ce5489b1b5.png)

莎伦·麦卡琴在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

如果我们想找到尽可能多的蛋呢，因为每个蛋都非常有价值。也许鸡蛋里有黄金或同等价值的东西。在这种情况下，如果我们的机器将一个鸡蛋误认为不是鸡蛋，那么我们可能会错过一些黄金。然而，即使我们的机器将一块石头误分类为一个鸡蛋，这个错误也不会像鸡蛋例子中那样代价高昂。

# 确定最大误差

从上面的例子中可以看出，根据问题的不同，每个错误都有自己的一组问题。没有最糟糕的错误，因为每个问题都有自己的复杂性。在整个项目和实验中都会出现错误。由项目设计人员、测试人员或数据科学家决定最需要减少哪个误差。

因为每个问题都有它自己的背景和障碍，你需要在设计你的实验和项目时把它们都考虑进去，以知道哪个错误是最糟糕的。希望在阅读完本文后，您对错误的类型以及假阳性和假阴性之间的区别有了更好的理解。

[*在 Twitter 上关注我:@_Marco_Santos_*](https://twitter.com/_Marco_Santos_)