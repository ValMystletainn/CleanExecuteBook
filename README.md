# Clean Execute Book

A clean and out-of-the-box jupyter book template.

## Features

1. Markdown and MyST extended syntax for easy editing.
2. Clean HTML published pages, including hover preview of cross reference, three columns blog pages, and so on.
3. JupyterBook that makes the static pages executable.
4. JupyterBook makes the single Markdwon converting to LaTeX seamlessly.

## Usage

``` bash
pip install -r requirements.txt
pip install -U sphinx-book-theme # mannully install to avoid the auto conflicts
pip install docutils==0.17.1 # mannully install
jupyter-book build docs
```

## RoadMap

- [ ] Multilanguage search
- [ ] Pyodide support

