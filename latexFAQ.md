<center><b>latex常见问题</b></center>
<center><b>JMx</b></center>
<center><b>2018-11-15</b></center>
<div style="page-break-after: always;"></div> 
[TOC]

<div style="page-break-after: always;"></div> 
# 数学相关

## 常用数学符号

- `x\overset{Delta}{= / \longrightarrow }y`  $x\overset{\Delta}{=}y,\ x\overset{\Delta}{\longrightarrow }y$。
- `a \xlongequal[abc]{def} b`  $a\xlongequal[up]{down}b$。
- 

## 公式编号

### 自动编号与章节

使用

```latex
∖begin{align}
...
∖end{align}
```

或者

```latex
∖begin{equation}
...
∖end{equation}
```

等时，系统会自动编号，如：
$$
u_t+6uu_x+u_{xxx}=0,\tag{1.1}
$$
其中(1.1)表示第一章第一个公式，另起一章则重新计数。如果还要需要区分节，则在文档配置区(begin{document}下面)添加

```latex
\numberwithin{equation}{section}
```

效果
$$
u_t+6uu_x+u_{xxx}=0,\tag{1.1.1}
$$

表示第一章，第一节中第一个方程。

也可以更深层

```latex
\numberwithin{equation}{subsection}
```

效果
$$
u_t+6uu_x+u_{xxx}=0,\tag{1.1.1.1}
$$
上面的两种情况是在report类或者book类中的效果，对于article类，没有章(chapter)的命令，所以效果分别为
$$
u_t+6uu_x+u_{xxx}=0,\tag{1.1}
$$

$$
u_t+6uu_x+u_{xxx}=0,\tag{1.1.1}
$$

### 取消自动编号

如果某些公式不需要标号

1. 可以使用双dollar符：

   ```latex
   $$...$$
   ```

2. 对于是对齐(algin)或者方程(equation)环境：

   - 如果全部不编号，则环境后面加星号：

     ```latex
     ∖begin{align*}
     ... 
     ∖end{align*}
     % 或者
     ∖begin{equation*} 
     ... 
     ∖end{equation*}
     ```

   - 如果部分不编号，在不编号的行后面(换行符\\\\之前)加<span style='color:blue'>\notag</span>或者<span style='color:blue'>\nonumber</span>.如

     ```latex
     \begin{align}
     a=1;\\
     b=1; \notag \\
     c=1; \nonumber \\
     d=1;
     \end{align}
     ```

### 修改自动编号

如果对于某些公式需要特殊标记

1. 对于双dollar环境，使用<span style='color:blue'>\eqno</span>{特殊标记}.如

   ```latex
   $$... \enqo{(*)}$$
   ```

2. 对于对齐或方程环境，使用<span style='color:blue'>\tag{}</span>或者<span style='color:blue'>\tag*{}</span>区别在于后者不加括号.如

   ```latex
   \begin{align}
   a=1; \\           			% (1.3)
   b=1; \tag{*} \\   			% 效果 (*)
   c=1; \tag*{*} \\  			% 效果 * 
   d=1; \tag{1.4.a} \\			
   e=1; \tag{1.4.b} \\
   f=1;			  			% (1.4)
   \end{align}
   ```

由注释部分可以看出，修改的自动编号，不计入编号计数器，即它下面的编号是接着它之前的编号，双dollar也一样。而这里(1.4)式应该是(1.5)式.这时，需要把编号计数器加1，即将上面修改为

```latex
\begin{align}
a=1; \\           			% (1.3)
b=1; \tag{*} \\   			% 效果 (*)
c=1; \tag*{*} \\  			% 效果 * 
d=1; \tag{1.4.a} \\
e=1; \tag{1.4.b} \\
addtocounter{equation}{1}   % 编号+1，当然可以加任意整数，这里是1.
f=1;			  			% (1.5)
\end{align}
```

### 编号引用

当我们要引用前面的公式，一旦公式编号改变，就很麻烦。解决的办法之一是对所要引用的公式添加标签，然后在引用的地方使用标签,这种也称为相对引用。如

