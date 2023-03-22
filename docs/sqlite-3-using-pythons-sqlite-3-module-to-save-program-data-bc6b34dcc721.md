# SQLite 3:使用 Python 的 SQLite 3 模块保存程序数据

> 原文：<https://towardsdatascience.com/sqlite-3-using-pythons-sqlite-3-module-to-save-program-data-bc6b34dcc721?source=collection_archive---------22----------------------->

![](img/c55a8a6e75da014f1f2d6517002c5d9b.png)

[Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 上 [AltumCode](https://unsplash.com/@altumcode?utm_source=medium&utm_medium=referral) 的照片

> “数据是网络运行的燃料，因此作为开发人员，我们绝对有必要以高效的方式处理和存储数据。”

当您在处理一个需要大量用户输入并存储各种用户数据的项目时，拥有一个好的数据库来管理用户数据并能够以高效的方式进行管理就变得至关重要。

虽然程序数据和实例通常以文件的形式存储，但是当您处理大量数据并且需要能够创建、检索、更新和删除(CRUD)这样的数据时，这不是存储数据的最有效方式，这对于文件的使用来说不是很方便。

这就是 SQLite 3 的用武之地，它是一种快速、轻便、简单的方式来存储即使是最复杂形式的数据，并且它以高效的方式执行 CRUD 操作。

您可以在下面找到 SQLite 3 模块的文档；

 [## sqlite 数据库的 sqlite3 - DB-API 2.0 接口- Python 3.9.0 文档

### 源代码:Lib/sqlite3/ SQLite 是一个 C 库，它提供了一个轻量级的基于磁盘的数据库，不需要…

docs.python.org](https://docs.python.org/3/library/sqlite3.html) 

我们将使用 SQLite 3 数据库创建一个基本的登录功能，其中我们将涵盖所有 CRUD 操作，即创建用户、检索用户数据、更新用户数据和删除用户数据。

让我们开始吧。

由于 SQLite 3 是一个内置模块，我们可以直接导入它，而无需安装任何东西。

```
import sqlite3
```

现在让我们开始设置我们的数据库；

因此，为了创建一个基本的登录程序，我们至少需要用户的两个输入，用户名和密码。为此，我们将创建一个包含两列的表，

就是这样，这就是创建一个数据库所要做的一切。看看有多快，现在让我们继续创建一个用户。

## 创造

我们从用户那里获得两个输入，用户名和密码，然后将它们提交到我们的表中。

游标功能帮助我们遍历数据库，并帮助我们执行 CRUD 功能。

## 恢复

如果我们想要检查用户是否存在，以及输入的密码是否与存储在数据库中的密码匹配，我们需要能够检索我们刚刚创建的用户数据。

光标遍历数据库，找到与我们输入的参数相匹配的条目。

在 SQLite 3 中，我们可以通过两种方式从数据库中获取数据，

`fetchone()`:这个函数从我们的表中获取第一行，该行与传入的参数相匹配。

`fetchall()`该函数获取所有符合我们设置的参数的行。

我们使用了`fetchone()`,因为理想情况下不应该有多个相同用户名的条目。

`cur.fetchone()[1]`检索给定用户 as 的密码，密码在我们的表的第 2 列。

## 更新

现在，如果我们的用户想要更改他的密码，我们需要能够处理这一点，并做到这一点，我们需要能够更新用户的凭证。

要更新密码，我们只需要一个输入，即用户名。

## 删除

我们需要能够删除任何我们不再需要的旧数据，并避免重复，

# 结论

在不到 15 行代码中，SQLite 3 使我们能够轻松创建一个强大、快速和动态的数据库。

现在，在您的下一个 Python 项目中使用 SQLite 3，感受它的强大。