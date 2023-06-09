# SQL 的 Git 最佳实践

> 原文：<https://towardsdatascience.com/git-best-practices-for-sql-5366ab4abb50?source=collection_archive---------9----------------------->

![](img/e150f74ca5d7a5e056dabb4d43ed994e.png)

安德鲁·西曼在 Unsplash 上拍摄的照片

## 数据工程

## 使用 GitHub、GitLab、BitBucket 等来存储和组织 SQL 查询，以实现发现和重用

随着数据科学、数据工程和数据运营团队的规模与日俱增，改善他们的协作方式非常重要。经常可以看到数据工程师和数据分析师在他们的本地机器上存储 SQL 查询、Python 脚本和 Jupyter 笔记本。强烈建议不要发生这种情况。尽管这些人的工作与应用程序开发人员的工作有很大不同，但毫无疑问，他们共享许多用于编写代码的通用工具。此外，在大多数情况下，工作流程也非常相似。

对于协作编写代码的团队来说，最重要的工具是版本控制系统，如 Git、Mercurial 或 Subversion。VCS 已经存在很多年了，但是数据团队仍然需要将它们完全融入到他们的工作流中。在这里，我们将讨论使用 VCS 进行数据工作的巨大好处，以及使用 VCS 进行数据工作的[最佳实践](https://linktr.ee/kovid)。我们走吧。

# 1.代码组织

组织你的代码、查询、工件、S3 桶等。，非常重要。不管你的基础设施是否在云上，你都可以设计方法来组织你的代码。它从获得正确的文件夹结构开始。应用程序的文件夹结构、数据库脚本和 DevOps 脚本都取决于您正在构建的应用程序和使用的工具。

> 结构很重要，结构很美

版本控制系统提供了一种强大的方法来确保每个人都了解文件夹结构以及代码的组织方式。我在 Medium 上找到两篇非常好的文章，它们都是关于代码组织的，其中一篇是—

[](https://medium.com/@egonelbre/thoughts-on-code-organization-c668e7cc4b96) [## 关于代码组织的思考

### 有许多方法可以构造代码。我一直在思考什么是最好的方法。我宁愿到达一个…

medium.com](https://medium.com/@egonelbre/thoughts-on-code-organization-c668e7cc4b96) 

还有一个是关于[代码组织的策略](https://medium.com/@msandin/strategies-for-organizing-code-2c9d690b6f33)。这些策略并不以同样的方式应用于数据库脚本、SQL 查询、报告和存储过程，但这个想法是一样的。代码应该以可读、可搜索、可理解和可编辑的方式编写和组织。

# 2.使用本地/远程分支

始终将所有相关工作推送到远程分支机构，即使工作正在进行中。我强烈推荐使用 git flow——git 开发方法使用三个层次的分支(有一些例外)——主、开发和特性。这里的特性分支可以是任何 CR 或新鲜的需求。

> 将您的工作推到远程分支，即使它正在进行中

不建议只在本地分支上存储，除非它对其他人来说是无用的，并且是为了您自己的实验和发现。毫不奇怪，本地分支容易丢失数据，因为您的查询不会驻留在宇宙中的其他地方。

这里有一个例子是关于对 SQL Server 脚本使用 [Git 的。git SQL——PostgreSQL 数据库的专用源代码控制解决方案。](https://www.red-gate.com/hub/product-learning/sql-source-control/github-and-sql-source-control)

# 3.强制性审查

对于每个合并请求，您应该有一个强制的审阅者。这确保没有任何可疑或不正确的东西进入生产。人工检查和平衡真的很重要。所有主要的版本控制系统都可以选择授权一个或多个人进行评审。

关于这一点，Atlassian 的工程团队有一个完整的帖子。一定要去看看。

[](https://www.atlassian.com/agile/software-development/code-reviews) [## 为什么代码审查很重要(并且实际上节省了时间！)

### 敏捷团队是自组织的，技能集跨越整个团队。这部分是通过代码实现的…

www.atlassian.com](https://www.atlassian.com/agile/software-development/code-reviews) 

重要的旁注——如果你的团队是评审过程的新手，他们可能会有点暴躁地执行它，因为它看起来像是无用的额外工作，但它几乎不是。从长远来看，额外的复习努力是有回报的。

# 4.拥有最新的试运行环境

我再怎么强调拥有最新的试运行环境的重要性也不为过。出于数据库测试的目的，没有必要一直将所有生产数据都放在这里。这实际上取决于您的测试需求。无论数据是否更新，数据库结构(表、视图、过程、函数和其他对象)应该总是同步的。

[](https://www.pulumi.com) [## Pulumi -作为代码的现代基础设施

### 建立服务于静态网站的基础设施通常比看起来更难——但幸运的是，这是一项任务…

www.pulumi.com](https://www.pulumi.com) 

像 Terraform 和 Pulumi 这样的 IaC 工具使得在几分钟内繁殖和破坏完整的环境变得非常容易。如果您正在使用所有这些工具，那么创建一个试运行环境应该不难，而且肯定不会花费太多时间。通常在数据仓库的上下文中更容易理解登台，数据仓库是在将数据写入主生产数据仓库之前进行大量预处理的层。但是这里我指的是为一个通常的开发环境准备，其他的是测试、开发和生产。登台通常也被称为预生产，但术语并不严格。

# 5.CI/CD 集成

在拥有 VCS 之后，拥有 CI/CD 管道是下一个发展步骤，因为它消除了另一个人为错误可能导致运行错误报告的步骤。本质上，这样的管道将确保您的最新代码被持续集成并自动部署到您的环境中。市场上有一些流行服务的工具可以解决这个问题，比如 Redshift、Tableau、Informatica 和大多数关系数据库。然而，他们中没有一个是完全成熟的，所以要小心这个事实。这里有一篇关于数据库 CI/CD 的好文章—

[](https://hackernoon.com/database-changes-can-be-scary-how-r1hy2gfe) [## 害怕数据库改变？用 CI/CD | Hacker Noon 控制他们

### 开发人员经常担心数据库的变化，因为团队中任何人的一个错误都可能导致重大停机，甚至…

hackernoon.com](https://hackernoon.com/database-changes-can-be-scary-how-r1hy2gfe) 

拥有 CI/CD 管道还可以减少为测试和开发设置环境和配置的大量时间。您没有必要使用市场上可用的工具之一，因为它们对于数据工程师来说都不如对于开发人员来说那么先进。您可以使用一组脚本和 Lambda 函数为您的用例创建自己的 CI/CD 工具，这些脚本和函数由通过监听 VCS 创建的事件调用。

# 6.创建查询库

最后但同样重要的是，为您的组织创建一个查询库是保持理智的最重要的事情之一。这可以防止不同团队再次重写相同的查询。我为几个团队做过，但从未在一个组织中做过。为查询库使用 VCS 很有意义，但是非技术团队可能会发现使用 VCS 很难操作。

Caitlin Hudon 在她的博客上发表了一篇令人惊叹的文章，她谈到了自己的心得，并将这些心得总结为关于 SQL 的真理，如下所示

*   您总是会再次需要该查询
*   查询是随着时间变化的活的人工制品
*   如果对你有用，对别人也有用(反之亦然)

有像 Metabase 这样的开源工具可以帮助你在集合中组织你的查询。如果不是这样，您可以使用您的 BI 工具作为查询库的存储。虽然不是最好的选择，但是如果团队有这样做的动机，这是可行的。

# 结论

由于 SQL 是应用开发、数据工程、数据科学和数据分析等许多开发领域广泛使用的语言，因此很容易找到不同的使用、存储和维护模式。话虽如此，我们不应该原谅，无论我们遵循什么模式，它都应该让其他人容易理解、探索和处理已经编写好的代码。这是唯一的要求。