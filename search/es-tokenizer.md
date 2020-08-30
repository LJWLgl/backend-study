## ES官方支持的Tokenizer
### Char Group Tokenizer
`char_group`定义一个字符集，每当遇到其中的一个字符，就会生成一个新的token，它比`pattern_tokenizer`的开销要小，所以在简单场景下可以优先使用`char_group`。
**参数**
- tokenize_on_chars：自定义字符串集，如“-”，或者es已支持的字符集，`whitespace`，` letter`， `digit`， `punctuation`，`symbol`等。

详细请参考[analysis-chargroup-tokenizer](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis-chargroup-tokenizer.html)

### Classic Tokenizer

`classic`分词器是基于语法的英语分词器，适用于英语文档，大多数情况下，它可以识别出首字母的缩写，公司名称，邮箱地址，ip等，`classic`分词器更适用于英语，其它语言表现不佳，以下几点是它分词依据：
- 一般它会依据标点符号拆词，但是不带空格的“'”号，则不会被拆分；
- 一般连字符也会作为分隔符，但是如果文本中若包含数字，则会被识别为一个整体；
- 它会识别email和ip地址为一个token；

**参数**

- max_token_length： 每个token最大长度，超过长度会被截取
详细请参考[analysis-classic-tokenizer](https://www.elastic.co/guide/en/elasticsearch/reference/7.7/analysis-classic-tokenizer.html)

### Edge n-gram tokenizer
`edge ngram`分词器在遇到一系列特殊字符时会将文本分割成单词，然后锚定单词的首字符输出ngram词，`edge-ngram`对于搜索类查询非常有用。当需要按类型搜索具有广为人知的顺序的文本时，例如电影或歌曲标题，`completion suggester`是比`edge ngram`更有效的选择，`edge ngram`在尝试自动补充可以按任何顺序出现的单词时更具优势。

**参数**
- min_gram：gram时最小长度，即滑动窗口最小长度，默认为1；
- max_gram：gram时最大长度，即滑动窗口最大长度，默认为2；
- token_chars：表示应在`tokens`中的字符集，ES将分割不在其中的字符，默认是“[]”，即保留所有字
  符，指定的字符集可以是：
  - letter：字母，比如a, b, ï or 京；
  - digit：数字，比如3或7；
  - whitespace：空格符，比如空格或者换行符\n；
  - punctuation：标点，比如!或"；
  - symbol：符号，比如$或√；
- custom_token_chars（7.6新增参数）：自定义字符集
- 详细请参考[analysis-edgengram-tokenizer](https://www.elastic.co/guide/en/elasticsearch/reference/7.7/analysis-edgengram-tokenizer.html#analysis-edgengram-tokenizer)
### Standard Tokenizer

standard分词器使用Unicode文本分割算法（定义来源于 [Unicode Standard Annex #29](http://unicode.org/reports/tr29/)）来寻找单词之间的界限，并且输出所有界限之间的内容。由于是基于Unicode分词，standard可以很好的处理混合语言，特别是西方语言。

**参数**
- max_token_length： 每个token最大长度，超过长度会被截取

## 参考
- [Text analysis](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis.html)
- [ES分析器](https://blog.csdn.net/jacksonary/article/details/83902325)

