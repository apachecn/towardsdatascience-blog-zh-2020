# 超负荷相似性度量计算

> 原文：<https://towardsdatascience.com/super-charged-similarity-metric-calculations-969116abd948?source=collection_archive---------17----------------------->

## 采用 NumPy 和 TensorFlow

![](img/6135981c0f9b9ed43b6515f2c8642f67.png)

乔·内里克在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

相似性检测是一种常用的方法，用于识别具有共同特征但不一定具有相同特征的项目。产品推荐和相关文章通常由相似性度量驱动。余弦相似性是最受欢迎的，将在这里讨论。本文将使用 NumPy 和 TensorFlow 评估 Python 中余弦相似性的性能。

## NumPy 和张量流

NumPy 是一个健壮而成熟的库，用于处理大型多维矩阵。NumPy 拥有丰富的线性代数函数集合。调得很好，在 CPU 上运行速度非常快。

TensorFlow 是一个数学和机器学习库，可以利用 CPU 和 GPU。TensorFlow 已经在生产中得到很好的证明，并用于支持高级机器学习算法。它还拥有丰富的线性代数函数集合。你用 NumPy 能做的大部分事情，在 TensorFlow 里也能做。

两者都是很棒的库，都可以计算数据集之间的相似性度量。

## **计算余弦相似度**

如果 NumPy 和 TensorFlow 尚未安装，可以通过 pip 安装。本文使用的是 NumPy 1.17.4 和 TensorFlow 2.1

```
pip install numpy
pip install tensorflow
```

以下示例代码显示了如何在 NumPy 和 TensorFlow 中计算余弦相似性。

NumPy 和张量流余弦相似性

运行上面的代码将产生类似下面的输出。还会有很多 TensorFlow 消息，重要的是你要看到顶行是粗体的，以确保 GPU 正在被使用。

```
**I tensorflow/core/common_runtime/gpu/gpu_device.cc:1555] Found device 0 with properties:**x: 
 [[0.16522373 0.55317429 0.61327354 0.74017118 0.54443702]
 [0.46154321 0.17925365 0.3785271  0.71921798 0.91126758]
 [0.10342192 0.96612358 0.06434406 0.85482426 0.7329657 ]
 [0.1333734  0.99817565 0.42731489 0.46437847 0.40758545]
 [0.43727089 0.91457894 0.21971166 0.24664127 0.61568784]]
y: 
 [[0.15979143 0.47441621 0.20148356 0.99541121 0.41767036]]np: 
 [[0.91509268]
 [0.83738509]
 [0.91553484]
 [0.80027872]
 [0.7071257 ]]
tf: 
 [[0.91509268]
 [0.83738509]
 [0.91553484]
 [0.80027872]
 [0.7071257 ]]
```

最上面的两个数组显示了 x 的 5x5 数组和 y 的 1x5 数组。它还显示了 y 相对于 x 中每一行的余弦相似性，这是用 NumPy 和 TensorFlow 计算的。

让我们试着用更多的数据来计算时间。

## 小型阵列的性能

对于第一个测试，我们将尝试两个小数组，计算 x 的 1000x25 数组和 y 的 50x25 数组之间的余弦相似性。

小型数据阵列的时序

运行上面的代码将产生以下输出:

```
np time = 0.2509448528289795
tf time = 0.7871346473693848
similarity output equal: True
```

在这种情况下，NumPy 比 TensorFlow 快，即使 TensorFlow 启用了 GPU。与所有软件开发一样，没有一种尺寸可以满足所有问题的答案。NumPy 仍然有一席之地，它在处理小数据时会表现得更好。

将数据从 CPU 复制到 GPU 会产生开销，构建要执行的 GPU 图形也会产生开销。随着数据的增长，开销与总体运行时间相比可以忽略不计，让我们尝试更大的数据阵列。

## 大型阵列的性能

我们将运行与上面几乎完全相同的代码，除了我们将增加数组的大小。

```
x = np.random.rand(10000, 25)
y = np.random.rand(50, 25)
```

对于这个测试，我们将对 x 使用 10000x25 数组，对 y 使用 50x25 数组。

```
np time = 3.3217058181762695
tf time = 1.129739761352539
similarity output equal: True
```

TensorFlow 现在比 NumPy 快 3 倍。将数据复制到 GPU 并编译 GPU 图形的开销现在值得在性能上进行权衡。

让我们尝试一个更大的数组。

```
x = np.random.rand(25000, 100)
y = np.random.rand(50, 100)
```

对于这个测试，我们将对 x 使用 25000x25 的数组，对 y 使用 50x100 的数组。

```
np time = 23.823707103729248
tf time = 2.93641996383667
similarity output equal: True
```

在这种情况下，TensorFlow 快了 8 倍。只要数据集能够适合 GPU，性能增益将继续快速增长。

## 选择前 N 个索引

计算余弦相似度将得到一个从 0 到 1 的浮点数组，1 表示最相似，0 表示最不相似。对于大多数用例，您需要计算相似性以及最佳关联记录。在 NumPy 和 TensorFlow 中都可以这样做，如下所示。

余弦相似度和最佳匹配选择

上面的代码获得了一个按照最高余弦相似度排序的索引列表。选择并打印最上面的记录。

## 结论

NumPy 和 TensorFlow 都有自己的位置。GPU 不只是在所有情况下都让一切变得更快。对较小的数据集使用 NumPy，对较大的数据集使用 TensorFlow。始终根据您自己的数据进行测试，看看在您的特定情况下什么最有效。