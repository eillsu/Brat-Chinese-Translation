# 2 brat 简单介绍

原网页：<http://brat.nlplab.org/introduction.html>

brat 是一个基于Web的文本标注工具；也就是说，用于向现有文本文档添加标注。

brat 是专门为*结构化*标注而设计的，其中标注不是自由格式的文本，而是具有固定的形式，可以由计算机自动处理和解释。

下面的屏幕截图显示了一个简单的示例，其中对一个句子进行了标注，以确定提到的一些现实世界实体（事物）及其类型，以及两者之间的关系。

![example annotation](http://brat.nlplab.org/img/annotation-example.png)

标注示例(遵循ACE 2005实体和关系标注指南http://www.itl.nist.gov/iad/mig/tests/ace/2005/)

此示例说明了标注的两个基本类别：

- **文本范围标注（text span）**，例如示例中标记有 Organization 和 Person 类型的标注
- **关系标注（relation）**，例如示例中标记有 Family 关系的标注

简单类型文本跨度类别适用于为命名实体识别创建标注，以及为简单关系信息提取任务创建二元关系等。

(http://en.wikipedia.org/wiki/Named-entity_recognition)

(http://en.wikipedia.org/wiki/Information_extraction)

brat 还支持N元关联的标注，可以将参与特定角色的任意数量的其他标注链接在一起。此类标注可用于*事件标注*，如以下示例中的 TRANSFER：

![example annotation](http://brat.nlplab.org/img/event-example.png)

标注示例(遵循 ACE 2005 实体、关系以及事件标注指南http://www.itl.nist.gov/iad/mig/tests/ace/2005/)

其他标注的详细类型和属性可以通过使用可以在标注上设置的**属性（attributes）**来进一步指定，例如，将事件标记为事实或推测性的，或将提及的实体标记为指一个团体或个人。

为了能够对特定文本表达式所引用的真实实体进行唯一标识，brat 还支持将其他标注与维基百科等资源中的条目相关联，以便对标注进行**归一化（normalization）**（brat v1.3（Crunchy Frog）和更新的版本）：

![example annotation](http://brat.nlplab.org/img/normalization-example.png)

用于显示维基百科信息的归一化标注的信息弹出式菜单(image © Andrés Monroy, licensed CC-BY-SA)

最后，虽然不是该工具主要关注的，但brat也允许将任意格式的文本“**notes**”添加到标注中。

标注的应用类别、它们的类型以及关于它们的使用的**约束**（例如，Family 关系必须始终连接 Person 类型的标注）都是完全可配置的，这允许 brat 可以应用于几乎任何文本标注任务。

brat 还利用自然语言处理技术（http://en.wikipedia.org/wiki/natural_language_processing）实现了许多功能，以支持人工标注工作。