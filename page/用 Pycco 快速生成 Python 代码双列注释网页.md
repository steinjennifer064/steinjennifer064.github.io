最近，我发现了一个专门介绍深度学习源代码的网站 [LabML](https://nn.labml.ai/index.html)，它的双列式结构非常吸引人：页面右侧显示代码，左侧显示每段代码的注释。这种布局对代码讲解非常直观高效。

受到启发，我决定在自己的博客中也采用这种方式介绍代码。经过一番研究，我找到了一个开源工具 **Pycco**，它可以快速为 Python 代码生成双列注释的静态网页。

---

## Pycco 的安装与使用

Pycco 是文档生成工具 Docco 的 Python 实现版。它的特点是简单直接，能够快速生成 HTML 页面。以下是安装和使用 Pycco 的步骤：

### 安装 Pycco

在终端中运行以下命令即可安装 Pycco：

bash
pip install pycco


### 使用 Pycco 生成文档

准备一个带注释的 Python 文件，例如 `hello.py`：

python
"""
Hello
World
"""
import torch
import pycco

# Hello
print("hello world")

"""
End of file
"""


运行以下命令生成文档页面：

bash
pycco hello.py


生成的文档会保存在 `docs` 子目录中，包含一个 `hello.html` 文件和一个 `pycco.css` 文件。用浏览器打开生成的 HTML 文件，即可看到双列注释页面。

### 注意事项

- Pycco 支持 `#` 开头的单行注释和 `""" """` 包裹的多行注释。
- 但不支持 `''' '''` 包裹的多行注释。

---

## 扩展功能：渲染公式

在深度学习代码中，公式是不可或缺的。默认情况下，Pycco 生成的页面不支持公式渲染。为此，我们可以通过引入 **MathJax** 来实现公式渲染。

### 添加 MathJax 支持

找到 Pycco 的模板文件 `pycco_resources/__init__.py`，在 `<head>` 部分插入以下代码：

html
<script>
    MathJax = {
      tex: {
        inlineMath: [ ["$", "$"] ]
      }
    };
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>


修改后重新生成文档，页面即可支持公式渲染。

---

## 扩展功能：高亮新增/删除代码

在讲解代码时，突出显示新增或删除的代码块可以提高可读性。以下是实现方法：

### 添加高亮样式

在模板文件 `pycco_resources/__init__.py` 中，添加以下 CSS 样式：

css
.highlighted-line-1 {
  background-color: #fa53208c; /* 删除代码的背景色 */
}
.highlighted-line-2 {
  background-color: #68fc5d; /* 新增代码的背景色 */
}


### 修改生成逻辑

在 `pycco/main.py` 中，添加以下逻辑：

python
delete_background_start = '<div class="highlighted-line-1">'
add_background_start = '<div class="highlighted-line-2">'
background_end = '</div>'

if section["docs_text"].startswith('===ADD==='):
    section["docs_text"] = section["docs_text"][9:]
    section["code_html"] = add_background_start + section["code_html"] + background_end
elif section["docs_text"].startswith('===DEL==='):
    section["docs_text"] = section["docs_text"][9:]
    section["code_html"] = delete_background_start + section["code_html"] + background_end


通过在注释中添加 `===ADD===` 或 `===DEL===` 标记，即可高亮对应的代码块。

---

## 修复多行注释缩进问题

Pycco 在处理多行注释时，可能会因为缩进导致页面布局混乱。为了解决这个问题，可以修改 `pycco/main.py` 中的多行注释处理逻辑：

python
docs_text += line.lstrip('\t ') + '\n'


这样可以去除多行注释左侧的所有空格和制表符，确保页面布局正常。

---

## 总结

Pycco 是一个简单高效的工具，适合用来生成带注释的 Python 代码文档。通过本文的介绍，我们实现了以下功能扩展：

1. 支持 MathJax 渲染公式。
2. 支持代码块的新增/删除高亮。
3. 修复了多行注释缩进问题。

Pycco 的代码短小精悍，非常适合二次开发。如果你需要在博客中详细讲解代码，不妨试试这个工具。

👉 [WildCard | 一分钟注册，轻松订阅海外线上服务](https://bit.ly/bewildcard)