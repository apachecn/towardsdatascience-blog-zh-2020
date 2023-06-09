# 数据驱动的 T-SQL 业务规则

> 原文：<https://towardsdatascience.com/data-driven-t-sql-business-rules-9ac1e6ad3b4a?source=collection_archive---------27----------------------->

## 创建具有动态和可互换业务规则的数据验证器，或者为什么(T-) SQL 比我们愿意承认的更强大

![](img/dcb4522362dec387d45c27ae23f1b666.png)

[图片由 PNGJoy 提供](https://www.pngjoy.com/preview/f9m4w4v8d8x8f0_web-development-images-full-stack-development-hd-png/)

硬编码。我敢肯定，在这一点上，你已经听说了使用它将如何把你带到编码器的地狱。专家似乎建议尽可能避免它。那么，为什么我们的大多数查询都是硬编码的呢？如果我们能够以一种集中的、可互换的方式指定查询的谓词，会怎么样？让我们看看(T-)SQL 到底有多动态。

然而，请注意，这可能不是一个好主意，但无论如何让我们玩得开心点。

# 什么？

为了说明数据驱动约束引入的可能性，我们将创建一个数据验证器，它强制执行一组约束(不要与 SQL 自身的约束混淆)、业务规则或简单的阈值，这些都是在表上定义的。此外，同样的模型可以扩展到定义您的 *where* 谓词，或者您的查询的任何部分。如果任何人发现这个帖子相关——怀疑——我会用这个扩展名创建另一个帖子。

我们的最终目标是获得一个存储过程，它允许用户根据一组给定的动态规则来验证给定的条目。例如，验证值 50 是否符合规则集 ID 2，并检索相关的输出代码:

```
exec ValidateThreshold 2, ‘50’, @returned_code OUTPUT;
```

# 为什么？

首先，你到底为什么要这么做？谁会将业务规则硬编码到数据库的查询中呢？事实证明我们大多数人。从数据模型的接近到职责的分离，有很多理由说明为什么需要这样做。

考虑一个拍卖网站的例子。如今，你有一条规则，规定你只接受不低于 0.05 的出价。如果明天你想把所说的价值改成产品估价的 0.01%到 10%之间的任何值呢？是否要更改包含新约束的每个过程、视图、触发器或查询？好吧，希望在这篇文章之后，你不用再这样做了。

实际上，我们引入了一个简单的模型，在实践中，拥有一个规则集表是有意义的，它创建了要应用的规则组。

需要做一个介绍性的说明，我绝不是 SQL 专家——我相信你已经注意到了——相反，我只是一个极其懒惰的人，喜欢想方设法避免手工劳动。希望它也能帮助你的懒惰性格。请务必阅读结尾部分，它可能是整篇文章中最重要的部分。

# 怎么会？

第一步是实际构建您的规则或阈值。

```
Create table Threshold
(
 ThresholdID int identity not null,
 ThresholdSetID int not null,
 VarName varchar(20) not null,
 Operator varchar(2) not null,
 TargetValue varchar(50) not null,
 [Description] varchar(100) not null,
 ThresholdOrder int not null,
 Deprecated bit not null default 0,primary key (ThresholdID)
);
```

并用一组虚拟内容填充它:

```
insert into Threshold values (1, '@input', '>=', '25', 'dbo.InsertAuctionBid(...)', 1, 0);insert into Threshold values (1, '@input', '<', '(select max(value) from dbo.AuctionDates)', 'dbo.InsertAuctionBid(...)', 2, 0);
```

注意 rows*@如何输入*参数，该参数表示要验证的值。第一个规则将确保我们的参数大于或等于 25 的**，而第二个规则确保传递的参数小于 AuctionDates 表中的最大日期**的**。**

进入验证程序！

```
create procedure dbo.ValidateThreshold
(
 @thresholdID int,
 @input nvarchar(50),
 @return_code int OUTPUT
)
as
 if @thresholdID is null 
 begin
  set @return_code = 2;
  return;
 endif @input is null  
 begin
  set @return_code = 2;
  return;
 enddeclare @statement nvarchar(max), @where_clause nvarchar(max);set @where_clause = stuff((
  select '  and '+ VarName +' '+ Operator  +' ' + TargetValue +char(10)
  from 
   Threshold
  where
   ThresholdID in (@thresholdID)
  order by 
   thresholdOrder
  for xml path (''), type).value('.','nvarchar(max)')
  ,1,6,'');set @statement = 'if exists(select 1 '+char(10)+'where '+ @where_clause + char(10) + ') select 0; else select 1;';set @statement = replace(@statement, '@input', @input)exec sp_executesql
  @query = @statement
  ,@params = N'@return_code INT OUTPUT'
  ,@return_code = @return_code OUTPUT;
```

对于我们这些 SQL 新手来说，有很多东西需要理解，所以让我们把它分成几个部分。

我们的过程应该有三个参数:2 个输入和 1 个输出。要应用的规则；要验证的参数，格式为文本。最后是操作的输出代码，0 表示成功，任何不同都表示特定的错误代码。

```
create procedure dbo.ValidateThreshold
(
  @thresholdGroup int,
  @input nvarchar(50),
  @return_code int OUTPUT
)
```

接下来，验证我们的输入并返回一个适当的错误代码

```
as
 if @thresholdID is null 
 begin
  set @return_code = 2;
  return;
 endif @input is null  
 begin
  set @return_code = 2;
  return;
 end
```

到目前为止一切顺利。果汁来了

```
declare @statement nvarchar(max), @where_clause nvarchar(max);-- Generate the underlying where clause by concatenatinc the Variable to test, the boolean operator and the test predicate
 -- using XML PATH to repeat the whole process, gluing subsequent predicates with an ' and'.
 -- Lastly, use stuff to collapse it all together, removing the first 6 characters (corresponding to ' and') starting on the first position.
 -- Note: If more than a @thresholdID is provided, the predicates will be passed according to Threshold.ThresholdOrder set @where_clause = stuff((
  select '  and '+ VarName +' '+ Operator  +' ' + TargetValue +char(10)
  from 
   Threshold
  where
   ThresholdID in (@thresholdID)
  order by 
   thresholdOrder
  for xml path (''), type).value('.','nvarchar(max)')
  ,1,6,'');set @statement = 'if exists(select 1 '+char(10)+'where '+@where_clause + char(10) + ') select 0; else select 1;';-- Feed the input variable
 set @statement = replace(@statement, '@input', @input)exec sp_executesql
  @query = @statement
  ,@params = N'@input nvarchar(50), @return_code INT OUTPUT'
  ,@input = @value
  ,@return_code = @return_code OUTPUT;
```

## 那么这是如何工作的呢？

[**FOR XML PATH**](https://docs.microsoft.com/en-us/sql/relational-databases/xml/for-xml-sql-server?view=sql-server-ver15) 顾名思义，允许您将查询结果转换成 XML 文件。但是，通过将一个空字符串传递给 RAW 参数，我们为返回的数据创建了一个串联的字符串。考虑以下用户表:

```
╔═══════════╗
║   Name    ║
╠═══════════╣
║ John      ║
║ Mary      ║
║ William   ║
║ Anthony   ║
╚═══════════╩
```

应用于前一个表:

```
select ','+ name 
        from Users
        FOR XML PATH('')Output: ‘,John, Mary, William, Anthony’
```

注意尾部的逗号，它虽然允许我们创建逗号分隔的字符串，但会完全破坏 SQL 语句。在我们的例子中，我们输入了一个*和*关键字，而不是逗号，这样我们就可以将多个子句粘在一起。

我们首先调用 [**value()**](https://docs.microsoft.com/en-us/sql/t-sql/xml/value-method-xml-data-type?view=sql-server-ver15) 函数将 XML 对象转换成字符串。然后，我们使用 [**STUFF()**](https://docs.microsoft.com/en-us/sql/t-sql/functions/stuff-transact-sql?view=sql-server-ver15) 函数检索逗号，或者在我们的例子中，检索 6 个字符，以从生成的字符串中删除‘and’部分。

下一步是将生成的 *where* 子句传递给一个布尔语句，使用 *Exists* 来测试返回的存在。如果返回为 1，则*@输入*有效，但是如果返回为空，则*@输入*验证*失败。*

通过用传递的 *@input* 替换@input 字段并通过 [**动态 SQL**](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql?view=sql-server-ver15) 执行查询，该过程结束。

但是请注意，动态 SQL 有很多缺点，从性能到安全性。我绝不是建议您的 DBA 应该实现这个模型，它仅仅是(T-)SQL 灵活性的一个展示，人们并不期望它存在。

我希望这个资源对你有所帮助，或者至少是有趣的。