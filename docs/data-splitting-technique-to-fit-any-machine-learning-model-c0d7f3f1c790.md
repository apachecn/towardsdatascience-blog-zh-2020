# 适合任何机器学习模型的数据分割技术

> 原文：<https://towardsdatascience.com/data-splitting-technique-to-fit-any-machine-learning-model-c0d7f3f1c790?source=collection_archive---------14----------------------->

## 将数据分成不同类别的目的是避免过度拟合

![](img/4e9ae777a38fd5082d1b355c458cea50.png)

[亚历克斯](https://unsplash.com/@worthyofelegance?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

这是一篇 4 分钟的短文，向大家介绍数据分割技术及其在实际项目中的重要性。

从伦理上讲，建议将数据集分为三部分，以避免过度拟合和模型选择偏差，称为-

1.  训练集(必须是最大的集合)
2.  交叉验证集或开发集或开发集
3.  测试设备

测试集有时也可以省略。这是为了获得真实世界中算法性能的无偏估计。将数据集分成两部分的人通常称他们的开发集为测试集。

> *我们试图在训练集上建立一个模型，然后尽可能地优化开发集上的超参数，然后在我们的模型准备好之后，我们试图评估测试集。*

## **#训练集**:

用于拟合模型的数据样本，即我们用于训练模型的数据集的实际子集(在[神经网络](/deep-learning-made-easy-part-1-introduction-to-neural-networks-434df17d8f03)的情况下，估计权重和偏差)。该模型观察并学习这些数据，并优化其参数。

## **#交叉验证集:**

我们通过最小化交叉验证集上的误差来选择适当的模型或多项式的次数(如果仅使用回归模型)。

## **#测试集:**

用于提供最终模型在训练数据集上的无偏评估的数据样本。只有在使用训练集和验证集对模型进行了完整的训练后，才使用它。因此，测试集是用于复制一旦模型被部署用于实时使用时将会遇到的情况类型的测试集。

测试集通常用于评估 Kaggle 或 [Analytics Vidhya](https://www.analyticsvidhya.com/) 竞争中的不同模型。通常在机器学习黑客马拉松中，交叉验证集与训练集一起发布，实际测试集仅在比赛即将结束时发布，并且是模型在测试集上的分数决定了获胜者。

## **#如何决定分割数据集的比例？**

![](img/e519b4f13d83282175c4b41b2ec37bee.png)

图:数据集分割，源-在[infogram.com](https://infogram.com/app/#/library)上制作

答案通常在于数据集本身。比例是根据我们可用数据的大小和类型(对于时间序列数据，拆分技术略有不同)决定的。

> 如果我们的数据集大小在 100 到 10，000，000 之间，那么我们以 60:20:20 的比例对其进行分割。也就是说，60%的数据将进入训练集，20%进入开发集，其余的进入测试集。
> 
> *如果数据集的大小超过 100 万，那么我们可以按照 98:1:1 或 99:0.5:0.5 这样的比例进行分割*

决定分割比的主要目的是所有三个集合应该具有我们的原始数据集的一般趋势。如果我们的开发集只有很少的数据，那么有可能我们最终会选择一些偏向于只存在于开发集中的趋势的模型。训练集的情况也是如此，太少的数据会使模型偏向于仅在数据集的该子集中发现的某些趋势。

我们部署的模型只不过是学习数据中统计趋势的估计器。因此，用于学习的数据和用于验证或测试模型的数据应尽可能遵循相似的统计分布，这一点非常重要。尽可能完美地实现这一点的方法之一是随机选择子集——这里是训练集、开发集和/或测试集。例如，假设您正在进行一个人脸检测项目，人脸训练图片来自 web，而开发/测试图片来自用户的手机，那么在训练集和开发/测试集的属性之间将存在不匹配。

将数据集划分为比率为 0.6、0.2、0.2 的 train、test、cv 的一种方法是使用 train_test_split 方法两次:

```
from sklearn.model_selection import train_test_split x, x_test, y, y_test = train_test_split (x_train,labels, test_size=0.2, train_size=0.8 )x_train, x_cv, y_train, y_cv = train_test_split(x,y,test_size = 0.25, train_size =0.75)
```

这篇文章就写到这里吧——如果你已经做到了，请在下面评论你的阅读经历并提供反馈，还可以在 [LinkedIn](https://www.linkedin.com/in/sachin-kumar-iit-kharagpur/) 上加我。

类似文章— [深度学习变得简单:第 3 部分:激活函数、参数和超参数以及权重初始化](/deep-learning-made-easy-activation-functions-parameters-and-hyperparameters-and-weight-c7bcfeb9af24)