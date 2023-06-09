# 我如何发布了一个应用程序和模型来对 85 种蛇进行分类(你也可以这样做)

> 原文：<https://towardsdatascience.com/how-i-published-an-app-and-model-to-classify-85-snake-species-and-how-you-can-too-c13ac8fdb6c?source=collection_archive---------40----------------------->

## 从 MOOC 到现实，你如何成为一名实践者，如何克服项目过程中的任何挑战！

# 为什么？

我刚刚完成了最后一门 MOOC 课程，不禁想知道自己是否准备好开始一个项目。我吓坏了，害怕了，缺乏自信。然而，经过数周的沉思，我咬紧牙关，宣布我将创建一个简单的图像分类模型。

现在我有一个在 Play Store 上正式可用的应用程序[和一个带有开源代码的](https://play.google.com/store/apps/details?id=com.kamwithk.snaked) [GitHub repo](https://github.com/KamWithK/Snaked) 。我想解释一下我所面临的障碍以及我在克服这些障碍时所学到的经验(希望这也能帮助你)！

![](img/9aff0532919e19198e998da950804555.png)

封面图片来源于[此处](https://en.wikipedia.org/wiki/Snake)

# 我的旅程

*   从谷歌图片搜索结果中创建了我自己的数据集
*   从最简单的线性回归模型开始
*   尝试使用我自己定制的 [CNN](https://www.kamwithk.com/convolutional-neural-networks-basic-theory-in-a-nutshell-ck6hl9wdl000qi5s1venh4nk1)
*   切换到一个 [**大得多的数据集**](https://www.aicrowd.com/challenges/snake-species-identification-challenge)
*   参加了斯坦福大学的 CS231n 课程来巩固我的基础(理论知识)
*   创建了基本代码来训练一个 [MobileNetV2 模型](https://www.kamwithk.com/modern-algorithms-choosing-a-model-ck6hwiovf004ndfs1529fcppy)
*   了解超级融合(关于 PURE PyTorch 超级融合的文章即将推出……)
*   为 Snaked 创建了一个 [Android 应用程序，可以在输出蛇的种类之前拍摄和导入照片](https://play.google.com/store/apps/details?id=com.kamwithk.snaked)

简而言之，我犯了很多错误，这也正是我学习的方式。谷歌图片报废让我体会到创建一个包含 **120，000 张图片**的数据集所付出的努力。从线性回归开始是一个重大的、愚蠢的和可笑的错误，但它教会了我 [CNN 的](https://www.kamwithk.com/convolutional-neural-networks-basic-theory-in-a-nutshell-ck6hl9wdl000qi5s1venh4nk1)和[预先训练好的模型](https://www.kamwithk.com/modern-algorithms-choosing-a-model-ck6hwiovf004ndfs1529fcppy)的第一手价值。在这样的任务中尝试线性回归也迫使我去发现神经网络是如何工作的以及为什么会工作！一个普通的预训练模型的长训练时间和平庸的结果使我发现了超级收敛！

> 我的错误就像一个个阶段，如果没有每一个阶段，我就不会学到我所学的全部内容

# 好处

一个显而易见的问题是，既然免费的 MOOC 可以教授相同的内容(甚至可能花费更少的时间和精力)，为什么还要克服一个又一个障碍呢？我已经[回答了问题](https://www.kamwithk.com/how-to-learn-data-science-and-eventually-become-an-expert-ck6j0fd7o00lodfs1bbhafek9)，但简而言之，归结为:

> 你记得你反复使用的信息，并逐渐忘记所有其他的信息

现在，这并不意味着你不去参加任何 MOOC 教程，只是**确保你不会陷入“教程地狱”**！相反，如果你知道基础知识，那么就把你现在学到的东西应用到创建一个你可以炫耀的又酷又有趣的项目中去！

# 我克服的挑战

## 我应该现在开始吗？

你质疑自己目前的技能、知识和理论基础水平的事实表明，你意识到了自己理解的局限性！这并不意味着你很笨，或者没有准备好，相反，你学到了足够多的东西，知道前方还有很多路等着你。

> 要明白总会有更多的东西要学，所以不妨开始使用你已经知道的东西

## 我的想法够好吗？

你可以做两件事来判断:

*   我的想法是不是太简单/复杂了？
*   问别人

如果你不确定这个项目会有多复杂，考虑一下其他人在类似任务中的表现。找到答案的一个方法是搜索在线文章或研究论文。如果你找到了数百个，那么问题可能太简单了，但是如果你只找到了几个，那可能就不现实了(或者你有一个天才的想法)。手头的主题知识是必须的，所以只要研究这个主题，看看你会发现什么！

如果你还没有任何与数据科学家的联系，那么你就必须伸出援手(像我一样)！无论如何，我都会尽快这样做，因为在任何情况下，拥有不同的观点总是非常有用的。我个人的方法是联系我附近的数据科学家，说我正在研究机器学习，寻求一些建议。大多数人拒绝，但如果你付出足够多，它仍然有效！

## 万一失败了呢？

> 找出**为什么**你的项目不能工作！

如果找出*为什么*一个想法行不通不能解开另一个解决方案，那么你已经发现了一些新的东西……这就是一种成就！

## 我不知道该怎么办！

找出与你试图解决的问题相似的问题。对我来说，我从如何使用 PyTorch 分类数字(MNIST)和更复杂的对象(CIFAR100)的教程开始。我跟着教程走，弄清楚他们是如何完成任务的。然后我使用**迁移学习**，复制每个教程所做的，但是这次是为了我自己的问题。

> 当然，我还远远没有准备好应对全部挑战，但是随着时间的推移，我越来越明白了。

如果你仍然停滞不前，你可能真的需要回到书本(或课程)中去。

## 什么都没用！

只要坚持下去，过一会儿，就会有所收获！在创建我的第一个模型的开始，我的代码都没有运行，但最终(几天后)，我设法找到了 bug 并修复了它。我知道如何用 PyTorch 运行培训和评估循环！请注意，通常是一个小小的微小变化最终会使代码复活(所以，四处试验，大量调试，你就会弄明白)。

## 我不明白*一切是如何运作的？*

理论可能很难。你可以有一个工作模型，但是不知道迁移学习模型、优化器、损失函数…或者你用过的其他东西是如何工作的。但是训练模型需要多长时间…几小时，几天，几周？如果你能写代码，就这么做，运行它，在它工作的时候学习理论。你们俩的*训练然后*(双关语)！

## 这是可行的，但是我如何改进它？

我有一篇关于如何改进你的模型的博文。一旦你有了一个工作模型，看看吧！

## 创建一个像样的模型后，我做什么？

这是一个循环:

> 学习，创造，提高，炫耀，冲洗，重复！

只是创建博客，创建项目，然后继续这个循环。

# 感谢阅读！

既然你已经听了我的漫谈，我想感谢你花时间通读我的博客(或者跳到最后)。

如果这对你有所帮助，请考虑查看[如何选择型号](https://www.kamwithk.com/modern-algorithms-choosing-a-model-ck6hwiovf004ndfs1529fcppy)！