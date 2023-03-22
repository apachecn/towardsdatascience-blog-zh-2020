# 预测查询与监督 ML 模型

> 原文：<https://towardsdatascience.com/predictive-queries-vs-supervised-ml-models-ee7f17e4840e?source=collection_archive---------35----------------------->

## 未来预测查询会取代有监督的机器学习模型吗？

![](img/86d56a53d7aa19c6c8b40412e4c66e52.png)

超过 4 个数据集的精度基准。本文比较了预测查询和监督 ML 模型的工作流程、架构和缩放/准确性。图像源 Aito

当今科技领域最大的趋势之一是[机器学习的民主化](http://knowledge.wharton.upenn.edu/article/democratization-ai-means-tech-innovMIT%E2%80%99sation/)。因为商品最先进的模型，更好的工具和更好的硬件:机器学习正在成为[公司工具箱中的日常工具](/why-every-company-will-have-machine-learning-engineers-soon-b7bc515a53b4)。

ML 民主化仍然是一个持续的趋势，鉴于这一领域的混乱，值得问一问:这一转变将把我们带向何方？未来的日常管理会是什么样子？

预测查询是机器学习的一种有趣的方式，尤其是在 ML 民主化的背景下。像[麻省理工学院的](http://probcomp.csail.mit.edu/) [BayesLite](https://github.com/probcomp/bayeslite) 和 [Aito](https://aito.ai/) 这样的解决方案提供了一种使用类似 SQL 的查询立即获得任意预测的方法。例如，Aito 中有一个预测查询:

```
{
  "from": "invoice_data",
  "where": {
    "Item_Description": "Packaging design",
    "Vendor_Code": "VENDOR-1676"
  },
  "predict": "Product_Category"
}
```

因此:预测查询似乎是一种更容易、更快、完全不同的机器学习方式。它们让我们看到了未来，任何人都可以像查询数据库一样轻松地进行机器学习。

本文简要介绍了预测查询，并从三个不同方面对预测查询和监督学习进行了比较:

1.  工作流，比较预测查询和监督机器学习之间的容易程度和成本
2.  该架构比较了使用预测查询和使用监督模型之间的高级差异
3.  质量是一项新兴的、有前途的技术的一个明显的关注点。

# 预测查询简介

预测查询类似于普通的数据库查询，除了它们提供关于未知的*的预测，而传统的数据库查询提供关于已知的*的事实。下面是一个针对 [BayesLite](https://github.com/probcomp/bayeslite) 数据库的 [BQL](http://probcomp.csail.mit.edu/dev/bayesdb/doc/bql.html) (贝叶斯查询语言)查询示例:

![](img/501191ef48af96d8dd5474da55babd40.png)

BayesLite 中的预测性 BayesQL 查询。BayesQL 基于 sQL，它提供了一种非常优雅的方式来查询任意估计值。该查询可以在创建群体、创建分析、初始化分析和分析操作之后执行。图片来源:Aito

本质上，预测查询可以为监督 ML 模型提供非常类似 SQL 的替代方案，主要区别在于:

1.  虽然受监督的机器学习模型需要在使用前进行配置、训练和部署，但预测查询可以在数据库准备好数据后提供即时答案。因此:预测查询具有不同的工作流程。
2.  虽然监督机器学习总是专门用于从 A 到 B 的单个预测，但是预测查询可以用于 A)基于任何已知的 Y 即时预测任何未知的 X，以及 B)还提供推荐、智能搜索和模式挖掘。因此，监督模型是狭窄的，而预测查询是多用途的，这对架构有影响。
3.  当有监督的机器学习时，*窄*模型被显式地形成训练时间，预测查询在查询时间期间做*多用途*建模*或*窄*建模。因此:预测查询在技术上更具挑战性。*

只有很少的解决方案提供这种预测查询。一个是提到的 BayesLite，它在一个特殊的准备阶段创建了一个内存中的多用途模型。另一个解决方案是 Aito.ai，它在没有显式准备的情况下进行查询时窄建模。这是 Aito 工作流程的一个例子。

![](img/ddfc65b522803cd36275826634fc52a6.png)

*Aito 中 3 步预测查询。数据上传到数据库后，可以立即运行预测查询。对于像 Titanic 这样的小数据集，预测通常需要几毫秒(图中可见的 187 毫秒延迟是由网络 ping 爱尔兰引起的)。图片来源:Aito*

我们将以下比较集中在 Aito 上。我们认为这种关注是合理的，因为在 Aito，我们更熟悉该解决方案，并且它足够成熟，可以在实际生产环境中为最终客户服务。虽然 BayesLite 非常令人印象深刻，他们的 BQL 界面和 DB/ML 集成值得羡慕:BayesLite 似乎有一些属性，如简单数据的 16 分钟准备阶段，这与提出的论点不一致。

因此，接下来让我们更深入地挖掘预测查询和监督 ML 模型之间在工作流、架构和质量方面的差异。

# 1.工作流程

预测查询和传统监督模型之间的第一个区别与工作流程和成本有关。

受监督的 ML 模型通常部署在数据科学项目中，这些项目有几个步骤，如移交给数据科学家、数据准备、特征工程、模型拟合、部署、集成、再培训以及监控和维护。作为这种线性进展的补充，您通常还会有一个迭代阶段，在此阶段，通过细化数据、准备、特性、模型、部署或集成来改进结果。

![](img/545e6bbdb3b9c0fb4f592c64cc54dd6b.png)

数据科学项目的简化版本。关于这些项目的更多信息可以在网上广泛获得。图片来源:Aito

一个人或两个人可能需要几个星期或几个月的时间将一个监督模型投入生产。这可以将每个型号的价格提高到 10 万欧元。如果你需要几个模型，你需要几个数据科学项目，导致成倍的费用和延迟。

现在，如果您使用预测查询来实现机器学习功能，这个过程会发生相当大的变化。对于预测查询，工作流本质上如下:

1.  准备一次辅助预测数据库(如果它不用作主数据库)
2.  用评估请求验证足够好预测质量
3.  像集成 SQL 查询一样集成预测查询
4.  编写测试/评估案例，将它们推给 Git，让 CI 处理回归测试
5.  如果认为有必要:通过分析跟踪生产预测质量，并在产品仪表板中显示指标。

![](img/ffc18ef984a1f2714ec9458e51820f6a.png)

预测查询的工作流程类似于数据库查询的工作流程。然而，由于预测功能是统计性的，其行为可能会随着数据的变化而变化:建议在实施之前验证预测质量(步骤 2)，并在生产中监控预测质量(步骤 5)。图片来源:Aito

虽然将辅助数据库(如 ElasticSearch)投入生产可能需要数周时间，但将每个查询投入生产的相关费用更接近于使用搜索/数据库查询的费用。这种查询通常只占相关功能费用的一小部分，而基于查询的功能通常可以在几小时内实现，几天内投入生产。

工作流程和费用之间的这种巨大差异可以解释为:a)预测数据库的 AutoML 功能被专用数据库加速；b)由于数据和 ML 已经集成到单个系统中，部署和集成的需求减少。数据科学项目的复杂阶段被系统地消除或简化:

