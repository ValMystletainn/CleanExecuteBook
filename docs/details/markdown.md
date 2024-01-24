# Markdown 语法支持

本节主要罗列 JupyterBook 所支持的 Markdown 语法，供参考查阅。

## 标准 Markdown (CommonMark)

事实上，这个世界并没有标准的 Markdown。 Markdown 最早是由 John Gruber 在 2004 年开发的一种简单的标记语言，用于尽可能地屏蔽样式、标签，快速书写 HTML 内容，并为之配套了一个 Perl 编写的转换器。
但在这之后有很多的 Markdown 解析器项目如雨后春笋冒了出来。
这些项目也往往想实现更多功能。
从而经过很多年的发展，便出现了很多类型的 Markdown 方言。
这样的发展历程使得 Markdown 没有类似传统的编程语言或者 LaTeX 这样的标记语言的中心化的“标准委员会”。

在十多年之后，CommonMark 并应运而生。
它的目标是通过观察总结主流的 Markdown 实现，提取出它们都支持的“最小语法规则集”，来作为后补的 Markdown 语言规范。
进而其他的 Markdown 实现都可以视为 CommonMark 和一些扩展功能。

作为文字记录的主打项目， JupyterBook 是完全支持 CommonMark 的所有语法规则的，罗列如下：


### 平文撰写

``````{list-table}
:header-rows: 1
:widths: 1 1 1

* - 语法
  - 效果
  - 注记

* - ```md
    一行内的句子
    以及紧邻行的句子都会被视为一个段落

    空行后，自然新起一段，在显示时换行。
    ```
  - 一行内的句子
    以及紧邻行的句子都会被视为一个段落

    空行后，自然新起一段，在显示时换行。
  - 对于修改频繁的文档，尽量遵循一行一个句子的写作准则，同时保证渲染效果和源文档追踪友好。
  
    当然，对于不按这个准则编写的文档，把 `git diff` 调成 word level 来做修改比较，也是可以的。

* - ```md
    *Italic 被倾斜的字*
    ```
  - *Italic 被倾斜的字*
  - 中文传统并没有斜体这类格式。
    
    西文斜体常用于表示文章标题等事物，类似书名号的作用。

* - ```md
    **被加粗的字**
    ```
  - **被加粗的字**
  - 

* - ```md
    > 引用块，块内可换行
    > 
    > 可混用其他格式，举例：**加粗**
    ```
  - > 引用块，块内可换行
    > 
    > 可混用其他格式，举例：**加粗**
  - 引用块是直接对应 `<blockquote>` 这个 HTML 原生标签。
    
    这个标签是从纸质书中的，长摘录、名人名言引申而来的。
    它的显示标准不定。
    通常为，框起的不同底色的文本。

``````

### 标题

``````{list-table}
:header-rows: 1
:widths: 1 1 1

* - 语法
  - 效果
  - 注记

* - ```md
    # 一级标题
    ## 二级标题
    ### 三级标题
    #### 四级标题
    ##### 五级标题
    ###### 六级标题
    ```
  - # 一级标题

  - 几个 `#`就是几级标题，一个文档开头的一级标题，会默认作为转码成的网页，以及在左侧目录的标题
``````

### 列表

``````{list-table}
:header-rows: 1
:widths: 1 1 1

* - 语法
  - 效果
  - 注记

* - ```md
    - 无序列表元素1
    - 无序列表元素2
    - 无序列表元素3
    ```
  - - 无序列表元素1
    - 无序列表元素2
    - 无序列表元素3

  - 起始的 `-` 也可以换为 `*`

* - ```md
    1. 有序列表元素1
    2. 有序列表元素2
    3. 有序列表元素3
    ```
  - 1. 有序列表元素1
    2. 有序列表元素2
    3. 有序列表元素3

  - 在部分的 Markdown 实现中（当然包括本方案的实现），源码里的数字无序按需（比如都用 `1.`），渲染时会帮你自动排序
    但为了兼容性和可读性，还是建议用 `1.`, `2.`, `3.` 按序书写。

    起始的 `1.` 也可以换为 `1)`
``````

### 链接

``````{list-table}
:header-rows: 1
:widths: 1 1 1

* - 语法
  - 效果
  - 注记

