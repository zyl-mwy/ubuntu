https://blog.csdn.net/Zhang_Pro/article/details/106988187

* sudo apt-get install texlive-full
```
安装时间有点长,其中的xetex集成了中文字体的环境，使得中文文档的生成变得很容易，可以使用系统自带得字体，使用更好看得字体。
```
* apt-cache search cjk
```
找到相关宏包，安装
```
* sudo apt-get install latex-cjk-xcjk cjk-latex latex-cjk-chinese

* sudo mkdir /usr/share/fonts/winfonts
* 将C:\Windows\Fonts下的字体copy进来
* cd /usr/share/fonts/winfonts
* sudo mkfontscale
* sudo mkfontdir
* sudo fc-cache -vf
```
刷新字体缓存
```

* vim test.tex
```
\documentclass{article}
\usepackage[a4paper, left=1in, right=1in, top=1in, bottom=1in]{geometry}
\usepackage{xeCJK} %调用 xeCJK 宏包
\usepackage{listings}
\author{ ice }
\date {2019.01.28}
\setmainfont{SimSun}   % 宋体
%\setCJKmainfont{WenQuanYi Micro Hei Mono:style=Regular} %设置 CJK 主字体为 SimSun （宋体）
\title{Latex入门学习}
\begin{document}
\maketitle
\begin{center}
\end{center}

\tableofcontents %添加目录

\tableofcontents 

\begin{abstract}
this is abstract。
\end{abstract}

\section{asf}
你好。

\section{as}
hello world  

% Lorem  \cite{Lutz2017} ipsum dolor sit amet, consectetur adipisicing

% \bibliography{info}
\bibliographystyle{ieeetr}

\end{document}
```
* xelatex test.tex
* vscode 安装 Latex Workshop 拓展
* 打开File->Preference->Settings并编辑settings.json，添加以下的内容(仅做参考)
```

{
  "latex-workshop.latex.recipes": [{
  "name": "xelatex",
  "tools": [
      "xelatex"
  ]
}, {
  "name": "latexmk",
  "tools": [
      "latexmk"
  ]
},

{
  "name": "pdflatex -> bibtex -> pdflatex*2",
  "tools": [
      "pdflatex",
      "bibtex",
      "pdflatex",
      "pdflatex"
  ]
}
],
"latex-workshop.latex.tools": [{
"name": "latexmk",
"command": "latexmk",
"args": [
  "-synctex=1",
  "-interaction=nonstopmode",
  "-file-line-error",
  "-pdf",
  "%DOC%"
]
}, {
"name": "xelatex",
"command": "xelatex",
"args": [
  "-synctex=1",
  "-interaction=nonstopmode",
  "-file-line-error",
  "%DOC%"
]
}, {
"name": "pdflatex",
"command": "pdflatex",
"args": [
  "-synctex=1",
  "-interaction=nonstopmode",
  "-file-line-error",
  "%DOC%"
]
}, {
"name": "bibtex",
"command": "bibtex",
"args": [
  "%DOCFILE%"
]
}],
"latex-workshop.view.pdf.viewer": "tab",
"latex-workshop.latex.clean.fileTypes": [
"*.aux",
"*.bbl",
"*.blg",
"*.idx",
"*.ind",
"*.lof",
"*.lot",
"*.out",
"*.toc",
"*.acn",
"*.acr",
"*.alg",
"*.glg",
"*.glo",
"*.gls",
"*.ist",
"*.fls",
"*.log",
"*.fdb_latexmk"
],
}
```
* xelatex test.tex
* bibtexx test.aux
* xelatex test.tex
* xelatex test.tex



