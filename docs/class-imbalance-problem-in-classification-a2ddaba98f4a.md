# 分类中的阶级不平衡问题

> 原文：<https://towardsdatascience.com/class-imbalance-problem-in-classification-a2ddaba98f4a?source=collection_archive---------19----------------------->

## 如果 SMOTE 和 TOMEK 没有改善你的模型怎么办？

![](img/925b18cd5812503efbaf88dd27cdd725.png)

当我们在处理分类的时候，我们会面临很多问题。其中之一是阶层失衡:一个阶层代表过多，另一个阶层代表严重不足。这个问题出现在许多研究领域，例如，当我们试图诊断一种罕见的疾病或检测欺诈交易时。在这篇文章中，我想谈谈在我的一个分类项目中，我是如何处理班级失衡问题的。

通常，当我们的阶级比例低于 10/90 时，我们可以说我们面临着阶级失衡。在某些情况下，甚至会更严重。我曾经做过一个分类项目，试图预测丝芙兰出售的哪种美容产品会赢得声望[倾城之美奖](https://www.allure.com/story/best-of-beauty-2019-winners)。在检查了我的数据后，我意识到我有 1920 件产品没有获奖，只有 81 件获奖。注意:有更多的获奖产品，但只有 81 个在丝芙兰售出，我只是在处理他们的数据。

## 传统方法

为了创建一个二元分类模型，我决定先采用一种简单的方法:不加任何处理地运行逻辑回归。结果是预期的:模型执行的准确率为 96%,但不存在召回。这意味着，这种方法将所有未被充分代表的类别视为背景噪音，或者简单地说，只是假设所有产品都不是赢家，并且在 96%的情况下都是正确的。

如果我们谈论的是赢得奖项的美容产品，这不是世界末日，但如果我们试图诊断一种致命的疾病呢？我们需要消除第二类错误。

有两种著名的处理类不平衡问题的传统方法:使用 TOMEK 链接的欠采样和使用 SMOTE 的过采样。

在第一种情况下，我们检测两个不同类的实例之间的链接，这两个类彼此靠近并且混淆了模型。在我的项目中，可能有两个非常相似的产品(相同的价格，相似的评级，等等。)但是其中一个得了奖，另一个没有。我们在这些实例之间创建一个链接并删除它们，尽可能地将两个类分开。

对于 SMOTE(合成少数过采样技术)，我们采用不同的方法。我们不是减少数据点的数量，而是创建代表性不足的类的合成实例。同样，在我的例子中，我们只是分析价格、评级和其他代表诱惑赢家的预测因素，并创建更多具有这些特征的实例。

在从事我的项目时，我尝试了这两种方法，但我建立的模型(逻辑回归、朴素贝叶斯、XGBoost)都没有超过 78%的准确率，也没有提高召回率。

## 我反而做了什么

经过慎重考虑，我决定采取循序渐进的方法。

首先，我需要创建两个独立的数据框架，赢家和非赢家(为了简单起见，让我们称他们为输家，尽管这听起来可能不太合适)

```
df_lose = df[df[‘Allure’] == 0]
df_win = df[df[‘Allure’] == 1]
```

接下来，为了确保我的欠采样是无偏的，我们需要打乱非获胜数据帧 df_lose 的行:

```
df_lose = shuffle(df_lose)
```

接下来，我们需要截断这个数据帧，以匹配 df_win 的维度(记住，我们只有 81 个获胜者):

```
df_lose_81 = df_lose[:81]
```

最后，我们将它们连接在一起，再次洗牌，以防万一:

```
twodf = [df_win, df_lose_81]
edf = pd.concat(twodf, ignore_index=True)edf = shuffle(edf)
```

现在，我们可以查看新数据框的数字，并直观地检查这些类在其预测列中是否不同。事实证明，确实如此，尤其是在“心”这个类别(有多少人“喜欢”这个产品)

![](img/c8aec6d545a5bed151231ee8426a0552.png)

最后，我们可以运行我们的分类模型。我最好的模型是 XGBoost，验证准确率为 96.97%，召回率为 0.93。在得到这些有希望的结果后，我有点怀疑，如果我只是碰巧选择了两个类中最不同的实例呢？我重复了这个过程，将行重新排列了四次，每次模型的性能都保持不变。

请随意叉克隆我的 [GitHub repo](https://github.com/agorina91/Sephora_Classification) ，希望我的小小研究有所帮助！