1.  不需要将数据科学项目移交给数据科学家，因为预测查询工作流对于软件开发人员来说已经足够简单。
2.  数据准备和特征工程步骤可以通过 ML-数据库集成大大减少。如果数据已经在数据库中，您不需要重新准备和重新上传数据。如果您可以通过数据库引用进行[推理，那么您不需要手动将数据聚合到平面数据框架中。您也不需要手动特征化文本，因为预测数据库](https://aito.ai/docs/articles/utilizing-relationships-in-aito/)[会像 ElasticSearch 一样自动分析文本](https://aito.ai/docs/api/#schema-analyzer)。最后:如果数据库有内置的[特征学习能力](https://aito.ai/blog/introducing-concept-learning-to-free-you-from-feature-engineering/)，你就不需要管理特征冗余。
3.  建模阶段可以通过一个复杂的模型实现自动化，这个模型可以为大多数应用程序提供足够好的结果。
4.  对于每个模型云部署，模型的实时集成和重新训练完全消失了，因为您不需要“部署”或重新训练预测查询。相反，你可以像集成 [ElasticSearch](https://www.elastic.co/) 一样集成一个辅助预测数据库。如果您使用预测数据库作为您的主数据库，您甚至可以省略那个集成。
5.  维护更容易，因为您不用为每个预测目标维护已部署的基础设施，而是像使用 Git & CI 维护代码一样维护类似 SQL 的查询。

因此，通过预测查询实现 ML 的工作流程和成本与通过 SQL 实现普通业务逻辑的过程相似。

# 2.建筑

预测查询和监督模型之间的第二个区别是狭窄性及其对软件架构的影响。

众所周知:受监督的 ML 模型在两个不同方面*狭窄*:

1.  预测设置的狭窄性。监督学习模型本质上是从 A(例如文本)到 B(类别)的狭窄函数，这意味着如果你有 10 个不同的问题，你最终会有 10 个不同的监督 ML 模型。
2.  预测功能类型的狭窄性。一种监督方法通常只能用于一种预测。因此，你经常需要完全独立的系统或产品来实现预测、推荐、智能搜索和模式挖掘。

这种组合的狭窄对架构有负面影响。如果你有 10 种不同的预测功能，混合了预测、推荐和智能搜索用例:你最终会陷入一个非常复杂的系统。该系统可以包括具有半打部署模型的单独的监督模型平台、单独的推荐系统、单独的智能搜索产品和单独的模式挖掘工具。这种复杂性很难学习、掌握和维护。智能搜索和基于内容的推荐引擎经常复制数据库的大部分，这导致了冗余。系统也可能不能很好地相互集成，并且它们可能以不一致的状态结束，其中智能搜索可能返回旧的信息，并且推荐和预测可能忽略新产品和数据。

![](img/15723539dbedc29560bc07cf87c63904.png)

监督模型的狭窄性推动了额外的部署和集成，因为每个预测模型通常需要单独的服务器用于模型特定的 API 和数据集成。每个外部服务通常通过单独的集成服务器集成。这扩大了维护的基础设施和复杂性。图片来源:Aito

另一方面，可以认为预测查询本质上是多用途的，并且在两个方面都不狭窄。首先:预测查询没有固定的预测设置，它们不需要针对 10 个不同的问题进行 10 个单独的模型部署。10 个问题可能需要 10 个预测查询，这是一个明显的优势:虽然创建和维护 10 个不同的监督 ML 模型可能很难，但大多数软件工程项目在创建、理解和维护数十甚至数百个 SQL 查询方面并不费力。

第二，关于预测类型的狭窄性:对于预测数据库，多用途的性质自然地从这种系统中不可避免的设计选择中显现出来。在某种程度上，它的出现与传统数据库中出现多用途的原因是一样的:数据库无法预先知道查询，因此从设计上来说，它必须准备好服务于任何通用需求。这使得设计选择通常是通用的，而不是特定的。

作为一个不太明显但不可避免的设计选择:教科书中的贝叶斯/概率方法最适合快速统计计算，这使得预测数据库成为可能。这在 BayesLite 和 Bayesian Aito 中都很明显。与此同时，如此坚实的数学基础很容易进一步推广，以创建一个多用途的预测系统，这在这两个系统中都很明显。BayesLite 和 Aito 都提供广泛的智能功能组合。

![](img/e913ad4ea128f080181d498a670dac77.png)

预测数据库本质上是多用途的。Aito [查询 API](https://aito.ai/docs/api/#query-api) 提供[预测](https://aito.ai/docs/api/#post-api-v1-predict)、[推荐](https://aito.ai/docs/api/#post-api-v1-recommend)、[匹配](https://aito.ai/docs/api/#post-api-v1-match)(例如从职位到候选人)和[统计关系发现](https://aito.ai/docs/api/#post-api-v1-relate)作为对[基本查询](https://aito.ai/docs/api/#post-api-v1-search)和[全文搜索(FTS)](https://en.wikipedia.org/wiki/Full-text_search) 功能的补充。推荐可以与全文搜索相结合，以提供个性化的搜索。预测、匹配和推荐查询也可以作为普通查询执行[，](https://aito.ai/docs/api/#post-api-v1-query)其中结果按[概率](https://aito.ai/docs/api/#schema-plain-probability)排序。图片来源:Aito

在 Aito 的例子中，贝叶斯数学被推广，不仅服务于预测，还服务于建议。因为[搜索](https://en.wikipedia.org/wiki/Information_retrieval)数学是基于贝叶斯[二元独立模型](https://en.wikipedia.org/wiki/Binary_Independence_Model)和预测数据库需要索引所有文本以发挥作用:扩展贝叶斯 Aito 以服务于传统搜索，匹配和个性化搜索用例是很自然的。同样，使用教科书数学来使[可解释的人工智能](https://en.wikipedia.org/wiki/Explainable_artificial_intelligence)变得极其简单。向一个需要快速模式挖掘才能正常运行的系统添加模式挖掘支持几乎是不可避免的。另一方面:BayesLite 通过广泛的分析能力、SQLite 广泛的数据库功能和令人印象深刻的生成数据的能力补充了 Aito 的功能组合。

因此，类似地，对于已知数据，数据库是非常多用途和通用的，对于未知数据，预测数据库也是非常多用途和通用的。现在，如果您将传统数据库和预测数据库功能结合起来，您将创建更多用途的系统，可以灵活地服务于所有知识相关的需求，包括已知和未知的需求。

![](img/c724524b0a42369b64a3cc188bd970de.png)

在预测方法中，1)客户端 API 集成、2)预测服务器和 3)每模型数据集成被 a)单个预测查询请求和 b)预测数据库的一次性集成所取代。该方法更符合行业最佳实践，如 [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) 、[可重用性](https://en.wikipedia.org/wiki/Reusability)，避免了 [NIH](https://en.wikipedia.org/wiki/Not_invented_here) 和[用代码](https://en.wikipedia.org/wiki/Serverless_computing)替换基础设施。图片来源:Aito

对于单个应用程序的结果是:也许您只需要一个预测数据库来满足您的所有需求。你得到查询，自然语言搜索，预测，推荐，智能搜索等。从单一来源。不需要额外的服务器部署、定制模型或数据集成，因为一切都由单个数据库提供。冗余、一致性和互操作性问题也消失了，因为所有功能都基于相同的事务数据。

面向预测查询的架构也更符合行业最佳实践。用查询替换预测服务器有助于用查询/代码替换基础设施，如在[无服务器计算](https://en.wikipedia.org/wiki/Serverless_computing)和[中将围绕数据(在数据库中)的关注点](https://en.wikipedia.org/wiki/Separation_of_concerns)与查询/代码(在 Git 中)分开。用单个集成替换多个冗余数据集成符合 [DRY 原则](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)，并且该方法允许[重用](https://en.wikipedia.org/wiki/Reusability)旧的数据集成。使用现成的解决方案通常比创建定制的解决方案更可取，以避免[重新发明轮子](https://en.wikipedia.org/wiki/Reinventing_the_wheel)和[不是在这里发明的](https://en.wikipedia.org/wiki/Not_invented_here) [反模式](https://en.wikipedia.org/wiki/Anti-pattern#Software_engineering)。总的来说，这种方法减少了需要维护的代码、基础设施和复杂性的数量，并且与良好的旧[软件架构](http://en.wikipedia.org/wiki/Software_architect)目标和原则相一致。

![](img/d8d3f582fb31e6d28c9cd896fe263905.png)

监督 ML 模型和预测查询之间的简化架构比较。图片来源:Aito

因此，面向预测查询/数据库的方法是对传统方法的彻底背离，对行业具有广泛的影响。就像一个思考游戏:如果您有一个可以回答已知和未知查询的数据库:为什么您要另外维护一个单独的普通数据库或者部署大量冗余的 ML 模型/系统？

# 3.质量

在人工智能的早期，你可以看到人们设想一个类似预测数据库的系统。一个愿景是 [McCarthy](https://en.wikipedia.org/wiki/John_McCarthy_(computer_scientist)) 对[的认识论部分](http://jmc.stanford.edu/articles/epistemological/epistemological.pdf)的想法，它将以无缝的方式将机器学习、知识表示和推理结合起来。这个认识论部分本质上是一个世界模型，它可以用来查询已知和未知，就像预测数据库一样。尽管如此，这个愿景从未完全实现，原因很明显:创建一个基于查询的统计推理系统在算法和性能方面都极具挑战性。

最基本的问题是预测总是需要一个模型，但是如果你事先不知道预测的细节，你就有三个相当具有挑战性的选择:

1.  “世界模型”，您可以在其中创建一个通用模型，为任意查询提供服务。这里的问题是很难创建一个通用的 ML 模型来服务任意的预测，如果你不想降低写/准备的性能就更难了。
2.  “特别模型”，您可以当场为每个查询训练一个单独的监督模型。这里的挑战是，在不降低查询延迟和吞吐量的情况下，创建高质量的模型查询时间是非常困难的。
3.  第三个也是直觉上最合理的选择是将这两种方法结合起来，因为这不仅可以提供最佳的结果，还可以提供最佳的写入和查询速度。从负面来看，它还结合了前两种方法的挑战。

BayesLite 是“世界模式”方法的一个很好的例子。它在额外的“创建群体”、“创建分析”和“分析”步骤中创建了一个内存通用模型。虽然这种方法很优雅，但是即使数据集有限，建模步骤也可能需要 10 分钟以上，这很好地说明了写入/准备时间方面的牺牲。不过，通过使用更专业的数据库(BayesLite 基于 SQLite)和不同的算法(查询时间[表示学习](https://aito.ai/blog/introducing-concept-learning-to-free-you-from-feature-engineering/)可以像在 Aito 中一样加速到毫秒级，这意味着快速的写时准备也应该是可能的)，准备速度可能会大大提高。

另一方面，Aito 使用“特定模型”方法，在这种方法中，性能损失发生在查询时。接下来，我将重点介绍我们如何利用这种方法解决一些固有的性能挑战。

![](img/27ce44a69ad33b8d9cbe8d9b4014ab26.png)

Aito 的统计推理管道。Aito 为每个预测查询执行[特征选择](https://en.wikipedia.org/wiki/Feature_selection)、[特征学习](https://en.wikipedia.org/wiki/Feature_learning)和[贝叶斯推理](https://en.wikipedia.org/wiki/Bayesian_inference)步骤。一种基于 [MDL 的](https://en.wikipedia.org/wiki/Minimum_description_length)表示学习技术创造了“[概念学习](https://aito.ai/blog/introducing-concept-learning-to-free-you-from-feature-engineering/)”用于特征学习，它为贝叶斯推理提供了[独立的](https://en.wikipedia.org/wiki/Independence_(probability_theory))高级特征。图片来源:Aito。

实质上，为特定查询创建“特定模型”通常需要:1)针对数百个查询特定特征的温暖且快速的数据结构；2)几千个相关统计测量；以及 3)每个感兴趣特征/检查的几千个相关样本。为了满足毫秒级的这些需求，Aito 1)为每个可能的特性快速准备了数据结构，2)使用专门的索引来计算微秒级的完整数据库统计数据，3)使用专门的数据结构来实现亚毫秒级的数据采样。

