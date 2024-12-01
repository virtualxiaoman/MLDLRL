# 记录一些LaTeX语法：

1. 引理的写法：

$A \Rightarrow C$ (by Lemma B)
或者
$A \overset{B}{\Rightarrow} C$

对应的代码是：

`A \Rightarrow C \quad \text{(by Lemma B)}`
或者
`A \overset{B}{\Rightarrow} C`


# CUMCM编译LaTeX的问题：
报错：（省略了部分信息）：
```
 * XeTeX is required to compile this document.
 * Sorry!
 ```
 报错原因：从错误日志中可以看出，问题的根本原因是你正在尝试使用 pdfTeX 编译一个需要 XeTeX 才能编译的文档。cumcmthesis.cls 模板文件中明确要求使用 XeTeX 编译器，而你使用的却是 pdfTeX。
解决方法：`xelatex -synctex=1 -interaction=nonstopmode -file-line-error -recorder "e:/LatexArticle/demo/main.tex"`