---
title: 电子表格中的数据整理
author: 任怡萌
date: '2018-07-28'
slug: data-organization-in-spreadsheets
meta_extra: '原作者：Karl W. Broman，Kara Woo；译者：任怡萌'
categories:
  - 统计软件
tags:
  - Excel
  - 统计计算
  - 数据整理
forum_id: 420095
---

> 本文翻译自Karl W. Broman和Kara H. Woo发表的[Data organization in spreadsheets](https://peerj.com/preprints/3183/)。作者Karl W. Broman，工作于威斯康星大学麦迪逊分校，担任生物统计和医学信息学部教授；作者Kara H. Woo，担任华盛顿大学信息学院信息管理员。本文已获得原作者授权。

## 引言

电子表格有着普通的矩形外表，但是它的使用存在数十年的争议。一些作者认为，真正的程序员绝不会使用电子表格，并且劝告大家不要再接触这个“灾难性”的事物 （[casimir1992](http://doi.acm.org/10.1145/130981.130982); [chadwick2003](http://link.springer.com/chapter/10.1007/978-0-387-35693-8_13)）；相反，也有一些作者推荐研究人员使用电子表格来提高工作效率（[wagner2006](http://pubsonline.informs.org/doi/abs/10.1287/educ.1063.0028)）。尽管大家对于电子表格的使用各执一词，但不能否认的是，它仍然在研究人员的工作过程中起着至关重要的作用，并且这个实用的工具是不会被完全摒弃的。

使用电子表格处理数据具有风险，这一点是毋庸置疑的。但是欧洲电子表格风险兴趣小组（European Spreadsheet Risks Interest Group）开了一个名为“恐怖故事”的专栏 (<http://www.eusprig.org/horror-stories.htm>) ，专门介绍电子表格在实际应用中的错误，可见它的出错可能性有多大。此外，很多研究者专门测试了电子表格的错误率，Panko（[Panko2008](http://panko.shidler.hawaii.edu/SSR/Mypapers/whatknow.htm)）的报告显示，对实际电子表格的13次审查中，平均88%的表格都有错误。就连经常使用的的电子表格软件也会出现一些难以检测到的问题，例如微软的Excel曾经把基因名称转变成日期数据，还会在不同的操作系统中以不同的形式保存日期数据——这些错误都会给后续的数据分析工作带来极大的问题（[zeeberg2004](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-5-80); [woo2014](https://datapub.cdlib.org/2014/04/09/abandon-all-hope-ye-who-enter-dates-in-excel/)）。使用电子表格的研究人员应该对这些常见的错误提高警惕，在设计表格的时候尽量保证整洁、前后连贯，并且减小出错的可能。

尽管大多数电子表格软件都可以同时用来做数据的输入、存储、分析和可视化，我们还是建议只将其用来输入和储存数据，数据分析和可视化应该考虑其他的选择。单独做数据的分析或可视化，或者用备份的数据文件来做，将会大大降低破环原始数据的风险。

Murrell（[murrell2013](https://www.mendeley.com/research-papers/data-intended-human-consumption-not-machine-consumption/)）对比了两种数据，一种是用眼睛人工格式化的，一种是计算机进行格式化的，并且提供了计算机提取复杂的文件中数据的示例代码。对于数据分析师而言，能处理非常复杂的数据文件是非常重要的，但是如果在分析开展之前，就用电脑的思维来对数据进行初步预处理，之后的工作就会简单很多。

在这篇论文中，我们将提出一些实用的建议，可以同时让人和计算机程序来系统地处理数据，通过这种方法，研究人员制作的电子表格中的错误会大大减少，这样的电子表格不仅更易于计算机处理数据，而且更易于他人理解。本文所使用的电子表格可以用文中提及的任何一种方法或处理数据的工具来处理，并且可以保证接下来的工作流程更加稳健，不易出错。

如果读者想优化一下已有的数据资料整理方式，我们建议使用本文接下来将介绍的几个原则来修正之后用于分析的数据集，而不要再运用其他冗杂并且容易出现错误的修正方式。

## 保持前后一致

整理数据的第一条原则是*保持前后一致*。无论是处理什么样的数据，一定要在一开始输入和整理的过程中保持一致，这样才可以保证之后使用这个数据的人不用浪费时间在调整数据的一致性上。

*使用一致的编码来标记分类变量。*比如要给基因研究中的小鼠性别编码时，最好给雄性和雌性分别只使用一个常用编码（比如雄性用“`male`”，雌性用“`female`”），切忌有时用“`M`”表示雄性，有时用“`male`”，甚至还穿插使用“`Male`”。如果选择了一种编码方式，就在整份数据文件中使用同一种。

*使用固定的编码来表示缺失值。*为了可以准确区分真正的缺失数据和不小心丢失的数据，最好将每一个单元格都进行编码。R的使用者一般用“`NA`”来表示真正的缺失值；当然，你也可以使用连字符来表示，前提是整份数据文件使用同一种表示真正缺失值的符号。尽量避免使用数值——比如`-999`或`999`——这样会给使用数据的人造成误解，认为是人为的丢失数据。需要注意的是，不要在数据之间插入额外信息来解释缺失值产生的原因，最好单独开辟一栏来写入诸如此类的备注。

*使用一致的变量名。*如果在整个项目中的某份文件中，你使用了“`Glucose_10wk`”作为变量名，那在这个项目其他的所有文件中都不要改变这个变量名。如果这个变量既被叫做“`Glucose_10wk`”，还会被叫做“`gluc_10weeks`”或是“`10 week glucose`”，可以想象，这将会给接下来的数据分析工作者带来额外的工作，需要搞清楚它们表示的是不是同一个变量。

*使用一致的标识符。*如果一条数据的标识符有时是“`153`”，有时是“`mouse153`”，有时还出现“`mouse-153F`”或“`Mouse153`”，接下来将会有大量的时间被花在辨别这些标识符上。

*在不同的文件中使用一致的数据布局。*如果你的数据在多份文件中使用了不同的布局格式，数据分析师就不得不花很长时间将这些数据整合成完整的数据集进行分析。一致的数据格式布局可以让整合数据这个过程十分简单。

*使用一致的文件名。*在给文件命名的时候尽量使用一套统一的方法。不要将名为“`Serum_batch1_2015-01-30.csv`”文件在第二次处理后命名为“`batch2_serum_52915.csv`”，而应命名为“`Serum_batch2_2015-05-29.csv`”。连贯的命名方式可以保证文件是安排有序的，而且当你需要处理这些文件的时候，你会发现系统化、统一化的命名方式简直太机智了。

*日期类型的数据使用一致的形式，*并且最好使用标准化的格式`YYYY-MM-DD`，比如`2015-08-01`。如果你一会儿用`8/1/2015`来表示，一会儿又用`8-1-15`，数据分析和数据可视化就会受到极大影响。

*在备注中使用一致的短语。*如果你的数据中有单独的一栏备注（例如“`dead`”或者“`lo off curve`”），一定要用同一种表达形式来记录同一个短语。切忌“`dead`”和“`Dead`”混用，或“`lo off curve`”和“`off curve lo`”混用。

*注意单元格中的空格。*一个空的单元格和含有一个空格的单元格是完全不同的，比如“`male`”和“<code>  male  </code>”是不一样的（没错，后者在单词的前后各加了一个空格）。

## 命名言简意赅

挑一个好的名字是很重要的，但是通常来说都比较难——这正是要在起名这个环节投入大量时间和精力的原因。

首要原则，无论是数据变量名（数据的列名）还是文件名，都不要使用空格。有空格的命名会使得写程序很麻烦——所有的名称都要放在双引号内，比如必须要写成`“glucose 6 weeks”`而不是简单的`glucose_6_weeks`。在需要空格的地方尽量选择下划线或连字符，而且别忘了上面说的，保持前后一致。

当心额外的空格（比如出现在变量名的前后）。举个熟悉的例子，“`glucose`”和“<code>glucose  </code>”是不同的，因为在第二个变量名后面多了一个空格。

尽量避免特殊符号（当然，下划线和连字符除外）。其他很多符号（比如`$`, `@`, `%`, `#`, `&`, `*`, `(`, `)`,
`!`, `/`等等）都在编程语言中有特殊含义，如果还出现在名称中就会很麻烦。此外，打出这些符号也挺麻烦的。

文件和变量命名的核心原则是*言简意赅*，但是也不能只追求*过于*简短。

Data Carpentry上的关于如何使用电子表格的课程（点击查看：<http://www.datacarpentry.org/spreadsheet-ecology-lesson/02-common-mistakes>）把好的和不好的变量名整理成了一张表格。

   **好的名称**     |     **备选名称**      |   **不好的名称**
------------------- | -------------------- | ---------
`Max_temp_C`        | `MaxTemp`            | `Maximum Temp ($^{\circ}$C)`
`Precipitation_mm`  | `Precipitation`      | `precmm`
`Mean_year_growth`  | `MeanYearGrowth`     | `Mean growth/year`
`sex`               | `sex`                | `M/F`
`weight`            | `weight`             | `w.`
`cell_type`         | `CellType`           | `Cell type`
`Observation_01`    | `first_observation`  | `1st Obs.`

我们认为这个表格列举的都很具有代表性，当然，有时候也可以换掉一些大写字母。也就是说，使用`max_temp`, `precipitation`和`mean_year_growth`等。

不要在文件名中使用“`final`”，不要在文件名中使用“`final`”，不要在文件名中使用“`final`”。如果一定要用的话，你肯定会有“`final_ver2`”。（这个观点来自于一个被广泛引用的PhD漫画：<http://phdcomics.com/comics/archive.php?comicid=1531>）

## 将日期写成YYYY-MM-DD的形式

在输入日期数据时，我们强烈建议使用“ISO 8601”标准，即将日期写成`YYYY-MM-DD`的形式，例如`2013-02-27`（点击查看和这个相关的xkcd漫画：<https://xkcd.com/1179>）

注意，Microsoft Excel处理日期数据的时候非常奇怪，它会把日期储存为数值型——在Windows系统上是从1900年1月1日起算的天数，而Mac上是从1904年1月1日起算的天数。因此，当数据是从Excel导出的时候，一定要亲自检查一下日期数据，确保其没有被损坏。

除此之外，Excel还会把其他类型的数据转换为日期。例如Roger Peng报道的一段来自于Kasper Hansen和Jeff Leek的对话（[这里](https://twitter.com/rdpeng/status/622067081748463616)和[那里](https://twitter.com/rdpeng/status/622067435022123008)）：

> Kasper: “你有没有最喜欢的转录因子？”
>
> Jeff: “有，是Oct-4。”
>
> Kasper: “为什么？”
>
> Jeff: “因为Excel会把它转换成日期数据，但实际上这个转录因子有非常厉害的作用。”

关于这个问题，Ziemann等（[ziemann2016](http://dx.doi.org/10.1186/s13059-016-1044-7)）研究了来自2005-2015年的18个期刊中补充文件的基因列表，发现大约20%的基因列表在基因名称上出现了错误，这些错误基本上都是刚才提到的被误转换成日期数据或者转换成浮点型数字的情况。

最好把要输入日期的那一列表格设置成文本格式，这样就不会出错了：

- 选中目标列
- 单击右键->“设置单元格格式”
- 在左边选中“文本”

但是，如果你*已经*将日期输入进去，再设置单元格格式的话，Excel会按照它们表示的数值型数据来转换成文本型数据（从1900年1月1日或1904年1月1日开始算的天数）。

还有一种方法可以让Excel在处理日期数据时直接将其识别成文本型数据，就是给日期前面加一个撇号，比如`'2014-06-14`（点击查看：<https://twitter.com/tjmahr/status/825047581113905153>）。Excel会将这种输入识别为文本型数据，并且你在看整张表的时候撇号是不会出现的。虽然这是一个方便的小技巧，但是这样处理数据必须得极为勤奋，确保前后保持一致。此外，你还可以把日期数据放在三列中，分别表示年、月、日，每一列数据只是普通的数字，Excel就不会出现混淆数据类型了。还有一种办法，可以把日期表示成8位数，比如用`20140614`表示`2014-06-14`（[briney2017](http://dataabinitio.com/?p=798)）。

要强调的是，在写日期的时候一定要保持前后一致，最好能一直以`YYYY-MM-DD`的格式写（或者把年、月、日分别写在三列也可以）。

图1是我们同事提供的部分电子表格，尽管这些数据是用来干什么的已经记不太清了，但很明显的是在一列中用不同的日期格式使得后续的分析和可视化工作变得更加困难。

对于日期的处理一定要小心，并且确保前后一致。

#### 图1

![01_bad_dates-1](https://user-images.githubusercontent.com/35906792/42447558-e58c9ef2-83ac-11e8-8d7b-ae556ad83c64.png)

## 不要留下空白单元格

尽量将单元格填满，如果有缺失值的话也选择一些常用的编码来表示。在这一方面，有一些人和我们持相反的观点（比如White等（[white2013](http://ojs.library.queensu.ca/index.php/IEE/article/view/4608)）更喜欢将单元格留空），但是我们还是建议用“`NA`”或者仅仅一个连字符来表示缺失值，这样可以确保这些数据是本身就缺失的，而非在输入中不小心遗漏了。

图2是两张有空单元格的电子表格，在图2A中，空白单元格是由于上一个数值要被重复若干次——千万不要这么做！数据分析师必须得一个接一个推断这些空白单元格的意义，并且如果数据按照行被重新整理后，这些空白单元格的真实日期就无法恢复了。

#### 图2

![02_blank_cells-1](https://user-images.githubusercontent.com/35906792/42447559-e63350b2-83ac-11e8-8158-532111dd40d9.png)

图2B中的电子表格用了复杂的数据布局，这张表格的信息是不同的治疗方案。在第一行中，B-E列可能都表示的是“1 min”的治疗方案，F-I列可能都表示“5 min”的治疗方案；在第二行中，B、C、F、G列都是“normal”，而D、E、H、I列都是“mutant”。尽管我们用眼睛看可以比较容易地识别，但是这些空白的单元格可能会给数据分析带来很大的不便。

为了使信息更加清楚，你可以把这些单元格都填满。或者也可以把数据以更“整齐”的形式呈现 （[wickham2014](https://www.jstatsoft.org/index.php/jss/article/view/v059i10)）——把每一条数据放在一行，所有的响应值放在单独的一列，如图3所示。关于这一点我们在下面还会讨论。

#### 图3

![03_fig2b_fixed-1](https://user-images.githubusercontent.com/35906792/42447561-e688ddfc-83ac-11e8-8789-8885c74be3d2.png)

## 一个单元格中只输入一个数据

电子表格中的每个单元格只能包含一个数据。

比如，你可能有一列数据“`plate-well`”表示“盘子的位置”，比如“`13-A01`”。最好能把这个数据拆分成“`plate`”列和“`well`”列（“`well`”列包含“`13`”和“`A01`”），或者你甚至可以分成三列：“`plate`”、“`well_row`”和“`well_column`”（对应的数据为“`13`”、“`A`”和“`1`”）。

当你想在单元格中包含数据的单位时，例如“`45 g`”，最好在单元格内只写`45`，把单位放在列名中，比如`body_weight_g`。把列名设置为`body_weight`并且把单位放在一个单独的数据字典中（在后面会讲到）是一个更好的选择。

常见的错误还有把数据的注释和数据本身放在同一个单元格中，例如“`0 (below threshold)`”。尽量不要这样处理，而在数据单元格中只写“`0`”，分出一个单独的列来记录注释。

最后，不要合并单元格。虽然这么做会使得电子表格看起来很漂亮，但是这违背了*不要留下空白单元格*的原则。

## 以矩形展示数据

电子表格最好的布局是行为对象、列为变量的一个大矩形，第一行应该包括所有的变量名。（*变量名不要超过一行*）图4展示了一张矩形布局的工作表。

#### 图4

![04_example_rectangle-1](https://user-images.githubusercontent.com/35906792/42447562-e6e2772c-83ac-11e8-839c-50e8c0e67886.png)

有些数据集不能放在一个矩形中，而是由多个矩形的数据构成，你可以把这种数据放在多个Excel文件中，每个文件由一个矩形数据构成。每个矩形最好就放在一个单独的文件中，因为处理分散的工作表比较麻烦，并且在输出为CSV文件时也很困难（这个我们一会儿简要讨论）。你可能会想在一个Excel文件中存放多张工作表，但是我们建议每个文件中只存放一张，这样的话导出CSV文件就很方便。当然，如果你一定要在一份文件中使用多张工作表，那确保不同的工作表结构前后一致。

有些数据不能用一个或若干个矩形来表示，很可能是说明了电子表格不是用于呈现这种数据的最好方式，因为电子表格生来就应该是矩形的。

我们刚拿到的数据文件一般都*不是*以矩形呈现的，更经常看到的是有很多数据是散落的，比如图5给出的一些例子。

#### 图5

![05_non_rectangular-1](https://user-images.githubusercontent.com/35906792/42447563-e73b5216-83ac-11e8-815a-f3dc01ed9524.png)

在5A和5B的示例中，数据分析师必须要先弄明白这个数据中每个地方都是什么意思，再花时间把所有的数据重新整理一遍。如果从一开始这些数据就被整理成一个矩形的布局，数据分析师就会省下很多时间。

图5C中的数据集对于每一个主题都有一张结构复杂的工作表，如果这些工作表有相同的布局形式，就会很容易找出它们之间相互联系的信息，然后合并成一个大的矩形工作表。（你可以使用R、Python或Ruby。）更好的处理方式是不要用平均值、方差和合并的计算来弄乱原始数据，在输入数据的时候，把所有的测量值放在一张工作表中会更简单一些。

像图5D显示的那样，有时候很难把一些数据识别成矩形的格式，但是它确实是一种矩形——我们可以把前两列的空白单元格都填满，分别重复输入individual、date和weight的值。但是重复weight的值似乎不太合理，因为它并不是一个重复测量变量。

最好可以把这个数据做成两张分开的工作表，一张表储存weight数据，另一张表储存其它测量值（这些测量值来自于葡萄糖耐受性的*活体*实验：给一只老鼠服用葡萄糖，在不同的时间段测量其体内的血糖和胰岛素水平）。图6展示了这样的数据布局，注意insulin列的注释“`lo off curve`”和“`off curve lo`”也被修改了，还给对应的地方添加了添加了“`NA`”，增加了注释列（注释中的文本保持一致）。除此之外，储存对象标识符的第一列也添加了列名。

#### 图6

![06_fix_fig5d-1](https://user-images.githubusercontent.com/35906792/42447564-e824e764-83ac-11e8-90c9-dcf56f3bf946.png)

图6A和6B是“整齐”的数据布局示例 （[wickham2014](https://www.jstatsoft.org/index.php/jss/article/view/v059i10)）：每一行都是一个实验单位，一般来说是一个对象，但是在6B中有一点不同——每一行是对一个对象的一次实验测量。将数据重新整理成“整齐”的格式可以简化后续的分析，但是矩形的外表是最重要的。

另一种经常可见的情况是两行列名，如图7所示。这种处理方式通常伴随着合并单元格：把“`week 4`”单元格和后面的两个合并起来，文字居中于“`date`”,“`weight`”和“`glucose`”上方。

#### 图7

![07_two_header_rows-1](https://user-images.githubusercontent.com/35906792/42447569-e91414ec-83ac-11e8-8c6d-0dd683bcfa76.png)

我们建议把week的也放在其他变量名的位置，也就是只保留一行列名，包括`Mouse ID`, `SEX`, `date_4`, `weight_4`, `glucose_4`, `date_6`,`weight_6`等。

也可以把每一行作为一个特定日期的对象，如图8所示。

#### 图8

![08_fig7_fixed-1](https://user-images.githubusercontent.com/35906792/42447570-e96c2628-83ac-11e8-8fbc-187cdfefc419.png)

请心疼你的数据分析师（当然，也可能是心疼你自己）：把数据整理成一个或若干个矩形。

## 建立一个数据字典

用一个独立的文件来解释所有的变量都表示什么含义是十分有帮助的，如果这个文件的布局也是矩形就更加完美了，这样的话数据分析师就可以在分析的时候利用上它。

一个“数据字典”可能会包含：
- 数据文件中的变量名
- 另一版可能会在数据可视化中用到的数据变量名
- 对变量名含义的解释
- 测量值单位
- 也可以包括最大值和最小值

你可能会需要这样一份“元数据”——呈现*关于*数据的信息，或者一份包含项目和数据概览的`ReadMe`文件。

图9展示了一个数据字典示例。注意，和其他的数据文件一样，它也是一个矩形的数据集：第一列是变量名；第二列使变量名可读性更强，一般会用在数据可视化中；第三列把这些变量分类，可视化有时候也会用到；第四列是简单的描述。

#### 图9

![09_data_dict-1](https://user-images.githubusercontent.com/35906792/42447571-e9c6259c-83ac-11e8-87ba-2a8330b59ef1.png)

这个数据字典文件也可以包含其他信息，比如变量的取值范围，这个可以帮助在数据输入时及时检查出错误。

## 不要在原始数据文件中计算

一般别人发给我们的Excel文件会包含各种各样的计算和图表，但是我还是强烈建议最初始的数据文件一定*只包含数据*，既不要有计算，也不要有图表。

如果你在数据文件中做了一些计算，这就意味着你会经常打开数据文件并且往里面添加新的东西。这样做很容易导致无意中把一些错误输入数据文件中。

（你有没有这样的经历？打开Excel文件后，选中一个单元格开始打字，但是这个单元格之前的东西去哪里了？有时候它们会被任意地输入在其他单元格中，当然这个也只能在后续的数据分析中才能发现。）

你的原始数据文件应该是一个干净的、原始的数据，给它写保护，做备份，然后封存在宝塔里不要再修改它了。

如果你想在Excel里做一些分析的话，拷贝一份数据文件，在复制的这一份里尽情地计算和画图。

## 不要在数据中设置字体颜色或者高亮

你可能把那些有异常数据的单元格或者某一行需要忽略的数据加高亮，或者改变有一些特殊含义的数据字体和字体颜色，但是我们建议你添加一个新列来表示指示变量（比如“`trusted`”列，取值为`TRUE`或`FALSE`）。

在图10A中，那个异常的数据加了高亮，但是如果给表格添加一列来说明数据是否是异常值则会更好一些（如图10B所示）。高亮只是看起来比较漂亮，但是很难在数据分析时从中提取出暗示的信息，毕竟数据分析软件更擅长处理储存在列中的数据，而不是被高亮的单元格或不同字体的数据所表示的信息（实际上这些标记在数据分析软件中很可能会直接丢失）。

#### 图10

![10_highlight_outlier-1](https://user-images.githubusercontent.com/35906792/42447574-eb005a7c-83ac-11e8-82eb-fd6cdf7d9457.png)

在老鼠葡萄糖耐受性的实验中，有的人还会用高亮来区别老鼠的性别——与其这样，不如专门设置一列性别，取值为`Male`或`Female`。

## 给数据做备份

经常备份数据，并且在不同的地方都储存一下。

几年前在威斯康星麦迪逊大学有一则段子——一篇文章引用了一个处于崩溃边缘的毕业生的一句话：“我的毕业论文唯一的备份就在那里！”——别让这件事也发生在你身上。

你可以用一个比较正式的控制系统，比如git，尽管它也不是最完美的数据文件储存方式。如果你想更炫酷一些，可以参考dat（<https://datproject.org/>）。

保存数据文件的所有版本，这样可以在某个地方出现了错误之后（比如你不小心打错了某个数据，并且很久之后才发现），仍然可以恢复出错数据本来的样子。在插入新的数据之前拷贝一份文件，并且根据数据版本进行重命名：`file_v1.xlsx`, `file_v2.xlsx`, ...

如果不是你主动地输入数据，尤其是被别人修改了数据，最好的方法是给数据文件*启用保护*，这样就不会不小心改了文件的内容。

- 在Mac上，打开Finder并选择要保护的工作簿，在文件菜单上单击“获取信息”，点击底部的“共享”，在权限设置中选择“只读”。
- 在Windows系统中，右击文件，选择“属性”，在“常规”标签下找到“属性”，选中“只读”后点击“确定”就可以了。

*备份你的数据文件！*

## 使用数据验证来减少错误

在输入数据的时候，尽可能保证整个过程不要出现错误和任何的重复性文件损伤，一个好用的工具是Excel中的“数据验证”（点击查看：<http://bit.ly/excel_dataval>），它可以控制输入的数据类型和取值范围。

- 选择一列
- 在菜单栏中选择“数据” -> “数据验证”
- 选择适当的数据验证标准，比如：
    - 某个范围内的整数
    - 某个范围内的小数
    - 一个可能的取值列表
    - 有长度限制的文本数据

同时，你可以给一列数据选择一个数据类型，比如使用文本类型数据来避免日期或转录因子的名称被Excel损坏，这个在之前的日期数据注意事项中也讨论过，但是它确实十分重要，所以这里再重复一次操作步骤：

- 选择一列数据
- 单击右键→“设置单元格格式”
- 在左侧选择“文本”

虽然似乎有点麻烦，但是为了避免数据输入出错，这个步骤是值得花时间的。

## 把数据保存成文本文件

以文本形式保存一份拷贝的数据文件，使用逗号或制表符，一般使用逗号分隔符（CSV）文件。图11A中的电子表格使用逗号分隔符保存后会呈现图11B的形式。

#### 图11

![11_example_rectangle-1](https://user-images.githubusercontent.com/35906792/42447578-eb82ac2a-83ac-11e8-9d72-9dc0d431b5ac.png)

虽然CSV格式看起来颜值不高，但这个文件不仅可以在Excel中打开，还可以在其他软件中以标准的形式打开。更重要的是，这种适用性很强的文件格式不需要任何特殊的软件来处理，编程时用起来也很方便。

如果单元格中有逗号，Excel会在文件保存成CSV格式时给单元格的内容加上双引号，这一点需要一些额外的处理，但是没有太大的影响。

将一个Excel文件保存成逗号分隔符文件的步骤：

- 在菜单栏中选择“文件” -> “保存为”
- 在“保存类型”点击下拉菜单栏，选择“CSV（逗号分隔符）”
- 点击“保存”
- Excel会提示“...您工作簿中的部分功能可能会丢失。是否继续使用此格式？”，选择“是”
- 关闭Excel，它会提示“是否保存所做的更改？”，点击“不保存”，因为你已经保存过了。（Excel非常不想让你用除了它默认格式之外的任何格式）

注意，在选择保存类型的时候，还有一个“文本文件（制表符分隔）”，许多人会倾向于选择这种类型，尤其是在逗号用于充当十进制分隔符的地区。

如果你的数据文件包含一些关键的特征，会因为保存成文本文件而不被一起保存下来，比如高亮的单元格，那你在保存成这个类型的时候要谨慎一些——因为这些特征*将会*丢失。也正是因为如此，我们建议最原始的数据文件尽量保证简洁一些。

## 总结

很多处理电子表格的软件（如Microsoft Excel, Google Sheets和LibreOffice Calc等）在数据的输入、整理和储存上都十分实用，并且还可以进行计算、分析和数据可视化。在这篇文章中，我们的重点是数据的整理，建议想要对数据进行计算加工或可视化的使用者尽量保持数据的原始状态，并且尽量只保留初始数据，而在另一份拷贝文件中进行计算和数据可视化。

我们列举出的一些原则，可以帮助数据的使用者更好地在电子表格中整理数据，这些都是为了保护数据的真实性，并且方便后续的数据分析工作。

本文的主要观点，也就是各个部分的小标题：保持前后一致，将日期写成 `YYYY-MM-DD` 的形式，不要留下空白单元格，每个单元格只输入一个数据，将数据整理成一个矩形的布局（每一行为一个对象，每一列为一个变量），建立数据字典，不要在原始数据文件中包含计算，不要更改字体颜色或高亮数据，选择合适的名称，给文件做备份，使用数据验证来减少输入错误，以及把数据文件保存为文本文件的格式。

首先保证遵循以上的原则，然后再进行项目的后续工作。可能你的数据文件目前没有完全达到所有的标准，但是也不要用“复制粘贴”的方法来对文件重新整理——这样很容易导致意想不到的问题。数据的重新整理最好用编程的方法（可以使用R, Python或Ruby脚本），这样你的所有操作记录都不会丢失。

## 致谢

Lance Waller, Lincoln Mullen和Jenny Bryan对本文的原稿都提出了大量的建议。
