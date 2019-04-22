# 8 brat  系统配置

原网页：<http://brat.nlplab.org/configuration.html>

翻译：eillsu

GitHub：<https://github.com/eillsu/Brat-Chinese-Translation>

当前，brat 标注系统的配置是由基于文本的配置文件进行控制，这些配置文件可以在任意的文本编辑器中创建和编辑。这里介绍如何进行配置。

( 更喜欢通过具体例子来学习？在brat的 configurations 目录中查看各种项目的配置。)

**注意**：我们计划在未来的版本中引入基于GUI的配置，但是到目前为止，我们已经将开发工作重点放在平台的其他方面，因为更改配置的需求很少出现，而且brat 配置语言非常简单，即使不是专家也可以编写。

## 目录

- [基础配置](http://brat .nlplab.org/configuration.html#configuration-basics)
- [标注配置 (annotation.conf)](http://brat .nlplab.org/configuration.html#annotation-configuration)
- [可视化配置 (visual.conf)](http://brat .nlplab.org/configuration.html#visual-configuration)
- [工具配置 (tools.conf)](http://brat .nlplab.org/configuration.html#tool-configuration)
- [快捷键配置 (kb_shortcuts.conf)](http://brat .nlplab.org/configuration.html#keyboard-configuration)
- [其他详细信息](http://brat .nlplab.org/configuration.html#additional-details)

## 基础配置

### 配置文件

标注项目的配置由四个文件控制：

- annotation.conf: 标注类型配置
- visual.conf: 标注显示配置
- tools.conf: 标注工具配置
- kb_shortcuts.conf: 键盘快捷方式配置

每个标注项目通常定义自己的 annotation.conf。不需要定义 visual.conf、tools.conf 和 kb_shortcuts.conf，如果这些文件不存在，系统将返回简单的默认视觉、工具和快捷方式。

配置文件可以放在 brat 数据目录中的任何位置，并且通常放在与其应用的集合的基目录对应的目录中。（要确定集合的配置，系统会从目录树中向上搜索收集数据所在的目录，使其朝向brat  data 目录的根目录，如果这些位置中没有任何配置，则返回默认配置。）

### 配置文件的结构

配置文件遵循简单的面向行的结构和许多其他基于文本的配置系统熟悉的语法。

配置文件的顶级组织为节，每个节都用一行标记，只包含 “[节名称]” ，其中节名称是为配置文件定义的一组预定义节名称之一。

在这些节中，每一个非空行定义一个配置项，其中第一个非空格序列命名该项，其余的行命名规范，各部分有所不同。

配置读取器将忽略空白行。同样，以数字符号“#”（也称为散列字符）开头的行将作为标注忽略。

定义两个实体和两个关系类型的简单标注配置文件的示例如下所示。

```
[entities]
Person
Organization

[relations]
Family      Arg1:Person, Arg2:Person
Employment  Arg1:Person, Arg2:Organization

# This is a comment line.
```

## 标注配置 (annotation.conf) 

标注配置文件 annotation.conf 被分为以下小节：

- [entities] 实体
- [relations] 关系
- [events] 事件
- [attributes] 属性

每个节都必须存在于配置文件中，但可以为空。例如，通过将其他三个节留空，配置只定义实体标注目标。

### 实体定义 ([entities] section) 

[entities]节定义了可在文本中标记为类型文本跨度的事物的类型，例如提及真实世界中的“事物”，例如人或位置。

[entities]节的基本格式是一个简单的列表，每行有一个实体类型。以下是简单[entities]节的示例：

```
[entities] 
Person
Location
Organization
```

除了列出实体类型，还可以使用[entities]节定义标注的一个附加方面：组织实体的层次结构。这是可选的，并且指定实体组织层次结构的语法仅由每行开头的制表符 TAB 组成。

```
[entities]
Living-thing
	  Person
    Animal
    Plant
Nonliving-thing
    Building
    Vehicle
```

![](http://brat.nlplab.org/img/entity-type-hierarchy.png) 

这种层次结构被系统解释为is-a分类。

定义实体类型层次结构的最直接可见差异在于标注是类型选择器显示层次结构并允许其部分折叠（隐藏）或打开以帮助找到可用的实体类型。（此功能主要用于大量已定义的类型。）

更多的信息可见高级实体配置。

### 关系定义 ([relations] section) 

[relations] 节定义了标注之间的二元关系。例如，关系可以标记由两个Person标识的实体之间的Family关系。

[relations] 节中的每一行定义一个关系类型，它可以关联的实体，以及可选的关系属性。关系的类型可以使用ARG:TYPE语法（其中ARG按照惯例分为Arg1和Arg2）来标识，用逗号分隔。

以下示例是一个简单的 [relations] 节。

```
[relations]
Family          Arg1:Person, Arg2:Person
Employment      Arg1:Person, Arg2:Organization
```

关系通常可以采用多种类型的参数。可以在配置中通过列出由管道符“|”分隔的所有可能类型。并非所有参数组合都有效的情况可以通过为每行定义一组有效组合来约束。以下示例说明了这些功能：

```
[relations]
Located    Arg1:Person,Arg2:Building|City|Country
Located    Arg1:Building,Arg2:City|Country
Located    Arg1:City,Arg2:Country
```

对于实体，可以通过在每行的开头放置TAB字符来定义关系类型的层次结构。

关系定义的更多信息可见高级关系配置。

### 事件定义 ([events] section) 

[events] 节定义了其他标注（实体或事件）之间的n元关联。标注的“事件”类别可用于标记文本中发生的事情，例如两个人结婚或公司破产。

定义事件的基本语法与关系类似。每行定义一个事件类型（或者更具体地说，一个事件“frame” - 可能的参数组合），使用ROLE:TYPE语法指定的事件参数，并以逗号分隔。可以自由定义参与者在事件（ROLE）中扮演的角色。

以下示例是一个简单的[events]。

```
[events]
Marriage    Participant1:Person, Participant2:Person
Bankruptcy  Org:Company
```

### 属性定义 ([attributes] section) 

[attributes] 定义了可用于标记其他标注的二元或多值“flags”。例如，可以使用 Negated 属性将标记事件的出现标记为在文本中明确拒绝，或使用 Confidence 属性将事件标记为 Certain，Probable 或 Doubtful 之一。

[attributes] 中的每一行都定义了一个属性类型以及它可以附加到的标注。对于二元属性，可能的值，true和false，是隐含的; 对于多值属性，还必须指定可能的值。

属性可以应用的标注类型（或多种类型）使用ARG:TYPE语法定义，该语法也用于关系和事件的定义（ARG按照惯例，“Arg”）。 可以使用语法Value:VAL1 | VAL2 | VAL3 [...]定义多值属性可以采用的值，其中“Value”是文字字符串，VAL1，VAL2等是可能的值。

以下示例是一个简单的 [attributes]。

```
[attributes]
Negated       Arg:<EVENT>
Confidence    Arg:<EVENT>, Value:L1|L2|L3
```

有关配置属性的可视显示的更多信息，请参阅高级属性配置。

## 可视化配置 (visual.conf) 

可视化配置文件 visual.conf 包含以下小节：

- [labels] 标签
- [drawing] 视觉

这些小节中的每一部分都必须存在于配置文件中，但它们可以为空。

### 标签定义 ([labels] section) 

[labels] 定义用于在用户界面上显示已定义标注类型的标签。如果没有为类型定义标签，则系统默认值会显示annotation.conf 中定义的已配置类型。

标签的定义有两个主要用途：允许用户界面中使用的标签使用任意字符（请参阅类型名称部分），以及网页布局中空间有限时使用的缩写。

[labels]的格式很简单：每行包含一组字符串，用竖线字符（“|”）分隔。

第一个字符串应该对应于annotation.conf 中定义的类型; 第二种被认为是用于该类型的首选完整形式，其余（如果有的话）应该与其逐渐缩短的缩写相对应。

下面的例子展示里一个简单的 [labels] 的例子：

```
[labels]
Organization | Organization | Org
Immaterial-thing | Immaterial thing | Immaterial | Immat
```

请注意，如果 annotation.conf 中定义的类型与显示它的首选方式匹配，则第一个和第二个字符串将是相同的。此外，标签中允许使用空格，并忽略标签周围的空间。

### 视觉定义 ([drawing] section) 

[drawing] 定义了视觉呈现的各种非文本方面。如果没有为类型定义可视配置，则系统使用默认设置，这些设置本身可以配置。

[drawing] 的格式类似于其他配置中使用的格式。每行包含可视配置所应用的标注类型，以及一组指定可视设置的KEY:VALUE 键值对。

下面的例子展示一个简单的 [drawing] 。

```
[drawing]
Person     bgColor:#ffccaa
Family     fgColor:darkgreen, arrowHead:triangle-5
```

此示例指定应使用颜色 #ffccaa 的背景绘制 Person 类型的标注，并且应使用以5像素三角形箭头结尾的深绿色线绘制表示 Family relations 的弧。

可以被识别的可视化配置键、值以及相应的目的如下：

- fgColor: 任何HTML颜色规范（例如“黑色”），在可视化中设置跨度文本的颜色。

- bgColor: 任何HTML颜色规范（例如“白色”），在可视化中设置跨度“框”背景的颜色。

- borderColor: 任何HTML颜色规范（例如“黑色”），在可视化中设置跨度“框”边框的颜色。 还支持特殊值“darken”，指定使用较暗的bgColor色调作为边框。

- color: 任何HTML颜色规范（例如“黑色”），在可视化中设置弧的颜色。

- dashArray: 任何有效的SVG stroke-dasharray规范，使用破折号（而不是逗号或空格）作为分隔符（例如“3-3”），设置跨度/圆弧可视化中线条的虚线/点图案（“ - ”适用于实线）

  (注解：SVG Stroke 属性 <http://www.runoob.com/svg/svg-stroke.html> strokedasharray属性用于创建虚线)

特殊标签“SPAN_DEFAULT”和“ARC_DEFAULT”被识别为设置默认值，将用于没有特定设置的类型。没有必要定义可视化的所有方面（例如，只能给出颜色）：默认值将用于未指定的情况。 以下示例说明了这些默认值的用法。

```
[drawing]
SPAN_DEFAULT    fgColor:black, bgColor:lightgreen, borderColor:darken
ARC_DEFAULT     color:black, dashArray:-, arrowHead:triangle-5
Person          bgColor:#ffccaa
Family          fgColor:darkgreen
```

在此配置中，将使用指定的默认值绘制除 Person 和 Family 之外的所有标注类型。进一步的 Person 和 Family 标注也将“继承”未明确定义的视觉呈现方面的默认值，例如， 对于 borderColor of Person 标注，系统将使用特殊值变暗。

## 工具配置 (tools.conf) 

标注工具配置文件 tools.conf 分为以下几个小节：

- [options] 选项
- [search] 搜索
- [normalization] 归一化
- [annotators] 标注器
- [disambiguators] 消歧

这些小节都是可选的：空文件是有效的 tools.conf。

### 选项配置 ([options] section) 

**注意**：从v1.3版本（Crunchy Frog）开始支持 [options]。有关这些选项如何与早期版本中的设置相对应，请参阅有关升级到v1.3的页面。(http://brat.nlplab.org/upgrading-to-v1.3.html) 

[options] 可用于设置brat 服务器如何执行句子分段（拆分），分词，标注验证和日志记录，如下所示：

- ```
  - Tokens tokenizer:VALUE, where VALUE =
    - whitespace: split by whitespace characters in source text (only)
      由源文本中的空白字符拆分（仅限）
    - ptblike: emulate Penn Treebank tokenization
      模仿宾州树库分词
    - mecab: perform Japanese tokenization using MeCab
      使用 MeCab 进行日语分词
  - Sentences splitter:VALUE, where VALUE =
    - regex: regular expression-based sentence splitting
      基于正则表达式的句子分割
    - newline: split by newline characters in source text (only)
      由源文本中的换行符分割（仅限）
  - Validation validate:VALUE, where VALUE =
    - all: perform full validation
      进行全面评估验证
    - none: don't perform any validation
      不执行任何评估验证
  - Annotation-log logfile:VALUE, where VALUE =
    - <NONE>: no annotation logging
      不进行标记记录
    - NAME: log into file NAME (e.g. "/home/brat /work/annotation.log")
      指定记录的log文件
  ```

例如，下面的 [options] 给出了v1.3之前的默认 brat  配置：

```
[options]
Tokens            tokenizer:whitespace
Sentences         splitter:regex
Validation        validate:none
Annotation-log    logfile:<NONE>
```

以下 [options] 使用 MeCab 启用日语分词，仅通过换行符进行句子拆分，完全验证和标注记录到给定文件中。

```
[options] 
Tokens            tokenizer:mecab
Sentences         splitter:newline
Validation        validate:all
Annotation-log    logfile:/home/brat /work/annotation.log
```

### 归一化数据库配置 ([normalization] section) 

[normalization] 定义了可用的归一化资源。有关设置归一化 DB 的信息，请参阅brat 归一化文档。

[normalization] 中的每一行都具有以下语法：

```
    DBNAME     DB:DBPATH, <URL>:HOMEURL, <URLBASE>:ENTRYURL
```

这里，`DB`，`<URL>`，`<URLBASE>`和`<PATH>`是文字字符串（它们是不变的），而“DBNAME”，“DBPATH”，“HOMEURL”和“ENTRYURL” “应该替换为适合正在配置的数据库的特定值：

- `DBNAME`: 设定数据库的名称，例如 Wiki、 GO。虽然名称是可以随意选择的，但是应该只使用以下字符组成：字母数字（“a” - “z”，“A” - “Z”，“0” - “9”），连字符（“ - ”）和下划线（“_”）。此名称将在brat  UI和标注文件中使用，以标识数据库 DB。
- `DBPATH` (optional): DBPATH 是可选的。提供相对于 brat  服务器根目录的服务器上归一化 DB 数据的文件系统路径。如果未设置`DBPATH`，则系统假定可以在给定的`DBNAME`下的默认位置找到 DB。
- `HOMEURL`: 设置归一化资源的主页的URL（例如“http://en.wikipedia.org/wiki/”）。用于比“DBNAME”更具体地标识资源，并在标注 UI 中提供用于访问资源的链接。
- `URLBASE` (optional): URLBASE是可选的。设置可以填写的URL模板（例如“http://en.wikipedia.org/?curid=%s”），以在标注 UI 中生成与归一化资源中的条目的直接链接。该值应包含字符“％s”作为占位符，将替换为条目的ID。

以下示例显示已配置的归一化 DB 的示例。

```
[normalization]	 
Wiki	DB:dbs/wiki, <URL>:http://en.wikipedia.org, <URLBASE>:http://en.wikipedia.org/?curid=%s
UniProt	<URL>:http://www.uniprot.org/, <URLBASE>:http://www.uniprot.org/uniprot/%s
```

第一行设置名为“Wiki”的数据库的配置，在brat 服务器目录中找到“dbs / wiki”，第二行用于名为“UniProt”的数据库的配置，该数据库位于具有此名称的 DB 的默认位置。

### 搜索配置 ([search] section) 

[search] 定义了标注对话框中可用的在线搜索服务。

[search] 中的每一行都包含搜索服务的用户界面中使用的名称，以及单个键值对。key 应具有特殊值“<URL>”，value 应为搜索服务的URL，并将要查询的字符串替换为“％s”。

以下示例显示了一个简单的 [search]。

```
[search] 
Google       <URL>:http://www.google.com/search?q=%s
Wikipedia    <URL>:http://en.wikipedia.org/wiki/%s
```

当选择字符的范围或编辑一个标注时，这些搜索选项将显示在 brat  标注对话框中。

![](http://brat.nlplab.org/img/search-config-1.png)

### 标注工具配置 ([annotators] section) 

[annotators] 定义了可以从brat 调用的自动标注服务。

[annotators] 中的每一行都包含服务的唯一名称和键值对，用于定义用户界面中显示的方式以及工具的Web服务的URL。应为“tool”，“model”和“<URL>”指定值（前两个仅用于用户界面）。

下面的例子是一个简单的 [annotators]。

```
[annotators] 
SNER-CoNLL    tool:Stanford_NER, model:CoNLL, <URL>:http://example.com:80/tagger/
```

### 消歧工具配置 ([disambiguators] section) 

[disambiguators] 定义了可以从 brat 调用的自动语义类（标注类型）消歧服务。

[disambiguators] 中的每一行都包含服务的唯一名称和键值对，用于定义在用户界面中显示的方式以及工具的Web服务的URL。应为“tool”，“model”和“<URL>”赋予值（前两个仅用于用户界面）。

下面的例子是一个简单的 [disambiguators]。

```
[disambiguators]
simsem-MUC    tool:simsem, model:MUC, <URL>:http://example.com:80/simsem/%s
```

要查询的字符串由URL中的“％s”标识。

## 快捷键配置 (kb_shortcuts.conf) 

键盘快捷键配置文件 kb_shortcuts.conf 不包含任何 section 结构，并且语法非常简单：每行包含一个字符和一个标注类型，指定给定字符的键应该用作选择给定字符的快捷方式类型。例如：

```
P    Person
O    Organization
F    Family
```

然后可以在适当的标注对话框中使用这些快捷方式来快速选择关联的类型。

**提示**：配置良好的键盘快捷键可以加快简单的标注任务，尤其是与*Normal* 和 *Rapid* 标注模式一起使用时，可以从brat  UI中的 *Options* 菜单中选择。

## 其他详细信息

### 高级实体配置

**已禁用的条目**：可以通过在 [entities] 中的类型名称前添加感叹号（“ ! ”）来禁用实体选择对话框中的条目。该类型将显示在结构的类型层次结构中，但不能自行选择。例如：

```
[entities]
!Living-thing 
                 Person 
                 Animal 
                 Plant
!Nonliving-thing 
                 Building 
                 Vehicle
```

上面的 [entities] 将 Living-thing 和 Nonliving-thing 定义为is-a层次结构的一部分，但不使这些类型可用于标注。

### 高级关系配置

关系定义支持通过特殊属性<REL-TYPE>设置关系属性，如下所示。

```
[relations] 
Equiv     Arg1:Person, Arg2:Person, <REL-TYPE>:symmetric-transitive
```

<REL-TYPE>规范目前支持两个属性，对称和传递，可以单独或一起应用。可以使用短划线字符（“ - ”）组合多个属性，如上例所示。

symmetric-transitive（对称 - 传递）的组合定义了*等价关系*。

[relations] 还用于定义允许哪些实体在其跨度范围中重叠的规则（在标注验证中进行检查）。 定义此功能的语法如下（自v1.3起支持）：

```
[relations] 
<OVERLAP>    Arg1:TYPE1, Arg2:TYPE2, <OVL-TYPE>:TYPE-SPEC
```

即，标准关系配置语法包含<OVERLAP>和附加的特殊属性<OVL-TYPE>。TYPE-SPEC可以包含任何值， contain、equal 或者 cross，解释如下：

- contain: 包含：TYPE1实体跨度可以（完全）包含在TYPE2实体的跨度内
- equal: 等于：TYPE1和TYPE2实体的跨度可能相等
- cross: 交叉：TYPE1和TYPE2实体的跨度可以交叉

contain、equal 以及 cross可以由“|”组合表达的字符，例如 equal | cross 表示“可以相等或交叉”，值<ANY>可用于表示允许任何重叠。

在标注验证的假定中，<OVERLAP>设置中未明确允许的任何实体重叠为错误。

下面显示了一些示例<OVERLAP>关系定义：

```
<OVERLAP>	Arg1:Country, Arg2:Organization, <OVL-TYPE>:contain
<OVERLAP>	Arg1:Person, Arg2:Person, <OVL-TYPE>:equal
<OVERLAP>	Arg1:<ENTITY>, Arg2:<ENTITY>, <OVL-TYPE>:<ANY>
```

它们分别被解释为“Country 标注可以包含在 Organization 标注中”（例如[Bank of [England]]），“Person 标注可以具有相同的范围”（例如[[Johnsons]]）和“ 任何实体标注都可以以任何方式与任何其他实体重叠“（参见下面的<ENTITY>快捷方式定义）。

### 高级属性配置

多值属性的定义可以使用以下示例（annotation.conf）进行说明：

```
[attributes]	 
Confidence	Arg:<EVENT>, Value:L1|L2|L3
```

然后，可以在以下示例之一中指定 visual.conf 中多值属性的可视配置：

```
[drawing]	 
Confidence	glyph:(1)|(2)|(3), position:left
```

或者

```
[drawing]	 
Confidence	dashArray:-|3-3|3-6
```

### 快捷方式和宏

为方便annotation.conf定义，定义了以下“快捷方式”：

- <ENTITY>: 任何实体类型（出现在[entities]中的任何类型）
- <RELATION>: 任何关系类型（出现在[relations]中的任何类型）
- <EVENT>: 任何事件类型（出现在[events]中的任何类型）
- <ANY>: 任何类型

这些快捷方式可用于定义，如以下部分 annotation.conf 示例所示：

```
[events] 
Transport      Theme:<ENTITY>, Cause:<ANY> 

[attributes]
Speculation    Arg:<EVENT>
Name           Arg:<ENTITY>
```

例如，Transport 事件的 Theme 是任何实体类型，Cause 是任何类型。

配置文件还支持定义任意“宏”的语法，如下所示：

```
<LIVING-THING>=Person|Animal|Plant
```

然后，定义的宏可以出现在配置中的任何位置，并将使用简单的文本替换进行解释; 任何在配置文件中定义为宏的字符串（例如“<LIVING-THING>”）的出现都将被处理，就像它的值（例如“Person | Animal | Plant”）被写入其位置一样。

这些快捷方式可以使许多类型的配置更简洁，更易于读写。

### 类型名称

每个标注类型由一个或多个字符组成，约束为一组字母数字字符（“a” - “z”，“A” - “Z”，“0” - “9”）、连字符（“ - ”） 和下划线（“_”）字符。

但是，这些限制仅适用于annotation.conf，它定义了系统内部和磁盘存储中使用的类型。在 visual.conf 中定义的用户界面上出现的相应标签没有这样的限制，并且可以包含例如空格或任意 Unicode 字符。

此外，可以在 visual.conf 中使用特殊值<EMPTY>来指定不应显示标签或类似标记（如属性字形glyph）。 

以下（部分）配置示例说明用户界面上的标签中的任意字符。

annotation.conf:

```
[entities]
Immaterial-thing
Organization
# (rest of config omitted)
```

visual.conf:

```
[labels]
Immaterial-thing | Immaterial thing
Organization | 組織
# (rest of config omitted)
```

![](http://brat.nlplab.org/img/nonascii-label-example.png)