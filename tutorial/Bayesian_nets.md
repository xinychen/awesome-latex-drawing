
贝叶斯网络
============

贝叶斯网络是一种应用极为广泛的概率图模型，由节点和有向边构成，能够通过有向边来描述变量之间的条件依赖关系。给定一个已经构造好的贝叶斯网络，通常可以采用一些贝叶斯推断算法对其中的变量进行推断或者学习，这些贝叶斯推断算法中既包括最为人所熟知的马尔可夫链蒙特卡洛算法，也包括形式上略显抽象的变分推断算法。

直观清晰的贝叶斯网络结构图可以帮助读者和研究者更好地理解贝叶斯网络，而LaTeX在绘制贝叶斯网络结构方面具有天然的优势，一是由于我们在使用LaTeX绘图的过程中，LaTeX能够最大程度上支持复杂的公式符号；二则得益于LaTeX的一系列兼容性极好的图模型绘制包，其中，最具代表性且使用最为广泛的工具库(对应于LaTeX则称为library)莫过于`bayesnet`。结合LaTeX中的绘图工具包`tikz`，我们可以使用LaTeX画出近乎完美的贝叶斯网络。

> `bayesnet`库是基于LaTeX绘图工具包`tikz`构建起来的贝叶斯网络绘图工具库，主要用于绘制贝叶斯网络、图模型以及有向图结构，其GitHub开发主页为[https://github.com/jluttine/tikz-bayesnet](https://github.com/jluttine/tikz-bayesnet)。

本文将对几个具有代表性的贝叶斯网络案例进行拆分讲解，通过介绍各行代码及其所对应的绘图图形，逐步讲解如何用LaTeX绘制出复杂的贝叶斯网络。在开始绘图之前，我们不妨回顾一下贝叶斯网络所遵循的几项绘图原则：
- 观测变量或者观测值要使用灰色节点表示；
- 底层超参数无需用节点表示；
- 除观测变量和底层超参数外的其他变量要使用白色节点表示；
- 有向边箭头的指向表示贝叶斯角度的概率依赖关系。

首先，我们在在线LaTeX编辑系统[overleaf.com](overleaf.com)中创建名称为latex-drawing-tutorial的项目，接下来就在项目中开启贝叶斯网络的LaTeX绘图之旅：

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

> **绘图任务**：如何使用LaTeX绘制出如下贝叶斯增强张量分解的贝叶斯网络？

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/BayesNet/BATF.png" alt="drawing" width="320"/>
</p>

<p align="center">
<b>图</b>: 贝叶斯增强张量分解的贝叶斯模型示意图 (图片案例取自文献[1])
</p>

### 绘制观测变量节点

以上述的几行LaTeX绘图的基本命令为基础，我们不妨在`\begin{tikzpicture} \end{tikzpicture}`之间编写关于绘制观测变量节点的代码：首先，我们将观测变量节点命名为`obs`，在`\node`命令中，指定该节点的位置为坐标原点`(0, 0)`，指定节点类型为`circle`，另外令节点边框为黑色（即`draw = black`）、填充为灰色（即`fill = gray!20`）、节点与边框之间无间隔（即`inner sep = 0pt`）、节点大小为0.65厘米（即`minimum size = 0.65cm`）、节点表示的参数为`{{$y_{ijt}$}}`。

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

将这几行简单的代码复制并粘贴到之前所创建的overleaf项目中，即可得到绘制好的观测变量节点示意图。从下图可以看出，左侧为代码区域，右侧为画图文档区域。

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/images/batf_01.png" alt="drawing" width="900"/>
</p>

<p align="center">
<b>图</b>: 绘制贝叶斯模型的观测变量节点
</p>

### 绘制模型参数节点

与绘制观测变量节点类似，我们可以通过`\node`设计模型参数节点。对于模型参数节点`ui`，在`\node`命令中，指定该节点的位置为坐标`(-0.9, 0.9)`，并使用`\boldsymbol`命令加粗符号`u`。类似地，可以指定模型参数节点`vj`、`xt`、`phi`、`theta`、`eta`、`tau`、`mu`的位置坐标。

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

同样，将这里的代码复制并粘贴到所创建的overleaf项目中，即可得到观测变量节点和模型参数节点示意图。

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/images/batf_02.png" alt="drawing" width="900"/>
</p>

<p align="center">
<b>图</b>: 新增贝叶斯模型的模型参数节点
</p>

### 绘制模型参数节点和观测变量节点之间的有向边

紧接着上面绘制观测变量节点和模型参数节点的代码，根据已经定义好的节点，可以使用`\path`来构造有向边，其中模型参数节点和观测变量节点之间要用`edge`关联，箭头方向为`->`。这里，有两种办法在模型参数节点和观测变量节点之间建立有向边：

- 第一种方法是依次对各个有向边进行建立，这种方法简单易懂，不足之处在于代码往往会出现冗余。

```tex
\path [draw, ->] (ui) edge (obs);
\path [draw, ->] (vj) edge (obs);
\path [draw, ->] (xt) edge (obs);
\path [draw, ->] (tau) edge (obs);
\path [draw, ->] (mu) edge (obs);
\path [draw, ->] (phi) edge (obs);
\path [draw, ->] (theta) edge (obs);
\path [draw, ->] (eta) edge (obs);
```

- 第二种方法是采用LaTeX中的`\foreach`命令，即一般意义上的for循环语句，在这里，我们可以使用`\foreach`命令对集合`{ui, vj, xt, tau, mu, phi, theta, eta}`内的变量进行遍历，这样对于简化代码大有裨益。

```tex
\foreach \n in {ui, vj, xt, tau, mu, phi, theta, eta}{\path [draw, ->] (\n) edge (obs);}
```

【注释】对LaTeX中`\foreach`命令感兴趣的读者，不妨阅读Stack Overflow里面的一篇回答：[Iteration in LaTeX
](https://stackoverflow.com/questions/2561791/iteration-in-latex/5958641)。`\foreach`的基本用法为：1) 对整数进行循环，例如，`\foreach \n in {0, ..., 22}{do something}`，2) 对字符进行循环，例如，`\foreach \n in {apples, burgers, cake}{Let's eat \n.\par}`。

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

\foreach \n in {ui, vj, xt, tau, mu, phi, theta, eta}{\path [draw, ->] (\n) edge (obs);}

\end{tikzpicture}
\end{document}
```

将这里的代码复制并粘贴到所创建的overleaf项目中，即可得到观测变量节点、模型参数节点以及有向边示意图。

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/images/batf_03.png" alt="drawing" width="900"/>
</p>

<p align="center">
<b>图</b>: 新增贝叶斯模型观测变量节点和模型参数节点之间的有向边
</p>

### 绘制部分观测变量的元素集合

对于部分观测变量，它可能只包括矩阵或张量元素的部分索引，因此需要指定出来。一般而言，我们可以用`\plate`在贝叶斯网络中进行标注，标注的方法是在`\plate`命令中罗列需要覆盖的变量。以第一个plate为例，我们可以将`{(obs) (ui) (m) (phi)}`作为所需要覆盖的集合。

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

\foreach \n in {ui, vj, xt, tau, mu, phi, theta, eta}{\path [draw, ->] (\n) edge (obs);}

\node [text width = 0.2cm] (m) at (-1.1, 0.3) {\small{$m$}};
\plate[] {plate1} {(obs) (ui) (m) (phi)} { };
\node [text width = 0.6cm] (n) at (0, -1.55) {\small{$n$}};
\plate[] {plate2} {(obs) (vj) (n) (theta)} { };
\node [text width = 0.2cm] (f) at (1.1, 0.3) {\small{$f$}};
\plate[] {plate3} {(obs) (xt) (f) (eta)} { };

\end{tikzpicture}
\end{document}
```

将这里的代码复制并粘贴到所创建的overleaf项目中，即可得到部分观测变量的元素集合示意图。

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/images/batf_04.png" alt="drawing" width="900"/>
</p>

<p align="center">
<b>图</b>: 新增贝叶斯模型部分观测变量的元素集合
</p>

### 绘制超参数节点及其有向边

在这里，超参数分为待估计超参数和底层超参数，待估计超参数顾名思义是一个变量，而底层超参数则是常量。对于待估计超参数，我们仍要像绘制模型参数一样绘制它，而底层超参数则不需要带有“圆圈”，不过需要注意的是，两者都可以用`\node`命令进行绘制，如下面代码所示。

- 待估计超参数包括`muv`和`lambdav`。在`\node`命令中，指定节点类型为`circle`，使用`draw = black`令节点边框为黑色，使用`inner sep = 0pt`令节点与边框之间无间隔，使用`minimum size = 0.6cm`将节点大小统一设为0.6厘米，并将字体大小统一设为`\small`；

- 底层超参数包括：`gamma`、`hyper1`、`hyper2`、`hyper3`、`hyper4`、`mu0`、`wnu0`。在`\node`命令中，使用`text width`指定不同大小的文本宽度，通过`at`指定各参数的位置，并将字体大小统一设为`\small`。

此外，为了表示其它未列出的参数名称，使用命令`\cdots`绘制了两个居中省略号，即`cdots1`和`cdots2`，并将字体颜色设为灰色`color{gray}`、字体大小设为`\Large`。

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

\foreach \n in {ui, vj, xt, tau, mu, phi, theta, eta}{\path [draw, ->] (\n) edge (obs);}

\node [text width = 0.2cm] (m) at (-1.1, 0.3) {\small{$m$}};
\plate[] {plate1} {(obs) (ui) (m) (phi)} { };
\node [text width = 0.6cm] (n) at (0, -1.55) {\small{$n$}};
\plate[] {plate2} {(obs) (vj) (n) (theta)} { };
\node [text width = 0.2cm] (f) at (1.1, 0.3) {\small{$f$}};
\plate[] {plate3} {(obs) (xt) (f) (eta)} { };

\node[circle, draw = black, inner sep = 0pt, minimum size = 0.6cm] (muv) at (-0.6, 2.8) {\small{$\boldsymbol{\mu}_{v}$}};
\node[circle, draw = black, inner sep = 0pt, minimum size = 0.6cm] (lambdav) at (0.6, 2.8) {\small{$\Lambda_{v}$}};
\node[text width = 0.8cm] (gamma) at (2, 0.8) {\small{$a_0,b_0$}};
\node[text width = 0.8cm] (hyper1) at (-2, 0.8) {\small{$\mu_{0},\tau_{0}$}};
\node[text width = 0.8cm] (hyper2) at (1.2, -2) {\small{$\mu_{0},\tau_{0}$}};
\node[text width = 0.8cm] (hyper3) at (2.1, -0.75) {\small{$\mu_{0},\tau_{0}$}};
\node[text width = 0.8cm] (hyper4) at (-2.1, -0.7) {\small{$\mu_{0},\tau_{0}$}};
\node[text width = 0.4cm] (mu0) at (-0.6, 3.6) {\small{$\boldsymbol{\mu}_{0}$}};
\node[text width = 0.9cm] (wnu0) at (0.6, 3.6) {\small{$W_{0},\nu_{0}$}};
\node[text width = 0.6cm] (cdots1) at (-1, 1.6) {\Large\color{gray}{$\cdots$}};
\node[text width = 0.6cm] (cdots2) at (1, 1.6) {\Large\color{gray}{$\cdots$}};

\path [draw, ->] (muv) edge (vj);
\foreach \n in {vj, muv}{\path [draw, ->] (lambdav) edge (\n);}
\path [draw, ->] (mu0) edge (muv);
\path [draw, ->] (wnu0) edge (lambdav);
\path [draw, ->] (gamma) edge (tau);
\path [draw, ->] (hyper1) edge (mu);
\path [draw, ->] (hyper2) edge (theta);
\path [draw, ->] (hyper3) edge (eta);
\path [draw, ->] (hyper4) edge (phi);

\end{tikzpicture}
\end{document}
```

将这里的代码复制并粘贴到所创建的overleaf项目中，即可得到我们希望得到的包含了超参数节点及其有向边的贝叶斯网络结构图。

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/images/batf_05.png" alt="drawing" width="900"/>
</p>

<p align="center">
<b>图</b>: 新增贝叶斯模型的超参数及其有向边
</p>

到这里，我们便完成了完整的贝叶斯网络绘制。

绘制贝叶斯时序矩阵分解的贝叶斯网络
--------------

> **绘图任务**：如何使用LaTeX绘制出如下贝叶斯时序矩阵分解的贝叶斯网络？

<p align="center">
<img src="https://github.com/xinychen/awesome-latex-drawing/blob/master/BayesNet/BTMF.png" alt="drawing" width="480"/>
</p>

<p align="center">
<b>图</b>: 贝叶斯时序矩阵分解的贝叶斯模型示意图 (图片案例取自文献[2])
</p>

完整代码预览：

```tex
\documentclass[border=0.1cm, 12pt]{standalone}
\usepackage{tikz}
\usetikzlibrary{bayesnet}
\usepackage{amsmath, amsthm, amssymb, amsfonts}
\usepackage{systeme, mathtools}
\usetikzlibrary{positioning, arrows.meta, quotes}
\usetikzlibrary{shapes, snakes}
\tikzset{>=latex}

\tikzstyle{plate caption} = [caption, node distance=0, inner sep=0pt,
below left=5pt and 0pt of #1.south]
\begin{document}
\begin{tikzpicture}

\node [obs,inner sep=0pt,minimum size=0.8cm] (obs) at (0.8+2.4,0+0.8-0.3) {\normalsize$y_{i,t+1}$};
\node [obs,minimum size=0.95cm] (obs1) at (-0.8+2.4,0+0.8-0.3) {\normalsize$y_{i,t}$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=0.8cm] (obs2) at (-0.8+2.4-1.6,0.5) {$y_{i,t-1}$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=0.8cm] (xtd1) at (-2.6,-2.0) {\scalebox{0.85}[1]{$\boldsymbol{x}_{t-d+1}$}};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=1cm] (xtd) at (-4.2,-2.0) {$\boldsymbol{x}_{t-d}$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=1cm] (xt1) at (3.2,-2.0) {$\boldsymbol{x}_{t+1}$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=1cm] (xt2) at (1.6,-2.0) {$\boldsymbol{x}_{t}$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=1cm] (xt3) at (0,-2.0) {$\boldsymbol{x}_{t-1}$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=1cm] (w) at (2.4-0.8,2.3-0.4) {$\boldsymbol{w}_{i}$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=0.9cm] (lambda) at (3.2-0.8,3.8-0.4) {$\Lambda_{w}$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=0.9cm] (mu) at (0+2.4-1.6,3.8-0.4) {$\boldsymbol{\mu}_{w}$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=0.9cm] (kappa) at (0.8,-4) {$\Sigma$};
\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=0.9cm] (thetak) at (-1.3,-4) {$A$};

\node[mark size=1pt,color=black] at (-1.6+2.4-1.6,0+0.8-0.3) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] at (-1.8+2.4-1.6,0+0.8-0.3) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] (leftnode0) at (-2.0+2.4-1.6,0+0.8-0.3) {\pgfuseplotmark{*}};

