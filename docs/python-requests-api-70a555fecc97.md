# 在 Python 中使用 API。

> 原文：<https://towardsdatascience.com/python-requests-api-70a555fecc97?source=collection_archive---------19----------------------->

## 高级概念包括面向对象程序设计、缓存

![](img/14b0718d76a033dc3eff85db5ef17bbc.png)

由[约书亚·阿拉贡](https://unsplash.com/@goshua13?utm_source=medium&utm_medium=referral)在 [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral) 拍摄

随着微服务的出现，有很多 API 可以与之交互，无论是用于编排系统还是提取数据。使用 Python 处理专用的 API 工作负载是合适的，因为它具有多用途的特性。

在本文中，我将与您分享 3 个代码片段，它们将帮助您更好地管理依赖于 API 的工作流。我将使用 J [子占位符假 API](https://jsonplaceholder.typicode.com/) 进行演示。

## 1.使用线程和异步实现并发的 Python API

当您希望用一个变化的参数对同一个资源进行多次调用时，您必须转向并发方法。事实上，编写顺序代码会产生低效的代码:您的代码将花费大部分时间等待服务器的响应。

要解决这个问题，有两种方法要么我们使用线程，要么从 python 3.5 开始我们可以使用异步。让我们看看这两种方法的代码是什么样子的，以便分别检索注释。让我们从线程方法开始。

线程方法来源:作者

我用一个`dataclass`来封装初始化整个过程的逻辑。线程是工作线程，每个线程并发地调用一个 URL。他们从队列中提取 URL，队列是一种支持并发的数据结构。当他们收到答案时，他们把它放到另一个队列中。最后，当所有的工人完成后，我们将队列转换成一个列表，并返回它。

现在让我们看看异步版本。

异步方法来源:作者

在这个版本中，我们不需要处理并发和多线程，因为没有并发线程产生。事实上，异步代码是基于事件循环和协程的，概括地说，我们不是等待 IO 代码解决，而是执行另一段代码，并在解决后返回到 IO 代码。

然而，为了能够等待代码和委托控制，我们必须使用异步函数，这意味着范式转换，并使用新的库。

因为，正如你所看到的，异步版本的缺点是不能使用通常的库，例如请求。事实上，使用支持异步的库是必要的。

另一方面，线程的缺点是必须考虑用专用数据结构管理并发线程。

## 2.使用重试修饰器重试 Python 代码失败

当使用 API 时，存在节流的情况并不少见。拥有一个允许您在函数失败时重试的实用程序可能会很有趣。为了实现这个实用程序，我使用了一个对很多情况都非常有用的 python 特性:decorators。

有状态重试装饰器源代码:作者

这是一个没有函数形式的装饰者，而函数形式是传统的呈现方式。这是一个类。当需要在内存中保存一个状态时，以类的形式实现的 Decorators 是很有趣的。这里我们需要在内存中保存尝试的次数。

因此，这个装饰器允许我们指定被装饰的函数必须重试的次数，也允许我们指定每次重试之间的等待时间。

## 3.缓存 Python HTTP 请求的结果

当您必须对某个 API 进行大量调用时，例如每天有一个限制，并且您的脚本在接近结束时由于失误而失败，您会丢失对该 API 的调用结果。

在这种情况下，实现一个缓存来保存我们的结果可能会很有趣，因为我们下次启动脚本时，只有未缓存的请求才会被执行。下面是实现本地缓存的代码示例。

简单的本地缓存实现来源:作者

这个缓存是作为一个类实现的。本地缓存只不过是一个 dict，我们用 URL 作为关键字来保存数据。然后，这个缓存以序列化 pickle 文件的形式保存在本地。在脚本的第二次执行期间，将加载缓存并从中提取结果。

然而，尽管这种缓存是合适的，但它不允许使用线程。这将需要实现另一个缓存，并使用像 REDIS 这样更健壮的东西。

因此，您可以像上面那样创建一个接口，它将定义所有缓存的框架。现在，您可以创建一个新的缓存实现，而无需更改整个脚本。

要做的另一个改进是管理缓存的有效性，实际上这里缓存并不管理它，您必须手动使缓存无效，在这个简单的例子中没有这样做。

## 结论

在本文中，我们看到了如何使用高级 python 特性和软件工程概念来改进与 API 交互的脚本。希望这对你有帮助。