```latex
\begin{align}
x^2+y^2=z^2 \label{eq:1} \\ % 添加标签
a=1;	\tag{\ref{eq:1}$'$} % 这里引用上一个公式编号，且在后面加'， 如(2.2.1')
x^2+y^2=z^2 \tag{1-1} \label{eq:2}\\ % 自定义编号，并添加标签
\end{align}
%引用
根据\eqref{eq:2}可知... 。如果使用\ref命令，则需要手动加括号。

\newcommand{\myeqref}[1]{Eq. \eqref{#1} }

\myeqref ==> Eq.10
```

注意，双dollar中使用\eqno无法引用。

### 大括号环境(cases)下添加多个编号

```latex
\begin{equation}
	\begin{cases}
			1, & x>0,\\ 
			2, & x=0,\\
			3, & x<0.\\
	\end{cases} 
\end{equation}
```

上述环境默认为一个公式，因此只有一个编号

![](https://cdn.nlark.com/yuque/0/2019/png/122742/1573278836225-bf2f32f4-c242-4a10-a6d5-d8cd7e3690e8.png)

有时可能想要在每种情况后面加上方程编号和字母，可以添加如下的包

```latex
\usepackage{subeqnarray}
\usepackage{cases}
```

然后使用如下的环境

```latex
\begin{subequations}  
	\begin{numcases}{f(x)=} 
		f_1(x), & $x>0$,\\ 
		f_2(x), & $x=0$,\\
		f_3(x), & $x<0$.
	\end{numcases} 
\end{subequations}
```

结果如下

![](https://cdn.nlark.com/yuque/0/2019/png/122742/1573280188924-79c44301-15db-40e1-99af-d7601dad41ca.png)

需要注意的是，如果使用了$\&$连接符，后面的环境默认是文本环境，数学公式需要加$$。也可以直接使用

```latex
\begin{numcases}{f(x)=} 
	f_1(x), & $x>0$,\\ 
	f_2(x), & $x=0$,\\
	f_3(x), & $x<0$.
\end{numcases} 
```

<img src="https://cdn.nlark.com/yuque/0/2019/png/122742/1573280463059-01baa941-e2ea-4de5-88e7-54a9ce3e0c7b.png" style="zoom: 67%;" />

## 公式太大

latex内置了多种命令改变局域字体，包括数学公式的大小

```latex
\tiny \scriptsize \footnotesize \small \normalsize \large \Large \LARGE \huge \Huge
```

如

​       <img src="https://cdn.nlark.com/yuque/0/2019/png/122742/1572850815789-c0293718-0777-4d4a-838d-fc4bfa665516.png" style="zoom: 50%;" />     <img src="https://cdn.nlark.com/yuque/0/2019/png/122742/1572850834669-a33dafed-2eda-4575-a5bf-bce5602529c2.png" style="zoom:67%;" />

## 括号问题

某些数学公式因其具有分式等而高度较高，如

```latex
(\frac{2}{3}+1)
[\frac{2}{3}+(x+y)]
```

$$
(\frac{2}{3}+1),[\frac{2}{3}+(x+y)].
$$

可以使用如下具有自适应的方法

```latex
\left(\frac{2}{3}+1\right)
\left[\frac{2}{3}+(x+y)\right]
```

$$
\left(\frac{2}{3}+1\right)
\left[\frac{2}{3}+(x+y)\right]
$$

需要注意的是两者需要成对出现，而且如果遇到公式太长需要换行，但‘(’与‘)’不在同一行时，该函数无法使用。此时可以考虑替换方案，利用<span style='color: blue'>∖big,∖bigg,∖Big,∖Bigg</span>。四者依次增大，用法与∖left,∖right)用法相同。

## 证明结束后居右的正方形

1. 直接使用∖qed命令，注意该命令需要放在数学环
   境以外。如

   ```latex
   证明：blablabla
   	blabla. \qed
   ```

2. 引入amsthm包，使用

   ```latex
   ∖begin{proof}
   ···
   ∖end{proof} 
   ```

   会自动添加。注意该命令默认为英文‘Proof’，如需中文‘证明’，需
   在文档设置区添加命令

   ```latex
   ∖renewcommand{∖proofname}{证明}
   ```

## 公式空格问题

当公式过长，需要换行，如下面公式
$$
\begin{align*}
\varphi(x, \zeta)
&=(\int^x_{-\infty}\frac{1}{2\mathrm{i}\zeta}u(\tau)\phi(\tau, \zeta)e^{\mathrm{i}\zeta \tau}d\tau + 1)
            e^{-\mathrm{i}\zeta x}+      \\
&e^{\mathrm{i}\zeta x}\int^x_{-\infty}-\frac{1}{2\mathrm{i}\zeta}u(\tau)\phi(\tau, \zeta)e^{-\mathrm{i}\zeta \tau}d\tau
\end{align*}
$$
第二行应该缩进，我们借助于占位符\qquad

```latex
...\\
&\qquad +...
```

$$
\begin{align*}
\varphi(x, \zeta)
&=(\int^x_{-\infty}\frac{1}{2\mathrm{i}\zeta}u(\tau)\phi(\tau, \zeta)e^{\mathrm{i}\zeta \tau}d\tau + 1)
            e^{-\mathrm{i}\zeta x}      \\
&\qquad + e^{\mathrm{i}\zeta x}\int^x_{-\infty}-\frac{1}{2\mathrm{i}\zeta}u(\tau)\phi(\tau, \zeta)e^{-\mathrm{i}\zeta \tau}d\tau
\end{align*}
$$

还有其他占位符，如下
$$
\begin{array}{|l|l|l|l|}
\hline
两个quad空格 & a \backslash qquad b & a \qquad b & 两个m的宽度   \\
quad空格   & a \backslash quad b  & a \quad b  & 一个m的宽度   \\
大空格      & a\backslash b       & a\ b       & 1/3m宽度   \\
中等空格     & a\backslash;b       & a\;b       & 2/7m宽度   \\
小空格      & a\backslash,b       & a\,b       & 1/6m宽度   \\
没有空格     & ab         & ab\,       &          \\
紧贴       & a\backslash!b       & a\!b       & 缩进1/6m宽度 \\
\hline
\end{array}
$$


# 文档相关

## 双击pdf文件无法返回代码处

是文件名中有空格导致，重命名，不能有空格。

## 生成中文pdf复制时乱码

在文档头部引入ccmap包即可。

## 特殊符号的使用

因部分符号在latex中作为命令的一部分，具有特殊含义，不能直接使用，如‘∖’，‘%,’‘&’，‘{’等，想要使用它们，需要转义，‘∖’需要用‘∖backslash’，而其他符号只需在符号前边加‘∖’,如‘∖&’。

## 生成中文pdf目录乱码

打开命令框(C:\\),运行下面命令

```bash
% 首先跳转到当前文件夹: 如要修改paper.tex,所在文件夹为E:/paper/paper.tex，输入
cd E:/paper
% 回车，然后输入
gbk2uni paper.out
% 回车，接着运行
pdflatex paper.tex
```

## 参考文献

### 参考文献列表

引用的参考文献分为两种，自己写的和其它地方导出。

**前者示例：**

```latex
\documentclass{article}
\begin{document}
\section{Introduction}
Partl~\cite{pa} has proposed that \ldots
Part2~\cite{ba} has proposed that \ldots


\begin{thebibliography}{2}

\bibitem{pa} H.~Partl: \emph{German \TeX}, 69 TUGboat Volume~9, Issue~1 (1988)
\bibitem{ca} H.~Part2: \emph{German \TeX}, 69 TUGboat Volume~9, Issue~1 (1988)

\end{thebibliography}

\end{document}

```

引用格式需自己写，较为麻烦。

**后者示例：**

```latex
\documentclass{article}
\bibliographystyle{plain}

\begin{document}
\section{Some words}
Some excellent books, for example, \cite{c1}
and \cite{c2} \ldots


\bibliography{books} %导出参考文献在同文件夹下的books.bib文件
\end{document}

```

books.bib文件内容如下(ResearchGate导出的BibTeX类型)

```latex
@article{c1,  % c1是自定义，与引用保持一致即可。
author = {Ayano, Takanori and Nakayashiki, Atsushi},
year = {2013},
month = {03},
pages = {},
title = {On Addition Formulae for Sigma Functions of Telescopic Curves},
volume = {9},
journal = {SIGMA},
doi = {10.3842/SIGMA.2013.046}
}

@article{c2,
author = {Ayano, Takanori and Nakayashiki, Atsushi},
year = {2013},
month = {03},
pages = {},
title = {On Addition Formulae for Sigma Functions of Telescopic Curves},
volume = {9},
journal = {SIGMA},
doi = {10.3842/SIGMA.2013.046}
}
```

**需要注意的是<span style='color: red'>books.bib</span>中的内容是要作为<span style='color: red'>.tex</span>文件的一部分，因此要符合latex书写要求。**如果使用*百度学术*导出，其格式如下：

```latex
@article{c1,
  title={Building Abelian functions with generalised Baker&ndash;Hirota operators},
  author={England, Matthew and Athorne, Chris},
  journal={Symmetry Integrability & Geometry Methods & Applications},
  volume={8},
  number={2},
  pages={037},
  year={2012},
}
```

如果直接引用就会报错

```latex
! Misplaced alignment tab character &.
```

原因在于书名和杂志名中函数<span style='color: red'>&</span>，  因为&是特殊字符，一般用于对齐环境中，想要使用需要加反斜杠转义。

### 参考文献引用

一般使用`\cite{name}`，效果为“blablabla[1]”。如果想要参考文献出现在右上角，且没有括号，则使用添加如下命令

```latex
\newcommand\upcite{\textsuperscript{\cite}}
\usepackage[numbers]{natbib}
\setcitestyle{open={},close={}}
```

然后使用`\upcite{name}`即可，"blablabla^1^"。



## 图片/图形

### latex绘制简单图形

借助于<span style='color: red;'>picture</span>环境，latex提供的一个作图环境，可以做一些简单的图形，如直线，向量，圆，椭圆等。此外，也可以将图片插入该环境。使用方法如下

```latex
%定义单位长度
\setlength{\unitlength}{1cm} 
% 线条粗细， thickness
\thicklines      
\def\width{10}
\def\height{6}
% 画图区域的(width, height)(x-方向偏移, y-方向偏移)
\begin{picture}(\width, \height)(0, 0)  
	% 画直线， \put(起点位置){\line(方向){长度}}
	\put(0, 0){\line(0, 1){\height}}
	\put(0, 0){\line(1, 0){\width}}
	\put(\width, \height){\line(0, -1){\height}}
	\put(\width, \height){\line(-1, 0){\width}}
	% 画圆
	\put(5, 3){\circle{1}}
	\put(5, 3){\circle{6}}
	\put(5, 3){\circle*{1}}
	% 画椭圆， \oval(中心)[l左/r右半部份]
	\put(5, 3){\oval(5, 3)[]}
	\put(5, 3){\oval(5, 3)[r]}
	\put(5, 3){\oval(5, 3)[l]}
	% 添加文字
	\put(7, 0.5){$x^2+y^2=1$}
	% 向量
	\put(0, 3){\vector(1, 0){10}}
	\put(5, 6){\vector(0, -1){6}}
	% 插入图片，可以用于精确图片定位
	\put(0.1, 0.1){\includegraphics[width=3cm]{bird.jpg}}
	\put(0.1, -3.5){\includegraphics[width=2cm]{bird.jpg}}
\end{picture}

这是一个段落，我是第一行，它是第二行，你是第几行？秦时明月光，疑是地上霜。巨头望明月，低头口手机。
```

效果如下所示

![1571394985076](https://cdn.nlark.com/yuque/0/2019/png/122742/1571975047539-e670575b-750a-494f-8123-2a59e6832237.png)

容易看出，当绘制的元素溢出绘图区域时，其浮于文档，不占空间。这样就导致其浮在后面的文字上方。因此，绘制的元素都应该位于绘图区域内。此外，如果绘图区域偏移，其所占空间仍为原区域。

### 文字环绕图片

借助于<span style="color: red">wrapfig</span>包，代码如下

```latex
%                  左  左偏距离
\begin{wrapfigure}{l}[0cm]{0pt}
	\includegraphics[width=2cm, height=3cm]{bird.jpg}
\end{wrapfigure}
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
text text text text text text text text text text text text
```

效果

![1571395045329](https://cdn.nlark.com/yuque/0/2019/png/122742/1571975047687-28c5c1a9-c814-4ec4-9cc0-2b787573a5ce.png)

## 摘要等命令

如果使用英文文档类，如(article)等，摘要等标题为英文。下面的命令可以改为中文(当然，首先要保证文档有中文环境)

```latex
\renewcommand\abstractname{摘要}
```

而如果在文档中引入了ctex包，因为其中重新定义摘要等标题为中文，所以如果想要改回英文，利用上述命令即可。

## 中文支持

1. 直接使用中文文档，即将

   ```latex
   \documentclass{article} -->   \documentclass{ctexart}
   \documentclass{report} -->   \documentclass{ctexrep}
   % and so on
   ```

2. 如果使用英文文档，则在文档设置区添加

   ```latex
   \usepackage{xeCJK}
   \setCJKmainfont{SimSun} % 设置字体，这一行可以没有，默认为黑体。如果系统缺失黑色字体，则中文不会显示
   ```

   一般而言，这样设置以后还是不显示中文字体。这是文件编码导致的，latex生成的文件默认编码是ASCII码，而我们需要将文件编码更改为**utf-8**。方法如下，用记事本打开该文件，然后选择另存，编码改为UTF-8即可。

   <img src="https://cdn.nlark.com/yuque/0/2019/png/122742/1571976267881-1e2029f1-a48b-4804-8716-caeec684ec25.png" style="zoom:50%;" />

# 错误提示



1. <span style='color: red'>Tex capacity exceeded, sorry[save size = ...]</span>

   可能情况：书写错误导致超出环境最大容纳量。如将

   ```latex
   ∖end{align}
   % 写成
   ∖end{align]
   ```

   导致环境中有大量字符，超出容纳量。

2. <span style='color: red'>Extra alignment tab has been changed to ∖cr</span>

   在使用矩阵时，实际的列数与声明的列数不同所致，如：

   ```latex
   
   \left(
   \begin{array}{cc} % 此处声明为两列
   a & a & a \\
   a & a & a \\
   a & a & a \\  	  %实际是三列
   {end}{array}
   \right)
   ```
   
3. <span style='color: red'>!Improper alphabetic constant.  ...</span>

    可能为编码问题，不支持中文的环境。引入中文环境或者可以尝试使用xeLatex编译。在文件头部添加
    
    ```latex
    % !Mode:: "TeX:UTF-8"
    % !TEX program = xelatex
    \documentclass{}...
    ```
    
4. <span style='color: red'>Unknown graphix extension eps.</span>

    引入.eps格式图片时出现，原因是使用了汉化模板，所使用的编译器不支持，更换其它编译器(pdflatex,latex等)即可。

5. <span style='color: red'>! Misplaced alignment tab character &.</span>

    在非对齐环境下使用了“&”，其是特殊字符，使用需要加反斜杠。

6. <span style='color: red'>fontspec error: "font-not-found"</span>

    <span style='color: red'>The font "SimHei" cannot be found.</span>
    
    电脑缺少该字体(黑体)，可以换一种字体。如
    
    ```latex
    \setCJKmainfont[BoldFont=SimSun]{SimSun} % 宋体
    \setCJKmonofont{SimSun}  % 设置缺省中文字体
    ```
    
7. <span style='color: red'>!File ended while scanning use of \\@argdef.</span>

    可能原因是自定义命令缺少括号：<span style='color: red'>}</span>.


