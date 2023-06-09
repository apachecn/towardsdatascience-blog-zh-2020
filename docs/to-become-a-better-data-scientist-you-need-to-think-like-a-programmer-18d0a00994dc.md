# 要成为更好的数据科学家，你需要像程序员一样思考

> 原文：<https://towardsdatascience.com/to-become-a-better-data-scientist-you-need-to-think-like-a-programmer-18d0a00994dc?source=collection_archive---------53----------------------->

## 拥有强大的编程技能将使你有能力探索数据科学的新领域。但是如何成为一个呢？

# 动机

随着您越来越多地参与数据科学，有时您需要实现研究论文中的新方法，或者为特定用途定制一个库。因此，对于一个数据科学家来说，成为一名优秀的程序员是非常重要的。

尽管我一直在使用 Python 的可视化和机器学习库，但对我来说，从理论上实现算法并开发 Django 应用程序是一项挑战。我花了一个多月的时间来实现 Voronoi 图。

[](/how-to-find-the-nearest-hospital-with-voronoi-diagram-63bd6d0b7b75) [## 如何用 Voronoi 图找到最近的医院

### 给定美国医院的大型数据集，我们如何快速找到最近的医院？

towardsdatascience.com](/how-to-find-the-nearest-hospital-with-voronoi-diagram-63bd6d0b7b75) 

但是就像人们常说的“成为一个好的编码者的最好方法是尝试从零开始实现一些算法”。实现算法后，我学会了调试代码和快速找到解决方案的基本策略。有了这些策略，与我过去的工作流程相比，我可以在更短的时间内达到同样的效果。这种能力让我有勇气**探索更具挑战性的领域，创造创新产品**。

我希望我即将分享的策略也能帮助你在数据科学的道路上成为一名更高效的程序员。

![](img/7ac0712e126fffdb11e0986ac60bcaaf.png)

