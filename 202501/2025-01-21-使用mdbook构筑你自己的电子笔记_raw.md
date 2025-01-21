Title: 使用mdbook构筑你自己的电子笔记

URL Source: https://www.aye10032.com/2023/09/12/2023-09-12-mdbook/

Published Time: 2023-09-12T15:32:50.000Z

Markdown Content:
鸽子窝
 首页
 归档
 分类
 标签
 关于
 我的追番
 友链
_
 Aye10032  2023年9月12日 下午
 1.9k 字  16 分钟
教程
(22)
JetBrains
(2)
开发文档
(1)
网络
(2)
计算机
(17)
Linux常用指令
Markdown闲谈
Nvidia-smi指令参数翻译
WIN10关闭蓝牙耳机绝对音量功能
git常用指令
More...

本文最后更新于 2023年8月27日 下午

前言

写下本文的动机其实是记录一下我自己准备跳出gitbook时所做的事情。在之前，我是拿gitbook来做笔记并且保存在GitHub的，gitbook很好用，渲染也漂亮，还提供免费的在线浏览。不过有一个问题就是这玩意在商业化之后吃相难看起来了，下载要收费，导出PDF要收费，什么都要收费。于是转而开始寻找替代品，找到了这个：mdbook。

mdbook是一个基于rust的电子书系统，使用起来和原来的gitbook别无二致，同时也有大量的第三方插件可供选择，基本上如果你以前使用的是gitbook，那么你将能够非常完美的转换为使用mdbook编写书籍.

一、安装[1]
1.1 安装rust[2]

由于mdbook是使用rust编写的，因此在使用时需要先安装rust，本教程使用的环境为Windows11，因此直接在下载界面下载官方的rustup-init.exe后运行即可。

运行之后会出现这样一个命令行界面，直接回车即可：

之后它就会开始自行安装相关组件并添加环境变量，当运行结束之后，再次回车退出即可：

此时再次打开命令行，输入以下指令：

1

	
cargo --version

POWERSHELL

如果能够正常输出，则说明安装成功：

image-20230912154940951
1.2 安装mdbook

打开命令行，运行以下指令：

1

	
cargo install --git https://github.com/rust-lang/mdBook.git mdbook

POWERSHELL

它会安装GitHub上最新版本的mdbook，不过如果你网络不太行，在这一步失败的话，也可以直接运行：

1

	
cargo install mdbook

CMAKE

这会安装发行版的mdbook，版本可能会存在些许的更新不及时，但一般也不会差太多。

安装完毕之后，运行：

1

	
mdbook --version

ADA
image-20230912160143716

正常输出，安装成功。

二、编写书籍
2.1 初始化目录

来到你想要创建书籍的根目录下，运行以下指令：

1

	
mdbook init 你的书籍名

CSHARP

这行指令会自动建立文件夹，例如你希望你的书存在D:/notebook/mybook下，那么实际上你需要做的是进入notebook目录，运行

1

	
mdbook init mybook

CSHARP

运行过程中会询问是否创建gitignore和书籍名称是什么，选是并输入你的书籍名称即可：

运行完毕之后，可以看到它自行创建了PRMLNote文件夹，并在其中创建了初始文件：

此时在这个目录中运行以下指令：

1

	
mdbook serve --open

ADA

mdbook就会自动生成html文件并在浏览器中打开：

由于我们还什么都没有写，因此这里就只有初始的默认界面。

2.2 配置文件

在我们的根目录中，有一个book.toml文件，这个文件就是我们书籍的配置文件，书籍的标题、渲染主题、第三方插件等都是在这里配置的。我这里贴一个我的示例：

1
2
3
4
5
6

	
[book]
authors = ["Aye10032"]
language = "zh"
multilingual = false
src = "src"
title = "PRML note"

TOML

当然你的肯定不会跟我一样，这里有几个条目：

authors：作者，可以有多个
language：书籍的语言，如果下面的multilingual没有启用，则这行意义不大
multilingual：是否有多个语言翻译
src：书籍源文件所在目录，默认为src
title：书籍的标题

后面我们还会多次用到这个文件，记好了。

2.3 新建章节

与gitbook一样，mdbook也是使用一个SUMMARY.md来管理文章组织结构的，我来贴一个例子加以说明：

1
2
3
4
5
6
7
8
9
10
11
12
13

	
# Summary

- [introduction](README.md)

# part1&2

- [Chapter 1](part1/chapter_1.md)
- [Chapter_2](part2/chapter_1.md)
  - [chapter_2.1](part2/chapter_2.md)

# part3
- [Chapter_3.1](part3/chapter_1.md)
- [chapter_3.2](part3/chapter_2.md)

MARKDOWN

同时附上目录结构：

通过这个SUMMARY.md渲染出来的目录是这样的：

这样一来就比较好理解了，实际上，本身markdown文件怎么存，其实和目录结构是完全无关的，我这里分成多个文件夹完全是为了自己看的时候方便组织管理。真正决定目录结构的就是SUMMARY.md中的缩进，每一级列表的缩进就代表一集目录，例如上图中的chapter_2.1，由于缩进了一级，因此在目录渲染后表现为一个二级目录。

同时，SUMMARY.md中的一级标题也在目录渲染中起到作用，它会表现为一条单纯的文本，不可点击，例如上图的part1&2和part3，这也可以用于章节管理。

SUMMARY.md的全文标题（默认为SUMMARY）在渲染时会被自动忽略