\node[mark size=1pt,color=black] at (1.6+2.4,0+0.8-0.3) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] at (1.8+2.4,0+0.8-0.3) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] (rightnode0) at (2.0+2.4,0+0.8-0.3) {\pgfuseplotmark{*}};

\node[mark size=1pt,color=black] at (-1.1,-2) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] at (-1.3,-2) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] at (-1.5,-2) {\pgfuseplotmark{*}};

\node[mark size=1pt,color=black] (leftnode1) at (-5.4,-2) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] at (-5.2,-2) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] at (-5.0,-2) {\pgfuseplotmark{*}};

\node[mark size=1pt,color=black] (rightnode1) at (4.4,-2) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] at (4.2,-2) {\pgfuseplotmark{*}};
\node[mark size=1pt,color=black] at (4.0,-2) {\pgfuseplotmark{*}};

\node [circle,draw=black,fill=white,inner sep=0pt,minimum size=0.8cm] (tau) at (3.0+2.4-1.2,-1.8+0.8) {$\tau$};
\node [text width=0.6cm] (gamma1) at (3.0+2.4,-1.8+0.8) {$\alpha,\beta$};
\node [text width=0.9cm] (gamma2) at (0+2.4,4.8-0.3) {\small $W_0,\nu_0$};
\node [text width=0.5cm] (mu0) at (0+2.4-1.6,4.8-0.3) {$\boldsymbol{\mu}_0$};
\node [text width=0.9cm] (gamma3) at (0.8,-5.1) {\small $S_0,\nu_0$};
\node [text width=1.2cm] (gamma4) at (-1.3,-5.1) {\small $M_0,\Psi_0$};
    
