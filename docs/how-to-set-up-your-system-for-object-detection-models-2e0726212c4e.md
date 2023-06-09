# 如何为对象检测模型设置您的系统

> 原文：<https://towardsdatascience.com/how-to-set-up-your-system-for-object-detection-models-2e0726212c4e?source=collection_archive---------15----------------------->

## 你应该从头开始，第一次尝试就把它做好

![](img/d0d78be92aedf6255f7c041877ca5491.png)

戴维·克洛德在 [Unsplash](https://unsplash.com/s/photos/structured-approach?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上的照片

计算机视觉是当今人工智能的一个热门领域。目标检测是计算机视觉中的一项特殊任务。它帮助机器在没有人眼帮助的情况下识别一组特定的对象。许多应用，如受保护区域中用于监视的人脸检测、商店中的脚步计数、通过跟踪来估计车辆速度的物体检测、制造业中的产品故障检测等。—正在使用物体探测技术。

在不同的社交媒体上，我看到许多机器学习爱好者正在尝试不同的对象检测技术，并分享他们的结果。

不知何故，我对应用这些物体检测技术有点怀疑。我对深度学习算法的基础和一般机器学习问题、NLP 和计算机视觉的方法有一个相当好的想法。我也做过一些基于文本的模型。但是由于一些未知的原因，计算机视觉总是排斥我。

在我的职业生涯中，我一直避免从事与愿景相关的项目。我曾经把它传给我的同事。但我做不了多久。当我不能再避免它的时候，一种情况出现了。我必须做一些与特定上下文相关的对象检测任务。所以我决定试一试。

起初，我不确定从哪里开始。我做了大量的网络搜索和阅读来寻找合适的材料来指导我。我意识到有很多关于物体检测的文章，但是大多数都不完整。由于对我来说这是一个新的领域，而且我有时间限制，我需要关于程序的每一步的详细指导，我还需要一个快速实施模型的策略。

我找到了一些不错的文章——Medium，Analytics Vidya，Machine Learning Mastery 等。但是当我要实现它的时候，我面临着许多与系统设置和模型执行相关的挑战。

我面对不同的错误信息，我无法理解。花了几天时间才找出这些错误的原因。最后，我知道你需要列出一个需求清单，并遵循一个循序渐进的方法来在这个旅程中取得成功。

在本文中，我将讨论首次尝试成功实现对象检测模型所需的策略。

# 在开始安装之前了解要求

有两种方法来建立对象检测模型。您可以实现现有的模型架构。这需要更少的时间，并且您可以从其他实现中获得指导。此外，您还可以从名为迁移学习的方法中受益，该方法使用以前构建的模型的权重，并根据当前上下文重新训练模型。

另一种方法是从头构建一个模型。训练模型需要更多的时间和资源。但是它给了你更大的控制权。

我决定使用现有的模型架构，并根据我手头的任务对其进行重新训练。我选择了掩膜 RCNN 模型进行物体检测。我在 Medium 和 Machine-Learning-mastering 中找到了一些关于其基本原理和实现的文章。

我有一台装有 Windows 10 和 4GB NVIDIA GEFORCE GTX 1650 GPU 的笔记本电脑。为了训练它完成我的任务，我需要设置 GPU，还需要安装 jupyter notebook 来访问它。

从[这里](http://How%20to%20Install%20Tensorflow-GPU%20version%20with%20Jupyter%20%28Windows%2010%29%20in%208%20easy%20steps.)找到一篇关于设置 GPU 的美文。在克服了一些障碍之后，我已经能够做到了。指南有点旧了。一些命令不起作用。我设法把它们换成了新的。

我的下一个任务是实现这个模型。我打算实现一个端到端的现有对象检测模型，这样我就可以快速适应我的新用例。

我跟随文章从[来到这里](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)。我做了所有必要的步骤——下载了 Mask RCNN git 存储库([这里是](https://github.com/matterport/Mask_RCNN))，下载了图像及其注释文件，导入了必要的包，以及所需的文件。但是，当我开始训练给定数据的模型时，我陷入了困境。

我遇到了一个与 TensorFlow 相关的错误—“*ModuleNotFoundError:没有名为‘tensor flow . contrib’*的模块。”我尝试了网络上的不同方法来修复它。但是我不能。他们每个人都把我引向另一个错误。

花了几天时间才明白成功实施的秘密。**您需要同步您为对象检测任务安装的软件包和软件的版本。它从设置 GPU 开始，适用于您在整个项目中安装的每个软件包。**

是包版本把事情搞砸了。对我来说，它是 TensorFlow 的版本。TensorFlow 的当前版本是 2.3.0。Mask RCNN 模型架构是为 TensorFlow 版本 1.14 或更早版本构建的。没有意识到这一点，我继续安装所有软件包的所有最新版本，包括 TensorFlow，除非特别提到。

意识到(在许多不成功的尝试之后)TensorFlow 版本导致了麻烦，我决定卸载所有东西并重新开始。

我再次从安装 GPU 和适当版本的 TensorFlow 开始。这一次成功了。我仍然面临一些 python 包的问题。但我知道解决方法。我根据发布日期匹配了包的版本。

我再也不用担心兼容性问题了。我可以完全专注于建立我的模型。

在开始构建任何对象检测模型之前，您可以按照以下步骤收集设置系统所需的所有信息。

1.  做一些阅读，找出你想要使用哪个模型(深度学习框架)来进行对象检测。在文献中，有大量的标准架构用于对象检测任务。RCNN，更快的 RCNN，掩膜 RCNN，YOLO，RetinaNet 等。是广泛使用的算法。
2.  找到您选择的算法的 git 存储库，并找到它的实现。
3.  在存储库中搜索实现的系统需求。
4.  确定算法支持的 TensorFlow-GPU 版本(如果模型使用 TensorFlow)。
5.  有关 TensorFlow 版本，请查看 python 的兼容版本。
6.  找到适合 TensorFlow 版本的 CUDA 版本。
7.  查找适用于 CUDA 的兼容 Visual Studio 版本
8.  找到 CUDA 版本各自的 cuDNN 包。
9.  搜索适用于 CUDA 实现的 Visual Studio 版本。
10.  搜索其他 python 包的版本，如——numpy、scikit-learn、opencv-python、keras 等。您应该选择存储库中提到的这些包的版本。如果没有特别提到它们，请使用在创建存储库时发布的包版本。

如果你正确地收集了所有这些信息，你就为旅程的第二阶段做好了准备。

# 遵循安装顺序

如果您已经收集了关于需求的所有信息，您就可以开始一个接一个地安装它们了。设置系统时，请遵循以下顺序。

## 1.可视化工作室

下载您选择的 CUDA 版本所需的 Visual Studio 版本。对于遮罩 RCNN，我需要 Tensorflow 1.14。与 Tensorflow 1.14 兼容的 CUDA 版本是 CUDA 10。在此[链接](https://www.tensorflow.org/install/source_windows)中找到与 TensorFlow 和 CUDA 版本相关的信息。

现在，CUDA 版本需要特定版本的 Visual Studio 和适当的 Visual C++编译器。我的情况是 Visual Studio 2017 有 Visual C++ 15.0 编译器。使用此[链接](https://my.visualstudio.com/Downloads?q=visual%20studio%202017&wt.mc_id=o~msft~vscom~older-downloads)获得合适的版本。

## 2.蟒蛇

从[这里](https://www.anaconda.com/products/individual)安装 Python 3.x 版本的 Anaconda。它将帮助您创建一个由 tensorflow-gpu 支持的虚拟环境。在这种环境下，你会推出 jupyter 笔记本。

## 3.库达

从[这里](https://developer.nvidia.com/cuda-downloads?target_os=Windows&target_arch=x86_64&target_version=10&target_type=exelocal)下载安装 CUDA。我不得不下载 CUDA 10(旧版本)。从[这里](https://medium.com/@viveksingh.heritage/how-to-install-tensorflow-gpu-version-with-jupyter-windows-10-in-8-easy-steps-8797547028a4)遵循 CUDA 的确切安装程序(除了 CUDA 版本)。CUDA 版本应该与您的 TensorFlow 版本兼容。

## 4.cuDNN

你的 cuDNN 版本必须符合你的 CUDA 版本。跟随这个[链接](https://developer.nvidia.com/rdp/cudnn-archive)找到合适的版本。只好下载了 cuDNN 7.4(老版本)。此处给出了 cuDNN 安装和设置环境变量的详细步骤[。](https://medium.com/@viveksingh.heritage/how-to-install-tensorflow-gpu-version-with-jupyter-windows-10-in-8-easy-steps-8797547028a4)

## 5.张量流

您需要使用 Anaconda 提示符创建一个环境来安装 TensorFlow。选择与您的模型兼容的支持 GPU 的 TensorFlow。从这里的[开始按照步骤](https://medium.com/@viveksingh.heritage/how-to-install-tensorflow-gpu-version-with-jupyter-windows-10-in-8-easy-steps-8797547028a4)进行操作。

安装 TensorFlow 后，应该检查一下是否可以访问 GPU。由于版本更改，上面链接中提到的代码片段不起作用。使用以下脚本来检查相同的情况。它将显示可用的计算资源。

```
from tensorflow.python.client import device_lib
print(device_lib.list_local_devices())
```

## 6.Jupyter 笔记本

是时候在您的环境中安装 jupyter 笔记本了。遵循此处给出的[指示。现在，您已经准备好探索对象检测模型了。](https://medium.com/@viveksingh.heritage/how-to-install-tensorflow-gpu-version-with-jupyter-windows-10-in-8-easy-steps-8797547028a4)

## 7.模型

下载要用于对象检测任务的模型。您需要从 git 存储库中克隆它。我用了面膜 RCNN。所以我使用下面的命令下载并安装了它。你可以在这里找到掩码 RCNN 模型[的实现。](https://github.com/matterport/Mask_RCNN)

```
# To clone the Model
!git clone https://github.com/matterport/Mask_RCNN.git 
# To change directory to the installation folder
cd Mask_RCNN
# To install the model
!python setup.py install
# To confirm the installation
pip show mask-rcnn
```

## 8.Python 包

现在，您可以下载构建模型所需的其他 python 包。在 Mask RCNN 库中有一个需求列表。它包含该实现所需的所有必需的包。不过，它没有提到所有软件包的版本。

为了避免进一步的版本冲突，我安装了所有必需的软件包和所需的版本。

```
pip install scikit-image==0.14.2
pip install Keras==2.2.4
pip install scipy==1.2.1
pip install Pillow==7.2.0
pip install Cython==0.29.6
pip install scikit-image==0.14.2
pip install opencv-python==3.4.5.20
pip install imgaug==0.2.8
pip install h5py==2.10.0
```

现在，您的 jupyter 笔记本已经准备好进行所有安装。你再也不用考虑兼容性问题了。您可以将全部精力用于训练和推断您想要建立的对象检测模型。

计算机视觉是人工智能的一个专门领域。解决计算机视觉问题的方法与通常的机器学习方法有点不同..我写这篇文章是为了帮助数据科学新手深入研究对象检测模型。这也将有助于像我这样的专业人士，他们以前从未尝试过物体检测任务。我以 Mask RCNN 为例来展示这个过程。我的意图是在开始任何目标探测任务之前，提出一种结构化的方法来配置系统。

## 附录:(一些问题和有用的链接)

1.  如果你用 cudnn64_7.dll 在 Windows 上构建时遇到“*导入错误”，请点击此[链接。](https://github.com/tensorflow/tensorflow/issues/28223)*
2.  如果您遇到“*导入错误:导入 win32api 时 DLL 加载失败:系统找不到指定的文件。*”，跟着这个[环节](https://github.com/xlwings/xlwings/issues/1174)。
3.  如果你面对“内核错误 win32api”，按照这个[链接](https://github.com/jupyter/notebook/issues/4980)。
4.  你可以在这里找到一个很好的对象检测模型[的实现。](https://www.analyticsvidhya.com/blog/2018/11/implementation-faster-r-cnn-python-object-detection/)

5.模型实现的另一个漂亮演示是这里的。

谢谢你的时间。如果你喜欢这篇文章，你可能会喜欢我的其他文章。这是其中之一。

[](https://medium.com/swlh/how-to-learn-new-programming-language-with-no-books-and-tutorials-862e8cf77d8f) [## 没有书籍和教程如何学习新的编程语言

### 经过检验的快速学习方法

medium.com](https://medium.com/swlh/how-to-learn-new-programming-language-with-no-books-and-tutorials-862e8cf77d8f)