---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

# JupyterNotebook 渲染支持


## 预设置

可以直接将 `.ipynb` 作为文件写入 `_toc.yml`, 然后就能进行转换。
使用 `.ipynb` 文件的时候，最开始的 Markdown Cell 的一级标题，会被当为转码后的标题。

`.md` 也可以通过 JupyterText 的方式转换为 JupyterNotebook，然后执行。这被 JupyterBook 的开发团队称为 [MyST-NB](https://myst-nb.readthedocs.io/en/latest/).
比较快速的设置方法是包括：

1. 在文件最开始，设置前导的 yaml 区，指定转码的格式，和所用的 kernel 的名字
2. 在相应的位置，插入 `{code-cell}` 的命令，写相应的代码。这些代码会在发布成网页时执行。

本文的前导 yaml 区和相应的注释如下：

```md
---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---
```

尝试输入一个 `{code-cell}`：

````md
```{code-cell} ipython3
print("Hello world!")
```
````

会得到如下的原始代码和结果：

```{code-cell} ipython3
print("Hello world!")
```

## 代码块设置

`{code-cell}` 里的一个可选参数是 tags，可传入一个列表，来控制转码后渲染网页的行为。
如果是用 `.ipynb` 也可以通过设置对应的 cell tag 为相应的字符串列表完成。

- `hide-input`: 用于折叠输入代码
- `hide-output`: 用于折叠输出结果
- `hide-cell`: 用于折叠输入和输出
- `remove-input`: 直接不渲染输入代码
- `remove-output`: 直接不渲染输出结果
- `remove-cell`: 直接不渲染输入输出
- `output_scroll`: 让输出可滚轮翻页

如果运行代码是一个作图代码，可以在代码块最开始添加 yaml 前导区

```md
---
mystnb:
  figure:
    caption: 标题
    name: 引用的 label
    ...
---
```

从而让输出的图像，像正常插入的图像一样，有图注，能被引用。

## 交互式运行

### 将变量“黏贴到”行文中

MyST-NB 提供了一个 Python 函数 glue, `glue(text_name: str, object: Any)`，来在代码运行后记录任意变量。
在正文中，使用 `glue:subcommand` 的指令或者角色，就可以将之前用 `text_name` 记录的变量名，用不同的形式呈现出来

```{code-cell} ipython3
from myst_nb import glue
my_variable = "here is some text!"
glue("the_text", my_variable)
```

这里再使用 `` {glue:text}`the_text` ``, 就能得到一个一直和输出随动的结果 {glue:text}`the_text`。

- `glue:text` 调用的是 `string.format` 函数，所以使用 `:.2f` 一类的格式字符串，是能将一个浮点数，按两位小数输出格式化的。
- `glue:figure`, 只能用指令模式, 可以和常规的 `figure` 指令对比，以指令的形式动态 fetch 代码执行的结果，并像常规的 `figure` 环境一样可以给图片加图注和引用。
- `glue:math`, 只能用指令模式，动态 fetch 的变量需要有 `text/latex` 这个 MIME type 的 display function（常见估计也只用于 sympy 的输出）

## 纯 JS 的实时交互

纯 JS 的实时交互，所用的是将 Python 处理后的数据，展示为 HTML + JS 显示的一些库，常见于绘图库。
如：Altair, Plotly, pythreejs


## 带 Python Kernel 或者 其他 Kernel 的实时交互

这类方案，通常来说，需要连接到有 IPython Kernel 的云平台，比如 Mybinder, Colab 等。
这些方案可能会远程跳转到云服务提供商的页面。

使用 Thebe 可以将 MyBinder 的 Kernel 绑定到当前页面上。
在这里点开右侧的火箭，点 Live Code 即可尝试。

在设置里，我们只需要写如下设置，即可在转换后有这样的功能。

```yaml
repository:
  url: https://github.com/xxxx
  path_to_book: docs 
  branch: master
launch_buttons:
  notebook_interface: "classic"
  thebe: true
```

## 使用纯浏览器交互方案 Pyodide

TheBe 已经有使用 Pyodide + Jupyterlite 的方案，使用 WASM 内嵌一个 Python 解释器，来达到在浏览器中运行 Python 的目的。
但 JupyterBook 还未跟进这个 0.9 版本。
可以跟踪 [Thebe](https://github.com/executablebooks/thebe) 和 JupyterBook 的开发进度。

或者有空可以试试 `jupyterlite-sphinx` 插件
