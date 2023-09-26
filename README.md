# 文件目录结构说明
	主文件main.tex，编译起点（应当编译该文件，而非其他任何子文件）
	sections子目录，包含了所有会被main.tex主文件所引用的子模块文件
	fig子目录，包含了该latex工程所有的图片
	references.bib文件，包含了该latex工程所有的参考文献的bib信息
	IEEEabrv.bib文件，定义了IEEEtran模板的参考文献显示格式，用于辅助references.bib文件，用法详见该文件内的文字说明

# 子模块和主模块
将传统的单个latex文件划分为一个main.tex文件和多个子模块，方便管理；
这些子模块均被放置在sections目录下，该目录与main.tex文件位于同一级目录，包括：
	% tex_config.tex
		% 用于文档格式定义、包引用等
	% PaperHeader_Title_Authors.tex
		% 包含了文章题目，作者信息等
	% 其余子模块则是将文章中每个章节单独拆分而来，如Abstract.tex, Introduction.tex等等

在main.tex文件中，使用 \input{} 命令即可在正文中插入各子模块内容
另外，在子模块tex文件首行，添加 % !tex root = ../main.tex 命令（该命令包含%符号）
	% 用于声明各个子模块和主文件之间的从属关系，并在所有模块之间实现全局引用源的索引

# 关于图片的说明：所有图片务必使用矢量图
关于矢量图的制作方法：
	% 对于框架图，可直接在 draw.io 线上绘图网站上，直接绘制所需框架图，并导出矢量图；
	% 对于数据结果图，可使用python脚本绘图，并直接输出矢量图
关于其他绘制矢量图的方法（过程较复杂）：
	% 对于框架图，可使用Visio软件进行绘图，并导出PDF格式的文件（矢量结果）；
	% 对于数据结果图，可使用Excel软件绘制柱状图、曲线图等，再将excel图粘贴到visio文件内（以“增强型图元格式文件”进行粘贴），再将visio文件导出为PDF即可。

# 关于交叉引用：使用\cref{lable}
文件中的交叉引用，可以使用更强大的\cref{lable}函数
	% 其中\cref需要提前引用以下两个宏包，中括号内的参数配置可自定义
		\usepackage[colorlinks=true,citecolor=blue]{hyperref}
		\usepackage[capitalise]{cleveref}
另外，交叉引用不建议使用传统的\ref{lable}函数
二者的用法对比如下：
	% Figure \ref{fig_1} 等价于 \cref{fig_1}
	% Table \ref{tab_1} 等价于 \cref{tab_1}
可见，\cref{}函数的功能更加强大、用法更加简洁

# 关于ACKNOWLEDGEMENTS章节
非必要在文章中呈现该章节

