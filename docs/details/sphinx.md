# Sphinx 支持

## 方法原理

通过阅读 [JupyterBook 的官方文档相应章节](https://jupyterbook.org/en/stable/explain/components.html)，
可以知道，它是通过 JupyterText 先把可能存在的 `.ipynb` 的文件转为 MyST Markdwon。
再通过 MyST Markdown 的 parser 建立语法树，然后可以映射到各种格式，在 JupyterBook 里就是 LaTeX 和 rst，然后 rst 通过 Sphinx 构建成网页。

## Sphinx 扩展

可以看到，在导出网页的最后一步，一定会经过 Sphinx build 的过程，也自然可以借助 Sphinx 的生态，添加插件。
在前面的介绍里，我们已经提到了 `sphinx_tippy` 用于悬停显示交叉引用，和 `sphinx_proof` 用于证明、算法类环境。

再介绍一个画图插件 `sphinxcontrib.kroki`，增加了一个 `kroki`导言，通过直接输入绘图内容，或者在 positional arg 里输入文件链接 (如下文代码)，将画图源语发送到 [https://kroki.io/](https://kroki.io/) 进行渲染，得到结果，如图{numref}`my-figure-kroki_excali`。

````md
```{kroki} ../assert/demo.excalidraw
:type: excalidraw
:caption: 标题
:name: my-figure-kroki_excali
```
````

```{kroki} ../assert/demo.excalidraw
:type: excalidraw
:caption: 标题
:name: my-figure-kroki_excali
```

还有就是 Sphinx 默认的静态搜索只对西文字体友好，中文的索引简历不佳，这个有空可以调整一下。
