# 使用 Python 原生编译 Julia 代码

> 原文：<https://towardsdatascience.com/run-native-julia-code-with-python-92d3e1079385?source=collection_archive---------12----------------------->

## 通过切换语言来加速 Python

![](img/9a445889aa48ff069f30d90776d09ca4.png)

我经常讨论使用 Julia 的好处，因为有很多好处。Julia 是一种可扩展的、高性能的高级语言，易于学习，几乎可以完成任何工作。对于数据科学家来说尤其如此，因为 Julia 的重心是统计计算和函数程序。在 Julia 的核心，它是一种为科学家用数据做统计而创造的语言，这种直接的意图使它在特定的事情上非常棒。

虽然我可以花很多年谈论 Julia 如何更快，具有更好的浮点精度，并且打字非常简单，但这不是我今天在这里的原因。虽然我已经表达了我的担忧，也可能夸大了我对朱莉娅的喜爱，但有一个大话题我还没有和朱莉娅谈过:

> 多才多艺

使用 Python 语言的一个巨大好处是 Python 是通用的。如果你不想使用 web 请求，可能有一个包装器，如果你想把时间戳从 Unix 转换成 UTC，有一个库。这是一个很大的好处，因为这意味着你的语言将永远支持你的工具。我已经提到过 Julia 的包是它最大的缺陷，但尽管如此，Julia 最初是在 2012 年发布的，也就是 8 年前。朱莉娅反驳说:

> 可翻译。

![](img/16c5ba182df7f4fb83342124a0a24a4d.png)

首先，我们有令人惊奇的包 PyCall.jl，它允许调用 Python 包，甚至在虚拟环境中。在数据科学领域，能够调用数百万个 Python 包是一件大事。

布丁中真正的水果是，反过来也是可能的。没错，从 Python 本地运行 Julia 非常容易。这很重要，因为我们都知道 Python 有时会相当慢。我承认，在大多数情况下，Python 很棒，但是当 Python 让你失望时，它真的会让你进退两难，不知道下一步该做什么。

PyJulia 或 julia.py 允许您发送类似 SQL 查询的代码行，并为实际返回标识一个返回变量。简而言之，你可以通过向 Julia 编译器发送字符串来运行 Python 中的 Julia。当然，第一步是从您的包管理器中获取 Julia，我将使用 APT。

```
sudo apt-get install julia
```

现在它就像进入朱莉娅 REPL，然后安装 PyCall 与]或使用 Pkg 一样简单。

```
julia
julia> using Pkg; Pkg.add("PyCall")
(or)
julia> ]
pkg> add "PyCall"
```

对于一些 Julia 包，包括 PyCall，我推荐构建代码:

```
julia> ]
pkg> build "PyCall"
```

现在，用退格键退出 Pkg，按 ctrl/command+D 退出朱莉娅 press。我们现在可以用 pip 安装我们的 Python 包了，我将使用 pip3。

```
sudo pip3 install julia
```

既然我们所有的依赖关系都得到了满足，我们就可以跳到笔记本上进行尝试了！第一步是使用 Julia 库中的安装方法:

```
import julia as jl
jl.install()
```

现在我们可以导入 Julia 可执行文件，并用它运行字符串代码！

```
from julia import Julia
jl = Julia()
average = jl.run("using Lathe.stats: mean; array = [1,5,4,5,6]; m = mean(array); return(m)")
```

> 所以…酷！

但这意味着什么呢？嗯，任何用 Julia 开发的包都可以用 Python 开发。不仅如此，该包还可以在 R 中与 JuliaCall.R 一起使用。我已经开始为 Julia 的车床机器学习模块开发包装器，这些包装器将在 native Julia 下与 Python 和 R 一起使用。我真的很高兴 Julia 代码既更快，又同时使该包在最流行的统计语言中通用。这对 Julia 开发者来说是一个很大的好处，因为我们不必为了维护一个 Python 和 R 版本而重写代码。当然，随之而来的是在编译时使用 Julia 而不是 Python 的实际好处。

# 下降趋势

在计算中没有什么是如此简单的，所以用这种了不起的方法翻译代码，也有一些不幸的问题。虽然很少，但我承认必须安装 Julia 和 PyCall 依赖项有点乏味，特别是对于一个以前从未使用过 Julia 的 Python 包的最终用户来说。此外，Julia 的版本控制和兼容性给这个包带来了很大的问题，让 PyJulia 运行起来可能会很困难。我遇到的问题主要是在 Unix 所有权中，编译器在我的非所有目录(由 root 所有)中，由于权限被拒绝，我将得到退出状态 1。

这当然是通过在我的 Python 位置上使用 chown 并在 Julia 的情况下做同样的事情来解决的。

除了这个问题，还有它的写作方式，有点乏味。诚实地说，通过字符串发送单行代码并不是最理想的，如果你打算在代码中使用引号，并使用字符串，那么在 Python 中的“、”和”之间导航将会非常困难。没什么大不了的，但绝对是需要注意的。

# 结论

总之，多才多艺是朱莉娅的一大优势。Julia 代码不仅速度快，而且扩展性极强，还可以写成其他语言。这是一个很大的优势，因为您的 mill Julia 包可以在一个包装器中轻松运行，并且当它在本地系统上更新时，可以与原始的 Julia 包一致地更新，所以…酷！我非常期待能让 R 和 Python 都了解 Lathe，这样更多的人就能使用 Lathe，并希望能喜欢上它。