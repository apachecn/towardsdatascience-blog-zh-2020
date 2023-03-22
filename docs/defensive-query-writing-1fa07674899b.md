# 防御性查询编写

> 原文：<https://towardsdatascience.com/defensive-query-writing-1fa07674899b?source=collection_archive---------82----------------------->

![](img/370c95c2fd035956fa9f33c316b5a240.png)

照片来自 [Pexels](https://www.pexels.com/photo/police-army-commando-special-task-force-20258/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

## 数据工程

## 使用防御性编码原则编写 SQL 查询

源自防御性编程，防御性查询编写是一种尝试确保查询运行不会失败的实践。就像在应用程序开发中一样，尽量避免愚蠢的错误，控制不可预见的情况。有时，您需要决定是希望查询失败，还是希望查询即使有一些不正确的数据也能运行。我将分享几个简单的例子，在这些例子中，我们可以在编写查询时使用这些实践。

# 检查数据库对象是否存在

以创建和删除数据库对象为例。不要使用`CREATE TABLE xyz`，使用`CREATE TABLE IF NOT EXISTS xyz (id int)`或者如果你想重新创建丢失所有数据的表，你可以运行`DROP TABLE IF EXISTS xyz`，然后运行`CREATE TABLE IF NOT EXISTS xyz (id int)`。

同样的实践可以用于创建和删除数据库、视图、索引、触发器、过程、函数等等。我开始意识到，在大多数情况下，使用这个是有帮助的。

# 使用数据库和列别名

防止自己出现*不明确的列*错误。参见下面的例子，列`city`可能同时出现在`TABLE_1`和`TABLE_2`中。你如何期望数据库知道你希望它选择哪个字段？

通常，为数据库对象创建别名，然后使用别名而不是完整名称来访问这些数据库对象及其子对象是一个非常好的做法。显然，为了高效地完成这项工作，您需要遵循 SQL 样式表。我在这里写了更多关于它的内容—

[](/how-to-avoid-writing-sloppy-sql-43647a160025) [## 如何避免编写草率的 SQL

### 让您的 SQL 代码更易读、更容易理解

towardsdatascience.com](/how-to-avoid-writing-sloppy-sql-43647a160025) 

# 使用极限，偏移

不，我不是在说使用`LIMIT`来限制最终查询中的记录数量。相反，我说的是这样的查询。

返回列的子查询中的`LIMIT`子句很重要，因为如果子查询返回多行，即对于`TABLE_1`中的每条记录，如果`TABLE_2`中有多条记录，它可以防止查询失败。这是编写更好的查询的一个非常有用的技巧。

使用`LIMIT`有一个警告。如果你不确定数据的质量或者你对数据库不够了解，使用`LIMIT`经常会给你错误的答案。在某些情况下，您更希望作业失败时抛出错误，而不是查询返回不正确的结果集。

# 使用存储过程和预准备语句

信不信由你，SQL 注入仍然非常流行。近年来，许多受欢迎的公司发现自己受到了黑客攻击 SQL 注入的摆布。有非常具体的方法来防止您的应用程序受到这种攻击。关于这个话题最有资源的网站是 OWASP。

[](https://owasp.org/www-community/attacks/SQL_Injection) [## SQL 注入

### SQL 注入攻击包括通过从客户端到客户端的输入数据插入或“注入”SQL 查询

owasp.org](https://owasp.org/www-community/attacks/SQL_Injection) 

防止这些攻击背后的想法是通过使用准备好的语句或使用存储过程来安全地参数化您的查询。即使这些解决方案也要求在运行查询之前进行严格的验证检查——使用特殊字符、转义字符等等。

# 小心使用触发器

我有触发器的问题。我曾经试图在生产数据库触发的触发器上构建一个轻量级的数据转换管道。我在想什么，对吧？它是轻量级的，它本来可以工作更长时间，但由于应用程序中的一些 bug(很可能是关于事务边界的),它没有得到解决。即使那没有成功，我仍然真的非常喜欢触发器，但它们确实会带来自己的痛苦。

必须格外小心，确保触发器不是相互依赖的，并且在数据库应用程序中不可能有循环触发器。

# 执行前模拟 DML 语句

总是试图将您的生产查询模拟成`SELECT`语句，即使您正在尝试`DELETE`或`UPDATE`。这样做会给你一个公平的想法，当你`DELETE`或`UPDATE`时，你实际上要做什么。这些年来，我发现这个方法真的很有用。这无疑增加了另一个耗费时间的步骤，但我认为这比额外的成本有好处。

除了嘲讽之外，您还必须在您的开发/测试环境中运行相同的`DELETE`和`UPDATE`语句，这样您就可以在生产中做任何激烈的事情之前签署它们。

这些是我的一些建议。[我发现这些在处理数据系统时非常有用](https://linktr.ee/kovid)。类似地，我在这里也谈到了许多提高数据库查询性能的好的、简单的 SQL 技巧

[](/easy-fixes-for-sql-queries-ff9d8867a617) [## SQL 查询的简单修复

### 查询任何传统关系数据库的经验法则

towardsdatascience.com](/easy-fixes-for-sql-queries-ff9d8867a617) 

快乐阅读！