# Markdown常用语法说明

本文记录关于Markdown纯文本标记语言的常用语法和使用心得。

## 注释（Comment）

Markdown沿用HTML Comment的注释格式：

```
    <!-- This is a comment! -->
```

## 标题（Header）

Markdown支持两种标题的语法，我采用的是类atx形式，即使用1到6个`#`来标注6级标题，对应HTML中的`<h1>`-`<h6>`标签。

```
    # 第一级标题 (H1，常为文档标题)
    ## 第二级标题 (H2)
    ### 第三级标题 (H3)
    #### 第四级标题 (H4)
    ##### 第五级标题 (H5) #####
    ###### 第六级标题 (H6) ######
```

最后两种在标题后加上对应的`#`也是可以的，但是为了简洁通常不用写。

## 分段（Paragraph）

Markdown中的分段需要空行来明示分隔。**建议在块引用（Blockquote）、预格式化（Preformatted code block）、列表（List）、表格（Table）等区块元素的上下插入空行。**

## 符号（Characters）

为了输入Markdown中的标记符号（比如：`#`，`*`等），则需要在符号前面使用反斜杠（`\`）来标注。

空格和tab常用来格式控制，行首插入tab或4个空格表示`<pre>`预格式化，引用、列表的bullet标记符前的tab或空格用于缩进嵌套层级。

Markdown中的普通段落一般顶格开始，没有缩进。如果要缩进，最好使用编辑相应的CSS来实现。

## 水平分隔线（Horizontal Rules）

使用三个以上的星号（\*）或减号（\-）或底线（\_）来建立水平分隔线，对应HTML中的`<hr>`标签。注意行内不能有其他内容，且使用减号时最好在用空格分隔并在上一行空一行。

```
    ---
    ***
    ___
```

## 文本格式（Text Styling）

### 斜体/强调（Italic / Emphasize）

使用一个星号（\*）或下划线（\_）包围文字来实现，对应HTML中的`<i>`/`<em>`标签。

```
    *Italic* and _emphasize_
```

**GFM（Github Flavored Markdown）中的建议是使用只星号来包围斜体，因为C语言等编程语言中常采用下划线定义变量。**

### 加粗（Blod）

使用两个星号（\*）或下划线（\_）包围文字来实现，对应HTML中的`<b>`/`<strong>`标签。

```
    **This** is very __important__.
```

### 别的格式

标准Markdown中没有突出、下划线、删除线、脚标的实现方式，如有相关的需求，可以使用Markdown编辑器来实现，比如[Macdown](https://macdown.uranusjr.com/)、[Haroopad](http://pad.haroopress.com/)。

## 链接（Hyperlink）

Markdown 支持两种形式的超文本链接语法格式：行内式（Inline）和参考式（Reference）两种形式。不管是哪一种，链接文字都是用方括号（square brackets：`[]`）来标记。

### 行内式（Inline）

在一行内构建链接的语法格式为`[text](url)`，HTML的源码为1`<a href="url">text</a>`。如果是要链接到本机资源，可以使用相对路径。

如果要加上链接的title，只要在网址后面用双引号把title文字包起来即可。

```
[Markdown Inline](http://example.com/index.html "Title")
```

### 参考式（Reference）

参考式的链接是在链接文字的括号后面再接上另一个方括号，在第二个方括号里面填入用以辨识链接的标记id，然后在其他另外的地方给出该标记id真正的链接地址。

定义参考refid：`[text][refid]`，定义refid所指的链接：`[refid]:URL`。

refid可以与text一致，从而进一步精简参考链接的书写格式：

```
    This is a [text][] example.
    [text]:URL
    或者
    This is a [text] example.
    [text]:URL
```

`[refid]:URL` 的URL后面可以选择性地用单引号、双引号或是括弧闭包起来标记title。
下面这三种链接的定义都是相同的：

```
    [foo]: http://example.com/ "Optional Title Here"
    [foo]: http://example.com/ 'Optional Title Here'
    [foo]: http://example.com/ (Optional Title Here)
```

## 图片（image）

图片的格式与超链接的形式差不多，只需要在前面加上一个感叹号，其语法格式为：
`![alt_text](url)`，等效的HTML源码为`<img src="url" alt="alt_text" />`，alt\_text可以为空。

## 代码（Code）

### 行内代码（Inline Code）

使用反引号（\` \`）来包围需要标记的代码片段。

### 代码块（Code Blocks）

可以使用在句段的行首插入1个tab或4个空格来表示代码块。
推荐使用GFM扩展的基于YAML标记语言的Fenced Code Block引用语法格式。它以3个反引号来包围代码块，并在第一行的反引号之后加上编程语言的YAML标记。格式如下：

```markdown
    ```python
        some phthon codes.
    ```
```

## 列表（List）

### 无序列表（Unordered List）

在行首使用一个星号（\*）、加号（\+）或减号（\-）加一个空格来作为无序列表的标记。如果需要嵌套效果，则在标记前增加不同长度的tab来实现。

```
    * Apple
    * Orange
    + Pear
    + Gold
    - Meat
    - Beef
```

### 有序列表（Ordered List）

有序列表项目的行首则使用数字加一个英文句点标记。

```
    1. Start
    2. Going
    3. End
```

## 表格（Table）

表格使用`|`来分隔不同的单元格，用`-`来分隔表头和其它行。示例如下：

```
| Left | Center | Right | 
| :--- | :----: | ----：|
| LLLL | CCCCCC | RRRRR |
| LL   | CC     | RR    |
```

效果为：

| Left | Center | Right | 
| :--- | :----: | ----：|
| LLLL | CCCCCC | RRRRR |
| LL   | CC     | RR    |

每行首尾的`|`可以省略，中间的不能省；`|`和`-`的两侧至少要有一个空格分隔；表格内容默认是左对齐，如果不需要自己定义内容的对齐方式，可以将`:`换成`-`。表格中的内容是支持Markdown的行内标记的，比如粗体、链接等。

## 数学公式

如果在行内加入公式，使用`$...$`格式，如果要让公式单独显示一行，则使用格式：`$$...$$`。

这是一个行内公式的样例：$\sum_{i=0}^n i^2 = \frac{(n^2+n)(2n+1)}{6}$

