[TOC]

# Overleaf写论文杂记





## 论文写作技巧

（大部分由他人总结，不建议外传）

* ##### 上传文件模板为zip格式

* ##### KeyWords

​		KeyWords中的首字母均大写

![image-20250706141123257](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250706141123257.png)

* ##### 不能用引用编号[x]作为主语

* ##### 方法不能使用propose(提出，建议)，即不可使用：某方法 propose XXX

* ##### ==特殊字体要求==
  
  * 向量：小写加粗字母 	$\mathbf{x}$
  * 矩阵：大写加粗字母 	$\mathbf{A}$
  * Scalar：大写不加粗字母	$A$
  * 参数：希腊小写字母	 $\alpha$
  * 集合：大写花体字母	 $\mathcal{A}$
  
  ![image-20250706143011993](C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250706143011993.png)
  
* ##### 模型缩写

  使用网站[Acronymify! - Automatically generate fun acronyms for your project](https://acronymify.com/)缩写；

  在筛选缩写的时候，一般选择缩写词对应是一个有意义的单词的缩写；

  在实验部分 baseline 方法列举时，使用模型缩写要注意：如果是某 一篇文章中采用过的 baseline，最好采用论文中的缩写方式，然后引用该论文；

* ##### 书写套路

​	From Table xx, we observe: 1)现象 1+原因；2)现象 2+原因...

* ##### Reference规范

  * 引用会议： 作者、会议名称全称，时间，出版社，页数范围；
  * 引用期刊 ：作者、期刊名称全称，时间，页数范围、vol, issue no （vol全称是Volume，即卷；no是期）；
  
  * 地点、doi等信息一律不要 （DOI，Digital Object Identifier，是一种用于唯一标识学术文献、数据集、专利等数字内容的永久性标识符。它通常由一串字母和数字组成，可以帮助快速定位和引用文献，格式形如 10.xxxx/xxxxxxxx）；
  * 所有的引用都需要加空格~\cite{x}  ；
  * SIGIR专用  (国际 ACM SIGIR 信息检索研究与发展会议，ai关联不大，先参考)
    * Reference里面需要有5-10个左右的SIGIR或者TOIS文章引用；
    * 长文的正文最好是9页整，reference占据最后一页； Reference里面的出版社需要写法一致，比如都用简写；
    *  年份只需要出现一次即可。

* ##### Rebuttal（答辩）

  * rebuttal的目的是让差的分数变高，好的分数尽量维持；尽管reviewer理解错了，author说话也不能言辞过激，而应该委婉的指出，让reviewer 很有面子的把自己的错误改过来；（该低头时就低头）
  * 论文就是考卷，rebuttal 的时候，作者给老师说，我错了，下次会改， 这样阅卷老师是不会给你该分数的；

  * 期刊rebuttal：会议和期刊的rebuttal意义不同。期刊让你rebuttal说明第一轮结果是major或minor，那距离命中其实很近了
    * 期刊的rebuttal，其实就是写response letter，更精准的说就是谦逊。 即使你的工作写的明明白白，条理清晰，也得谦逊的说自己没写好从而导致了 reviewer 的误解，该加实验加实验，reviewer 让改哪里你就老老实实修改哪里；
  * 会议rebuttal：会议是给所有人rebuttal的机会
    * 会议的reviewer 愿意把负分改成正分的前提是那个 reviewer的逻辑错了，或者是他理解错了，亦或他没读明白。所以 rebuttal 的时候就要自信；
    * 会议 rebuttal 的目的是，让给了你负分的 reviewer 改变看法，让给 了你正分的 reviewer 维持原有的形象。所以针对后者，不要去惹们就是最好的维持；

