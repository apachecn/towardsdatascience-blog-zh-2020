# 探索 CDI 数据集中糖尿病、高血压和高胆固醇之间的关系

> 原文：<https://towardsdatascience.com/exploring-the-relationship-between-diabetes-high-blood-pressure-and-high-cholesterol-in-the-cdi-16f15fc80b73?source=collection_archive---------62----------------------->

## 使用数据分析和统计

我的[上一篇文章](https://medium.com/@zainab.haider/exploring-gender-and-ethnicity-differences-in-diabetes-health-outcomes-from-the-cdi-dataset-1bc95da826ac)讨论了糖尿病带各州糖尿病患病率和糖尿病相关死亡率的性别和种族差异。这些数据来自 [CDC 的慢性病指标(CDI):糖尿病数据集](https://chronicdata.cdc.gov/Chronic-Disease-Indicators/U-S-Chronic-Disease-Indicators-Diabetes/f8ti-h92k)，它提供了 2010 年至 2018 年所有州和地区的糖尿病相关信息的汇编。

在本文中，我想使用 CDI 糖尿病数据集的数据来探讨糖尿病与其共病(高血压和高胆固醇)之间的关系。就像糖尿病一样，这两种共病是心脏病的已知风险因素。我想看看在糖尿病带诊断为糖尿病的成人中，一种共病是否比另一种更普遍。我还想了解在糖尿病带中诊断为糖尿病的成年人中，高血压患病率和高胆固醇患病率是否存在性别偏见。

这种探索性数据分析是在 Jupyter Notebook/Python 中完成的。用于生成本文中使用的这些可视化和统计测试的代码已经发布到 GitHub [这里](https://github.com/zainabhaider/CDI-Project/blob/master/EDA%20Diabetes%20and%20Comorbidities%20-%20CDI%20Diabetes%20.ipynb)。

巴克等人在 2011 年描述的糖尿病带包括“阿拉巴马州、阿肯色州、佛罗里达州、佐治亚州、肯塔基州、路易斯安那州、北卡罗来纳州、俄亥俄州、宾夕法尼亚州、南卡罗来纳州、田纳西州、德克萨斯州、弗吉尼亚州和西弗吉尼亚州……密西西比州。”在我的上一篇文章中，我关注的是这些州的子集，因为这些州比美国其他州受糖尿病的影响更大，因此可以进行更有针对性的分析。在本文中，我将继续分析这些数据，并仅针对构成糖尿病带的州得出结论。

在开始之前，我想提供一些关于这个主题的技术背景。高血压、高胆固醇和糖尿病都是心脏病的危险因素。高血压意味着血管中的血流量增加，使心脏工作更多，心脏变弱(美国心脏协会，2016)。高水平的胆固醇(体内发现的一种脂肪)会阻塞血液流动。如果血管被胆固醇堵塞，它们就会变得狭窄，需要更高的血压来保持血液流动，最终削弱心脏，增加心脏病的可能性。因此，研究这些共病的患病率对人群健康研究很重要。

与上一篇文章类似，我将继续分析 2017 年的数据，因为这是可用数据中最近的一年。

首先，我想看看糖尿病共病的总体患病率:高血压和高胆固醇。

![](img/91f736f22e8c4692b49d88d2ffabd236.png)

2017 年糖尿病共病患病率。来源:我自己的数据分析。

从上图可以看出，在诊断为糖尿病的成年人中，高血压的患病率高于高胆固醇的患病率。统计测试证实两者之间存在显著差异:

*   使用独立的 t 检验来确定在诊断为糖尿病的成人中高血压患病率和高胆固醇患病率之间是否存在统计学显著差异。使用 Levene 方差相等性检验(p > 0.05)，满足正态性(p > 0.05)和方差齐性假设。对于确诊为糖尿病的成年人，**高血压患病率** (M = 65.81，SD = 4.81)，**明显高于高胆固醇患病率** (M = 56.31，SD = 4.37)，p = 0.00 < 0.05。

这一观察结果与 CDC 的《2020 年国家糖尿病统计报告》的数据相吻合，该报告指出，2013 年至 2016 年，68.4%的诊断为糖尿病的成年人患有高血压(血压> 140/90)，或目前正在接受高血压药物治疗，43.5%的人胆固醇水平高(LDL 胆固醇> 130 mg/dl)。糖尿病带和美国的高血压患病率相似。然而，糖尿病带的高胆固醇患病率高于美国。与美国其他地区相比，高胆固醇患病率的增加可归因于糖尿病带中诊断为糖尿病的成年人密度的增加。

接下来，我想看看被诊断为糖尿病的成年人中高血压患病率和高胆固醇患病率之间的性别差异。

![](img/3a7634bc4fb4a1581b002cdc66bc19e6.png)

2017 年诊断为糖尿病的成年人中高血压的患病率

从诊断为糖尿病的成年人中高血压的患病率开始，我可以看到男性和女性成年人的患病率相似。两组之间没有显著差异，这一点通过统计检验是显而易见的:

*   使用独立的 t 检验来确定男性和女性成人高血压患病率之间是否存在统计学显著差异。使用 Levene 方差相等性检验(p > 0.05)，满足正态性(p > 0.05)和方差齐性假设。**男性** (M = 67.64，SD = 4.90) **和女性** (M = 64.24，SD = 7.15)，高血压患病率无显著差异，p = 0.15 > 0.05。

![](img/30782abea806eb97b75f251c77712c1a.png)

2017 年诊断为糖尿病的成年人中高胆固醇的患病率

上述诊断为糖尿病的成年人中高胆固醇患病率的图表显示，男性和女性成年人具有相似的高胆固醇患病率。统计测试证实了这一点:

*   使用独立的 t 检验来确定男性和女性成年人的高胆固醇患病率之间是否存在统计学显著差异。使用 Levene 方差相等性检验(p > 0.05)，满足正态性(p > 0.05)和方差齐性假设。**男性** (M = 58.41，SD = 9.00) **和女性** (M = 56.13，SD = 5.36)，高胆固醇患病率无显著差异，p = 0.42 > 0.05。

CDI 糖尿病数据集还包括种族数据；然而，由于缺少大量数据，我没有考虑种族在共病患病率中的作用。黑人(非西班牙裔)和西班牙裔人口的数据缺失太多，我无法做出有意义的见解。尽管如此，我还是很想知道在糖尿病共病的种族差异方面做了哪些研究。根据 Walker 等人(2016)的研究，与其他族裔群体相比，黑人(非西班牙裔)个体“始终表现出最低的血压控制率”。在黑人(非西班牙裔)的血脂控制中也发现了类似的趋势(Walker 等人，2016)。在我之前的文章中，一项种族差异分析显示，黑人(非西班牙裔)在整个糖尿病带中具有最高的糖尿病患病率和糖尿病相关死亡率。黑人(非西班牙人)受糖尿病的影响很大；由此可见，他们也会受到糖尿病共病的严重影响。

在我的上一篇文章中，我讨论了数据的局限性。同样的限制也适用于此。这些数据的来源是行为风险因素监测系统(BRFFS)，该系统通过调查收集数据，并为诊断为糖尿病的成年人提供数据。因此，没有通过 BRFFS 的调查收集方法接触到的任何人都不包括在内，未确诊的糖尿病患者也不包括在内。此外，1 型和二型糖尿病之间没有区别。

另一个限制是 CDI 糖尿病数据集中这两个特定问题的种族数据缺失。性别、种族、环境因素和社会文化因素都有助于糖尿病的发展；因此，没有所有的碎片，很难拼凑出一幅画。

总之，糖尿病是一种复杂的疾病，有许多危险因素和并发症。我对 CDI 糖尿病数据集的分析着眼于高血压、高胆固醇和糖尿病之间的相互联系。在这个数据集中，在诊断为糖尿病的成年人中，高血压或高胆固醇没有性别偏见，但在 2017 年糖尿病带诊断为糖尿病的成年人中，高血压的患病率明显高于高胆固醇。

## 引用:

美国心脏协会。"血压多高会导致心力衰竭."2016，[https://www . heart . org/en/health-topics/高血压/高血压对健康的威胁/高血压会导致心脏衰竭](https://www.heart.org/en/health-topics/high-blood-pressure/health-threats-from-high-blood-pressure/how-high-blood-pressure-can-lead-to-heart-failure)

美国已诊断糖尿病的地理分布:糖尿病带。*美国预防医学杂志*第 40 卷，4(2011):434–9。doi:10.1016/j . amepre . 2010 . 12 . 019

疾病控制和预防中心，2020 年全国糖尿病统计报告。第 9 页。“糖尿病相关并发症的风险因素”。[https://www . CDC . gov/diabetes/pdf/data/statistics/national-diabetes-statistics-report . pdf](https://www.cdc.gov/diabetes/pdfs/data/statistics/national-diabetes-statistics-report.pdf)

种族、民族和健康的社会决定因素对糖尿病结果的影响。*美国医学科学杂志*第 351 卷，4(2016):366–73。doi:10.1016/j . amjms . 2016 . 01 . 008