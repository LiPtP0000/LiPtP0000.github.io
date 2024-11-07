---
layout: post
title: LaTeX 的环境配置与基本命令
subtitle: Long Term Support
tag: [LaTeX]
cover-img: /assets/img/miku.jpg
share-img: /assets/img/miku.jpg
thumbnail-img: /assets/img/miku.jpg
author: LiPtP
mathjax: true
---

{: .box-note}
在本教程中，你可以掌握 Vscode 本地 $$\latex$$ 编辑器的使用，以及在线 $$\latex$$ 编辑器 `Overleaf` 的使用方法。你还可以学到一些 $$\latex$$ 的基础指令，生成一个基本的文档。

# LaTeX 是什么？
参见 [【LaTeX】新手教程：从入门到日常使用](https://www.zhihu.com/tardis/zm/art/456055339?source_id=1005)

# 如何使用 LaTeX 写文档？
## 本地撰写
笔者推荐基于 Vscode 插件 `LaTeX Workshop` 的 $$\latex$$ 编写方法。配置结束后，你可以在 Vscode 中编写并运行 $$\latex$$ 文件并生成文档。

请参照：[Vscode-Latex配置教程](https://zhuanlan.zhihu.com/p/166523064) 进行配置。

{:.box-warning}
注意教程中`settings.json`文件的配置，这很重要。如果在后续的过程中发现编译失败但不报错，那么很可能是你环境配的有问题。第一次动这种配置的话可以多看看教程。

## 合作撰写

我们也会经常碰到合作写文档的问题。我们迫切地需要一个能够同时编辑的在线平台。那么请试试[Overleaf]{https://overleaf.com}吧。只需要注册一个账号就能提供多人共享（免费版只能两人同时编辑，但也OK）的tex编辑器，非常爽。



# tex文件怎么写？

配置完成后，就可以开始写代码了。在工作区新建一个`.tex`文档，试着写一个文档吧。

## 常用的 tex 命令
- 添加标题、目录、附录并自动编号

```latex
% 导言区
\documentclass[12pt]{article} % 指定文章类型，或者引入.cls模板的名字
\title{Virtues of LiPtP's Wife}
\author{LiPtP}
\date{\today} % 指定日期为生成pdf的日期

% 正文
\begin{document}
\maketitle      % 生成标题、作者、日期等等
\tableofcontents % 生成目录

\chapter{Virtue Catagory 1}
\section{Virtue 1}
\subsection{Proof 1}
\subsubsection{Proof 1.1}

\end{document}
```

- 数学公式

```latex

    $ a = b + c $   % 行内嵌入
                    
    % 独立行，有编号
    \begin{equation}
        a = b + c
    \end{equation}
```

- 插入图片

```latex
% 导言区
\usepackage{graphicx}
\usepackage{subfloat}
% 正文
\begin{document}
% 单张图片
\begin{figure}[htbp]
    \centering
    \includegraphics[0.8\textwidth]{./your/path/to/figure.png}
    \caption{Photo of my GF}
\end{figure}

% 子图(2*2)
\begin{figure}[htbp]
    \centering
    \subfloat[your name of subfigure]{0.5\textwidth}{./your/path/to/subfigure1.png}
    \hfill
    \subfloat[your name of subfigure]{0.5\textwidth}{./your/path/to/subfigure2.png}
    \newline % 换一行
    \subfloat[your name of subfigure]{0.5\textwidth}{./your/path/to/subfigure3.png}
    \hfill
    \subfloat[your name of subfigure]{0.5\textwidth}{./your/path/to/subfigure4.png}
    \caption{caption}
\end{figure}
\end{document}
```

- 插入表格

三线表采用 `longtable` package就可以了。正常的网格表可以使用[表生成器]{https://www.tablesgenerator.com/}，注意加上`[htbp]`使其浮动，从而灵活排版。


# 报错怎么办？
$$\latex$$ 报错太玄学，建议不看。