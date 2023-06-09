# 自然语言处理—从初级到高级(第三部分)

> 原文：<https://towardsdatascience.com/natural-language-processing-beginner-to-advanced-part-3-bbd536a89ecb?source=collection_archive---------27----------------------->

## NLP 项目

## 高级词汇处理——如何处理文本数据中的杂波，以及如何构建自己的拼写校正器。

![](img/f9fc153886b794933599d0a3f931c1c0.png)

图片由[洛伦佐·卡法罗](https://pixabay.com/users/3844328-3844328/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1870721)从[皮克斯拜](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=1870721)拍摄

在“NLP 项目”系列的[前一部分](/lexical-processing-for-nlp-basic-9fd9b7529d06)中，我们学习了所有基本的词汇处理技术，比如去除停用词、标记化、词干化和词条化。

即使经过了所有这些预处理步骤，文本数据中仍然存在大量噪声。例如，由于错误和选择而发生的拼写错误(非正式的词，如' lol '，' u '，' gud '等。).此外，由于发音不同(例如 Mumbai，Bombay)而出现的单词拼写变化问题。

我们在上一部分中谈到的两种方法——词干化和词汇化——都是称为**规范化**的技术的一部分。基本上，规范化意味着将一个单词简化为它的基本形式。

有些情况下，我们不能仅仅通过词干化和词汇化来规范化一个单词。因此，我们需要另一种技术来正确地规范化单词。例如，如果单词“allowing”被拼错为“alowing ”,那么在阻止拼错的单词后，我们将有一个多余的标记“alow ”,并且词条化甚至不起作用，因为它只对正确的词典拼写起作用。

同样的问题也存在于不同方言中相同单词的发音上。例如，英式英语中使用的单词“幽默”在美式英语中被拼写为“幽默”。这两种拼写都是正确的，但是在词干之后，当用于形式“幽默”和“幽默”时，它们会给出两种不同的基本形式。

# 语音散列法

有些词在不同的语言中有不同的发音。因此，它们最终的写法是不同的。例如，一个常见的印度姓氏如“Srivastava”也被拼写为“Shrivastava”、“Shrivastav”或“Srivastav”。因此，我们必须把一个特定单词的所有形式简化为一个单一的普通单词。

为了达到这个目的，我们将了解一种叫做语音哈希的技术。语音散列法将相同的**音素**(声音的最小单位)组合到一个桶中，并为所有变体赋予相同的散列码。所以，单词“color”和“colour”有相同的代码。

> 语音哈希是一种用于将具有不同变体但语音特征相同(即发音相同)的单词进行规范化的技术。

现在， **Soundexes** 是可以用来计算给定单词的哈希码的算法。语音哈希使用这些 Soundex 算法。算法因语言而异。美国的 Soundex 是最流行的 Soundex 算法，我们将使用它。此外，输入的单词来自哪种语言并不重要——只要单词听起来相似，它们就会获得相同的哈希代码。

拼音哈希是一个**四字**码。因此，让我们通过应用以下步骤来计算单词“Chennai”的散列码(也称为 Soundex)

1.  保留单词的首字母——Soundex 的基本原理是，英语发音取决于辅音的首字母和模式。所以，C 变成了第一个字母。
2.  去掉所有的元音。所以我们现在有了“CHNN”。
3.  用数字替换辅音，如下所示(第一个字母后)

*   b，f，p，v → 1
*   c，g，j，k，q，s，x，z → 2
*   d，t → 3
*   l → 4
*   m，n → 5
*   r → 6
*   h、w、y→未编码/已移除

编码后，代码变成 C55。

4.如果原姓名中有两个或两个以上同号字母相邻(步骤 1 之前)，只保留首字母；同样，由“h”或“w”分隔的具有相同数字的两个字母被编码为单个数字，而由元音分隔的这种字母被编码两次。这条规则也适用于第一个字母。现在，我们有两个 5，所以我们将它们合并成一个，得到 C5。

5.如果单词中的字母太少，我们无法分配三个数字，请添加零，直到有三个数字。如果我们有四个或更多的数字，只保留前三个。由于我们只有一个字母和一个数字，我们将在编码的末尾添加两个零，使其成为一个四字符代码。因此，我们得到 C500 作为“钦奈”的最终代码。

因此，我们看到像“Bengaluru”和“Bangalore”这样的城市名称的 Soundex 代码是相同的，B524，这就是我们的目标。

所以，我们看到了如何处理一个特定单词的不同发音。接下来，让我们看看如何处理拼写错误。

# 编辑距离

简而言之，编辑距离是将一个字符串转换为另一个字符串所需的最小编辑次数，即给定字符串到目标字符串。

现在，你一定想知道什么是编辑。因此，可能的编辑如下:-

*   **将一个字符插入给定的字符串。要将拼写错误的单词“Aquire”转换为正确的拼写“Acquire ”,我们需要在给定的拼写错误的字符串中插入字符“c”。**
*   从给定的字符串中删除一个字符。要将“necessary”转换为“必需的”，我们需要从给定的字符串中删除多余的“c”。
*   给定字符串中字符的替换。为了将 Absense 转换成正确的形式 Absense，我们需要用字符 c 代替字符 s。

最常见的编辑距离算法是 **Levenshtein 编辑距离**，你可以在这里详细了解[。还有另一个编辑选项叫做“转置操作”，你可以交换给定字符串的两个相邻字符。但是，该操作仅在](https://medium.com/@ethannam/understanding-the-levenshtein-distance-equation-for-beginners-c4285a5604f0)[**damer au-Levenshtein**](https://en.wikipedia.org/wiki/Damerau%E2%80%93Levenshtein_distance)编辑距离中可用。

# 拼写纠正器

拼写校正器是一个广泛使用的应用程序。如果您在电话上启用了“自动更正”功能，不正确的拼写将被正确的拼写替换。另一个例子是，当你使用谷歌这样的搜索引擎搜索任何东西，却打错了一个单词，它会提示正确的单词。拼写纠正是词汇处理的重要组成部分。在许多应用中，拼写校正形成了初始预处理层。

我们看到了如何计算两个单词之间的编辑距离。现在，我们将使用编辑距离的概念来制作拼写校正器。我们现在来看看如何制作著名的 **Norvig** 法术修正器。

我们需要大量拼写正确的文本。这个文本语料库也将作为我们的拼写校正器的字典搜索。在这里，文本“big.txt”的大型语料库只不过是一本书。这是古腾堡计划网站[上以文本格式呈现的《夏洛克·福尔摩斯历险记》一书。](https://www.gutenberg.org/)

```
# function to tokenise words
def words(document):
 “Convert text to lower case and tokenise the document”
 return re.findall(r’\w+’, document.lower())# create a frequency table of all the words of the document
all_words = Counter(words(open('big.txt').read()))
```

我们将使用五个主要函数来查找单词的正确拼写，它们如下:

1.  **edits_one()** :函数创建与输入单词相距一个编辑距离的所有可能单词。这个函数创建的大多数单词都是垃圾，即它们不是有效的英语单词。例如，如果我们将单词' laern '(单词' learn '的拼写错误)传递给 edits_one()，它将创建一个列表，其中将出现单词' lgern '，因为它是远离单词' laern '的编辑。但这不是一个英语单词。只有一部分单词是真正的英语单词。

```
def edits_one(word):
 “Create all edits that are one edit away from `word`.”
 alphabets = ‘abcdefghijklmnopqrstuvwxyz’
 splits = [(word[:i], word[i:]) for i in range(len(word) + 1)]
 deletes = [left + right[1:] for left, right in splits if right]
 inserts = [left + c + right for left, right in splits for c in alphabets]
 replaces = [left + c + right[1:] for left, right in splits if right for c in alphabets]
 transposes = [left + right[1] + right[0] + right[2:] for left, right in splits if len(right)>1]
 return set(deletes + inserts + replaces + transposes)
```

2. **edits_two()** :函数创建一个所有可能的单词的列表，这些单词与输入单词相差两个编辑点。这些话大部分也会是垃圾。

```
def edits_two(word):
 “Create all edits that are two edits away from `word`.”
 return (e2 for e1 in edits_one(word) for e2 in edits_one(e1))
```

3. **known():** 函数从给定单词列表中过滤出有效的英语单词。它使用频率分布作为使用种子文档创建的字典。如果使用 edits_one()和 edits_two()创建的单词不在词典中，它们将被丢弃。

```
def known(words):
 “The subset of `words` that appear in the `all_words`.”
 return set(word for word in words if word in all_words)
```

4. **possible_corrections():** 该函数获取输入单词，并使用上述三个函数返回给定输入单词的正确拼写。首先，它检查输入单词的拼写，如果拼写是正确的，也就是说，如果该单词存在于字典中，它不返回拼写建议，因为它已经是一个正确的字典单词。

如果拼写不正确，它将搜索与输入单词相差一个编辑的每个词典单词，并返回它们的列表。如果词典中没有与给定单词相距一个编辑点的单词，那么它将搜索相距两个编辑点的所有词典单词，并返回它们的列表。如果没有两个编辑之外的单词，输入的单词被返回，这意味着拼写纠正器找不到替代词。

```
def possible_corrections(word):
 “Generate possible spelling corrections for word.”
 return (known([word]) or known(edits_one(word)) or known(edits_two(word)) or [word])
```

5.**prob():**prob()函数将创建与每个建议的正确拼写相关联的概率，并返回具有最高概率的拼写，或者我们可以说，它采用建议的正确拼写并返回在我们的文本语料库中的输入单词中最频繁出现的拼写。

这就是为什么我们需要一个大的文本语料库，而不是一本字典。字典只包含所有正确英语单词的列表。但是，文本语料库不仅包含所有正确的单词，还可以用来创建所有这些单词的频率分布。

```
def prob(word, N=sum(all_words.values())): 
 “Probability of `word`: Number of appearances of ‘word’ / total number of tokens”
 return all_words[word] / N
```

现在，我们几乎完成了拼写校正器的构建。我们只需要把所有的代码片段放在一起，并把它们包装在一个新的函数中，这个函数使用到目前为止创建的所有函数。

```
def spell_check(word):
 “Print the most probable spelling correction for `word` out of all the `possible_corrections`”
 correct_word = max(possible_corrections(word), key=prob)
 if correct_word != word:
 return “Did you mean “ + correct_word + “?”
 else:
 return “Correct spelling.”
```

瞧啊。我们已经成功地创建了一个简单却非常有效的拼写纠正器。我们现在可以使用它来纠正任何给定文本语料库的拼写。

这就是第三部分的内容。我们已经在第 2 部分和第 3 部分[中介绍了整个词汇处理过程。现在，我们将进入 NLP 的下一个主要部分——句法处理。干杯！](/lexical-processing-for-nlp-basic-9fd9b7529d06)