因此:预测性查询通常可以在毫秒级提供服务，如图 1 所示。您可以在本笔记本中找到关于基准的更多信息。

![](img/5af1ed63023a77d005221ed3a3744e31.png)

**图一。**根据 7 个平均词或 31 个平均词(在高端笔记本电脑上测量)预测二进制值或预测 128 个备选项的分类值时的 Aito 性能。根据查询的规模，可用于推理的文本特征的数量在 10k 和 1.5M 之间。**注意对数刻度**。 *Benchmark 的 Jupyter 笔记本和更多信息可从* [这里](https://colab.research.google.com/github/AitoDotAI/aito-benchmark-notebook/blob/master/speed.ipynb)获得。图片来源:Aito

虽然大多数预测可以以较低的延迟提供服务:因为 Aito 当前使用完整的数据库统计信息，所以 Aito 的伸缩有一个 O(N)组件。这意味着一旦你开始接近百万个数据点:性能就会下降。此外，查询中已知功能的数量和预测类别中备选功能的数量会影响性能，如图所示。

目前，这些性能特征对 Aito 的可能用途造成了一定的限制，因为大数据集和复杂推理可能会影响延迟和吞吐量。然而，值得注意的是，受监督的机器学习性能和资源需求也经常在百万样本规模或例如基准 SVM 实现的 10k 样本规模中开始下降。Aito 查询性能对于数据集有限、延迟和吞吐量要求不严格的应用程序来说也是绰绰有余，例如公司内部工具、PoCs/MVP、后台流程、智能流程自动化和 [RPA](https://en.wikipedia.org/wiki/Robotic_process_automation) 。

虽然性能质量对于许多用途来说已经足够好了，但我们确实希望它在未来会更好。对更加专门化的数据库结构的早期实验表明，写速度和采样速度仍然可以提高 10-50 倍。这可以让预测数据库具有 a)与搜索数据库相当(或更好)的写性能，b)更好的缩放，因为基于采样的推理缩放更像 O(1)而不是 O(N ),以及 c)大大提高的预测速度。在未来，通过进行写入时间特征/表示学习来集成“世界模型”方法可以使预测速度更接近我们在传统监督学习中看到的速度，但写入性能会有所下降。