照片由[杰佛森·桑多斯](https://unsplash.com/@jefflssantos?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上拍摄

# 一次消除一个潜在错误

## 我过去做的事

当我的代码中出现错误时，如果代码很长，我可能会怀疑代码的不同部分可能是潜在的原因。代码的 10 个部分中可能只有 3 个部分导致了问题。但是因为我花了很多时间去修复每一个我怀疑的部分，所以我浪费了时间去修复不必要的部分。更糟糕的是，我还可能导致我的代码遇到更多的错误。

## 我的新方法

一次排除一个可能原因。再次运行代码，看看是否有效。如果没有，请排除下一个可能的错误。我经常惊讶于发现和修复错误的速度有多快。

# 停止尝试，开始尝试

## 我过去做的事

当用 Django 实现一个应用程序时，由于 Django 对我来说是新的，我在 Google 上搜索如何开发一个特定的功能。我对许多可供选择的方案感到困惑。经过近一个小时的寻找，最终一无所获。

## 我的新方法

我没有试图去寻找做某事的完整教程，而是挑选了一些旨在做类似任务的教程，并试图理解它为什么有效。然后我会从教程中挑选一些可能对我的代码有用的元素，并对其进行测试。通过这样做，我可以比严格遵循教程更快地创建个性化功能。

# 使用 Git Commit 保存工作

## 我过去做的事

在我的代码中引入更多元素后，我最终遇到了一些错误。我想**回到代码运行时的状态，并从那里重新开始我的工作**。但是我不记得为了恢复到那个状态，删除哪个代码，保留哪个代码。那时我才意识到**用 git commit** 保存我工作的不同状态是多么重要。

![](img/2e147e1eaa3d63f2d0853fe9955a9a53.png)

## 我的新方法

我保持着为我的项目创建 Github repo 的新习惯。然后使用克隆它

```
git clone url/of/yourgithubproject
```

我也提醒自己在成功开发某个特定功能后，保存工作的某个状态。这些是我最喜欢用来完成这项任务的命令行:

```
git add .
git commit -m "Add id"
```

然后我在 VSCode 中使用 Git Lens 在我的工作的不同提交之间来回切换。右键单击要返回的提交，然后选择*切换到提交*。当前文件将切换回这种状态。

![](img/0b751ece239d0d7f5342cc7dbd99e858.png)

检查完此状态后，如果您想要重置到此状态，只需右键单击提交，然后选择*重置以提交*。现在你又回到以前的状态了！最棒的是，如果你不喜欢你正在切换到的版本，你可以通过切换回你当前的分支很容易地切换回你当前的版本。

查看我关于 VSCode 的文章，了解使用该工具可以获得的更多生产力技巧:

[](/how-to-leverage-visual-studio-code-for-your-data-science-projects-7078b70a72f0) [## 如何在数据科学项目中利用 Visual Studio 代码

### 直到发现一种新的有效方法，我们才意识到我们是多么低效

towardsdatascience.com](/how-to-leverage-visual-studio-code-for-your-data-science-projects-7078b70a72f0) 

# 别想太多，试出来就好

## 我过去做的事

实现一个特定的任务有不同的方法，所以我试着在选项之间权衡，以得出最佳的实现。在许多情况下，我可能有一个特定功能的解决方案，但认为一定有更好的方法。我最终花了几个小时寻找替代解决方案，并对自己无法完成任何事情感到沮丧。

## 我的新方法

通过简单地**实现我想到的第一个选项**，我很快解决了一个特定的问题。一旦使功能工作，我可以寻找一个更好的，如果有必要的。

例如，我希望每次用户进入数据库时，都会创建具有新 id 的新数据。但是新数据不断得到 0 的 id，导致主键重复的错误。研究了几下一无所获，我问自己如果只是把当前的 id 0 加到数据的长度上会怎么样？随着数据的增加，id 也会增加，我再也不会出现重复的错误。像这样一个简单的解决方案是有效的！

# 旨在制造错误

## 我过去做的事

在测试代码的每个部分之前，我尝试开发一个长代码。我非常害怕如果不完善我的代码，我会遇到错误。当运行我的代码时，我最终得到了一堆错误，我不知道错误来自哪里。它可能是我的未测试代码的任何部分。

## 我的新方法

只是**运行一小部分我已经实现的代码**。当我有错误时，我知道下一步我需要处理什么来使整个代码工作。

# 认为这很容易

## 我过去做的事

想想我需要实施的所有步骤。当我知道我需要学习很多新的东西来完成这项工作时，我感到气馁。

## 我的新方法

我将复杂的实现分解成更小的容易理解的任务。在试图寻找完成任务的方法之前，我告诉自己，也许我**已经具备了实现这个**的条件。我只需要找到一种方法**将我的旧知识应用于这个新问题**。

这种想法防止我过度思考，并使我能够用我的知识创造。如果应用旧知识不起作用，至少我知道是什么使它不起作用。这将帮助我有效地过滤和缩小搜索范围。

# 结论

这些策略帮助我提高了我的编码技能。我希望你可以采用这些策略来改进你当前的编码实践。拥有一个好的编码方法会给你勇气和动力去尝试新的方法，用创新的方法解决挑战性的问题。

我喜欢写一些基本的数据科学概念，并尝试不同的算法和数据科学工具。你可以在 LinkedIn 和 Twitter 上与我联系。

如果你想查看我写的所有文章的代码，请点击这里。在 Medium 上关注我，了解我的最新数据科学文章，例如:

[](/how-to-learn-data-science-when-life-does-not-give-you-a-break-a26a6ea328fd) [## 当生活不给你喘息的机会，如何学习数据科学

### 我努力为数据科学贡献时间。但是发现新的策略使我能够提高我的学习速度和…

towardsdatascience.com](/how-to-learn-data-science-when-life-does-not-give-you-a-break-a26a6ea328fd) [](/how-to-accelerate-your-data-science-career-by-putting-yourself-in-the-right-environment-8316f42a476c) [## 如何通过将自己置于合适的环境中来加速您的数据科学职业生涯

### 我感到增长数据科学技能停滞不前，直到我有了一个飞跃

towardsdatascience.com](/how-to-accelerate-your-data-science-career-by-putting-yourself-in-the-right-environment-8316f42a476c) [](/how-to-create-reusable-command-line-f9a2bb356bc9) [## 如何创建可重用的命令行

### 你能把你的多个有用的命令行打包成一个文件以便快速执行吗？

towardsdatascience.com](/how-to-create-reusable-command-line-f9a2bb356bc9) [](/achieve-reproducibility-in-machine-learning-with-these-two-tools-7bb20609cbb8) [## 使用这两个工具在您的机器学习项目中实现可重复性

### 你能打包你的机器学习模型，并根据你的需要挑选一个最好的吗？

towardsdatascience.com](/achieve-reproducibility-in-machine-learning-with-these-two-tools-7bb20609cbb8) [](https://medium.com/skilluped/how-to-finish-your-side-projects-in-times-of-uncertainty-d7af45330ac0) [## 如何在不确定时期完成你的兼职项目

### 有什么方法可以让你在隔离期间工作得更有效率？

medium.com](https://medium.com/skilluped/how-to-finish-your-side-projects-in-times-of-uncertainty-d7af45330ac0)