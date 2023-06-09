# 我的机器学习模型表现很好，但我希望它失败

> 原文：<https://towardsdatascience.com/my-machine-learning-model-performs-well-but-i-want-it-to-fail-640660fe0d2c?source=collection_archive---------38----------------------->

## 探索数据科学家的伦理责任

![](img/ef1918f7c94d080040f58536a7feb440.png)

来源:图片 via [Pikist](https://www.google.com/search?q=moral+ethics+Pikist&tbm=isch&ved=2ahUKEwi6142L9_XrAhUC_qwKHVkkBhoQ2-cCegQIABAA&oq=moral+ethics+Pikist&gs_lcp=CgNpbWcQAzoCCABQgEpYoJ4BYNOhAWgAcAB4AIABTogBiwGSAQEymAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=3FhmX7r5AYL8swXZyJjQAQ&bih=581&biw=1221#imgrc=v2e1iWuA-kKaLM) 在知识共享许可下。

我是 Metis 数据科学训练营的应届毕业生，在那个项目中，我们的一个项目专注于建立一个分类模型。我们可以选择任何我们选择的数据集来工作，在我的情况下，我选择使用疾病控制中心 2007-2016 年的国家健康和营养检查调查(NHANES)结果，并训练一个模型来预测一个人是否患有高血压(二元分类:是或否)。我在我的机器学习模型中测试了一系列 28 个变量，包括人口统计数据、饮食习惯、酒精摄入量、活动水平、职业等。在测试了各种模型之后，我选择了一个逻辑回归模型，它使用了 5 个变量、过采样，并将阈值设置为 0.34，从而将我的目标召回率提高到 0.899。我构建了一个漂亮的 Tableau 图形来表示我的发现，这样，我在技术上实现了我的目标:分类模型完成。检查。

对于数据科学社区的人来说，这可能不是一项突破性的工作。对于数据科学社区之外的人来说，你可能会想(如果我还没有失去你的话)，“我不知道什么是逻辑回归模型或者你在那之后说的任何事情。”不管你的观众是谁，我都明白。但是我的模型的技术细节不是我想谈论的。

## 我想谈谈为什么我希望我的模型失败。

为什么？

在我的模型中，五个变量中有四个是在意料之中的。首先是**年龄**，这是不幸但不可避免的。年龄越大，患高血压的几率就越高。然后，体重、**的增加、酒精摄入**和**吸烟**都增加了预测高血压的机会，这可能很难，但可以由个人控制或改变。

但让我困惑的是模型的第五个变量。这个变量是一个特殊的少数民族——如果一个人是这个民族的，他就会有更高的血压。我觉得没有必要在这里说种族，因为我不想这篇文章是关于我(白人妇女)谈论另一个种族。那不是我的位置，也不是我应得的平台。如果你真的想知道，用谷歌很快就能找到答案，因为我看到了我的模型的结果，并搜索了让人们处于高血压风险的因素，以检查我的变量(并希望能告诉我为什么我的种族变量是错的)。

我想谈的是如何看待我的模型中的种族变量，以及在这种情况下数据科学家的责任。有可能在种族和高血压之间有一种[基因联系——这本身是令人悲伤的——但也有可能它代表了这个种族面临的许多其他可能导致高血压的社会问题。那是…真的很难过。即使这个特定的模型不是这样，这种相同的思路也可以应用于任何一个模型，在这个模型中，由于历史上对种族的压迫，种族作为一个变量出现。](https://www.heart.org/en/health-topics/high-blood-pressure/why-high-blood-pressure-is-a-silent-killer/high-blood-pressure-and-african-americans)

# 当数据科学家看到他们的模型结果代表更大的社会问题时，他们会怎么做？

有些人可能认为这不是数据科学家的责任，而是其他人的责任，数据科学家只是构建东西。我不太同意这一点，并认为有义务做得更多，但我也不知道这看起来像什么。所以我想在这里提出这个问题，因为我相信这应该是一个更广泛的对话。对我来说，很难将这种模式视为“完成”并继续前进。我对我在建模方面的技术工作感到自豪，但不能说我对展示这些发现感到自豪。我很难过，很生气，也很不舒服。

也许我的机器学习模型很简单，但它提出的道德问题很复杂。

我鼓励并希望对这篇文章的评论。如前所述，我不是带着答案来的；我来这里是为了开始一场对话，希望你能加入进来，这样我们就能一起努力找到解决方案。

*这款机型的完整代码可以在 github 上的* [*这里*](https://github.com/cecann10/high-blood-pressure) *找到。*