
贝叶斯网络
============

贝叶斯网络是一种应用极为广泛的概率图模型，由节点和有向边构成，能够通过有向边来描述变量之间的条件依赖关系。给定一个已经构造好的贝叶斯网络，通常可以采用一些贝叶斯推断算法对其中的变量进行推断或者学习，这些贝叶斯推断算法中既包括最为人所熟知的马尔可夫链蒙特卡洛算法，也包括形式上略显抽象的变分推断算法。

直观清晰的贝叶斯网络结构图可以帮助读者和研究者更好地理解贝叶斯网络，而LaTeX在绘制贝叶斯网络结构方面具有天然的优势，一是由于我们在使用LaTeX绘图的过程中，LaTeX能够最大程度上支持复杂的公式符号；二则得益于LaTeX的一系列兼容性极好的图模型绘制包，其中，最具代表性且使用最为广泛的工具库(对应于LaTeX则称为library)莫过于`bayesnet`。结合LaTeX中的绘图工具包`tikz`，我们可以使用LaTeX画出近乎完美的贝叶斯网络。

> `bayesnet`库是基于LaTeX绘图工具包`tikz`构建起来的贝叶斯网络绘图工具库，主要用于绘制贝叶斯网络、图模型以及有向图结构，其GitHub开发主页为[https://github.com/jluttine/tikz-bayesnet](https://github.com/jluttine/tikz-bayesnet)。

本文将对几个具有代表性的贝叶斯网络案例进行拆分讲解，通过介绍各行代码及其所对应的绘图图形，逐步讲解如何用LaTeX绘制出复杂的贝叶斯网络，在开始绘图之前，我们不妨回顾一下贝叶斯网络所遵循的几项绘图原则：
- 观测变量或者观测值要使用灰色节点表示；
- 底层超参数无需用节点表示；
- 除观测变量和底层超参数外的其他变量要使用白色节点表示；
- 有向边箭头的指向表示贝叶斯角度的概率依赖关系。

绘制贝叶斯网络的基本语句
-----------

使用LaTeX绘制贝叶斯网络时，我们需要用到一些最为基本的LaTeX命令：

```tex
\documentclass[tikz, border = 0.1cm]{standalone}
\usepackage{tikz}
\usetikzlibrary{bayesnet}
\usepackage{amsmath, amsthm, amssymb, amsfonts}
\tikzset{>=latex}

\begin{document}
\begin{tikzpicture}

\end{tikzpicture}
\end{document}
```

在这几行基本命令中，它们各自都发挥着一定的作用，我们不妨来逐行看一下这些命令的“功效”：

- 准备阶段：
  - `\documentclass[tikz, border = 0.1cm]{standalone}`的作用在于指定所创建文件的类型，确定`tikz`绘图风格的同时可设置绘图边框的页边距，这里选取的页边距是0.1厘米。当然，这里的页边距是可以根据我们自身的审美标准进行设置的。
  - `\usepackage{tikz}`的作用在于启用LaTeX中的绘图工具包`tikz`。
  - `\usetikzlibrary{bayesnet}`的作用在于调用绘制贝叶斯网络所需的`bayesnet`库。
  - `\usepackage{amsmath, amsthm, amssymb, amsfonts}`的作用在于启用LaTeX中支持公式编译的工具包。
- 绘图阶段：
  - `\begin{document} \end{document}`是LaTeX编辑各类文档时首先要申明的语句，在`\begin`和`\end`之间写语句才能有效地映射到所创建的文档中。
  - `\begin{tikzpicture} \end{tikzpicture}`是用于生成`tikz`绘图的基本语句，在`tikzpicture`中，我们可以通过指定各个节点(`\node`)的横纵坐标来进行绘图。

绘制贝叶斯增强张量分解的贝叶斯网络
--------------

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/BayesNet/BATF.png" alt="drawing" width="280"/>
</p>

<p align="center">
<b>图</b>: 贝叶斯增强张量分解的贝叶斯模型示意图 (图片案例取自文献[1])
</p>

以上述的几行LaTeX绘图的基本命令为基础，我们不妨在`\begin{tikzpicture} \end{tikzpicture}`之间编写关于绘制观测变量节点的代码：首先，我们将观测变量节点命名为`obs`，在`\node`命令中，指定该节点的位置为坐标原点(0,0)，指定节点类型为`circle`，另外令节点边框为黑色（即`draw = black`）、节点大小为0.65厘米（即`minimum size = 0.65cm`）。

```tex
\documentclass[tikz, border = 0.1cm]{standalone}
\usepackage{tikz}
\usetikzlibrary{bayesnet}
\usepackage{amsmath, amsthm, amssymb, amsfonts}
\tikzset{>=latex}

\begin{document}
\begin{tikzpicture}

\node[circle, draw = black, fill = gray!20, inner sep = 0pt, minimum size = 0.65cm] (obs) at (0, 0) {{$y_{ijt}$}};

\end{tikzpicture}
\end{document}
```

将这几行简单的代码复制粘贴到所创建的overleaf项目中，即可得到我们希望得到的观测变量节点示意图。另外，从下图可以看出，左侧为代码区域，右侧为画图文档区域，我们在在线LaTeX编辑系统[overleaf.com](overleaf.com)中创建的项目名称为latex-drawing-tutorial.

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/images/batf_01.png" alt="drawing" width="900"/>
</p>

<p align="center">
<b>图</b>: 绘制贝叶斯模型的观测变量节点
</p>

与绘制观测变量节点类似，

```tex
\documentclass[tikz, border = 0.1cm]{standalone}
\usepackage{tikz}
\usetikzlibrary{bayesnet}
\usepackage{amsmath, amsthm, amssymb, amsfonts}
\tikzset{>=latex}

\begin{document}
\begin{tikzpicture}

\node[circle, draw = black, fill = gray!20, inner sep = 0pt, minimum size = 0.65cm] (obs) at (0, 0) {{$y_{ijt}$}};
\node[circle, draw = black, inner sep = 0pt, minimum size = 0.6cm] (ui) at (-0.9, 0.9) {{$\boldsymbol{u}_{i}$}};
\node[circle, draw = black, inner sep = 0pt, minimum size = 0.6cm] (vj) at (0, 1.8) {{$\boldsymbol{v}_{j}$}};
\node[circle, draw = black, inner sep = 0pt, minimum size = 0.6cm] (xt) at (0.9, 0.95) {{$\boldsymbol{x}_{t}$}};
\node[circle, draw = black, inner sep = 0pt, minimum size = 0.6cm] (phi) at (-0.9, -0.7) {{$\phi_{i}$}};
\node[circle, draw = black, inner sep = 0pt, minimum size = 0.6cm] (theta) at (0, -2) {{$\theta_{j}$}};
\node[circle, draw = black, inner sep = 0pt, minimum size = 0.6cm] (eta) at (0.9, -0.75) {{$\eta_{t}$}};
\node[circle, draw = black, inner sep = 0pt, minimum size = 0.55cm] (tau) at (2, 0) {{$\tau$}};
\node[circle, draw = black, inner sep = 0pt, minimum size = 0.55cm] (mu) at (-2, 0) {{$\mu$}};

\end{tikzpicture}
\end{document}
```


参考文献
------------

[1] Xinyu Chen, Zhaocheng He, Yixian Chen, Yuhuan Lu, Jiawei Wang (2019). Missing traffic data imputation and pattern discovery with a Bayesian augmented tensor factorization model. Transportation Research Part C: Emerging Technologies, 104: 66-77.
