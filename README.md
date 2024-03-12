# 文件目录

### 结构说明

__main.tex主文件__：编译起点（应当编译该文件，而非其他任何子文件）

__sections子目录__：包含了所有会被main.tex主文件所引用的子模块文件

__fig子目录__：包含了该latex工程所有的图片

__references.bib文件__：包含了该latex工程所有的参考文献的bib信息

__IEEEabrv.bib文件__：定义了IEEEtran模板的参考文献显示格式，用于辅助references.bib文件，用法详见该文件内的文字说明

### 子模块和主模块
将传统的单个latex文件划分为一个main.tex文件和多个子模块，方便管理；

这些子模块均被放置在sections目录下，该目录与main.tex文件位于同一级目录，包括：
	
* __tex_config.tex__：用于文档格式定义、包引用等

* __PaperHeader_Title_Authors.tex__：包含了文章题目，作者信息等
	
其余子模块则是将文章中每个章节单独拆分而来，如Abstract.tex, Introduction.tex等

在main.tex文件中，使用 `\input{}` 命令即可在正文中插入各子模块内容
另外，在子模块tex文件首行，添加 `% !tex root = ../main.tex` 命令（该命令包含%符号）用于声明各个子模块和主文件之间的从属关系，并在所有模块之间实现全局引用源的索引

# 正文格式

`\section{}`内的标题内容首字符大写（不是全部大写）。

"**.**"的使用：如果是表示句号，则直接使用，如果表示et al. 或其他缩写形式，则应该写为 "**.~**"保证正确格式，因为latex默认句号后的空隙更大。

使用**适当的字体**，如：

  - 斜体 `\emph{}` 表示强调

  - 公式中有单词时使用`\mbox{}` 确保单词是一个整体

正确编写公式、伪代码等。

# 图片

__所有图片务必使用矢量图__

### 矢量图制作方法

对于 __框架图__，可直接在 draw.io 线上绘图网站上，直接绘制所需框架图，并导出矢量图；

对于 __数据结果图__，可使用python脚本绘图，并直接输出矢量图

关于其他绘制矢量图的方法（过程较复杂）：

 * 对于框架图，可使用Visio软件进行绘图，并导出PDF格式的文件（矢量结果）；

 * 对于数据结果图，可使用Excel软件绘制柱状图、曲线图等，再将excel图粘贴到visio文件内（以“增强型图元格式文件”进行粘贴），再将visio文件导出为PDF即可。

### 其他注意事项

确保图片内容大小适中，字体清晰，配色合理。

调整图片在正文附近，便于阅读。

# 参考文献

**参考文献要自己录入，确保格式一致性，尽量不要直接使用谷歌学术的引用格式**

* 命名一致性，如“论文简称-发表年份-期刊/会议简称”，即 “hop-2020infocomm”，命名清晰易懂，在自己工程内保持一致。

* latex会将Title中的全部内容转换为小写，为确保论文名称大小写的正确性，可以使用双括号`{{xxx}}`形式，例如：

   ```tex
   Title = {{CUBIC}: a New {TCP}-Friendly High-Speed {TCP} Variant},
   ```

* Booktitle项尽量使用简称，会议简称为 "in Proc.~会议名"，期刊简称为 "Trans.~期刊名"。 %注：~是LaTeX中半个字符大小的空格

* 不要重复出现相同内容，若在Booktitle中已有出版方（如IEEE），则不需要再加入publisher。

### 会议论文

- 使用 **@inproceedings** 类型，如：

  ```tex
  @inproceedings{hop-2020infocomm,
  	Title={{Hop-by-hop Multipath Routing: Choosing the Right Nexthop Set}},
  	Author={Schneider, Klaus and Zhang, Beichuan and Benmohamed, Lotfi},
  	Booktitle={in Proc.~IEEE INFOCOM},
  	Pages={2273--2282},
  	Year={2020}
  }
  ```

  对于既有全称又有缩写的会议，如"USENIX Symposium on Networked Systems Design and Implementation (NSDI)"，同时使用全名和首字母缩略词（在括号中），而不是只有字母缩写，例如：

  ```tex
  @inproceedings{hull-nsdi12,
  	Title = {Less is More: Trading a Little Bandwidth for Ultra-low Latency in the Data Center},
  	Author = {M. Alizadeh and T. Edsall and B. Prabhakar},
  	Booktitle = {in Proc.~10th USENIX Symposium on Networked Systems Design and Implementation(NSDI)},
  	Year = {2012}
  }
  ```

### 期刊论文

- 使用 **@article** 类型，如：

  ```tex
  @article{fasttcp-ton06,
  	Title = {{FAST TCP}: Motivation, Architecture, Algorithms, Performance},
  	Author = {D. Wei and C. Jin and S. Low and S. Hegde},
  	Journal = {IEEE/ACM Trans.~Netw.},
  	Month = {December},
  	Number = {6},
  	Pages = {1246-1259},
  	Volume = {14},
  	Year = {2006}
  }
  ```

期刊的卷期号和页码号很重要，注意已检索的论文要加入该字段；如已录用但未正式发表的论文，暂无卷期号和页码号，增加DOI号可唯一标识论文

一般期刊都会有对应的简称，如"IEEE/ACM Transactions on Networking"的简称为"IEEE/ACM Trans.~Netw."。可以在IEEE官网查到论文简称，参考文献格式尽量使用简称。

# 引用

### 交叉引用

文件中的交叉引用，可以使用更强大的`\cref{lable}`函数

 其中\`cref`需要提前引用以下两个宏包，中括号内的参数配置可自定义

```tex
\usepackage[colorlinks=true,citecolor=blue]{hyperref}
\usepackage[capitalise]{cleveref}
```
  
另外，交叉引用不建议使用传统的\ref{lable}函数
二者的用法对比如下：

`Figure \ref{fig_1}` 等价于 `\cref{fig_1}`
`Table \ref{tab_1}` 等价于 `\cref{tab_1}`

可见，`\cref{}`函数的功能更加强大、用法更加简洁

### 美观性

导入并修改hyperref宏包，提高引用格式的美观性：

  ```tex
  \usepackage[colorlinks=true,citecolor=blue]{hyperref}
  ```

# ACKNOWLEDGEMENTS章节
非必要在文章中呈现该章节

# 编译

可以直接通过run code进行编译，也可以加入makefile文件：

```makefile
# Makefile for LaTeX document files
# Created by Baochun Li, bli@eecg.toronto.edu, March 30 2001
# Last modified: September 27 2002 

DOCUMENT=main

default: $(DOCUMENT).pdf

$(DOCUMENT).toc: $(DOCUMENT).tex
	pdflatex $(DOCUMENT).tex

$(DOCUMENT).pdf: $(DOCUMENT).toc
	bibtex $(DOCUMENT)
	pdflatex $(DOCUMENT).tex
	pdflatex $(DOCUMENT).tex

#--------------------------------------------------
# $(DOCUMENT).ps: $(DOCUMENT).dvi
# 	dvips -t letter -Ppdf -G0 -o $@ $<
# $(DOCUMENT).pdf: $(DOCUMENT).ps
# 	cat $(DOCUMENT).ps | ps2pdf - > $(DOCUMENT).pdf 
#-------------------------------------------------- 

all: $(DOCUMENT).pdf

clean:
	rm -rf *.aux $(DOCUMENT).log $(DOCUMENT).toc \
     $(DOCUMENT).bbl $(DOCUMENT).blg $(DOCUMENT).pdf \
```



