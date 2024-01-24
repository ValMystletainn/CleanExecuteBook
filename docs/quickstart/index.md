# 快速上手

## 方案特点

1. 专注内容，文本编辑轻量。以 Markdown 和其为学术写作扩展的 MyST 语法为写作工具。
2. 可交互性强，代码友好。支持将本地 Jupyter Notebook 的运行结果一并展示，也支持动态连接到在线的 Jupyter 云平台，交互式地修改代码查看结果。
3. 版式美观清晰。基于 [Executable Books Project](https://github.com/executablebooks) 项目的组件库后修改，使得文档内容导出为 html 或者直接导出为 latex 再编译为 pdf 都有着丝滑的体验和高的质量。
4. 动静结合，性价比高。导出的网站为静态网站，可以使用大部分免费的静态网站托管服务，但又有着丰富的动态交互，由前端、 Python 、Jupyter 云服务生态共同实现的。

## 如何使用(以本文档为例)

```sh
git clone <this repo>
pip install -r requirements_build.txt  # 安装构建文档时的支持
jb build docs
```

在 `docs/_build/html` 的目录下，就是构建后的静态站点。
你可以直接用浏览器打开本地的 `docs/_build/html/indexl.html` 文件。
也可以将这个目录下启动一个服务器，并打开相应地址，来访问 （如 `python -m http.server -d docs/_build/html`, vscode live server 插件启动此目录下的 `index.html`）

当然，对于团队协作文档或者公开发布的需求，本方案也能支持。
通过将构建后的网页发布到静态网站托管服务器，这写内容就能公开在线访问了。
当然一般而言，会通过 GitHub Action 或者其他托管源码服务器上的 CI/CD 功能，只追踪 Markdown 等文件的修改，推送服务器后 CI 自动触发以上构建过程，并推送到相应的网址托管网站。
这样，分布式的团队协作功能，也由 Git 本身的管理功能进行了实现。

## 扩展阅读

其实没啥好扩展的，一个文档写作方案，就应该让使用者尽可能地专注于输出内容，安装用户原本理解的写 Markdown 文档的方式去写就好。

当然在[细节陈列](../details/index.md)这一节中，会以罗列式的风格展示支持的语法，使用方法，以及该方案的底层工作原理，以供查询。
