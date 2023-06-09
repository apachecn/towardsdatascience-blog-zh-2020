# 机器学习技巧:处理不平衡数据集

> 原文：<https://towardsdatascience.com/machine-learning-tips-handling-imbalanced-datasets-328422ef3054?source=collection_archive---------61----------------------->

## 处理数据不平衡的不同方法

![](img/beea93474f7b870b90dc38199c45ead3.png)

菲德尔·费尔南多在 [Unsplash](https://unsplash.com/s/photos/scale?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

假设您有一项任务，要创建一个模型来检测欺诈性的信用卡交易。提供给你的数据集包含 100 万笔交易，但其中只有 3 万笔被标记为欺诈，这使得数据集**不平衡**。这是欺诈检测任务类别的典型比例。否则，我们会有更严重的问题要解决。

数据不平衡通常是分类问题中的一个问题，它表示类别分布不均匀。如果这是一个二元分类问题，我们可能有 95%的 A 类和 5%的 b 类。如果分类模型是在不平衡的数据集上训练的，它将高度偏向主导类。因此，该模型将反映潜在的类别分布。为了有一个准确的模型，我们需要解决不平衡问题。作为解决方案，有不同的使用方法。

在本帖中，我们将讨论和解释最常用的方法，并提及适用于不平衡数据集的评估指标。

# **重采样**

重采样可以有两种不同的形式，欠采样和过采样。

**欠采样**仅从多数类中选择一些观察值(行)来匹配少数类中的观察值数量。

让我们看一个例子。我将使用 kaggle 上的[信用卡欺诈检测数据集](https://www.google.com/search?q=credit+card+fraud+detection+dataset&oq=cre&aqs=chrome.0.69i59j0j69i57j0j69i60l3j69i65.1516j0j7&sourceid=chrome&ie=UTF-8)。我们首先将数据集读入熊猫数据帧。

```
import numpy as np
import pandas as pddf = pd.read_csv("/content/creditcard.csv")df.Class.value_counts()
0    284315 
1       492
```

有 492 笔交易被标记为欺诈，近 285，000 笔交易不是欺诈。让我们想象一下“类别”列:

```
#data visuzalization libraries
import matplotlib.pyplot as plt
import seaborn as sns
sns.set(style='darkgrid')
%matplotlib inlineplt.figure(figsize=(8,5))
plt.title('Credit Card Transactions')
sns.countplot('Class', data=df)
```

![](img/b2bceae40f99d7ac4df762e1cbd52eac.png)

欺诈(1)交易的数量如此之少，以至于我们甚至无法在图上看到。在这种情况下，我们可以通过随机选择 492 个观察值(少数类中的观察值数量)对多数类(0)进行**欠采样。**

```
df = df.sample(frac=1, random_state=42)
fraud = df[df.Class == 1]
nonfraud = df[df.Class == 0].sample(n=492, random_state=32)
df_new = pd.concat([fraud, nonfraud])df_new.Class.value_counts()
1    492 
0    492 
Name: Class, dtype: int64
```

我们执行的步骤:

*   使用 **sample** 函数混洗整个数据集，并通过过滤数据帧来分离类。
*   使用样本函数随机选择 492 行非原始数据帧。
*   用 **concat** 功能合并两个数据帧。

最后，我们有一个等类分布的欠采样数据帧。

![](img/3b360b6435318ecec499a60d1090cb44.png)

**过采样**是欠采样的反义词。我们使用少数类的观察值生成合成数据。过采样过程比欠采样稍微复杂一点。当生成新的观察值时，我们需要保持在少数类的特征空间内。例如，如果一个特征的范围在 10 到 30 之间，那么对于一个合成样本来说，该特征具有 100 是没有意义的。

有不同的过采样技术。其中最常见的是 **SMOTE** (合成少数过采样技术)。SMOTE 算法根据已有的样本创建新的样本。它需要两个或更多相似的观察值，并通过一次改变一个属性来创建一个综合观察值。变化量是随机的，但会将新观测值保持在所用现有观测值的相邻距离内。在不平衡学习库中可以找到 [SMOTE](https://imbalanced-learn.readthedocs.io/en/stable/generated/imblearn.over_sampling.SMOTE.html) 的实现。

# **等级权重**

一般来说，分类模型对每个类别的权重是相等的。因此，每一个错误分类的观察结果都会导致不同类别的等量损失(不考虑概率)。但是，我们可以改变类的权重，使得少数类中观察值的错误分类超过多数类的错误分类。

大多数机器学习模型都有一个名为 **class_weight** 的参数来调整权重。我们只需要通过字典来确定权重。

```
from sklearn.linear_model import LogisticRegressionweights = {0:1, 1:10}
lr = LogisticRegression(class_weight = weights)
```

我们创建了一个逻辑回归模型，负类和正类的类权重分别为 1 和 10。在这种情况下，当一个正类被错误分类时，该模型比错误分类一个负类的情况受到更多的惩罚。

# **不平衡数据集的评估指标**

不平衡的数据集需要特殊的评估指标。仅仅使用准确性并不能提供彻底的评估。假设我们正在创建一个模型，对一个具有不平衡类分布的数据集执行二元分类。93%的数据点属于负类，7%属于正类。如果一个模型只预测负类，它将达到 93%的准确率，这是非常好的。然而，它只是反映了类分布，而不是学习观察值之间的关系。这种情况被称为**准确性悖论。**

如果正确地检测阳性类别是至关重要的，并且我们不能对它们中的任何一个进行错误分类(即癌症预测)，该怎么办？在这些情况下，我们需要其他指标来评估我们的模型。

**混淆矩阵**

混淆矩阵不是评估模型的指标，但它提供了对预测的洞察。学习混淆矩阵对于理解其他分类度量是很重要的，例如精确度和召回率。

混淆矩阵通过显示每个类别的正确和错误(即真或假)预测，比分类准确性更深入。在二进制分类任务的情况下，混淆矩阵是 2×2 矩阵。如果有三个不同的类，那就是一个 3x3 的矩阵，以此类推。

![](img/1c7199b6294809337b5881b087a44ab3.png)

假设 A 类是正类，B 类是负类。混淆矩阵的关键术语如下:

*   **真阳性(TP)** :预测阳性类别为阳性(ok)
*   **假阳性(FP)** :将阴性类别预测为阳性(不正常)
*   **假阴性(FN)** :预测阳性类别为阴性(不正常)
*   **真阴性(TN)** :预测阴性类为阴性(ok)

混淆矩阵用于计算精度和召回率。

**精度和召回**

精确度和召回率度量将分类准确性向前推进了一步，并允许我们获得对模型评估的更具体的理解。选择哪一个取决于任务和我们的目标。

> **精度**表示有多少正面预测是正确的。

![](img/fe63228841f8b29bb85649a53e28596d.png)

精度的焦点是**正面预测**。

> **Recall** 表示所有肯定类别中有多少被正确预测。

![](img/aaa080263688c8c57515695709978b92.png)

召回的重点是**实际正班**。

我们不能试图同时最大化精确度和召回率，因为它们之间有一个平衡。提高精度会降低召回率，反之亦然。我们可以根据任务来最大化精确度或回忆。对于垃圾邮件检测模型，我们试图最大限度地提高精确度，因为我们希望在电子邮件被检测为垃圾邮件时是正确的。我们不想将一封普通的电子邮件标记为垃圾邮件(即误报)。另一方面，对于肿瘤检测任务，我们需要最大化召回率，因为我们希望尽可能多地检测到阳性类别。

还有一个将精确度和召回率结合成一个数字的方法，那就是 F1 分数。

**F1 得分**

F1 分数是精确度和召回率的加权平均值。

![](img/f9c118ceaaa93f715e0ecfc578958110.png)

对于类别分布不均匀的问题，F1 分数是比准确度更有用的度量，因为它考虑了假阳性和假阴性。

f1 得分的最佳值是 1，最差值是 0。

**卡帕(科恩的卡帕)**

Kappa 是通过考虑类别不平衡而归一化的分类精度。

感谢您的阅读。如果您有任何反馈，请告诉我。