\path [draw,->] (w) edge (obs);
\path [draw,->] (w) edge (obs1);
\path [draw,->,dashed] (w) edge (obs2);
\path [draw,->] (lambda) edge (w);
\path [draw,->] (kappa) edge (xtd);
\path [draw,->] (kappa) edge (xtd1);
\path [draw,->] (kappa) edge (xt1);
\path [draw,->] (kappa) edge (xt2);
\path [draw,->] (kappa) edge (xt3);
\path [draw,->] (gamma1) edge (tau);
\path [draw,->] (gamma2) edge (lambda);
\path [draw,->] (gamma3) edge (kappa);
\path [draw,->] (gamma4) edge (thetak);
\path [draw,->] (lambda) edge (mu);
\path [draw,->] (mu) edge (w);
\path [draw,->] (mu0) edge (mu);
\path [draw,->] (tau) edge (obs);
\path [draw,->] (tau) edge (obs1);
\path [draw,->,dashed] (tau) edge (obs2);
\path [draw,->] (xt1) edge (obs);
\path [draw,->] (xt2) edge (xt1);
\path [draw,->] (xt3) edge (xt2);
\path [draw,->,dashed] (xt3) edge (obs2);
\path [draw,->] (xt3) edge [bend left] node [right] {} (xt1);
\path [draw,->] (xtd) edge [bend left] node [right] {} (xt2);
\path [draw,->] (xtd) edge [bend left] node [right] {} (xt3);
\path [draw,->] (xtd) edge (xtd1);
\path [draw,->] (xtd1) edge [bend left] node [right] {} (xt1);
\path [draw,->] (xtd1) edge [bend left] node [right] {} (xt2);
\path [draw,->] (xtd1) edge [bend left] node [right] {} (xt3);
\path [draw,->] (xt2) edge (obs1);
\path [draw,->] (thetak) edge (xt1);
\path [draw,->] (thetak) edge (xt2);
\path [draw,->] (thetak) edge (xt3);
\path [draw,->] (thetak) edge (xtd);
\path [draw,->] (thetak) edge (xtd1);
\path [draw,->] (kappa) edge (thetak);

\node [text width=2.2cm] (m) at (-1+2.5-1.5,2.6+0.8-1.6) {\small{$i\in\left\{1,...,N\right\}$}};
\plate [color=black] {part1} {(leftnode0)(rightnode0)(obs)(obs1)(w)(m)} { };

\end{tikzpicture}
\end{document}
```

### 绘制模型参数节点



参考文献
------------

[1] Xinyu Chen, Zhaocheng He, Yixian Chen, Yuhuan Lu, Jiawei Wang (2019). Missing traffic data imputation and pattern discovery with a Bayesian augmented tensor factorization model. Transportation Research Part C: Emerging Technologies, 104: 66-77.

[2] Xinyu Chen, Lijun Sun (2019). Bayesian temporal factorization for multidimensional time series prediction. arXiv: 1910.06366.