* - ```md
    [显示的文字](http://www.baidu.com)

    [**粗体百度**](http://www.baidu.com)
    ```
  - [显示的文字](http://www.baidu.com)

    [**粗体百度**](http://www.baidu.com)
  - 显示的文字可以复合其他 Markdown 语法，如示例第二行

* - ```md
    ![图片加载不出时的文字](../logo.png)
    ```
  - ![图片加载不出时的文字](../logo.png)

    ![markdonw icon](https://commonmark.org/help/images/favicon.png)
  - 图片的地址可以是本地地址，也可以是网络上的地址（如第二张图）。

``````


### 代码段


``````{list-table}
:header-rows: 1
:widths: 1 1 1

* - 语法
  - 效果
  - 注记

* - ````md
    行内代码段，`variable`

    ```
    # 代码块
    print("Hello World!")
    ```
    ````
  - 行内代码段，`variable`

    ```
    # 代码块
    print("Hello World!")
    ```
  - 建议用行内代码来书写命令、变量名；代码块写代码片段

``````

### 分隔符

用独立成行的 `---` 或者 `***` 添加一个分隔符，直接对应于 `<hr>` 这个 HTML tag。
在本文档的使用场景下，不常见。


## MyST Markdown

### 在 CommonMark 上的拓展

这些扩展内容，基本是直接从前面罗列的 CommonMark 语法中更进一步。
往往已经被很多主流的其他 Markdown 标准所实现。
使用这些特性时，你不太需要担心你 Markdown 文件迁移到其他渲染标准下出现不兼容的问题。

#### 链接

图片链接插入的语法，也同时支持视频插入

#### 代码块

代码块可以通过在起头的 \``` 后添加语言的名字来决定代码块的高亮模式。
下表展示的是 C 和 Python 混写的一个代码段，可以看到在不同的代码块备注下，渲染后，产生了不同的高亮。

``````{list-table}
:header-rows: 1
:widths: 1 1

* - 语法
  - 效果

* - ````md
    ```c
    #include <stdio.h>
    int main();

    def main():
        pass
    ```

    ```python
    #include <stdio.h>
    int main();

    def main():
        pass
    ```
    ````
  - ```c
    #include <stdio.h>
    int main();

    def main():
        pass
    ```

    ```python
    #include <stdio.h>
    int main();

    def main():
        pass
    ```
``````

#### 数学公式

用 `$` 符号环绕来开启数学环境，开启后输入相应指令就能获得公式。
在本文档的构建配置中使用的是 mathjax 来做渲染，它实现了 LaTeX 中比较常见的数学指令。

``````{list-table}
:header-rows: 1
:widths: 1 1

* - 语法
  - 效果

* - ```md
    行内的公式：$E = mc^2$, 其中 $E$ 代表能量
    ```
  - 行内的公式：$E = mc^2$, 其中 $E$ 代表能量


* 
  - ```md
    行间的公式
    $$
    \begin{aligned}
      \min_{x} & \quad & f(x) + g(y) \\
      \text{s.t.} & \quad & x \in \mathbb{R}^n_+
    \end{aligned}
    $$
    ```
  - 行间的公式

    $$
    \begin{aligned}
      \min_{x} & \quad f(x) + g(y) \\
      \text{s.t.} & \quad x \in \mathbb{R}^n_+
    \end{aligned}
    $$ 

``````


#### 表格

支持 [Github 风格 Markdown 语法](https://github.github.com/gfm/#tables-extension-) 所提出的表格形式。
可做简单列对齐调整。
适合书写“没有单元格合并”的形式的表格。

``````{list-table}
:header-rows: 1
:widths: 1 1

* - 语法
  - 效果

* - ```md
    | foo | bar |
    | --- | --- |
    | baz | bim |
    ```
  - | foo | bar |
    | --- | --- |
    | baz | bim |

* - ```md
    | left | center | right |
    | :--- | :----: | ----: |
    | a    | b      | c     |
    ```
  - | left | center | right |
    | :--- | :----: | ----: |
    | a    | b      | c     |

``````

#### 列表

支持打钩打叉的 Task List 语法

``````{list-table}
:header-rows: 1
:widths: 1 1

* - 语法
  - 效果

* - ```md
    - [x] TODO1
    - [ ] TODO2

    1. [ ] TODO3
    2. [ ] TODO4
    ``` 
  - - [x] TODO1
    - [ ] TODO2

    1. [x] TODO3
    2. [ ] TODO4

``````

#### 平文撰写

可以用 `[^脚注变量名]` 写在需要添加脚注的地方。
然后再在源码中合适的地方（比如这一自然段的附近，方便维护）用 `[^脚注变量名]:` 写明具体脚注的内容。这个脚注会被渲染到页面最后的位置。


``````{list-table}
:header-rows: 1
:widths: 1 1

* - 语法
  - 效果

* - ```md
    行文脚注[^foot1]，接着行文

    [^foot1]: 一个样例脚注
    ```
  
  - 行文脚注[^foot1]，接着行文

    [^foot1]: 一个样例脚注

* - ```md
    行文长脚注[^foot2]，接着行文

    [^foot2]: 脚注可以在 4 个以上的缩进下换行
        可以写任意的 Markdown 内容。
        用于编写复杂内容

        **加粗换行的脚注2的内容**
    ```
  
  - 行文长脚注[^foot2]，接着行文

    [^foot2]: 脚注可以在 4 个以上的缩进下换行
        可以写任意的 Markdown 内容。
        用于编写复杂内容

        **加粗换行的脚注2的内容**

``````

### 指令 (Directive)

指令，是继承自 Sphinx RST 的语法。可以类比理解为 LaTeX 的环境，通过展开一个特殊的环境把里面的环境中的文字，转义成相应的内容。

抽象地来说，指令是服从这样语法格式的语句，可以看到它和代码块有着很近似的语法。

``````md
```{指令名} 环境的其他配置按位置入的参数
:参数形参名: 参数值

指令环境下的约定的其他代码

```
``````

以下列举一些指令，更多的指令可见 [JupyterBook 的语法列表](https://jupyterbook.org/en/stable/reference/cheatsheet.html) 和 [Sphinx 的指令列表](https://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html#directives)

**注意**：还有常规的数学公式、图片、表格、引用文件中的代码、转为 Jupyter 运行的代码块，都可以以指令环境来进行，这些部分放在交叉引用、 Jupyter 等小节或模块来进行描述。

``````{list-table}
:header-rows: 1
:widths: 1 1 1

* - 语法
  - 效果
  - 注记

* - ````md
    ```{admonition} Admonition 的标题
    :class: note

    框内的文字
    ```

    ```{admonition} warning
    :class: warning, dropdown

    默认折叠的 warning
    ````
  - ```{admonition} Admonition 的标题
    :class: note

    框内的文字
    ```

    ```{admonition} warning
    :class: warning, dropdown

    默认折叠的 warning
    ```
  - Admonition 提供了很多个种类，修改的是方框左上角的符号和方框的颜色。
    
    包括 admonition, attention, caution, danger, error, hint, important, note, tip, warning 等

    比较特殊的 class 还有 dropdown，是一个额外的 class 用来把  Admonition 默认折叠
  
* - `````md
    ````{grid}
    ```{grid-item}
    :outline:
    :columns: 3
    A
    ```

    ```{grid-item}
    :outline:
    :columns: 9
    B, **Bold**
    ```

    ```{grid-item}
    :outline:
    :columns: 12
    C, **Bold**
    ```
    ````
    `````
  - ````{grid}

    ```{grid-item}
    :outline:
    :columns: 3
    A
    ```

    ```{grid-item}
    :outline:
    :columns: 9
    B, **Bold**
    ```

    ```{grid-item}
    :outline:
    :columns: 12
    C, **Bold**
    ```

    ````
  - grid 默认的总宽度是 12，会根据所给定的 grid-item 的宽度来决定如何排版。

* - ````md
    ```{prf-algorithm} 算法名
    :label: algo-xx

    **输入** xxxx
    **输出** yyyy

    过程
    ```
    ````
  - ```{prf:algorithm} 算法名
    :label: algo-xx

    **输入** xxxx

    **输出** yyyy

    过程
    ```
  - 这是由 sphinx-proof 插件提供的环境。提供的环境涵盖定理，公理，证明，推论，算法等等。可见 [包的文档](https://sphinx-proof.readthedocs.io/en/latest/syntax.html#proofs)

* - `````md
    ````{card} 卡片标题
    卡片上头
    ^^^
    卡片主体
    +++
    卡片脚注
    ````
    `````
  - ````{card} 卡片标题
    卡片上头
    ^^^
    卡片主体
    +++
    卡片脚注
    ````
  - 标题、上头、脚注都是可省略的内容。省略上头/脚注时，不写 `^^^` 或 `+++` 即可。

    还有更多配置选项可见 [文档](https://sphinx-design.readthedocs.io/en/sbt-theme/cards.html)

* - `````md
    ````{tab-set}
    ```{tab-item} label1
    :sync: key1
    内容1
    ```
    ```{tab-item} label2
    :sync: key2
    内容2
    ```
    ````

    ````{tab-set}
    ```{tab-item} o_label3
    o 内容3
    ```
    ```{tab-item} o_label1
    :sync: key1
    o 内容1
    ```
    ````
    `````
  - ````{tab-set}
    ```{tab-item} label1
    :sync: key1
    内容1
    ```
    ```{tab-item} label2
    :sync: key2
    内容2
    ```
    ````

    ````{tab-set}
    ```{tab-item} o_label3
    o 内容3
    ```
    ```{tab-item} o_label1
    :sync: key1
    o 内容1
    ```
    ````
  - `sync` 选项的原理是，当切换到有这个属性的标签时，发送一个事件，这个事件会被所有拥有这个属性的标签响应，并切换到这一页。
    自然地，当一个标签组没有含这个属性的标签页，该组不会发生切换；或者没有 `sync` 属性的标签被点击时没有额外的响应。
* - ````md
    ```{literalinclude} ../_toc.yml
    :language: YAML
    :linenos: True
    :lineno-match: true
    :lines: 3-4
    :emphasize-lines: 2
    ```
    ```` 
  - ```{literalinclude} ../_toc.yml
    :language: YAML
    :linenos: True
    :lineno-match: true
    :lines: 3-4
    :emphasize-lines: 2
    ```
  - 用于显示很长的代码文件的部分内容，`linenos` 为 `line number show`, `lineno-match` 是说使用原始的文件意义下的行号（但这里有 bug 的是，emphasize 是用截断后的行号来标记的）
``````



### 图注表注

常规的 Markdown 插图并不支持图注，和再引用。
常见的 Markdown 扩展语法的表格插入，也不支持表注和再引用。

但在比较学术的场景下，给这两个东西添加一个 caption, 给它们编号，以及再引用都是非常常见的需求。

这里就需要指令环境下的图表插入功能，通过指令环境的其他入参来指定 label (一般在 name 这个参数下设定) 和 caption (可能是正文内容，可能是指令旁的参数).



``````{list-table}
:header-rows: 1
:widths: 1 1

* - 语法
  - 效果

* - ````md
    ```{figure} ../logo.png
    :name: my-fig-ref

    图注
    ```
    ````

  - ```{figure} ../logo.png
    :name: my-fig-ref

    图注
    ```

* - ````md
    ```{table} 表注
    :name: my-table-ref

    | 真的表 | header 2 |
    |---|---|
    | 3 | 4 |
    ```
    ````
  - ```{table} 表注
    :name: my-table-ref

    | 真的表 | header 2 |
    |---|---|
    | 3 | 4 |
    ```

* - ````md
    ```{math}
    :name: my-eq-ref

    a + b = c
    ```
    ````
  - ```{math}
    :name: my-eq-ref
    
    a + b = c
    ```
``````

图片环境还可以设置更精细的缩放，对齐方式等，见 [文档](https://jupyterbook.org/en/stable/content/figures.html?highlight=list-table#figure-parameters)


### 交叉引用

引用，可以用行内的 `` {ref}`label-text` `` 的语句来引用，当然也有引申的语法，来自定义引用编号，引用后的文本格式。
见下表：

| 源码                                            | 效果                                    |
|-------------------------------------------------|-----------------------------------------|
| `` 引用图片 {ref}`my-fig-ref` ``                | 引用图片 {ref}`my-fig-ref`               |
| `` 引用 [](my-fig-ref) ``                       | 引用 [](my-fig-ref)                     |
| `` 引用 [自定义的所有链接文本](my-fig-ref) `` | 引用 [自定义的所有链接文本](my-fig-ref)       |
| `` 数字引用 {numref}`my-fig-ref` ``            | 数字引用 {numref}`my-fig-ref`             |
| `` 数字引用 {numref}`自定义文本 %s 后缀 <my-fig-ref>` `` | 数字引用 {numref}`自定义文本 %s 后缀 <my-fig-ref>` |


同样，引用表也是可以的，比如 {numref}`my-table-ref`。

引用公式的语法比较特殊是 `` {eq}`label` ``, 会拿到括号编号的数字，前缀的字得自己打（比如常见的 式xx 的“式”字）

引用 bibtex 中的文章的语法和 LaTeX 比较相似，在设置中指定所需要的参考的一个或一组 `.bib` 文件，然后用类似的 `` {cite}`bib 项目开头` `` 或  `` {cite加料}`bib 项目开头` `` 来进行引用。
比如：

- `` {cite}`vaswani2017attention` `` 是 {cite}`vaswani2017attention`
- `` {cite:t}`vaswani2017attention` `` 是 {cite:t}`vaswani2017attention`
- `` {cite:authorpar}`vaswani2017attention` `` 是 {cite:authorpar}`vaswani2017attention`


### 角色 (Role)

上面其实已经接触到了 Role 这个设定，可以看成一个行内的指令，主要都是用来表示特殊的引用。

## References

```{bibliography}
:style: unsrt
:filter: docname in docnames
```

## 脚注