不过目前来看，mdbook好像还不能像gitbook那样通过命令行自动生成新的章节文件，因此你得每次手动编辑SUMMARY.md来添加新的章节。

三、使用插件

mdbook本身有着丰富的第三方插件，官方列了一个插件列表：https://github.com/rust-lang/mdBook/wiki/Third-party-plugins。

每一个插件都有说明，你可以根据需要寻找符合要求的插件点进去链接查看如何配置，我这里说几个我常用的

3.1 数学公式支持

插件仓库链接：https://github.com/lzanini/mdbook-katex

安装&配置

运行以下命令进行安装：

1

	
cargo install mdbook-katex

CMAKE

安装完毕后，在book.toml中添加以下内容：

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17

	
[preprocessor.katex]
after = ["links"]
# KaTeX options.
output = "html"
leqno = false
fleqn = false
throw-on-error = true
error-color = "#cc0000"
min-rule-thickness = -1.0
max-size = "Infinity"
max-expand = 1000
trust = false
# Extra options.
no-css = false
include-src = false
block-delimiter = { left = "$$", right = "$$" }
inline-delimiter = { left = "$", right = "$" }

TOML

具体参数的含义，这是官方的说明：

Argument	Type
output	"html", "mathml", or "htmlAndMathml"
leqno	boolean
fleqn	boolean
throw-on-error	boolean
error-color	string
min-rule-thickness	number
max-size	number
max-expand	number
trust	boolean

不过基本上不需要修改，保持默认即可。

演示

源文件：

渲染结果：

3.2 HINT

在gitbook中，可以使用hint来实现一些提示块，在mdbook中，同样也有类似的插件实现这一功能，mdbook-admonish：

仓库链接：https://github.com/tommilligan/mdbook-admonish

安装&配置

首先安装该插件：

1

	
cargo install mdbook-admonish

CMAKE

接下来，在书根目录下运行：

1

	
mdbook-admonish install

CMAKE

运行结束后，你会发现你的book.toml中多了以下内容：

1
2
3
4
5
6
7
8

	
[preprocessor.admonish]
command = "mdbook-admonish"
assets_version = "2.0.2" # do not edit: managed by `mdbook-admonish install`

[output]

[output.html]
additional-css = ['.\mdbook-admonish.css']

TOML

同时，根目录下多了一个mdbook-admonish.css文件，说明安装完毕。

演示

源代码：

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20

	
```admonish info
A beautifully styled message.
```


```admonish warning
A beautifully styled message.
```

```admonish danger
A beautifully styled message.
```

```admonish example
A beautifully styled message.
```

```admonish
A plain note.
```

MARKDOWN

渲染结果：

3.3 PDF导出

所使用的插件为mdbook-pdf，仓库地址：https://github.com/HollowMan6/mdbook-pdf

安装&配置

安装：

1

	
cargo install mdbook-pdf

CMAKE

这里安装的时候需要电脑上有chrome或者edge，如果没有，可以安装一个，或者运行以下指令：

1

	
cargo install mdbook-pdf --features fetch

ADA

程序会制动下载chromium并编译运行。

安装完毕后，在book.toml中添加以下内容：

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27

	
[output.pdf]
## Set for auto-retrying if failed to generate PDF.
# trying-times = 1
## This backend only support latest Chromium based browsers, not Safari and Firefox currently.
## If needed, please specify the full path.
## If you specify the wrong binary, chances are that there will be a timeout error.
# browser-binary-path = ""
## Assign the static hosting site url so that relative links outside the book can be fixed.
static_site_url = "https://aye10032.gitbook.io/computernetwork/"
## Check Chrome Devtools Protocol Docs for the explanation of the following params:
## https://chromedevtools.github.io/devtools-protocol/tot/Page/#method-printToPDF
landscape = false
display-header-footer = true
print-background = true
theme = ""
scale = 0.8
paper-width = 8
paper-height = 10
margin-top = 0.5
margin-bottom = 0.5
margin-left = 0.5
margin-right = 0.5
page-ranges = ""
ignore-invalid-page-ranges = false
header-template = "<h3 style='font-size:8px; margin-left: 48%' class='title'></h3>"
footer-template = "<p style='font-size:10px; margin-left: 48%'><span class='pageNumber'></span> / <span class='totalPages'></span></p>"
prefer-css-page-size = true

TOML
支持目录

默认渲染出来的pdf是没有目录的，可以使用

1

	
pip install mdbook-pdf-outline

POWERSHELL

安装mdbook-pdf-outline，并在book.toml中添加：

1
2

	
[output.pdf-outline]
like-wkhtmltopdf = true

TOML

之后通过mdbook build编译，即可得到PDF文件。

参考文档
https://rust-lang.github.io/mdBook/guide/installation.html ↩︎
https://www.rust-lang.org/tools/install ↩︎
教程 > 计算机
 #教程 #计算机
使用mdbook构筑你自己的电子笔记
https://www.aye10032.com/2023/09/12/2023-09-12-mdbook/
作者
Aye10032
发布于
2023年9月12日
更新于
2023年8月27日
许可协议
自用ffmpeg脚本合集
在自己的电脑上布置chatGPT

 目录

前言
一、安装[1]
1.1 安装rust[2]
1.2 安装mdbook
二、编写书籍
2.1 初始化目录
2.2 配置文件
2.3 新建章节
三、使用插件
3.1 数学公式支持
3.2 HINT
3.3 PDF导出
参考文档
Hexo Fluid
苏ICP备19040408号-2
苏公网安备 32108102010462号