最后，但同样重要的是:让我们考虑预测质量。在[基准测试](https://colab.research.google.com/github/AitoDotAI/aito-benchmark-notebook/blob/master/accuracy.ipynb)中，我们将 Aito 与 7 ML 模型进行了比较，包括 4 个不同分类数据集上的随机森林和离散数据(Aito 不做回归)。

![](img/118c855b2d9978df088a2a21f1c55f57.png)

**图二。** Aito 基准测试超过 4 个数据集和 8 种算法( [RF](https://en.wikipedia.org/wiki/Random_forest) 、 [CART](https://en.wikipedia.org/wiki/Decision_tree_learning) 、 [AITO](http://aito.ai) 、 [LDA](https://en.wikipedia.org/wiki/Linear_discriminant_analysis) 、 [LR](https://en.wikipedia.org/wiki/Linear_regression) 、 [KNN](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm) 、 [NB](https://en.wikipedia.org/wiki/Naive_Bayes_classifier) 、 [SVM](https://en.wikipedia.org/wiki/Support_vector_machine) )。你可以在这里找到基准代码[](https://colab.research.google.com/github/AitoDotAI/aito-benchmark-notebook/blob/master/accuracy.ipynb)**。图片来源:Aito**

*正如我们在基准测试中看到的那样，尽管训练预测模型的预算是毫秒级的，但临时模型方法产生了非常好的预测质量。*

*创建一个毫秒级的好的即席模型是可行的，因为创建一个特定的模型来为特定的预测服务比创建一个通用的模型来为通用的预测服务要快得多。如前所述，训练阶段不需要考虑每百万个特征和每百万个可用样本，而只需要考虑与查询相关的几百个特征和几千个样本。降低的复杂性和专用的数据库使得能够立即服务于适度复杂的特定于查询的模型。*

*临时模型也可能出奇地好，因为该模型针对单个预测进行了微调。当预测必须基于稀有特征时，传统的监督模型可能丢弃稀有特征并忽略数据中的稀有模式以限制模型的复杂性，这成为一个问题。有了预测查询，问题就简单地消失了，因为查询时间训练允许选择最适合每个单独查询的特征和模型细节。*

*同样值得注意的是，数据库包含大量的元数据。公司 ID 可以指整个公司表，其元数据可以通过贝叶斯先验用于预测。还有一些数据库友好的机制，如类推(已经在 Aito 中实现了)，它可以假设像('消息有 Bob '，'接收者是 Bob ')和('消息有 John '，'接收者是 John ')这样的关系具有共享的结构('消息有 X '，'接收者是 X ')和共享的统计行为。这种技术可以通过利用传统方法无法获得的数据和模式来改进预测。*

*这都提出了一个问题:通过各种技术，预测查询不仅可以达到奇偶性，而且在许多实际应用中可以达到比最佳监督 ML 模型更好的性能吗？*

# *结论*

*因此，预测查询可以通过以下方式颠覆机器学习领域…*

1.  *…用类似于数据库查询相关工作流的更快的工作流取代昂贵的监督式 ML 工作流…*
2.  *…用一个多用途系统和类似 SQL 的查询取代狭窄的监督模型和产品的复杂性…*
3.  *…同时保持与监督学习相比具有竞争力的性能和预测质量。*

*作为这 3 个因素的结果:可以想象，在未来的现实世界应用中，预测查询将取代大多数监督 ML 模型。这是一个简单的思维体验所暗示的:如果你可以从数据库中即时获得预测:你为什么要花数周时间生产和集成冗余的监督模型？*

*此外，可以想象，预测查询/数据库将成为机器学习民主化的主要驱动力。就像思想实验一样:如果做 ML 就像数据库查询，那么为什么没有开发人员能做 ML 呢？还有:如果基于 ML 的功能成本变得类似于基于数据库的功能成本，为什么 ML 不能像数据库一样用于每个公司、每个项目和每个功能中？*