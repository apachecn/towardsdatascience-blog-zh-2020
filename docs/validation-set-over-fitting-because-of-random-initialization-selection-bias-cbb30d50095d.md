# 由于随机初始化和选择偏差，验证集过度拟合

> 原文：<https://towardsdatascience.com/validation-set-over-fitting-because-of-random-initialization-selection-bias-cbb30d50095d?source=collection_archive---------23----------------------->

## “提前停止”真的能保证 AI 模型泛化吗？

![](img/b2ad0937a8007a554e14e1fcd13cb71b.png)

hawk 的标志:AI，我在这里担任首席数据科学家，感谢同事们的不断支持。

深度学习模型被称为通用函数逼近器。他们的优势来自于他们对给定的输入和输出之间的关系进行建模的强大能力。然而，这也是他们对问题提出一般化解决方案的主要弱点，也是他们如此倾向于过度适应(记忆)训练集而不使用新数据的原因。目前确保深度学习模型泛化的方法是简单地使用验证集来决定为训练模型应该进行多少次迭代(时期);或者换句话说，提前停止。然后，数据科学家将在盲测试集上测试训练的模型，以确保没有训练超参数也是过度拟合的。到目前为止，这种方法在处理这样的问题时效果很好，在这些问题中，你可以有这样的独立数据集，每个数据集都有相似的分布。然而，对于金融或医疗保健(这两个领域我都有很深的经验)中的一些问题来说，情况并非如此，对于强化学习问题来说当然也是如此，在强化学习问题中，新数据既依赖于环境，也依赖于行动。

## 早期停止经常失败的关键场景示例！

在医疗保健中，部署的模型对每个看不见的患者进行概括是极其重要的，这些患者既不会出现在训练集中，也不会出现在测试集中。由于这个原因，通常的做法是用留一个受试者出来交叉验证来验证模型，其中每个留一个受试者将是不同的，并试图基于每个折叠的统计来决定早期停止时期；这在人口众多的情况下是可以接受的。在金融领域，情况甚至更糟，因为人们需要对未来数据进行归纳；同时，股票市场数据的分布总是变化的，几乎不可能有如此同质的训练、验证和测试集。一些定量分析师训练人工智能模型进行交易，尽管他们在实验期间的回溯测试中表现很好，但他们在真实数据中往往表现不佳。最后，大多数强化学习方法都有再现性问题(特别是当使用不同的随机种子时)，而像增强随机搜索这样的无梯度方法在这些方法中表现得更好。最后，相同模型的集合(甚至)通常会产生更好的结果。

## 良好的验证性能并不是概括的指标！

深度学习模型(迭代机器学习模型)的持续学习也是一场噩梦，需要同样的验证。事实上，如果使用相同数量的历元用相同大小的新数据集从头开始重新训练，人们永远无法确保深度学习模型在泛化方面收敛到相同或更好的解决方案。简直是一团糟！经过多年训练模型的经验，我已经确定了这种情况的主要原因是验证集过度拟合。由于任何机器学习模型都是随机初始化的，它们可以收敛到局部最小值，这在使用验证集时表现很好，如果你在这一点上提前停止训练，模型的泛化能力将低于最优解。对于我作为例子给出的问题，没有办法通过检查验证集来确保这种情况不会发生。我发现了一种仅通过使用训练集来检测过度拟合的好方法，即跨许多小批量检查模型性能。由于该模型在过拟合期间会失去其泛化能力，当试图学习其他模型时，它会在某些小批量中表现更差，因此在训练期间损失的变化会在它们之间波动。

## “基于群体”的持续再平衡投资组合选择！

最近，我在研究投资组合选择(优化)问题时遇到了这个问题，我终于发现了一个解决方案，它可能适用于其他领域。我发明了一种方法，我将其命名为“基于群体的常数再平衡投资组合选择”。对于这种方法，我使用 PyTorch 中的自动签名功能在 GPU 中同时优化 8192 个投资组合。然后，我使用前 50%投资组合的平均权重来检查验证集的性能，而不是从正在训练的投资组合权重中选择一个候选。(当它们都用于取平均值时，该方法收敛到类似的结果，并且使用前 50%只是加速了训练过程。)总之，结果证明我能够获得平滑的训练和验证曲线，我能够使用该曲线来确定没有随机初始化偏差的早期停止时期。这种方法的另一个有趣的可能用途是同时进化的对抗例子，用于攻击深度学习模型。与现有的进化优化方法的主要区别在于，在所提出的方法中，每个候选项被独立地优化。关于该方法的进一步细节如下:

关于提议的“基于群体”的常数再平衡投资组合选择方法的陈述。

## 文献中现有的投资组合选择方法已经过时了！

以前的投资组合选择方法只解决了最优购买和持有投资组合的选择，但没有帮助选择一个不断再平衡的投资组合。同时，一个最小波动率常数再平衡投资组合，当简单持有时没有正回报，也可以由于均值回复而产生利润。因此，我更倾向于在交易成本(1%)之下，为给定的交易政策(如 UCRP)和风险调整后的回报选择一个最佳投资组合。此外，用于决定何时重新平衡回所选恒定投资组合的散度阈值也与投资组合权重一起被优化。据我所知，这也是第一个投资组合选择方法，通过模拟策略来优化投资组合以及定义的交易策略的参数。奖励函数作为有效前沿优化的替代。

## 80%胜率和 20 倍盈亏比的战略源代码

总之，这种方法使我能够为给定的交易策略(在这种情况下是常数再平衡投资组合)找到通用的投资组合权重和参数，并定义风险敏感的回报函数。事实上，我已经能够优化这样一个交易策略，在 QuantConnect 进行的样本外回溯测试中，它能够实现 80%的胜率和 20 倍的盈亏比。为了展示这种方法的优势，我在下面的链接中分享了这种策略的源代码；这样任何人都可以自己复制结果。请注意，即使在训练集上也很难找到这样的策略。最后，我期待其他研究人员为我在本文中定义的问题开发更多的解决方案；我希望它能引发更多高质量的研究来解决人工智能中的这个严重问题。

[](https://www.quantconnect.com/terminal/processCache?request=embedded_backtest_dfc0fa7d17e0029e9a7dee3483fe8b7c.html) [## 基于群体选择的交易策略源代码

### 在基于群体的常数再平衡投资组合选择的策略参数的优化过程中，不利用该回测期。

www.quantconnect.com](https://www.quantconnect.com/terminal/processCache?request=embedded_backtest_dfc0fa7d17e0029e9a7dee3483fe8b7c.html) 

## 感谢阅读！作者(我)的简短自动传记:

我是一名前院士(T-Labs，微软研究院)和企业家(OTA 专家，客厅)，他改革了工作中的帕金森病治疗(ConnectedLife ),同时入侵了国内的股票市场。我以前在著名的研究机构工作过，包括微软剑桥研究院计算机媒介生活实验室的社会数字系统(人类体验和设计)组和德国电信创新实验室(T-Labs)的质量和可用性组。我领导了几个关于深度学习、机器学习、模式识别、数据挖掘、人机交互、信息检索、人工智能、计算机视觉和计算机图形学的研究项目；并在许多会议和期刊上合作发表了 35 篇论文。我目前在 hawk:AI 从事金融科技领域的工作，担任首席数据科学家。