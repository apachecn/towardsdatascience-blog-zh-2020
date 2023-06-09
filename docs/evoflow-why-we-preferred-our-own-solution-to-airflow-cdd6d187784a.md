# EvoFlow:为什么我们更喜欢自己的气流解决方案

> 原文：<https://towardsdatascience.com/evoflow-why-we-preferred-our-own-solution-to-airflow-cdd6d187784a?source=collection_archive---------71----------------------->

![](img/e5cf7dd13d2a4e45951552d1e0389997.png)

## [商业科学](https://medium.com/tag/business-science)

## 通用的流量检查流程

# EvoFlow 简介

EvoFlow 是由 Evo 的数据工程师和 devOps 团队开发的多功能平台，用于创建、调度和监控工作流。

编码工作流允许开发团队创建和共享他们产品的版本。这种协作过程可以在保持产品结构的同时进行，或者更好的是，在改进这些结构的同时进行。

EvoFlow 的创建是为了增强 ETL、Scraper 和其他数据管道检查的流程，但是它的功能远远超出了这些用途。

# **EVO 之路**

那么我们为什么要创建自己的平台呢？毕竟，广泛采用的气流(【https://airflow.apache.org/】)可以做 EvoFlow 做的所有事情；早已成为标配。虽然气流的用处是没有争议的，但这个工具可能有点笨拙。有了这么多的功能，它实际上可以减慢简单的检查。我们需要一个工具来简化 ETL 和 Scraper 流程，而不是使流程进一步复杂化。

EVO 数据工程师和 DevOps 团队决定构建一个简化的平台，以便更快地实现我们的目标。我们将它命名为 EvoFlow，因为它是作为流检查的流而诞生的。

与气流相比，EvoFlow 的创建给了该团队一些显著的优势。使用 EvoFlow，我们可以受益于:

*   由于平台的功能减少，结构更简单；
*   由于对整个平台的了解而具有更高的控制能力；
*   由于在使用的基础设施上构建了 EvoFlow 代码，因此具有更高的适应性；
*   由于平台需求减少，基础设施成本降低；
*   由于与广泛采用的警报管理器([https://prometheus.io/docs/alerting/latest/alertmanager/](https://prometheus.io/docs/alerting/latest/alertmanager/))的结合，警报管理具有更高的灵活性。

# 结构

EvoFlow 有五个关键组件，所有这些组件都可以在图 1 中看到:

1.  来源包括 JSON、R、SQL、txt、Python、CSV 文件，加载所需任务中使用的数据；
2.  规则指定了平台执行任务和进来所需的所有信息。yml 文件；
3.  Python 中定义的函数详细描述了要执行的操作；
4.  日志在执行时打印出来，并存储在 SQL 数据库中；
5.  警报由 Alertmanager 管理；
6.  报告构建为元数据库([https://www.metabase.com/](https://www.metabase.com/))仪表板。

![](img/1c59cdafcf991ab02da1e026757be5c3.png)

图 EvoFlow 平台的方案(图片由作者提供)。

# 成分

源文件包括几个扩展名，通常用于将数据加载到 EvoFlow 平台中。对数据源的唯一要求是它们不能在加载过程中改变数据。例如，SQL 查询应该只包含 select 语句:

```
SELECT'dates/weeks' AS items_type,'sql execute' AS check_message,MIN(date) AS start_date,MAX(date) AS end_date,MIN(CONVERT(int, week)) AS min_week_diffFROMclient_calendar
```

规则是。定义 EvoFlow 要求(数据)、数据源路径(源)、检查要求(接受)、错误消息(error_message)、描述(check_descriptions)和严重性(severity)的 yml 文件:

```
# Check etl executionParameters:# Define the parameters required by the projectsql_string: 'TRUE'sql_connection: 'TRUE'sql_logs: 'TRUE'is_check: 'TRUE'email_alert: 'TRUE'Checks:
# Check files importfiles_check:type: sqlpath: '/functions/check_last_import_file_amount.sql'check_description: 'Check amount of files imported'error_message: 'The imported files amount is wrong'severity: Criticalacceptances:- compare_to_acceptance(comparison="(abs(data['last_import'] - data['previous_import']) / data['previous_import']) < 0.1")package_check:
# Check ETL package executiontype: sqlpath: '/functions/check_package_error.sql'check_description: 'Check errors in the ETL package'error_message: 'Errors in the ETL packages execution'severity: Erroracceptances:- compare_to_acceptance(comparison="data['count_value'] == 0")
```

函数指定规则接受所需的所有动作和检查。它们通常用 Python 编写:

```
def compare_to_acceptance(comparison):"""Compare a given field to a provided acceptanceParameters:comparison (string): the comparison to executeReturns:0 if the results are within the acceptance, 1 otherwise"""# Initialise the list of resultsresults = list()# Iterate for each element and get the results of the checkfor i in range(0, len(self.data)):result = 0 if eval(comparison) else 1results.append(result)return(results)
```

日志通常存储在 SQL 数据库中，由 Alertmanager 管理，并报告为元数据库仪表板。

# 功能

EvoFlow 主要处理 ETL 和 scraper 自动化的检查。也就是说，它的功能还可以执行任何可能的脚本并管理相应的警报。

EvoFlow 目前用于:

*   检查客户端 ETL 输出的质量；
*   检查自动刮刀产生的数据质量；
*   分析工具文件夹并识别自动化的问题；
*   将每日汇率导入 SQL 数据库。

如果我们将来需要扩展 EvoFlow 的使用，该平台也具有完成这些任务所需的灵活性。

# 结论

EvoFlow 平台的开发改变了 EVO 组织的游戏规则。有了这个新的基础设施，我们能够:

1.  识别和纠正自动化中的问题和错误的速度至少快四倍；
2.  创建对数据和流程的新检查，并使用仪表板对其进行监控；
3.  提醒所有参与使用工具的人，而不仅仅是开发人员；
4.  创建独立的流动，可以存在于最常用的管道之外；
5.  在运行代码流之前，自动评估代码的质量。

为了评估 EvoFlow 的性能，我们希望量化其影响。我们主要测量了在一项任务上花费的时间和警报的数量。根据任务的不同，花在这些任务上的时间减少了 2 到 4 倍。警报数量每周下降约 10%。

主要由于 EvoFlow 与 Alertmanager 的集成，警报数量持续下降。这个联合允许我们根据关联项目的名称和警报的严重级别(错误、警告、严重)来管理警报。此外，该集成还会自动创建与触发的警报相关的 Gitlab 问题，以确保每个警报都有适当的优先级，并确保解决该问题的任务被委派给正确的团队成员。

我们的早期结果显示了年轻的 EvoFlow 平台的前景。它已经带来了显著的投资回报，我们乐观地认为不久会有更好的表现。虽然我们不能建议像 EvoFlow 这样的简化平台是每个团队的正确解决方案，但我们对它迄今为止的成功感到高兴。