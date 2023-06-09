# 新冠肺炎聚类分析

> 原文：<https://towardsdatascience.com/covid-19-cluster-analysis-405ebbd10049?source=collection_archive---------14----------------------->

## 聚集受冠状病毒影响的世界国家

![](img/44b17cff238276f54dee5595f69c6e0a.png)

马丁·桑切斯在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的照片

***编者按:*** [*走向数据科学*](http://towardsdatascience.com/) *是一份以数据科学和机器学习研究为主的中型刊物。我们不是健康专家或流行病学家，本文的观点不应被解释为专业建议。想了解更多关于疫情冠状病毒的信息，可以点击* [*这里*](https://www.who.int/emergencies/diseases/novel-coronavirus-2019/situation-reports) *。*

# 介绍

在过去的两个月里，冠状病毒疾病 2019(新冠肺炎)的新的主要流行病灶已被确定，并在全球迅速传播。到 2020 年 3 月 16 日，中国以外的新冠肺炎病例数量急剧增加，向世界卫生组织(世卫组织)报告感染的受影响国家、州或地区数量众多。

基于“令人震惊的蔓延和严重程度，以及令人震惊的不作为程度”，2020 年 3 月 11 日，世卫组织总干事将新冠肺炎局势描述为疫情[1]。这一事实和冠状病毒的快速传播导致全球许多国家采取严格措施限制公民。

另一方面，来自不同领域的许多科学家试图提供关于这种疫情水平疾病的见解。包括世卫组织和约翰·霍普斯金大学(JHU)在内的许多组织和大学向公众提供了呈现冠状病毒传播的数据和可视化结果[2，3]。JHU 系统科学与工程中心及其研究人员在 [Github](https://github.com/CSSEGISandData/COVID-19) 中创建了一个数据仓库，提供世界各国关于冠状病毒的时间序列数据。这些数据包括每天确诊的病毒病例总数、死亡人数和从病毒中康复的人数。

本文试图利用聚类技术和可视化技术，对上述 [Github](https://github.com/CSSEGISandData/COVID-19) 中的数据仓库提供的数据提供见解。

# 数据分析

首先，数据由三个数据集组成，即确诊病例、死亡病例和痊愈病例。每个数据集由数据集中每个国家从 2020 年 1 月 22 日到 2020 年 4 月 11 日的时间序列组成。每个数据集中还有一些额外的列，包括每个国家的省/州和经纬度坐标。下图提供了在任何预处理之前对其中一个数据集的一瞥。

![](img/247298a914d68e13e2f3a8fa5939f1ec.png)

图 1:任何预处理之前的数据集。

在执行了一些数据预处理之后，我们得到了干净的、准备好进行分析的数据集。此外，源数据是累积的时间序列，这意味着第二天的值是前一天的值加上新的案例。因此，对于该分析，时间序列被转换以表示每天的新情况。

此外，通过执行线性回归，为每个变换的时间序列计算趋势线系数。为了在 95%的显著性水平下获得具有统计显著性的结果，不具有统计显著性趋势(即趋势线系数的 *p 值*大于 0.05 的α水平)的国家将从分析中剔除。

此外，对相应国家的趋势线系数进行了聚类分析。关于算法部分，对标准化系数使用了 **K 均值**算法。该算法通过尝试将样本分成等方差的 *n* 组来对数据进行聚类，从而最小化被称为*惯性*或类内平方和的标准。使用基于*惯性*和平均轮廓法【4】的肘法【4】确定聚类数。

这些集群在交互式世界地图中被可视化，以便更好地了解情况。请注意，地图上未着色的国家不在本分析中，因为它们的趋势线系数在统计上不显著，或者没有它们的时间序列数据。图 1、图 3 和图 5 分别显示了基于确诊病例、死亡病例和康复人员的国家分组，而图 2、图 4 和图 6 分别显示了每个分组关于确诊病例、死亡病例和康复人员分组的百分比值的平均趋势系数。将鼠标悬停在图表 1、3、5 上，可以看到国家名称、它们所属的集群以及它们的百分比趋势线系数。此外，在图 2、4、6 中，有聚类名称、趋势平均值和属于该聚类的国家。

## 确诊病例

图 1:确诊病例的聚类

图 2:每个集群的平均趋势——案例

就对这些病例群的解读而言，美国的确诊病例似乎每天都在大幅增加。另一方面，第三组国家，即法国、德国、意大利和西班牙每天都有小幅增长。最后，土耳其，伊朗和英国描绘了大约一半的集群 3 的增量。这组国家中的所有其他国家显示出稳定的低增长。

## 确认死亡

图 3:确诊死亡病例的聚类

图 4:每组死亡人数的平均趋势

关于死亡数据集中的聚类，很明显，美国和意大利比其他国家具有最高的增长趋势。在第五组中，紧随其后的是西班牙和法国，其趋势略低于美国和意大利。第三组包括联合王国，第四组包括德国、伊朗、比利时和荷兰。这组国家中的所有其他国家都略有增加。

## 确认恢复

图 5:已确认恢复的集群

图 6:每个集群的平均趋势—已恢复

下面，关于从冠状病毒中康复的人的趋势的聚类可以在上面看到。包括德国和西班牙在内的第 3 组显示了最高的每日增量。第二组排在第二，包括伊朗和中国。增量等级中的第三组是组 5，包括法国、意大利和美国，其百分比增量值大约是第一组 3 的一半。此外，聚类 4 包括诸如奥地利、韩国、比利时、加拿大和瑞士之类的国家，聚类 5 包括集合中的所有其他国家，这些国家显示出较小的增量。

# 结果

根据上述关于冠状病毒确诊病例、死亡病例和康复人员的趋势线系数分析，在他们的日常增长中存在一些可识别的聚类。具体而言，在全世界确诊病例中，有四个不同的组群。在全球范围内确认死亡和康复人员的情况下，每组分别有五个聚类。请注意，每日新增病例数量低的国家，其死亡和康复数量也低，因此其增量也低。

# 结论

综上所述，本文利用 JHU 系统科学与工程中心提供的聚类技术和可视化数据，努力提供关于新冠肺炎病毒情况的见解。数据由三个数据集组成，特别是确诊病例、死亡和从病毒中康复的人。每个数据集包括世界各国的时间序列。对每个时间序列的趋势线系数使用 **K-means** 算法的聚类方法突出了经历某种程度上相同情况的世界国家的有意义的聚类。

# 参考

[1]世卫组织总干事在 2020 年 3 月 11 日新冠肺炎媒体吹风会上的开幕词。检索自:[https://www . who . int/DG/speechs/detail/who-总干事-s-open-remarks-at-media-briefing-on-新冠肺炎-2020 年 3 月 11 日](https://www.who.int/dg/speeches/detail/who-director-general-s-opening-remarks-at-the-media-briefing-on-covid-19---11-march-2020)

[2]冠状病毒(新冠肺炎)。世界卫生组织。检索自:【https://who.sprinklr.com/ 

[3]冠状病毒资源中心。约翰·霍普斯金大学。检索自:【https://coronavirus.jhu.edu/ 

[4]袁，陈，杨，何(2019).K-Means 聚类算法中 K 值选择方法的研究。