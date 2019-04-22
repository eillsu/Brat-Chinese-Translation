# 9 brat standoff 格式

在 brat 中创建的标注以 standoff 格式存储在磁盘上：标注与带标注的文档文本分开存储，文档永远不会被工具修改。

对于系统中的每个文本文档，都有一个相应的标注文件。这两者通过文件命名约定关联，它们的基本名称（不带后缀的文件名）是相同的：例如，文件DOC-1000.ann包含文件DOC-1000.txt的标注。

在文档中，单个标注通过字符偏移连接到特定的文本跨度。例如，在文章开头“Japan was today struck by ...”中，文本“Japan”由偏移范围0..5标识。（所有偏移都从0开始索引并包含起始偏移处的字符，但在结束偏移处排除字符。）

brat 使用的特定 standoff 格式类似于BioNLP共享任务的 standoff 格式，并在下面详细描述。(http://2011.bionlp-st.org/home/file-formats)

## 文本文件 (.txt)

文本文件应具有后缀.txt，并包含输入系统的原始文档的文本。

```
Sony formed a joint venture with Ericsson, a mobile phone company based in Sweden.
Sony announced today that ...
```

文档文本存储在使用UTF-8编码的纯文本文件中（ASCII的扩展 - 纯ASCII文本也可用）。文档文本可能包含换行符，这些换行符将由 brat 显示为换行符。但是，文档不必包含任何换行符：brat可以使用可靠的算法执行其句子分段以进行显示。（无论原始文本文档中是否包含换行符，文本文件本身不会被修改。）

## 标注文件 (.ann)

标注存储在带有.ann后缀的文件中。 以下讨论可能包含在这些文件中的各种标注类型。

### 一般标注结构

所有标注都遵循相同的基本结构：每行包含一个标注，每个标注都有一个首先出现在该行上的ID，通过单个TAB字符与标注的其余部分分开。结构的其余部分因标注类型而异。

以下示出了实体（T1），事件触发器（T2），事件（E1）和关系（R1）的标注的示例。

```
T1	Organization 0 4	Sony
T2	MERGE-ORG 14 27	joint venture
T3	Organization 33 41	Ericsson
E1	MERGE-ORG:T2 Org1:T1 Org2:T3
T4	Country 75 81	Sweden
R1	Origin Arg1:T3 Arg2:T4
```

下面给出这些标注的详细描述。

### Text-bound 标注

Text-bound 标注是与实体和事件标注相关的重要标注类别。Text-bound 标注识别特定的文本范围并为其指定类型。

```
T1	Organization 0 4	Sony
T2	MERGE-ORG 14 27	joint venture
```

从v1.3开始，brat还支持不连续的 text-bound 标注，其中标注涉及多个连续的字符跨度。这些标注的间隔表示是单跨案例的直接扩展。例如，“North and South America”的一个可能的标注将表示如下：

```
T1	Location 0 5;16 23	North America
T2	Location 10 23	South America
```

形成不连续标注的（start-offset, end-offset）对由分号分隔，并且这些跨度的文本由单个空格字符连接以形成标注的参考文本。

### 标注 ID 的惯例

所有标注 ID 都由一个标识标注类型和数字的大写字符组成。初始 ID 字符与标注类型相关，如下所示：

- T: text-bound 标注
- R: relation 关系
- E: event 事件
- A: attribute 属性
- M: modification (alias for attribute, for backward compatibility) 修饰（属性的别名，用于向后兼容）
- N: normalization 归一化  **[new in v1.3]**
- \#: note 注意

此外，在特殊情况下，星号（“*”）可用作ID的占位符。

### 实体标注

每个实体标注具有唯一ID，并且由类型（例如，Person 或者 Organization）和包含实体的字符范围（表示为“start end”偏移对）来定义。

```
T1	Organization 0 4	Sony
T2	Organization 33 41	Ericsson
T3	Country 75 81	Sweden
```

每行包含一个text-bound 标注，用于标识文本中提到的实体。

### 事件标注

每个事件注释都有一个唯一的ID，并由类型（例如MERGE-ORG）、事件触发器（event trigger）（声明事件的文本）和参数定义。

```
T2	MERGE-ORG 14 27	joint venture
E1	MERGE-ORG:T2 Org1:T1 Org2:T3
```

事件触发器和事件标注都是 text-bound 标注，它标注了说明这个事件的词，并且它们的格式与实体的格式相同。（触发器的ID占用与实体ID相同的空间，并且这些ID不得重叠。）

对于所有标注，事件ID首先出现，由TAB字符分隔。事件触发器指定为 TYPE:ID，并通过 ID 标识事件类型及其触发器。按照惯例，事件类型在触发器标注和事件标注中都指定。事件触发器由SPACE（空格）与事件参数分开。事件参数是一组SPACE分隔的ROLE:ID对，其中ROLE是特定于事件和任务的参数角色之一（例如，Theme, Cause, Site），ID标识填充该角色的实体或事件。请注意，多个事件可以共享相同的触发器，并且应该首先指定事件触发器，但事件参数可以按任何顺序出现。

### 关系标注

二元关系具有唯一的ID，并由其类型（例如Origin，Part-of）及其参数定义。

```
R1	Origin Arg1:T3 Arg2:T4
```

格式类似于应用于事件的格式，但标注不标识表达关系的特定文本（“触发器 trigger”）：ID由TAB字符分隔，关系类型和参数由SPACE分隔。

关系参数通常简单地标识为 Arg1 和 Arg2，但系统可以配置为在 standoff 表示中使用任何标签（例如 Anaphor 和Antecedent）。

#### 等价关系

系统还支持等价关系的特殊语法。等价关系是对称、传递的关系，其定义标注集在某种意义上是等同的（例如，指代相同的现实世界实体）。

```
T1	Organization 0 43	International Business Machines Corporation
T2	Organization 45 48	IBM
T3	Organization 52 60	Big Blue
*	Equiv T1 T2 T3
```

为了与现有的支持格式向后兼容，brat还支持等价关系注释的特殊“空”ID值“*”。

### 属性和修饰（modification）标注

属性标注是二元或多值“flags”，用于指定其他标注的更多方面。属性具有唯一ID，属性的定义包含这个属性所标记的标注的ID和属性值。

```
A1	Negation E1
A2	Confidence E2 L1
```

对于其他标注，ID由TAB分隔、其他字段由空格分隔。

上例中的二元属性（如A1）只需指定属性名称和标记的标注 ID：值为true表示二元属性。 缺少二元属性标注被解释为具有值false的属性。

多值属性还指定由SPACE分隔的属性值。多值属性的值是完全可配置的。

为了与现有的支持格式向后兼容，brat 还识别属性的 ID 前缀“M”。

### 归一化标注

从**v1.3**开始支持归一化注释。每个归一化标注都有一个唯一的ID，归一化标注包含附加标注的ID以及标识外部资源（`RID`）和该资源中的条目（`EID`）的`RID:EID`对。另外，每个归一化标注都有“Reference”类型（当前没有定义该类型的其他值）以及所引用的条目的人类可读字符串值。

以下示例显示附加到 text-bound 标注 “T1”（未示出）的归一化标注，并将其与维基百科条目“534366”（“Barack Obama”）关联。

```
N1	Reference T1 Wikipedia:534366	Barack Obama
```

（请注意，“EID”值（例如“Wikipedia”或“GO”）与相关外部资源的关联不会在 standoff 中表示，而是由`tools.conf`配置文件控制。）

对于 text-bound 标注，ID 和文本由 TAB 字符分隔，其他字段由 SPACE 分隔（此处为 “Reference”、 “T1” 和 “Wikipedia:534366”）。

### 注意标注

注意标注提供了一种方法将自由格式文本与文档或特定标注相关联。标注行以符号＃开头。

```
#1	AnnotatorNotes T1	this annotation is suspect
```

Notes 以＃加 "ID"开头，后跟TAB字符。对于这些 notes，第二个TAB分隔字段包含标注类型和 note 附加到的标注的ID，第三个TAB分隔字段包含标注的文本。

可以自由设置 note 的类型，并且可以将任意数量的 note 附加到单个标注。 （但是，目前只能从 brat UI 编辑一个 AnnotatorNotes 类型的 note。）