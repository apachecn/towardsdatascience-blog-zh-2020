# 80/20 分割直觉和另一种分割方法

> 原文：<https://towardsdatascience.com/finally-why-we-use-an-80-20-split-for-training-and-test-data-plus-an-alternative-method-oh-yes-edc77e96295d?source=collection_archive---------9----------------------->

![](img/e3f25b175a948e5a5b99be99e8ec616c.png)

凯文·施密德在 [Unsplash](https://unsplash.com/s/photos/splitting-wood?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

我是一个好奇的人。这是我的天性。这就是为什么我小时候会拆解很多圣诞礼物，我想知道“为什么”。所以当我问这个问题时，“为什么我们在这个数据集上使用 80/20 的训练/测试分割？”而且得不到具体的答案，简直让我抓狂。我一头扎进了训练/测试分裂的“为什么”。可能有比我所能找到的更多的方法，但是我将在“interverse”中介绍几个训练/测试分离练习，看看它们如何达到标准，或者是否重要。

![](img/de77d7390c9adc3c1853c472e1ce35cb.png)

照片由[奥斯汀·迪斯特尔](https://unsplash.com/@austindistel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/80%2F20?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄

**帕累托原理**

帕累托法则也被称为 80/20 法则。总的来说，在大多数情况下，80%的结果来自 20%的原因。对于那些想进入这个兔子洞的人，请随意查看维基百科[。虽然该原则的序言是基于财富分配，但从统计学角度来看，它确实接近于解释许多人类、机器和环境现象。由于这个原因，并且通常在不知道来源的情况下，许多人使用 80/20 分割来进行训练和测试。](https://en.wikipedia.org/wiki/Pareto_principle)

![](img/5797cccf78ab71a0ae2db25ed30cff9e.png)

[Calum MacAulay](https://unsplash.com/@calum_mac?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 在 [Unsplash](https://unsplash.com/s/photos/scaling?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

**缩放定律**

1997 年，在一篇名为 [*的论文中讨论了一种新的方法——验证集训练集大小比*](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.33.1337&rep=rep1&type=pdf) *(Guyon)的标度律。*在这里，他们引用了*“*针对特定问题的最佳训练/验证分割:防止神经网络的过度训练。他们发现为验证集保留的模式部分应该与自由可调参数数量的平方根成反比。我们的结果推广并证实了他们的结果。”(Guyon，1997 年)。本质上，分裂是由数据集中有多少独特的特征(不包括目标)而不是观测值的数量决定的，这与大多数关于该主题的观点相反。

让我们用可靠的泰坦尼克号数据来看看标度律是否优于假设的帕累托分裂。该数据集已经被估算以填充来自前一个 post [预处理的空值:编码和 KNN 快速估算所有分类特征](/preprocessing-encode-and-knn-impute-all-categorical-features-fast-b05f50b4dfaa?source=your_stories_page---------------------------)。

首先，我们将加载数据，确保所有列都可见，并运行. head()方法来验证数据。

```
import pandas as pd
import numpy as np
from sklearn.model_selection import train_test_split
split_data = pd.read_csv('titanic_encoded_scaled-Copy1.csv')
pd.options.display.max_columns = None
split_data.head()
```

接下来，我们将去掉未命名的列，并将数据拆分为 X 和 y 变量。因为我们正在测试模型改进，所以最好使用多类目标，所以使用 deck1 列(7 个类)。

```
split_data = split_data.drop('Unnamed: 0', axis=1)
X = split_data.iloc[:,:-2]
y = split_data.iloc[:,-2]
```

在之前的另一篇文章中，我们发现将 PowerTransform scaler 设置为“yeo-johnson”方法时，该数据的缩放效果最好。如果您想一窥究竟，只需看一看:[预处理:标准化方法的差异](/preprocessing-differences-in-standardization-methods-de53d2525a87?source=your_stories_page---------------------------)

```
from sklearn.preprocessing import PowerTransformer
yj = PowerTransformer(method = 'yeo-johnson')
yj_data = yj.fit_transform(X)
```

现在，我们将使用 sklearn 库将我们的数据分成 train 和 test。一、帕累托原理(80/20):

```
#Pareto Principle Split
X_train, X_test, y_train, y_test = train_test_split(yj_data, y, test_size= 0.2, random_state= 123)
```

接下来，我们将运行该函数来应用比例法则，并将该数据拆分为不同的变量:

```
#discover scaling law split
columns = 14
test = 1/np.sqrt(columns)
train = 1 - test
print(test)
print(train)
#Scaling Law Split
A_train, A_test, b_train, b_test = train_test_split(yj_data, y, test_size= test, random_state= 123)0.2672612419124244 #test
0.7327387580875756 #train
```

帕累托定律和标度定律之间的差异几乎为 7%。现在运行两个数据集的标准逻辑回归模型:

```
#perform logistic regression using pareto split
from sklearn.linear_model import LogisticRegression
bn1 = LogisticRegression(max_iter=1000)
bn1.fit(X_train, y_train)
pp_preds = bn1.predict(X_test)# use logistic regression using scaling law split
bn2 = LogisticRegression(max_iter=1000)
bn2.fit(A_train, b_train)
sl_preds = bn2.predict(A_test)
```

以下是帕累托原则的分类报告:

```
#classification report from pareto split
from sklearn.metrics import classification_report
print(classification_report(y_test, pp_preds)) precision  recall   f1-score    support

         0.0       0.00      0.00      0.00         5
         1.0       0.38      0.33      0.36        15
         2.0       0.37      0.59      0.45        17
         3.0       0.38      0.16      0.22        19
         4.0       0.52      0.34      0.41        38
         5.0       0.67      0.87      0.76        69
         6.0       0.82      0.88      0.85        16

    accuracy                           0.59       179
   macro avg       0.45      0.45      0.44       179
weighted avg       0.55      0.59      0.55       179
```

相当不错的 59%的准确率。现在，比例定律报告:

```
#classification report from scaling law
print(classification_report(b_test, sl_preds)) precision    recall  f1-score   support

         0.0       0.50      0.20      0.29         5
         1.0       0.31      0.26      0.29        19
         2.0       0.35      0.52      0.42        21
         3.0       0.30      0.12      0.17        26
         4.0       0.61      0.47      0.53        53
         5.0       0.71      0.88      0.78        97
         6.0       0.84      0.89      0.86        18

    accuracy                           0.61       239
   macro avg       0.52      0.48      0.48       239
weighted avg       0.59      0.61      0.59       239
```

**准确率提高了 2%,精确度、召回率和 f1 得分也有所提高！**

**包装完毕**

在我看来，从全局来看，2%是一个相当大的增幅。当然，这是一个简单的多类逻辑回归模型，但是正如我所鼓励的，在你拥有的任何数据集上测试这两种分割方法。这真的是一个简单的算法，可以产生额外的差异。

和往常一样，你可以在 Github 上找到我的作品。这个特别的回购在这里是。祝你愉快！