# 4 brat 功能

原网页：<http://brat.nlplab.org/features.html>

此页面提供了brat功能的概述。 有关详细说明，请参阅[brat手册]（http://brat.nlplab.org/index.html）。

## 全面可视化

brat 标注可视化基于“所见即所得”的概念：基础标注的所有方面都以直观的方式进行可视化表示。

![feature example](http://brat.nlplab.org/img/visualization-1.png)

标注可视化

## 直观的编辑

标注编辑是基于鼠标的，并使用文本编辑器、演示软件和许多其他工具熟悉的直观“手势”。 要标记文本范围，只需通过“拖动”或双击单词鼠标选择它。

![feature example](http://brat.nlplab.org/img/selection-1.png)

选择标注的文本

连接标注（例如，在两个标注之间添加关系）同样简单：在一个标注上单击鼠标并将连接拖到另一个标注上。

![feature example](http://brat.nlplab.org/img/relation-1.png)

Connecting annotations

连接标注

## 与外部资源集成

从v1.3（Crunchy Frog）开始，brat 提供对[normalization]（http://brat.nlplab.org/normalization.html）的支持以及将标注与外部数据库、词汇和本体资源中的数据相关联的各种功能。 例如Freebase，Wikipedia和Open Biomedical Ontologies。

![normalization example](http://brat.nlplab.org/img/normalization-example-2.png)

展示来自Wikipedia的信息

## Zero setup

brat 完全基于标准Web技术构建，没有必要安装任何本地软件或浏览器插件来使用它。

标注人员可以“设置”并开始使用brat，只需在浏览器的地址栏中输入 brat 安装的地址即可。

（设置一个全新的brat服务器确实需要一些操作，但是在运行Web服务器的任何系统上只需五分钟即可完成。）

## 任何语言的文本标注

brat服务器和客户端都实现了完整的Unicode支持，从而支持近100种不同的脚本。

![feature example](http://brat.nlplab.org/img/japanese-example.png)

日文文本的标注

任何语言的文本文档都可以转换为UTF-8编码的Unicode，可以用与ASCII格式的文本相同的方式标注。

## Integrated annotation comparison 集成标注比较

从版本1.3开始，brat包含许多功能用于比较相同文档的多组标注，包括用于识别和标记差异的自动比较以及并排可视化。

![feature example](http://brat.nlplab.org/img/comparison-example-1.png)

并排的标注比较

这种比较可用于评估自动系统或人类标注者之间是否协调一致，差异的可视化可帮助快速识别常见的错误来源。

## 每个标注的地址

每个 brat 标注都可以在 brat 服务器中唯一地寻址。与服务器的URL一起，这种寻址形式为每个 brat 标注提供全局唯一的地址。

![feature example](http://brat.nlplab.org/img/URL-example.png)

使用给定的 URL 聚焦标注结果

在浏览器中输入这样的地址不仅会显示相关文档，而且还会进一步突出显示特定标注并使其居中。因此，这些地址可用于电子邮件和在线文档和讨论，以简单明确地引用 brat 中的任何标注。

![feature example](http://brat.nlplab.org/img/link-URL-emphasized.png)

通过双击标注，可以从显示的对话框轻松访问每个标注的地址。

## 与自动标注工具集成

brat 实现了一个简单的界面，用于将可作为Web服务访问的自动文本标注工具的输出集成到标注工作中。

![feature example](http://brat.nlplab.org/img/automatic-annotation-dialog.png)

只需单击一下，即可将自动标注工具作为Web服务调用

brat 还与最先进的基本标注方法的透明集成，例如句子分割（英语和日语）和分词（日语）。

## 任意规模的高质量可视化

brat 的可视化基于可缩放矢量图形（SVG），能够以任意细节和精度呈现。

![feature example](http://brat.nlplab.org/img/zoomin-example.png)

放大标注

因此，brat 标注的可视化满足打印质量，可以用作出版物中的图片来说明标注。

SVG允许浏览器的内置缩放功能用于特写或文档标注的高级视图。

![feature example](http://brat.nlplab.org/img/zoomout-example.png)

缩小标注以看到概况

## 轻松导出多种格式

在brat中创建的标注可以通过界面中的几次单击以简单的 standoff 格式导出，可以轻松分析、处理和转换为其他格式。

可视化可以类似地以其原生 SVG 格式导出、呈现为位图（PNG格式）、或转换为其他矢量格式以嵌入到文档（PDF或EPS）中。

## 始终保存，始终保持最新状态

brat 通过透明地将标注器的所有编辑操作传递给 brat 服务器，消除了工具崩溃、忘记保存工作、甚至运行标注器的计算机宕机带来的标注工作的风险。

类似地，维护工作在项目中的所有标注器共享的单个权威版数据，brat 服务器消除了出现的标注版本冲突或使用过时数据的可能性，以及标注者需要使用单独的版本控制系统来协调他们的工作。

## 实时协作

brat 采用 client-server 体系结构和设计允许多个标注器同时在同一文档集合上工作，甚至在同一文档上工作，看到彼此的编辑几乎就像他们自己编辑的一样（也存在通信中固有的一些延迟）。

所有编辑操作都由服务器协调，以确保即使多个用户尝试同时修改单个标注，标注仍保持一致。

## 详细的标注过程时间记录

brat可以选择性地配置为记录标注器打开文档的精确时间，记录每个编辑操作的时间，甚至是记录在选择了要进行标注的位置后，选择要分配给标注的类型所花费的时间。

## 丰富的标注原语集

brat 提供了一组丰富的基本标注类别：文本跨度标记（例如实体标注）、二元关系、等价类、 n元关联（例如事件标注）和属性可以任意组合应用于一起定义特定的标注任务。

一些可以应用 brat 的标注任务在[examples]（http://brat.nlplab.org/examples.html）页面进行介绍。

## 完全可配置

标注系统的所有方面都使用简单的声明性配置语言进行配置。每个文档集合都拥有自己的配置，允许单个 brat 服务器托管许多具有不同标注目标的项目。

此外，可以使用广为人知的HTML / CSS样式规范来控制可视化的大多数方面，例如字体，标注“框”和“弧”的颜色以及箭头和弧形绘制样式。

有关如何配置brat的详细信息，请参阅[配置页]（http://brat.nlplab.org/configuration.html）

## 始终进行检查

brat 结合了标注验证，能够检查在其表达配置中定义的所有约束。

对在 brat 中创建的标注进行的验证不会被隔离到单独的过程中，而是紧密集成到标注过程中：在每个编辑选项之后检查标注的有效性，通过简单的视觉提示为标注者提供即时反馈。

![feature example](http://brat.nlplab.org/img/incomplete-ann-example.png)

不完整的标注示例及其详细信息

缺少强制性内容的标注没有给出彩色填充并给出灰色突出显示。将鼠标放在这样的标注上可提供标注验证器检测到的问题的详细信息。

![feature example](http://brat.nlplab.org/img/error-ann-example.png)

带有错误和详细信息的示例标注

具有额外或错误部分的标注被赋予红色“光环”，其指示标注的问题。同样，将鼠标放在这样的注释上会详细说明检测到的问题。

## 搜索

brat 实现了一整套函数，用于搜索文档或文档集合，以获得具有一组详细可配置约束的任意类型的标注。

![feature example](http://brat.nlplab.org/img/search-dialog-only-advanced-1.png)

显示高级设置的文本搜索

## 语料库检索

brat 支持基本的 key-word-in-context（KWIC）风格的语料库检索。

![feature example](http://brat.nlplab.org/img/concordancing-example.png)

语料库搜索结果