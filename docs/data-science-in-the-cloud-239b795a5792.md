# 云中的数据科学

> 原文：<https://towardsdatascience.com/data-science-in-the-cloud-239b795a5792?source=collection_archive---------5----------------------->

## Azure vs AWS vs GCP

![](img/445328e1d3d41356e1a382199e958fef.png)

在 [Unsplash](https://unsplash.com/s/photos/code?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 上由 [Max Duzij](https://unsplash.com/@max_duz?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) 拍照

数据科学领域是多种多样的，如今在这个过程中涉及到许多不同的角色和职责。数据科学工作通常涉及处理非结构化数据、实施机器学习(ML)概念和技术、生成见解。这一过程通常以数据驱动的洞察力的可视化呈现结束。

机器学习是该过程的关键要素，但训练 ML 模型通常是一个耗时的过程，需要大量资源。过去，获取 ML 资源既困难又昂贵。今天，许多云计算供应商提供云中数据科学的资源。

本文回顾了 AWS、Azure 和 FCP 上的机器学习选项，以帮助您决定哪种资源满足您的 ML 需求。

# 云计算对数据科学的重要性

机器学习和深度学习模型的训练涉及成千上万次迭代。您需要这些大量的迭代来产生最精确的模型。例如，如果您有一组只有 1TB 数据的训练样本，该训练集的 10 次迭代将需要 10TB 的 I/O。当计算机视觉算法处理高分辨率图像时，输入数据集的大小非常大。您可以通过消除任何相关的网络延迟来减少处理时间。这可以帮助您确保读取源数据的最佳 I/O 性能。

云计算使您能够模拟存储容量和大规模处理负载，或者跨节点扩展处理。例如，AWS 提供具有 8–256 GB 内存容量的图形处理单元(GPU)实例。这些实例按小时定价。GPU 是专门为复杂图像处理而设计的处理器。Azure 为[高性能计算](https://cloud.netapp.com/hpc-file-services-on-azure-netapp-files)算法和应用提供 NC 系列高性能 GPU。

# AWS 机器学习服务和工具

亚马逊提供了几种机器学习工具和服务。这些服务使组织和开发人员能够提高计算密集型和高性能计算模型的性能。下面的列表回顾了其中的一些服务。

**亚马逊 SageMaker**

SageMaker 是一个完全托管的机器学习平台，面向数据科学家和开发人员。该平台运行在弹性计算云(EC2)上，使您能够构建机器学习模型、组织数据和扩展运营。SageMaker 上的机器学习应用包括语音识别、计算机视觉和推荐。

AWS 市场提供您使用的模型，而不是从零开始。然后，您可以开始训练和优化您的模型。最常见的选择是像 Keras、TensorFlow 和 PyTorch 这样的框架。SageMaker 可以自动优化和配置这些框架，或者您可以自己训练它们。您也可以通过在 Docker 容器中构建算法来开发自己的算法。你可以使用 Jupyter 笔记本来构建你的机器学习模型，并可视化你的数据。

**亚马逊 Lex**

Lex API 旨在将聊天机器人集成到应用程序中。Lex 包含基于深度学习的自然语言处理(NLP)和自动语音识别功能。

API 可以识别口头和书面文本。Lex 的用户界面(UI)使您能够将识别的输入嵌入到许多不同的后端解决方案中。除了独立的应用程序，Lex 还支持为 [Slack](https://docs.aws.amazon.com/lex/latest/dg/slack-bot-association.html) 、Facebook Messenger 和 Twilio 部署聊天机器人。

**亚马逊认知**

Rekognition 是一种计算机视觉服务，它简化了图像和视频识别应用程序的开发过程。Rekognition 使公司能够根据业务需求定制应用程序。Rekognition 的图像和视频识别功能包括:

*   **对象检测和分类** —使您能够在图像和视频中找到并识别不同的对象。例如，您可以检测正在跳舞的人或正在灭火的火。
*   **人脸识别** —用于人脸检测和匹配。例如，你可以用它来检测图像和视频中的名人面孔。
*   **面部分析** —用于分析面部表情。你可以检测微笑，分析眼睛，甚至定义视频中的情感情绪。
*   **不当场景检测** —使您能够确定图像或视频是否包含不当内容，如露骨的成人内容或暴力。

# Azure 机器学习服务和工具

与 AWS 相比，Azure 机器学习产品在开箱即用的算法方面更加灵活。Azure 机器学习产品可以分为两大类——Azure 机器学习服务和 Bot 服务。

**Azure 机器学习(Azure ML)服务**

Azure ML 是一个巨大的预训练、预打包的机器学习算法库。Azure ML 服务还提供了一个环境来实现这些算法，并将它们应用到现实世界的应用程序中。Azure ML 的 UI 使您能够构建结合多种算法的机器学习管道。您可以使用 UI 来训练、测试和评估模型。

Azure ML 还为人工智能(AI)提供解决方案。这包括可视化和其他可以帮助理解模型行为的数据，并比较算法以找到最佳选项。

Azure ML 服务产品包括:

*   **Python 包** —包含用于计算机视觉、文本分析、预测和硬件加速的函数和库。
*   **实验** —使你能够构建不同的模型，比较它们，将项目设置为特定的历史配置，并从那时起继续开发。
*   **模型管理** —提供一个环境来托管模型、管理版本和监控运行在 Azure 或内部的模型。
*   **工作台** —一个简单的命令行和桌面环境，带有仪表盘和模型开发跟踪工具。
*   **Visual Studio Tools for AI** —使您能够添加用于深度学习和其他人工智能项目的工具。

**Azure 服务机器人框架**

Azure Service Bot 提供了一个使用不同编程语言构建、部署和测试 Bot 的环境。Bot 服务不一定需要机器学习方法，因为微软提供了五个预定义的 bot 模板。这包括基本、形式、主动、语言理解和问答。只有语言理解模板需要先进的人工智能技术。

您可以使用 Node.js 和。NET 技术来用 Azure 构建机器人。你可以在 Skype、Bing、Office 365 电子邮件、Slack、Facebook Messenger、 [Twilio](https://docs.microsoft.com/en-us/azure/bot-service/bot-service-channel-connect-twilio?view=azure-bot-service-4.0) 和 Telegram 等服务上部署这些机器人。

# 谷歌云机器学习服务和工具

谷歌在两个层面上提供机器学习和人工智能服务——面向经验丰富的数据专业人士的谷歌云机器学习引擎和面向初学者的 Cloud AutoML 平台。

**谷歌云汽车**

为没有经验的用户构建的基于云的机器学习平台。您可以上传数据集、训练模型并将其部署到网站上。AutoML 集成了谷歌的所有服务，并将数据存储在云中。您可以通过 REST API 接口部署训练好的模型。

您可以通过图形界面访问许多可用的 AutoML 产品。这包括结构化数据、图像和视频处理服务的培训模型，以及自然语言处理和翻译引擎。

**谷歌云机器学习引擎**

Google Cloud ML 引擎使您能够大规模运行机器学习训练作业和预测。你可以使用谷歌云 ML 通过利用 GPU 和张量处理单元(TPU)基础设施的[来训练一个复杂的模型。您还可以使用该服务来部署外部培训的模型。](https://www.run.ai/guides/gpu-deep-learning/)

Cloud ML 自动执行所有监控和资源配置流程，以运行作业。除了托管和训练，Cloud ML 还可以执行影响预测准确性的超参数调整。如果没有超参数调整自动化，数据科学家需要手动试验多个值，同时评估结果的准确性。

**张量流**

TensorFlow 是一个开源软件库，使用数据流图进行数值运算。这些图中的数学运算由节点表示，而边表示从一个节点传输到另一个节点的数据。TensorFlow 中的数据表示为张量，即多维数组。TensorFlow 通常用于深度学习研究和实践。TensorFlow 是跨平台的。您可以在 GPU、CPU、TPU 和移动平台上运行它。

# 结论

您很容易迷失在云中各种可用的数据科学解决方案中。它们在算法、特性、定价和编程语言方面有所不同。此外，解决方案列表总是在变化。很有可能你会选择一个供应商，突然另一个供应商会发布更适合你的业务需求的产品。选择的时候，先搞清楚你想用机器学习达到什么目的，然后选择能帮助你完成目标的服务。