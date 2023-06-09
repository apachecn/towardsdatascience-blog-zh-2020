# 亚马逊 Sagemaker 上深度学习的一个非常简单的介绍

> 原文：<https://towardsdatascience.com/a-very-simple-introduction-to-deep-learning-on-amazon-sagemaker-b6ca2426275a?source=collection_archive---------17----------------------->

## 这里有一个非常简单的方法来开始在云中进行深度学习！

# 介绍

在本文中，我将引导您将数据加载到 S3，然后在 Amazon Sagemaker 上构建一个 Jupyter 笔记本实例来运行深度学习作业。

![](img/83c82805b6f269f7c3110c8039ac3225.png)

🇨🇭·克劳迪奥·施瓦茨| @purzlbaum 在 [Unsplash](https://unsplash.com/s/photos/easy?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片

我将要回顾的方法并不是在云中运行深度学习的唯一方法*(事实上它甚至不是推荐的方法)*。但是这个方法是一个很好的开始方式。

**优点:**

*   轻松过渡到云！比方说，我想在一台更大的机器上运行我已经建立的代码，或者我没有本地 GPU，我想在没有 Google Colab 超时的情况下运行一个更长的作业，那么这个方法应该允许您以更少的代码更改启动并运行 AWS！
*   一旦你掌握了这种方法，你就可以转向更强大的选项。

**CONS:**

*   目前，Sagemaker 没有针对笔记本实例的自动关机功能。为什么这很重要？好吧，假设我做一份培训工作，然后去看电影。当我回到家，我的笔记本\GPU 实例仍然在运行，即使作业在几个小时前就结束了。这样不好，因为我是为那个时间付费的(而且 GPU 也不便宜)。所以用这种方法，你基本上不能让你的机器处于无人监控的状态。

*边注:有一种使用“脚本模式”自动关机的方法，但是它需要一些额外的编码。这是一个你可以探索的选项，如果你愿意，你可以在这里* *阅读我关于脚本模式* [*的文章。*](/bring-your-tensorflow-training-to-aws-sagemaker-with-script-mode-aba9e73aa36b)

在我创建了一个 S3 桶和一个 Sagemaker 笔记本实例之后，我将向您介绍一些我编写并存储在 GitHub 上的示例代码。GitHub 上的笔记本遍历了如何在 S3 连接到您的数据，然后遍历了一些 hyperpt+tensor flow \ Keras 代码。在我的远视例子中，我正在为一个递归神经网络进行超参数搜索。

# 神经网络超参数调整动机

*(有一点需要注意，笔记本上没有提到的是，远视是在* ***负*** *精度上进行优化。***是重要的。Hyperopt 希望找到您的成本指标的最小值，在我的情况下就是准确性。所以用* ***负*** *精度找到精度最高的网络！)**

*好吧，如果你正在读这篇文章，那么你可能以前训练过神经网络。你甚至可能用 sklearn 来做神经网络随机搜索交叉验证，但是你想把它带到下一个层次。*

*首先，我推荐阅读下面这篇关于超参数调优的[文章。简而言之，随机搜索实际上做得很好，不需要运行大量的迭代。但是不管你是使用随机搜索还是贝叶斯方法，你都可能遇到以下问题…](https://www.kaggle.com/ilialar/hyperparameters-tunning-with-hyperopt)*

*1.神经网络上的超参数调整需要很长时间(即使使用 GPU)。*

*2.在任何免费培训平台上运行长时间的作业(例如 Google Colab，Kaggle)通常会超时。*

*现在，你做什么？*

*![](img/ae5e9d94cffdf159967b7a8f1545f6f2.png)*

*照片由[艾米丽·莫特](https://unsplash.com/@emilymorter?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)在 [Unsplash](https://unsplash.com/s/photos/question?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄*

*好吧，你有两个选择:*

*1.买一台带 GPU 的个人电脑*(这是要花钱的，大一点的会好一点)**

*2.在云上租一个 GPU*(也要花钱)**

*就我个人而言，我最终购买了一台带 GPU 的笔记本电脑，但在此之前，我尝试了云选项。拥有一个个人 GPU 是很棒的，但随着你的进步，你会发现自己需要更多的能力，无论如何你都会回到云中*(至少我是这么发现的)*。*

*好了，节目已经开始了，我们如何使用 Sagemaker 来建立我们的神经网络！*

# *第一步:进入 AWS 并创建一个帐户。*

*似乎是合乎逻辑的第一步。转到下面的链接，然后单击“创建 AWS 帐户”*(如果您还没有帐户)*。*

*[https://aws.amazon.com/](https://t.umblr.com/redirect?z=https%3A%2F%2Faws.amazon.com%2F&t=M2IzZjYyZDkxNjhjYWY2MjY4MWMzYmI1ZDJlM2QzMTkxOTZmMmFkYyxkYzdlZTQ0NTNmZDgxNmNjMTdiNWJlODAwNTNiN2U0MzllZTc3MDky&ts=1599344215)*

# *步骤 2:将数据保存到 S3*

*因此，此时您应该在管理控制台上。*

*接下来，点击“服务”，然后点击“S3”。*

*现在点击“创建存储桶”。*

*现在按照提示创建您的 bucket，给它命名，等等。确保你选择了你所在的地区。我在美国东海岸，所以对我来说，北弗吉尼亚的作品。*

*如果你像我一样，只是在玩 Sagemaker，并且不太关心权限*(因为存储的信息都不是敏感的)*那么你可以点击“下一页”进入第 2-4 页。*

*当你完成后，你应该有一个新的 S3 桶！现在点击你的 S3 桶名。*

*这应该带你到你的 S3 桶，你可以上传数据！点击“上传”,然后点击“添加数据”,从本地机器中选择您的数据，并按照提示进行操作。再说一次，我并不太关心权限，所以我只是在选择了我的数据后，点击了很多次“下一步”。*

*(*注:S3 是有代价的。因此，当您完成时，您可能希望删除您的数据集，甚至您的存储桶。)**

# *第三步:启动 Sagemaker 笔记本*

*返回“服务”并找到\点击“Sagemaker”。*

**(注意:我们将启动一个运行在 ml.p2.xlarge 上的笔记本实例，它有一个 GPU，成本大约为 1.20 美元/小时。当您完成培训后，请确保关闭笔记本实例。还要注意的是，这份工作是要花钱的！！)**

*[https://aws.amazon.com/sagemaker/pricing/](https://t.umblr.com/redirect?z=https%3A%2F%2Faws.amazon.com%2Fsagemaker%2Fpricing%2F&t=NDU1ZWIxMzNiZjY1MmQ2OTM0OTY3MDM5ZjE5ZDFiZWU0YjRiOGRmMiw0MzY5MTFiYTQ5MWY5MWJhOGJhY2UzODE4MThlZjZiYzQxMDI4Mjhk&ts=1599344215)*

*单击笔记本实例>“创建笔记本实例”*

*现在，我们将为笔记本命名，并确保选择一个 ml.p2.xlarge 来获取一个 GPU 实例。*

*你可能必须通过一些权限，如果你像我一样，你可以绕过很多这种。*(我在这里不打算涉及这些)*。此外，如果您像我一样，在访问 GPU 时可能会遇到一些问题，在这种情况下，只需通过“支持”下拉菜单联系支持人员，并提交专门针对 GPU 实例的配额增加。当 AWS 完成您的配额增加后，您必须返回“创建笔记本实例”并重新开始。*

*一旦您完成了“创建笔记本实例”步骤，笔记本实例现在将被创建。这可能需要一些时间…*

*![](img/f9734433e97cb428a5b74c7e84788cc5.png)*

*迈克·肯尼利在 [Unsplash](https://unsplash.com/s/photos/coffee?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上拍摄的照片*

*创建实例后，您应该能够单击“打开 Jupyter ”,这将带您进入运行在新 GPU 实例\机器上的 Jupyter！*

*Jupyter 打开后，单击“新建”下拉菜单并选择“conda_tensorflow_36”，创建一个新的“conda_tensorflow_36”笔记本。*

# *第四步:运行一些代码！*

*现在，您可以在 GitHub 上查看我的完整笔记本，其中包括如何连接到您的数据、安装 hyperopt 以及运行您的作业的注释！查看完整的 GitHub repo 与笔记本[此处](https://github.com/yeamusic21/Hyperopt_On_Sagemaker)。*

# *第五步:全部关闭！*

*完成后，记得通过单击您的笔记本实例名称，然后单击“停止”来关闭您的笔记本实例。我甚至建议删除笔记本实例，以及重新访问您的 S3 存储桶并删除您的存储桶，否则将所有这些工作放在亚马逊上会让您损失金钱！*

# *结束了！*

*谢谢大家，希望这对你有所帮助。快乐学习！:-D*

# ***其他资源\参考资料:***

*【https://github.com/hyperopt/hyperopt *

*[https://hyperopt.github.io/hyperopt/](https://t.umblr.com/redirect?z=https%3A%2F%2Fhyperopt.github.io%2Fhyperopt%2F&t=NDE5MDMzNjk0Yzk4YzgwMTExZTI5Yjk0NGUzMDliZDE0YWJlZDkxYSxmMjQ2ZDkxYmU0M2RiNWI1MGM5MjBlMjA4NWVjODZmMTY2MDYxZmNl&ts=1599344215)*

*[https://sci kit-learn . org/stable/modules/generated/sk learn . model _ selection。RandomizedSearchCV.html](https://t.umblr.com/redirect?z=https%3A%2F%2Fscikit-learn.org%2Fstable%2Fmodules%2Fgenerated%2Fsklearn.model_selection.RandomizedSearchCV.html&t=NDFjZDlmOGMxYjUzNWRkMzg1OTA3ODk5NTU2ZTIyZWM1ODYwZWQyMiw0MzRhZjI1OWE1Mjk4ZWU1ZGE4Y2FmNzVkY2YyNTExYjY3MjdlZGRj&ts=1599344215)*

*[https://aws.amazon.com/](https://t.umblr.com/redirect?z=https%3A%2F%2Faws.amazon.com%2F&t=M2IzZjYyZDkxNjhjYWY2MjY4MWMzYmI1ZDJlM2QzMTkxOTZmMmFkYyxkYzdlZTQ0NTNmZDgxNmNjMTdiNWJlODAwNTNiN2U0MzllZTc3MDky&ts=1599344215)*

*[https://blog . cloud ability . com/AWS-S3-了解-云存储-节省成本/](https://t.umblr.com/redirect?z=https%3A%2F%2Fblog.cloudability.com%2Faws-s3-understanding-cloud-storage-costs-to-save%2F&t=MmZhYWVhODBkNTk1ZGY5ODBhZTA3MDVlMGM5ZTJiYTMyZTYyZjBkNyxjMDcyNzdkY2ZhNDllNTE4YzFjMmNhNTY4ZjMzZjAzYjk5NDE2NDU1&ts=1599344215)*

*[https://github . com/yea music 21/Hyperopt _ On _ sage maker/blob/master/Hyperas _ mjy _ v1 _ 3 . ipynb](https://t.umblr.com/redirect?z=https%3A%2F%2Fgithub.com%2Fyeamusic21%2FHyperopt_On_Sagemaker%2Fblob%2Fmaster%2FHyperas_mjy_v1_3.ipynb&t=N2YzYjljZTMyOTE2NjdmMjI4NzI2ZWZhZGM2Yzc1NjM4NmY3MWM5NCxlY2UyYWViYTA2ZTNlYzQ1MWRhMTEzMTMxZjQ5YmJkYWIxMDE0ODNl&ts=1599344215)*