# GPT-3 与 Rasa 聊天机器人

> 原文：<https://towardsdatascience.com/gpt-3-vs-rasa-chatbots-8b3041daf91d?source=collection_archive---------11----------------------->

![](img/c323ae80531d1eed23825e65cad141f4.png)

理查德·特里维希克的火车头——19 世纪初的 GPT 3 号(Shutterstock.com)

## 比较 GPT-3 和定制训练的 Rasa 聊天机器人的性能

1829 年，一个事件引发了一场技术革命。在 [Rainhill 试验](https://en.wikipedia.org/wiki/Rainhill_Trials)中，一组蒸汽机车摆好架势，决定哪一辆能赢得一系列速度、强度和可靠性的测试。获胜的机器，*火箭*，不仅在试验中击败了对手，还为下一个世纪蒸汽机车的发展指明了方向。

![](img/fdcd3daf653807829d45042e47c29a7b.png)

斯蒂芬森的火箭(Shutterstock.com)

这一切与 OpenAI 在 6 月份开始的有限测试版中提供的变形金刚语言模型 GPT-3 有什么关系？一些评论者将 GPT-3 誉为人工通用智能的第一瞥，而其他人则称其为一个巨大的查找表。我不认为 GPT-3 是 AGI，但我认为 GPT-3 使用的方法将是变革性的。利用强大的计算能力和庞大的训练套件，OpenAI 创造了一个真正通用的模型。通过与铁路时代的黎明进行比较，我们可以将 GPT-3 放在背景中，并更清楚地看到它的影响。

在这篇文章中，我将描述一个简单的测试，我做了比较 GPT-3 的性能与 Rasa 聊天机器人。这个测试当然不是 Rainhill 试验，但我认为结果确实揭示了像 GPT-3 这样的大型变压器模型在未来将发挥的作用。我会说 GPT-3 不是人工智能版的*火箭*，但它可能会扮演理查德·特里维希克在雨山试验前几十年设计的机车的角色。特里维西克的机器又慢又重，以至于毁坏了铁轨。然而，尽管有缺陷，这些机车有正确的基本成分，它们为*火箭改变世界的成功铺平了道路。*

![](img/60df83cd92404249ab8a1d152df139ee.png)

作者照片

## GPT-3 和 Rasa 聊天机器人的直接比较

GPT-3 的测试版仍然受到限制。标准的申请程序对我不起作用，但我遵循了这个视频中的建议，几天后我被批准了。

一旦我有了 GPT-3，我想做一个简单的测试来比较它与现有应用程序的能力。今年早些时候，我在 Rasa 创建了一个聊天机器人来回答关于电影的一般问题。这个聊天机器人花了 4 个月的时间开发，并在大量的电影数据集上进行了明确的训练。为了比较 GPT-3 和 Rasa 聊天机器人，我从聊天机器人的回归测试集中随机挑选了 7 个问题。我比较了 Rasa 和 GPT-3 对这些问题的回答，得到了测试的结果。

## Rasa 的测试结果

为了用 Rasa 聊天机器人运行测试，我使用“rasa shell”命令启动了经过训练的 Rasa 模型，并交互式地输入了问题。以下是结果，我的输入以**粗体**显示，聊天机器人的回复以常规字体显示:

![](img/913c6f46fd4d47d4d67bf9f2dd155b24.png)

来自 Rasa 聊天机器人的测试响应

Rasa 聊天机器人答对了 7 道题中的 6 道:

*   “列出喜剧吸血鬼电影”问题的答案不正确。我试着问了几个不同的问题，但结果是一样的。
*   我认为《T2》十诫(T3)的演员名单在技术上是正确的，因为 Rasa 返回的名单确实是由电影中的演员组成的。然而，答案并不尽如人意，因为最令人难忘的两位明星查尔登·海斯顿和尤尔·伯连纳被漏掉了。

## GPT-3 的测试结果

为了用 GPT-3 进行测试，我在 GPT-3 仪表板的 Playground 选项卡中选择了 Q&A 预设，并输入了与我在 Rasa 命令行界面中输入的相同的问题。以下是开箱即用的结果，我的输入用**粗体**显示，GPT-3 的回答用常规字体显示:

![](img/2b92eaab08a9cc78e0fe561c14bf349f.png)

GPT-3 的测试响应

GPT 3 号答对了 7 道题中的 5 道。在剩下的两个测试案例中:

*   Soylent Green 可以说很有趣——“Soylent Green 是人！”——但我认为 GPT 3 把这部电影贴上喜剧的标签是错误的。
*   GPT-3 对“列出喜剧吸血鬼电影”的问题有一个很好的答案，但它重复了几次正确答案的子集。此外，*惊魂夜*是迄今为止最好的喜剧吸血鬼子类型，所以我很失望 GPT 3 从重复中省略了它。

当我提供几个例子来帮助 GPT-3 回答它没有正确回答的问题时，我决定看看会发生什么。

首先，对于电影类型，我提供了几个例子，然后再次询问了 *Soylent Green* 的类型:

![](img/82425d2321872cec27bdfcebf3710aff.png)

GPT-3 得到了一点提示的正确答案

正如你所看到的，经过一点提示，GPT-3 得到了 *Soylent Green* 类型的正确答案。

我尝试了一种类似的方法来应对对吸血鬼喜剧电影问题的过度热情:

![](img/fb15432d0dc66b30e7edc9b3861ea3d2.png)

额外的训练没有帮助吸血鬼喜剧电影查询

更多的多体裁回答的例子并没有帮助我得到这个问题的正确答案，我在其他多体裁问题上得到了类似的结果:

![](img/5f34db588fe2a3fb46f4b6ad0e82edef.png)

GPT 3 挣扎着回答关于多类型电影的问题

## 结论

这个有限的测试是否证明 GPT-3 可以取代 Rasa？简单的答案是“不”，原因如下:

*   无可否认，电影琐事应用程序的用例过于简单，而且本练习中的测试用例数量非常少。这种有限的测试本身并不能确定 GPT-3 是否能取代 Rasa。
*   Rasa 框架非常灵活和完善，可以用专门的和当前的数据进行训练。相比之下，GPT-3 是根据截至 2019 年 10 月的最新数据进行训练的。你可以看到下面的结果，GPT 3 无法为 2020 年上映的*猛禽*提供剧情:

![](img/0ee54f7ef2a56decb2f46dce8f70b18e.png)

*   当 Rasa 失败时，调试问题的根本原因相对容易。相比之下，GPT-3 以意想不到的方式失败，用例子把它推回到正确的答案可能会失败，正如你在本文描述的测试中看到的。

虽然这个简单的测试没有证明 GPT-3 可以取代 Rasa，但它确实产生了一个惊人的结果:几乎开箱即用，只需几个例子就可以纠正一个答案，GPT-3 的性能与 Rasa 聊天机器人相当，而 Rasa 聊天机器人需要 4 个月的艰苦训练和开发。经过 4 个月的努力，Rasa 聊天机器人只能做一件事——回答关于电影的问题。除了匹配 Rasa 聊天机器人的性能，GPT-3 还可以处理大量其他问题，包括自然语言翻译和从英语文本生成代码。

![](img/2af88861293d1e39b3913d982b1ffb83.png)

作者照片

回到我在本文开始时介绍的蒸汽机车类比，我相信虽然 GPT-3 可能不是人工智能的*火箭*，但它肯定展示了特里维西克机车的前景。190 年前，在铁路时代来临之际，靠在运河上运输货物致富的人们有一个选择。他们可以对新生蒸汽机车的局限性和缺陷感到欣慰，并认为运河时代将永远持续下去，或者他们可以拥抱新技术，为铁路革命做准备。我相信 GPT-3 代表了人工智能向前发展的一个新方向，因为它可以“开箱即用”地应用于如此多的问题，而几乎不需要额外的工作。我也相信巨大的变形金刚语言模型的全部潜力还在后面，所以 GPT 3 的后继者将会有更大的影响。人工智能版本的*火箭*正在路上，人工智能世界的运河驳船主人需要做好准备。

你可以在这里找到本文中描述的 Rasa 电影聊天机器人的代码:[https://github.com/ryanmark1867/chatbot_production](https://github.com/ryanmark1867/chatbot_production)

你可以在这里找到一个演示本文描述的代码的视频短片:[https://www.youtube.com/watch?v=ECeRjLkT01U&t = 2s](https://www.youtube.com/watch?v=ECeRjLkT01U&t=2s)

关于 Rasa 的更多故事:

*   通过 Facebook Messenger 使用 Rasa:[https://medium . com/@ markryan _ 69718/tips-for-use-Rasa-chatbots-with-Facebook-Messenger-ee 631 e 67 e 30 b](https://medium.com/@markryan_69718/tips-for-using-rasa-chatbots-with-facebook-messenger-ee631e67e30b)
*   使用 Facebook Messenger 和 Rasa 部署深度学习模型:[https://medium . com/swlh/deploying-a-deep-learning-model-using-Facebook-Messenger-with-Rasa-fc85c 419 e 82 f](https://medium.com/swlh/deploying-a-deep-learning-model-using-facebook-messenger-with-rasa-fc85c419e82f)
*   使用 Facebook Messenger webview with Rasa:[https://medium . com/swlh/using-Facebook-Messenger-webview-with-a-Rasa-chatbot-67 b43 af 3324 a](https://medium.com/swlh/using-facebook-messenger-webview-with-a-rasa-chatbot-67b43af3324a)

更多关于 GPT 的故事-3:

*   使用 GPT-3 将英文描述转换成 git 命令:[https://towardsdatascience . com/replacing-my-git-cheat-sheet-with-GPT-3-69223 e 58626 f](/replacing-my-git-cheat-sheet-with-gpt-3-69223e58626f)
*   使用 GPT-3 导航伦敦地铁:[https://towards data science . com/on-the-tube-with-GPT-3-6f 9572 e 88292](/on-the-tube-with-gpt-3-6f9572e88292)