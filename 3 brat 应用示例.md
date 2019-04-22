# 3 brat 应用示例

原网址：<http://brat.nlplab.org/examples.html>

brat 可以通过多种方式应用，并用于完成和正在进行的标注工作和其他任务：

- brat 中的标注示例
- 使用 brat 标注语料库
- brat 的其他应用

# brat 标注示例

下面使用可用语料库中的示例介绍了可以在 brat 中执行的各种标注任务。本节中讨论的示例最初是在 brat 以外的各种工具中创建的，并转换为 brat 格式。许多原始格式的转换器与 brat 一起发布。在这里所包括的示例的选择中，优先考虑具有自由可用数据的任务。

## 实体提及检测

![annotation example](http://brat.nlplab.org/img/examples/esp.train-doc-536-small.png)

### 示例：CoNLL 2002 共享任务：独立于语言的命名实体识别

2002年计算自然语言学习会议（CoNLL）就独立于语言的命名实体识别共享了一项任务，提供了两个已标注的语料库（西班牙语和荷兰语），注有四种类型的实体（person, organization, location and miscellaneous）。

将CoNLL 2002 共享任务格式转换为brat standoff格式的转换脚本，以及标注语料库的示例将与brat一起发布。

完整的共享任务数据可从共享任务网站免费获取。

**Examples in brat:** [see it live on brat](http://weaver.nlplab.org/~brat/demo/latest/#/not-editable/CoNLL-ST_2002_train/) (read-only data)

**Project website:** [CoNLL 2002 shared task website](http://www.cnts.ua.ac.be/conll2002/ner/)

**Publications:** [Tjong Kim Sang, 2002](http://www.cnts.ua.ac.be/conll2002/pdf/15558tjo.pdf) [PDF]

## 事件抽取

![annotation example](http://brat.nlplab.org/img/examples/PMID-20300060-small.png)

### 示例：BioNLP 共享任务：生物医学事件提取

2009年和2011年举行的 BioNLP 共享任务事件和正在进行的 BioNLP 共享任务2013（http://2013.bionlp-st.org/）包含了几个事件提取任务。

brat standoff 格式与 BioNLP 共享任务的数据发布格式兼容，并为该任务提供的各种语料库的标注样本与 brat 一起发布。

完整的共享任务数据可从共享任务网站免费获得。

**Examples in brat:** [see it live on brat](http://weaver.nlplab.org/~brat/demo/latest/#/not-editable/BioNLP-ST_2011_ID_devel/) (read-only data)

**Project website:** [BioNLP shared task 2011 website](http://2011.bionlp-st.org/)

**Publications:** [Kim et al. 2009](http://aclweb.org/anthology-new/W/W09/W09-1401.pdf), [2011](http://aclweb.org/anthology-new/W/W11/W11-1801.pdf) [PDFs]

## 指代消解 (Coreference resolution)

![annotation example](http://brat.nlplab.org/img/examples/PMID-1492121-small.png)

### 示例：CO 支持任务：科学出版物中的指代消解

2011年 BioNLP 共享任务包括科学出版物中指代消解的支持任务。

brat standoff 格式与 coreference 任务中使用的表示兼容，并且为该任务提供的语料库的标注样本与brat一起分发。

完整的共享任务数据可从共享任务网站免费获得。

**Examples in brat:** [see it live on brat](http://weaver.nlplab.org/~brat/demo/latest/#/not-editable/BioNLP-ST_2011_coreference_development_data/) (read-only data)

**Project website:** [BioNLP ST 2011 CO task home page](http://2011.bionlp-st.org/home/protein-gene-coreference-task)

**Publications:** [Nguyen et al. 2011](http://aclweb.org/anthology-new/W/W11/W11-1811.pdf) [PDF]

## 归一化 (Normalization)

![visualization example](http://brat.nlplab.org/img/examples/CRAFT-16507151-small.png)

### 示例：科罗拉多富标注的全文语料库 (CRAFT)

科罗拉多富标注的全文语料库（CRAFT）是全文生物医学期刊出版物的标注语料库。包含的概念来自七个生物医学本体/术语，包括 ChEBI、Go 和 NCBI Taxonomy 被标注并归一化为适当的本体标识符。

语料库创建者已将标注转换为brat格式，并提供在线服务以浏览brat中的CRAFT概念标注。

完整的语料库可以从项目主页免费获得。

**Examples in brat:** [see it live on brat](http://compbio.ucdenver.edu/Craft/index.xhtml) (read-only data)

**Project website:** [CRAFT home page](http://bionlp-corpora.sourceforge.net/CRAFT/index.shtml)

**Publications:** [Bada et al. 2012](http://www.biomedcentral.com/1471-2105/13/161/), [Verspoor et al. 2012](http://www.biomedcentral.com/1471-2105/13/207)

![visualization example](http://brat.nlplab.org/img/examples/EVEX-PMID-9144171-small.png)

### 示例：EVEX：具有多级基因归一化的大规模事件抽取资源

EVEX 数据库建立在一个自动标注的语料库上，涵盖了来自 PubMed Central 的2200万篇 PubMed 摘要和46万篇开放访问全文文章，使用诸如 Turku 事件提取系统等工具创建和基因归一化系统 GenNorm。 数据中提到的每个基因和蛋白质被归一化到不同粒度水平的几个数据库，范围从规范符号到广泛基因家族和独特的Entrez基因ID。

语料库创建者已将标注转换为 brat 格式。下面链接是一个（非常）小的样本。

完整语料库可从 bionlp.utu.fi/pubmedevents.html 免费获得。

**Examples in brat:** [see it live on brat](http://weaver.nlplab.org/~brat/demo/latest/#/not-editable/EVEX/) (read-only data)

**Project website:** [EVEX home page](http://evexdb.org/)

**Publications:** [Van Landeghem et al. 2011](http://www.aclweb.org/anthology-new/W/W11/W11-0204.pdf)

## 分块 (Chunking)

分块是将文本划分为非重叠段的任务，通常进一步分配标签，例如NP（名词短语）。

![annotation example](http://brat.nlplab.org/img/examples/train.txt-doc-109-small.png)

### 示例：CoNLL 2000 共享任务：分块 Chunking

2000年计算自然语言学习会议（CoNLL 2000）分享了关于分块的任务，提供免费的训练和测试数据。

从CoNLL 2000共享任务格式到brat对等格式的转换脚本和语料库标注的样本与brat一起分发。

完整的共享任务数据可从共享任务网站免费获得。

**Examples in brat:** [see it live on brat](http://weaver.nlplab.org/~brat/demo/latest/#/not-editable/CoNLL-00-Chunking) (read-only data)

**Project website:** [CoNLL 2000 shared task website](http://www.clips.ua.ac.be/conll2000/chunking/)

**Publications:** [Tjong Kim Sang and Buchholz (2000)](http://www.clips.ua.ac.be/conll2000/pdf/12732tjo.pdf) [PDF]

## 依存语法

依存分析（句法分析）是指定单词之间的二元关系以标记其头部依赖关系的任务。

![annotation example](http://brat.nlplab.org/img/examples/swedish_talbanken05_train.conll-doc-880-small.png)

### 示例：CoNLL-X共享任务：多语言依存分析

第十届计算自然语言学习会议（CoNLL-X）分享了多语言依存分析的任务，提供了13种语言的标注语料库，其中四种语言可免费提供（丹麦语，荷兰语，葡萄牙语和瑞典语）。

从CoNLL-X共享任务格式到 brat standoff 格式的转换脚本和这四种语言的语料库标注样本与brat一起发布。

完整的共享任务数据可从共享任务网站免费获得。

**Examples in brat:** [see it live on brat](http://weaver.nlplab.org/~brat/demo/latest/#/not-editable/CoNLL-X-Swedish) (read-only data)

**Project website:** [CoNLL-X shared task website](http://ilk.uvt.nl/conll/)

**Publications:** [Buchholz and Marsi (2006)](http://aclweb.org/anthology-new/W/W06/W06-2920.pdf) [PDF]

![annotation example](http://brat.nlplab.org/img/examples/TDT-w078-small.png)

示例：Turku 依存树库 (TDT)

TDT 是使用斯坦福依存（SD）方案手动标注的芬兰语树库。除了基本句法树之外，TDT还包括其他关系，例如协调扩展。底层语料库包括许多不同类型，包括法律术语、百科全书文本、小说和新闻。 可以根据要求提供从TDT的原生XML格式到brat standoff格式的转换脚本，并使用 brat 分发树库的样本。

**Examples in brat:** [see it live on brat](http://weaver.nlplab.org/~brat/demo/latest/#/not-editable/Turku_Dependency_Treebank) (read-only data)

**Project website:** [TDT website](http://bionlp.utu.fi/fintreebank.html)

**Publications:** [Haverinen et al. (2010)](http://hdl.handle.net/10062/15936)

## 元知识 (Meta-knowledge)

元知识标注是根据文本上下文确定如何解释事实陈述的任务。例子包括是否有描述事实，假设，实验结果或结果分析的陈述，作者对其分析的有效性有多自信等等。

![annotation example](http://brat.nlplab.org/img/examples/nactem-metaknowledge-1545132-small.png)

### 示例：丰富 GENIA 事件语料库的元知识

完整的 GENIA 事件语料库由36,858个事件标注的1,000个摘要组成，已经人工丰富了元知识标注。这将促进更复杂的IE系统的培训，这允许将解释性信息指定为搜索标准的一部分。这样的系统可以协助许多重要任务，例如，找到新的实验知识以促进数据库管理，使文本推断能够检测蕴涵和矛盾等。

每个事件都注释了5个不同维度的元知识，即知识类型（KT）、确定性等级（CL）、方式、倾向和来源。标注包括为每个维度分配适当的值，并在每个维度存在时识别每个维度的文本线索。

可以从项目网站免费获得包含GENIA语料库的元知识。

**Examples in brat:** [see it live on brat](http://www.nactem.ac.uk/brat/#/GENIA-Metaknowledge/) (read-only data)

**Project website:** [NaCTeM Meta-knowledge Project](http://www.nactem.ac.uk/meta-knowledge/)

**Publications:** [Thompson et al. (2011)](http://www.biomedcentral.com/1471-2105/12/393/abstract)

# 使用brat标注语料库

本节介绍一系列使用 brat 标注的语料库。

## 信息抽取

信息提取是捕获文本中包含的基本信息并将其转换为适合自动处理的正式表示的任务。

![annotation example](http://brat.nlplab.org/img/examples/PMID-7806663-small.png)

### 解剖实体语料库（AnEM）

brat 被用于创建AnEM，这是从 PubMed 摘要和 PMC 全文提取中提取的500个文档的语料库，标注了11类解剖实体。语料库旨在作为生命科学出版物中解剖实体提及检测的训练和评估方法的参考。

**Examples in brat:** [see it live on brat](http://weaver.nlplab.org/~brat/demo/latest/#/not-editable/AnEM-1.0.4/) (read-only data)

**Project website:** [Nactem anatomy page](http://www.nactem.ac.uk/anatomy/)

**Publications:** [Ohta et al., 2012](http://www.nactem.ac.uk/anatomy/docs/ohta2012opendomain.pdf) [PDF]

![annotation example](http://brat.nlplab.org/img/examples/cellfinder_corpus2-small.png)

### CellFinder 语料库

brat 被用于标注10篇论文的 CellFinder 语料库，标注了六个生物医学实体：基因/蛋白质、细胞成分、细胞类型、细胞系、解剖部位（组织/器官）和生物体。该语料库是在CellFinder项目的范围内开发的，该项目旨在建立一个中心干细胞数据库。

**Examples in stav:** [see it live](http://corpora.informatik.hu-berlin.de/index.xhtml#/cellfinder/version1_sections/) (read-only data)

**Project website:** [CellFinder project resource page](http://www.informatik.hu-berlin.de/forschung/gebiete/wbi/resources/cellfinder/)

**Publications:** [Neves et al., 2012](http://www.informatik.hu-berlin.de/forschung/gebiete/wbi/research/publications/2012/lrec2012_corpus.pdf) [PDF]

![annotation example](http://brat.nlplab.org/img/examples/MLEE-PMID-15975645-small.png)

### 多级事件抽取语料库 (MLEE)

brat 用于创建260个 PubMed 摘要的多级事件抽取（MLEE）语料库，其中注释了16种物理生物医学领域实体类型，范围从分子实体到细胞、组织和器官，涉及这些实体的29种事件类型，主要是参考 Gene Ontology 定义的。(http://www.geneontology.org/)

该语料库目前正在 BioNLP 共享任务2013癌症遗传学任务中应用和扩展。

**Examples in brat:** [see it live](http://www.nactem.ac.uk/eccb2012/index.xhtml#) (read-only data)

**Project website:** [Multi-Level Event Extraction (MLEE) project homepage](http://nactem.ac.uk/MLEE/)

**Publications:** [Pyysalo et al., 2012](http://bioinformatics.oxfordjournals.org/content/28/18/i575.full)

## 通过自下而上的识别进行隐喻标注

自下而上的隐喻标注是识别文本中的语言隐喻并推断构成它们的概念隐喻的任务。

![annotation example](http://brat.nlplab.org/img/examples/russian_metaphor-small.png)

### 俄语概念隐喻（conceptual metaphor）语料库

人工标注的俄语概念隐喻语料库是处于初始阶段的正在进行的项目。标注在两个级别执行。在浅层，隐喻相关词根据MIPVU的略微修改的规则进行标注，MIPVU是隐喻识别的语言过程。每个与隐喻相关的单词被分配给10个类中的一个。形成隐喻基础的词义是针对每个隐喻相关词而描述的。

深层标注包括标注 Source 和 Target 的概念域之间的隐喻映射，并从中推断出概念隐喻。

该方案适用于识别和标注部分表现在文本中的概念隐喻，只有 Source 明确存在，而 Target 和映射是隐含的。

**Publication:** [Badryzlova et al. (2014)](http://www.aclweb.org/anthology/W13-0910)

# brat 其他应用

brat 也可用于人工标注以外的任务。

## 可视化

brat 不仅用于创建标注，还可用于其他工具的标注结果的可视化输出，以进行手动分析和评估。有关如何在网页中嵌入brat可视化的说明，请点击此处 (http://brat.nlplab.org/embed.html)。

![visualization example](http://brat.nlplab.org/img/examples/Stanford-CoreNLP-small.png)

### 自然语言分析工具可视化

Stanford NLP 小组正在使用 brat 来提供由Stanford CoreNLP 自然语言分析工具的在线演示创建的标注结果的可视化。

CoreNLP 工具执行词性标注、命名实体识别、共指消解和句法分析。演示使用嵌入式 brat 提供所有这些标注图层的单独可视化。

**Examples in brat:** [see it live](http://nlp.stanford.edu:8080/corenlp/) (online demo)

**Project website:** [Stanford CoreNLP home page](http://nlp.stanford.edu/software/corenlp.shtml)

**Publications:** [Toutanova et al. 2003](http://nlp.stanford.edu/~manning/papers/tagging.pdf), [Finkel et al. 2005](http://nlp.stanford.edu/~manning/papers/gibbscrf3.pdf),[Klein and Manning 2003](http://nlp.stanford.edu/~manning/papers/unlexicalized-parsing.pdf), [Raghunathan et al. 2010](http://nlp.stanford.edu/pubs/coreference-emnlp10.pdf) [PDFs].

### 信息抽取系统评估

![evaluation example](http://brat.nlplab.org/img/examples/PMID-10860807-eval-small.png)

示例：BioNLP 共享任务：生物医学事件提取

BioNLP 共享任务2011和~~正在进行的~~ BioNLP 共享任务2013使用 brat 将 gold 标准标注与信息抽取系统预测结果的比较结果可视化。

评估系统评估两组标注之间的差异，并以 brat 格式生成视觉比较，使用 brat 特征使视觉上的差异明显。