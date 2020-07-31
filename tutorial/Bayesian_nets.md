
贝叶斯网络
-----------

LaTeX在绘制贝叶斯网络结构方面具有天然的优势，一则是由于LaTeX绘图能够最大程度上支持复杂的公式符号，二则是得益于LaTeX的一系列兼容性极好的图模型绘制包，其中，最具代表性且使用最为广泛的包莫过于`bayesnet`，结合LaTeX中的绘图包`tikz`，我们几乎能够使用LaTeX画出近乎完美的贝叶斯网络。

> `bayesnet`包的GitHub主页为[https://github.com/jluttine/tikz-bayesnet](https://github.com/jluttine/tikz-bayesnet)，主要用于绘制贝叶斯网络、图模型以及有向图结构。

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

在这几行基本命令中，它们各自都会发挥一定的作用：

- ```{tex}\documentclass[tikz, border = 0.1cm]{standalone}```的作用在于指定所创建文件的类型，确定`tikz`绘图风格的同时可设置绘图边框的页边距，这里是0.1厘米。
- 



> **案例1: 如何绘制如下贝叶斯增强张量分解的贝叶斯网络示意图？**

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/BayesNet/BATF.png" alt="drawing" width="250"/>
</p>

<p align="center">
<b>图</b>: 贝叶斯增强张量分解的贝叶斯模型示意图 (图片案例取自文献[1])
</p>


参考文献
------------

[1] Xinyu Chen, Zhaocheng He, Yixian Chen, Yuhuan Lu, Jiawei Wang (2019). Missing traffic data imputation and pattern discovery with a Bayesian augmented tensor factorization model. Transportation Research Part C: Emerging Technologies, 104: 66-77.
