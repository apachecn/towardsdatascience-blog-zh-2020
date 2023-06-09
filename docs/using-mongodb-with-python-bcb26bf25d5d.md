# 通过 Python 使用 MongoDB

> 原文：<https://towardsdatascience.com/using-mongodb-with-python-bcb26bf25d5d?source=collection_archive---------13----------------------->

![](img/3fc4861c51c0dea8b1a020b1ffaa4e4a.png)

照片由 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上的 [h heyerlein](https://unsplash.com/@heyerlein?utm_source=medium&utm_medium=referral) 拍摄

在这篇文章中，我们将学习如何在 Python 中使用 MongoDB。MongoDB 是一个非常快速灵活的 NoSQL 数据库。它非常受欢迎，应用广泛。

在潜水之前，让我们先来学习三个我们会经常用到的术语。

*   **文档:** MongoDB 是一个文档数据库，这意味着集合中的每条记录都是一个文档。
*   **集合:**一个集合可以存储多个文档。
*   数据库:数据库保存文档的集合。

我们来深入探讨一下。

## *目录*

*   [安装 MongoDB](#d824)
*   [连接到您的集群](#f481)
*   [创建数据库](#9a1f)
*   [插入文件](#3e32)
*   [插入多份文件](#af8d)
*   [更新一份文件](#9c71)
*   [更新多个文档](#ea99)
*   [获取一份文件](#64d1)
*   [根据 id 获取文档](#913f)
*   [获取多个文档](#4360)
*   [更复杂的查询](#a6cd)
*   [删除一个文件](#0a5e)
*   [删除多个文档](#f92e)
*   [限制](#d0ef)
*   [分拣](#2fc4)

# 1.安装 MongoDB

我将使用 MongoDB Atlas 免费层，这样您就不需要在您的计算机上安装 MongoDB，这样我们将只关注 MongoDB 和 Python。你可以从[这里](https://www.mongodb.com/cloud/atlas/register)得到。在那里创建一个集群并设置你的账户。

建立帐户后，不要忘记将您当前的 IP 地址添加到白名单中，并创建一个 MongoDB 用户，否则您将无法访问您的集群。

## **安装 PyMongo**

我们需要安装`pymongo`和`dnspython`。我们需要`dnspython`来连接`mongo+srv`协议。要安装两者，可以使用下面这个命令。

```
pip install pymongo[srv]
```

# 2.连接到您的集群

设置好账户后，点击控制面板中的`connect`按钮，然后点击`connect your application`，再选择`Python driver`。您将在那里看到您的连接字符串，复制它。

不要忘记将`admin`和`<password>`占位符替换为您在设置用户时创建的用户名和密码。请注意，此用户不是您注册时的用户，而是您在创建集群后创建的用户。

我将使用环境变量，因为我不想公开我的用户信息。您可以简单地将`user`变量分配给用户名，将`password`变量分配给密码。

# 3.创建数据库

连接到您的集群后，您可以作为`client`的属性访问您的数据库。所以当我们说`client.test`时，我们基本上是访问一个名为`test`的数据库。如果我们还没有`test`数据库，它将在插入一个文档到数据库后被创建。我们将在本节中看到如何做到这一点。

> 立正！如果您的数据库名称是`test-db`，您将不能使用类似`client.test-db`的属性样式。你应该使用字典风格。`client[‘test-db’]`会起作用。

让我们看看我们的`test`数据库是否存在。运行下面的代码后，您期望哪个输出？输出将是`test database was not created.`,因为我们还没有向`test`数据库插入任何文档。一旦我们将文档插入到数据库中，数据库就会被创建。

## 在数据库中创建集合

让我们创建一个名为`col`的集合，看看会发生什么。检查输出，我们没有名为`test`的数据库和名为`col`的集合。让我们插入一个文档，看看会发生什么。

## 插入文档

首先，我们需要创建一个`user`字典来将文档插入到集合中。`user`字典的关键字将是文档的字段，`user`字典的元素将是文档中该字段的值。

我们将把`user`插入到`col`集合中，我们可以用`insert_one`的方法来完成。插入这个文档后，您可以获得它的 id。`insert_user.inserted_id`是 bson 对象，不是常规字符串。

如果您没有自己指定`_id`字段，它会自动添加到您的文档中。

> 你可以很容易地在你的面板中创建一个数据库和集合，但我也想用这种方式来展示。

# 4.插入文档

到目前为止一切顺利。我们已经创建了我们的`test`数据库，我们可以使用`client`的属性访问风格来访问它。现在我们可以在这个数据库上创建一个名为`blog`的集合，并将文档插入到这个集合中。

我们首先选择`test`数据库，然后`db`指向该对象。然后我们创建一个`blog`集合，`blog_collection`指向那个对象。

我们可以在插入文档后检索它的 id。请参见我们文档第 13 行插入的 id。

在将第一个文档插入到`blog`集合之后，博客集合就在我们的数据库`test`上创建了。

## 我想自己指定文档的 id，可以吗？

是的，你可以！`_id`会自动确定，除非你亲自动手。我自己来，把我的`_id`设为`1`。

要非常小心！如果您插入另一个带有`1`的`_id`的文档，id 在文档中应该是唯一的。您将得到一个重复的密钥错误。身份证就像你的公民身份证，他们应该是唯一的，以被正确识别。

# 5.插入多个文档

我们可以插入多个文档，看看如何看到代码片段。我希望你在这个片段中关注 3 件事。

*   首先，我们需要传递一个字典列表来插入多个文档，其中每个字典代表一个文档，检查第 10 行的`posts`变量。
*   其次，看看我们的文档有多灵活，不需要模式！每个文档都不一样！你可以在 MongoDB 中做到，没有什么可以阻止你去做！
*   第三，看插入多个文档和一个文档的区别，我们用`insert_many`代替`insert_one`，用`inserted_ids`代替`inserted_id`。

我们将把`posts`变量作为第一个参数传递给`insert_many`方法。

# 6.更新一个文档

我们可以更新数据库中的文档。我们将使用`update_one`方法对我们的数据库执行一次更新。让我们回顾一下所有的步骤，并很好地理解如何去做。

*   首先，我在第 9 行检索匹配我们的`query`过滤器的文档。我这样做是因为我想在更新之前/之后给你看。
*   第二，我们准备一本字典，然后`new_document`指向它。重点看那本字典，`‘**$set**’`和`{'content': 'I love MongoDB and Python', 'title': 'Updated Post'}`。我们这里基本讲的是**设置** `content`到`I love MongoDB and Python``title`到`Updated Post`。
*   最后，我们检索更新后的文档，看看它是否有效。看看`updated_document`的输出，我们的修改被应用了。Id 和其他我们没改的还是一样，只有`content`和`title`按照我们的本意改了。

`update_one`方法的第一个参数是你的过滤器，第二个参数是你要应用的修改和`upsert`。如果您将`upsert`设置为`True`，如果没有符合您的过滤器的文件，它将插入一个新文件。默认是`False`。

> 如果有多个文档与您的过滤器匹配，将更新第一个匹配项。

# 7.更新多个文档

您博客中的一个用户已经更改了用户名，因此，您想要更新他的所有文档，以便将他的旧用户名更改为新用户名。我们将使用`update_many`方法更新多个文档。

# 8.获取一个文档

目前我们已经填充了数据库。现在我们想搜索我们的数据库，并检索与我们的查询相匹配的文档。

我们将使用`find_one`方法。我们将把`{‘title’: ‘Second’}`字典作为第一个参数传递给这个方法。通过传递这个字典，我们基本上告诉我们要从`blog`集合和`test`数据库中检索一个标题为`Second`的文档。我们只使用`title`进行过滤，但是我们可以向我们的`{‘title’: ‘Second’}`字典中添加更多像`‘user’: ‘halilylm’`这样的字段。

注意`document`是一个字典，所以您可以使用 get 函数来检索第 12 行的内容。

> 如果我们有不止一个带有`Second`的`title`的文档怎么办？向下滚动到下一个例子，看看会发生什么！

如果有多个文档匹配我们的查询，我们只检索第一个匹配。请参见下面的示例。有多个文档与我们的查询匹配，我们只得到第一个匹配项。

# 9.通过 id 获取文档

让我们假设，您创建了一个博客，并希望按 id 显示一篇文章。URL 是`/blog/posts/5ed0254d97e5367d20c22e63`，而`5ed0254d97e5367d20c22e63`是帖子的 id。因为这是一个普通的字符串，如果你用它作为`_id`，你将得到`None`。因为这是一个普通的字符串，而不是 bson 对象。您需要将这个字符串对象转换为 bson 对象。我假设这里的 id 是自动添加的，而不是你自己指定的。

您只需要导入`ObjectId`并将插入的 id 作为第一个参数传递给它。

我还想排除`title`和`content`，我可以传递一个我想排除的字段字典，并将字段设置为`0`作为`find_one`方法的第二个参数。看输出，`title`和`content`排除在外。

# 10.获取多个文档

您也可以一次获得多个文档。让我们尝试检索具有`halilylm`的`user`字段的所有文档

# 11.更复杂的查询

查询并不总是简单的。如果你在你的博客中建立一个搜索系统，你可能想要使用更复杂的查询。我的意思是，当一个用户搜索一个关键字时，你也希望显示与该关键字相关的帖子，而不仅仅是与用户完全匹配的帖子。

假设我们想要显示文档以及这些文档中以`I love`开头的`content`字段。你会怎么做？我们将使用正则表达式来实现这一点。我将传递一个字典来过滤我们想要的结果。这本字典将作为第一个参数传递给`find`方法。

我还想排除`id`、`post_date`和`user`。我将把字典作为第二个参数传递给`find`方法。

看到输出，我们得到所有匹配我们的查询的文档。

# 12.删除一个文档

我们将使用`delete_one`方法从数据库中删除一个文档。

我们想要删除一个带有`First post`的`title`的文档，因此我们需要将`{'title': ‘First post'}` dictionary 作为第一个参数传递给`delete_one`方法来定义我们到底想要删除哪个文档。

您可以使用`deleted_count`属性访问方式检查删除了多少个文档。第 9 行的输出是 1，因此一个与我们的查询匹配的文档如预期的那样被删除。

> 如果有多个文档匹配该查询，该怎么办？答案是只有第一个匹配会被删除。

# 13.删除多个文档

我们可以一次删除多个文档。假设`halilylm`用户已经删除了他的账户。我们想删除所有属于他的帖子。我们将使用`delete_many()`方法来执行此操作。

> 立正！如果您将空字典传递给`delete_many()`方法，它将从该集合中删除所有文档！非常小心！！！

# 14.限制性的

假设我们的查询与`2 posts`匹配，我们希望将结果限制为仅与`1 post`匹配。我们可以限制从数据库中获取的文档数量。为此，我们将使用`limit`方法。只需将您想要从我们的数据库中检索多少个文档传递给`limit`方法

看看输出，我们只得到一个文档。输出更长，因为这次我没有排除任何字段。

# 15.整理

我们将使用`sort`方法按照`title`字段对结果进行排序。

将字段名作为第一个参数传递给`sort`方法。将`1`或`–1`作为第二个参数传递给`sort`方法。然而，你不必通过`1`来指定方向，因为默认是升序。

> 排序('标题'，1)升序(默认)
> 排序('标题'，-1)降序

我们先按升序排序，排除`id`、`post_date`、`user`和`category`字段。

注意，一个空字典向`find`方法传递了第一个参数。这意味着你不想应用任何过滤器。第二个参数是要排除的字段的字典。

对于降序，只需将`-1`放在`sort`方法的第二个参数中。

# 结论

我希望您喜欢这篇文章，并且很好地理解了如何在 Python 中使用 MongoDB。敬请关注未来的作品。