* ##### Other Details

  * 投文章不管是期刊还是会议，请务必坚持代码和数据的匿名公开发布，否则不用投稿。
  * 论文里面可给一个长的名字起简称，方便后文引用。若后文没有引用，则不必要简称；
  * 缩写在全文只需要出现一次，杜绝每出现一次就缩写一次；
  * 若url很长，通过tiny url(https://tinyurl.com/)缩短；

  * 解释一个公式里面的字母的时候，句子之间可以是句子1, 句子2, 句子i, and 句子i+1。（只在最后使用and）

  * 所有的 comments，修改的时候，先备份一遍，然后修改一个comment，删除一个；

  * 所有equation的引用，全部统一成: Eqn.($\ref{x}$)；（这种写法将引用的公式编号放在数学模式中，直接看似乎与Eqn.(\ref{x})没有区别）

  * 用vspace 命令，缩小 caption和 figure 或者 table 或者正文之间的空白；

  * 表格中的精准度或者统计数据，小数点后面保留的位数要一致。（大部分似乎保留两位）

  * caption（表或图的标题）和footnote（脚注，^脚注^）后面必须有句点.

  * footnote的标号和前面的单词之间不留空格，错：<img src="C:\Users\SHI\AppData\Roaming\Typora\typora-user-images\image-20250706233316011.png" alt="image-20250706233316011" style="zoom: 50%;" />

  *  e.g., 后面要有空格。

* ##### 待补充







## 英文写作注意点

* 主语为人时，句子使用过去式；主语为工作时，句子一般使用现在时;
* Abstract 不需要用过去式。实验和 related work 部分当主语为人的时候，才用过去式；
*  注意英文计数法，比如：13,118； 
* promising performance 中的 performance是不可数名词;
* 可数名词，尤其单数出现时，前面需加冠词；
* 一句话前后单复数要一致。
* data是复数。
* respectively 放在句子时，需要在前面加一个逗号；
* however 后要加逗号：however, XX，so 比较口语化，尽量不要使用在academic writing；（总而言之避免一切口语化表达）
* can not是错误的，应该是 cannot，can't 过于口语化，不可应用在论文中；
* 在写 academic paper 的时候，尽量不要用 want to, 可以用 expect, intend 等替代；
* don't 和doesn't不可用在academic writing中；
* on the one hand 和 on the other hand 这对词不能单独使用，需成对使用，修饰的是一个事物的两方面。用法：On the one  hand, A XX. On the other hand, A XX. 
* including, such as 等词本身即为列举，其后面不要跟etc；
* 给模型或者图中每个 component 起名字时，要用名词或者动名词词组。
* then是副词，需要和连词and一起用: XX, and then XX.
* 在实验分析中，引用一个表格或者 figure 的时候，table 和  figure 的首字母应该大写。正确的案例如下：As shown in  Figure 2,
* 很多单词有英氏拼写和美式拼写，一篇论文里的词汇拼写要统一：比如全篇要么都用美式dialog，要么都用英氏dialogue；
* auto 一般是作为前缀使用，后面需要加破折号 auto-generated  guideline；除非是表示自动化/汽车等可以单用，其他情况都要写全称 automatic evaluation; geo 同理；
* 换行符
  * 使用方法：换行符“-”一般是放在单词的音节后，比如separate, 如果 不确定它的音节可以直接搜索单词得“sep·a·rate”, 那换行符就可以是 “sep-a-rate”；
  * %%% 避免单词被-分割，具体解决方法：
    * %% 1  \hyphenpenalty=5000 %%\tolerance=1000; %可以把这两个参数的调 整加到tex文件里。hyphenpenalty的意思比较显而易见，这个值越大断 4   强哥写论文  How to write academic papers  字出现的就越少。tolerance越大，换行就会越少，也就是说，latex会把 本该断开放到下一行的单词，整个儿的留在当前行；
    * %% 2. \hyphenation{hy-phen-a-tion}%这个命令告诉 latex，hyphenation只 能从标有短横线(-)的地方断开；
    * \clubpenalty=10000 \widowpenalty = 10000 \hyphenpenalty=7000  \tolerance=7000 放 begin{document}前面； 

* 注意every和each的区别:
  * **"Every"**：表示“每个”或“所有”，后面接的是单数名词，但它表达的是整个集合中所有的个体。
  * **"Each"**：强调每个单独的个体或元素，通常用于强调个体之间的独立性,后面接的是单数名词,通常用于描述较小的、个别的或被明确列出的集合。
* 写作的措辞
  * 写作要用中性和褒义词，不确定的时候可以百度谷歌。比如形容一个胖的身型，不要用fat figure, 要换成plump; 
  * 不要一直用同一个简单词，在不影响句意的前提下，多用近义词增加文采和可读性，部分近义词替换如下：
    * show-----represent, present, illustrate, exhibit, demonstrate, summarize; 
    *  use-----utilize, adopt, employ, exploit, resort to, exercise; 
    * boost-----enhance, strengthen, improve, advance;





## Overleaf语法规范

#### 基本结构（视模板而定）

```latex
\documentclass{article}			%根据模板调整
\newcommand{\命令名}{替换内容}		%自定义命令 若干
\usepackage{宏包}					%若干
\definecolor{颜色名}{模型}{参数}	%自定义颜色，若干

\begin{document}
\title{论文标题}
\author{作者}

\begin{abstract}
摘要
\end{abstract}

\keywords{关键词}

\section{}						%若干
\input{}						%若干

\bibliographystyle{ACM-Reference-Format}	%参考文献格式
\bibliography{reference}					%参考文件内容

\end{document}
```

##### \newcommand

```latex
\newcommand{\命令名}{替换内容}		%自定义命令 若干

\newcommand{\ModelName}{R-MFDN}
{\ModelName}					%在文档中会被替换为 R-MFDN
ewcommand{\PersonNum}{$54$}		%表示数字54
```

注意：文字段中出现较大数字建议按千位分隔，Latex写为：`$249{,}138$`

##### \usepackage  常用包

```Latex
% 页面与字体
\usepackage[a4paper, margin=2.5cm]{geometry}  % 页面边距
\usepackage{times}                            % 字体（如需符合会议格式）
\usepackage{setspace}                         % 行距（如 \onehalfspacing）

% 图表插入
\usepackage{graphicx}                         % 插入图像
\usepackage{float}                            % 精确控制图表位置（[H]）
\usepackage{subcaption}                       % 多子图布局
\usepackage{booktabs}                         % 美观的表格线条
\usepackage{multirow}                         % 表格跨行
\usepackage{makecell}                         % 表格内换行

% 数学公式
\usepackage{amsmath, amssymb, bm}             % 公式符号与变量加粗
\usepackage{mathtools}                        % 数学增强（如 \coloneqq）

% 颜色与标注
\usepackage{xcolor}                           % 自定义颜色
\usepackage{colortbl}                         % 表格背景色

% 引用与跳转
\usepackage{cite}                             % 压缩引用，如 [1–3]
\usepackage{hyperref}                         % 超链接支持（引用跳转）
\hypersetup{colorlinks=true, linkcolor=blue, citecolor=blue}

% 算法伪代码
\usepackage{algorithm}
\usepackage{algorithmic}                      % 或 algorithmicx + algpseudocode 更强
```

##### \definecolor

```latex
\definecolor{颜色名}{模型}{参数}	%自定义颜色，若干

\definecolor{myblue}{RGB}{0, 100, 200}
\textcolor{myblue}{这是蓝色文字}	%用于文字
\cellcolor{myblue} 精度			%用于表格	
```

##### \begin{}  \end{}

```latex
\begin{环境名}
  % 这里写环境内容
\end{环境名}
```

##### \section{}

```Latex
\section{}			%一级标题
\subsection{}		%二级标题
\subsubsection{}	%三级标题
\paragraph{}		%四级标题（不编号）

\section*{研究背景}	%去掉编号标题（但保留目录）
\addcontentsline{toc}{section}{研究背景}
```

##### \input{}

```Latex
\input{chapters/introduction}
```

将另一个 `.tex` 文件的内容原样插入到当前位置,不需要加 `.tex` 后缀。

适用于论文分章节写作或模块化排版。

##### \bibliography{}

```Latex
\bibliographystyle{ACM-Reference-Format}
\bibliography{reference}
```

在.tex文件中引用reference.bib生成参考文献，并采用ACM-Reference-Format.bst文件的格式排版,不需要加文件后缀。



#### 插图片

```latex
\begin{figure}[t]		%[t]表示尽量在页面顶部top插入该图；[b]底部、[h]当前位置、[H]强制当前位置，table同理
	\centering			%图片居中显示
	\includegraphics[width=0.45\textwidth]{图片路径}		%宽度为页面宽度45%的图片
	\caption{图片描述}
    \label{图片标签}	%给图片添加标签，方便在正文中通过\ref{图片标签}引用图片序号
    \vspace{-5mm}		%插图后垂直空间向上收紧5mm
\end{figure} 
```



#### 插表格

```latex
\begin{table*}[t]		%table*表示跨双栏表格，table为单栏表格，figure同理
    \vspace{-2mm}		%调整与上文距离（可选）
    \caption{表格描述}
    \label{表格标签}	 %使用\ref{标签}引用
    \vspace{-3mm} 		%调整与表格距离（可选）
    \centering			%居中显示
    \begin{tabular}{lcccccr}  % 每列对齐方式：l=左对齐，c=居中，r=右对齐
        \toprule		%第一条横线
        Dataset & Year & Real Data & Fake Data & Total & Fake Audio & Fake Text \\
        \midrule		%第二条横线
        Dataset-A \cite{ref1} & 2018 & 500 & 1,000 & 1,500 & No & No \\
        Dataset-B \cite{ref2} & 2019 & 1,200 & 1,200 & 2,400 & Yes & No \\
        Dataset-C \cite{ref3} & 2020 & 10,000 & 50,000 & 60,000 & Yes & Yes \\
        Dataset-D (Ours) & 2024 & 
        \makecell{\textbf{79,827} +\\ 214,438 (\textit{Ref})} & 
        \textbf{169,311} & 
        \makecell{\textbf{249,138} +\\ 214,438 (\textit{Ref})} & 
        Yes & Yes \\	%\makecell 单元格中多行显示；\textbf 加粗突出重点数据（如自己的方法）
        \bottomrule		%第三条横线
    \end{tabular}
\end{table*}
```



#### 插公式

```latex
\begin{equation}	%单行公式
  E = mc^2
  \label{公式标签}
\end{equation}
```

多行公式对齐

```latex
\begin{equation}	
    \left\{		%左侧大括号，\left.表左侧无大括号
    \begin{aligned}		%公式在多行中对齐。用&来指定对齐位置
    \mathbf{f}^{a}& = \mathbf{f}^{a} + \text{SA}(\mathbf{f}^{a}) \\
    \mathbf{f}^{t}& = \mathbf{f}^{t} + \text{SA}(\mathbf{f}^{t}) \\
    \end{aligned}
    \right.		%右侧无大括号，\right\}表右侧有大括号
\end{equation}
```

- `\mathbf{}`：加粗字形（通常用于表示向量、矩阵）。
- `\text{}`：用于公式中的普通文本（例如函数名称）。
- `&`：在 `aligned` 环境中用于指定公式的对齐位置。
- `\left ... \right`：自动调整括号大小。



#### @String{label = "string"} 可以定义多次使用的字符串

用于论文引用中，例如：

```bibtex
@String{Crelle = "Crelle's Journal"}

@article{example,
  author  = "John Doe",
  title   = "A Study on Something",
  journal = Crelle,
  year    = "2020",
}
```

#### 引用文献方法

使用 \cite{引用键} 引用文章，引用前加空格，多写为~\cite{引用键}

##### 1 **@article** - 用于引用期刊文章的条目类型

例如：

```bibtex
@article{smith2021example,
  author    = {John Smith and Jane Doe},
  title     = {Example of a Great Study},
  journal   = {Journal of Examples},
  year      = {2021},
  volume    = {10},
  number    = {3},
  pages     = {123--130},
  doi       = {10.1016/j.example.2021.01},
}
```

##### 2 **@book** - 引用书籍

```bibtex
@book{kosiur2001,
  author    = {David Kosiur},
  title     = {Understanding Policy-Based Networking},
  publisher = {Wiley},
  year      = {2001},
  address   = {New York, NY},
  edition   = {2nd}
}
```

##### 3 **@inbook** - 引用书中的章节或部分

```bibtex
@inbook{miller2005chapter,
  author    = {Frank Miller},
  title     = {Understanding Algorithms},
  chapter   = {5},
  pages     = {101--120},
  publisher = {Springer},
  year      = {2005}
}
```

##### 4 **@inproceedings** - 引用会议论文

```bibtex
@inproceedings{johnson2019conference,
  author    = {Alice Johnson and Bob White},
  title     = {The Future of AI in Healthcare},
  booktitle = {Proceedings of the 10th International Conference on AI},
  year      = {2019},
  pages     = {50--55},
  publisher = {IEEE}
}
```

##### 5 **@techreport** - 引用技术报告

```bibtex
@techreport{doe2020techreport,
  author      = {John Doe},
  title       = {Technical Report on Quantum Computing},
  institution = {XYZ Research Institute},
  year        = {2020},
  number      = {TR-2020-05},
  url         = {http://www.xyz.org/reports/TR-2020-05.pdf}
}
```

##### 6 **@misc** - 引用其他杂项文献, 如个人网站、博客文章、GitHub 仓库等

```bibtex
@misc{rw2019timm,
  author        = {Ross Wightman},
  title         = {PyTorch Image Models},
  year          = {2019},
  publisher     = {GitHub},
  journal       = {GitHub repository},
  doi           = {10.5281/zenodo.4414861},
  howpublished  = {\url{https://github.com/rwightman/pytorch-image-models}}
}
```

##### 7 **@phdthesis** / **@mastersthesis** - 引用博士/硕士论文

```bibtex
@phdthesis{smith2018thesis,
  author    = {John Smith},
  title     = {Advanced Machine Learning Techniques},
  school    = {University of Example},
  year      = {2018}
}
```

#### .cls文件

LaTeX 文档类定义文件，定义文档整体结构、排版样式、章节布局、字体规范等



