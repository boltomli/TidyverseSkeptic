# TidyverseSkeptic

从另一种视角看 R 语言的 Tidyverse “方言”，以及 RStudio 对 Tidyverse 的提倡。

## Norm Matloff, Prof. of Computer Science, UC Davis (former Prof. of Statistics at UCD)

作者 Norm Matloff 为 UC Davis 计算机科学教授（曾任 UCD 统计学教授）。本中文翻译经过作者[同意](https://github.com/matloff/TidyverseSkeptic/issues/22)。文中的“我”为作者视角，但译文中存在的任何不妥之处当然很可能是由译者引入的，还望读者不吝[赐教](https://github.com/boltomli/TidyverseSkeptic/issues/new)。

## 注意：此为简版

在我看来，Tidyverse 的主要问题在于其不利于教学。我相信使用 Tidyverse 而非 base-R 实际上会**阻碍**对没有编写代码背景的初学者进行教学。这个简洁的版本仅保留了 TidyverseSkeptic 文中关于教学的部分。我在完整的文档中还谈及了其它问题，详见[英文原文全文](https://github.com/matloff/TidyverseSkeptic/blob/master/READMEFull.md)。

## 声明

本文在某种程度上比较坦率，并且涉及非常流行的 Tidyverse 及 RStudio。我想本文是有礼貌的，并且应被视为具有建设性的批评。

我对 RStudio 的人们抱有喜爱和尊敬的态度，包括 Tidyverse 的提出者 Hadley Wickham。我也一直支持他们，无论私下或是[公开](https://matloff.wordpress.com/2018/02/22/xie-yihui-r-superstar-and-mensch/)。从公司只有创始人 JJ Allaire 和首席开发 Joe Cheng 的时候开始，我们就一直互动。我向我的学生们高度赞扬 RStudio 公司，我使用并推荐 Hadley 的包 **ggplot2** 和 **stringr** （均不属于 Tidyverse），有时 **devtools** 确实节省了我大量时间。

换句话说，我并没有把 RStudio 当作什么邪恶社团。我在本文中的不少地方都表明我认为他们的行为具有良好的意图。然而，我持有如下看法：**决定推广 Tidyverse 是 RStudio 作出的错误抉择**，这使 R 语言的一致性和健康性遭到威胁。

[这里是我的简历。](http://heather.cs.ucdavis.edu/matloff.html) 关于 R 语言的部分，我从几乎最开始就是 R 的用户和开发者，在那之前我使用 R 的前身 S。我出版过几本使用 R 语言的书，还担任过 *R Journal* 的主编。Hadley 也曾任此期刊的主编。

## 可教学性概览

* 我最大的担忧来自 R 语言教学。**对于需要学习 R 语言的非程序员来说，Tidy 让精通这门语言变得更困难**。

* Tidyverse 来自这样一种渴求，即要有一组相互兼容、行为一致的函数或包。这种“纯正”哲学对计算机科学家有着难以抗拒的吸引力。Tidyverse 也借鉴了其它“纯正”计算机科学（CS）哲学，特别是 *函数式编程*（FP）。FP 抽象化且理论化，**即使对 CS 专业的学生来说也较困难**。因此，显然 **若学习 R 语言的人并非程序员，Tidy 是一种不甚明智的方案**。

* **纯正带来的其它代价包括更复杂和更抽象**，代码更容易出错（同时还牺牲了性能）。

* 实际上，**如果学习者之前没有编写代码的背景，Tidyverse 总体来说过于复杂**，这会引发心理学家所称的 <i>认知过载</i> 现象。

* 确实，很多 Tidy 的倡导者也承认在各种意义下 Tidy 代码比 base-R 更难编写。比如，Hadley 说“可能需要一些时间让你的头脑适应 [FP].”

* RStudio 提倡 Tidyverse 的时候声称它能够使非程序员更容易学习 R。出于上述原因，与之正相反，**我要提出异议：Tidyverse 让这个群体的人们学 R 变得 *更难***。

* RStudio 作了可敬的工作，让更多女性及未被充分代表的少数群体能接触到 R。然而，由于被限制在复杂的 Tidyverse 系统中，这些群体将很难为 R 语言作出更多贡献，诸如编写 CRAN 包、撰写书籍等等。这些工作需要相当熟悉 base-R 的使用，即使代码本身仍然可以主要由 Tidyverse 写就。当然，也不只是这些群体，这对任何人都适用。可惜的是 RStudio 正在伤害它本想要帮助的那些人。

## <a name="teachable"> </a> 可教学性

从大学以来，教学一直是我兴趣所在。我成为统计和计算机老师很多年，也得过一些教学奖项。我写的课本 *Statistical Regression and Classification: from Linear Models to Machine Learning* 获得 2017 年的 Ziegel Award。

远不止于此，我对人们如何学习有浓厚的兴趣，从孩童到中年。除了上述课程以外，我还教过移民成年人作为第二语言的英语，他们大多数没有完成高中教育。

关于教学的讨论，我这里把对象定为 **想用 R 进行数据分析的非程序员**，而不是想成为专业 R 语言程序员的人。

### 案例分析：R 语言第一课

Tidyverse 对初学者过于复杂。这里有一些便捷的例子显示 Tidy 的复杂性及其后果，非程序员学生学习 R 的时候难以适应。

来看一下我的在线 R 教程 [**fasteR**](http://github.com/matloff/fasteR)。比如，考虑下面这样无害的一行

``` r
> hist(Nile)
```

即用 R 内置的尼罗河数据集绘制一副简单的直方图。

这就是我教程的第一课。简单！作为对比，用 Tidy 的群体不许使用 base-R 绘图，而是坚持使用 **ggplot2**（再说一次，其实这并不属于 Tidy，只不过有 Tidy 的倡导者常如此描述）。要想用 Tidy，教员需要如下操作

``` r
> library(ggplot2)
> dn <- data.frame(Nile)
> ggplot(dn) + geom_histogram(aes(Nile))
```

如此，教员有太多东西需要解释——包、数据框、**ggplot()**、**aes** 参数、`+` 的作用（在这里并不表示加法）等等——因此教员也许本不该在第一堂课就展示这种用法。

同样出自我的第一课，还有

``` r
> mean(Nile[80:100])
```

打印给定年份区间内尼罗河流量的平均数。令人惊奇的是，这不仅不会出现在 Tidy 第一课，使用 Tidy 教程的学生甚至有可能 *永远不会* 学到如何做这件事。典型的 Tidy 教员并不认为向量对学习者有多么重要，更不要说向量下标了。

作为这个 Tidy 观点的实例，请见 *Getting Started with R*，作者 Beckerman *et al*，Oxford University Press，second edition，2017。这本书特别强调 [“遵循 Tidyverse”](https://twitter.com/GSwithR/status/996830294367002625)。书共231页，仅简略地提到向量，并且完全没有提及下标。

### 案例分析：Dalgaard 的书

2019年12月，一位研究者发推特说 Peter Dalgaard 的一本讲统计学概论的书“过时了”，因为用的是 base-R 而非 Tidy。想一想如果要更新到 Tidy 会涉及什么，又会强加给学生多少复杂性。这里是书中的一个例子：

``` r
> thue2 <- subset(thuesen, blood.glucose < 7)
```

基于 base-R 的话，这第二课可以轻松讲到，说不定第一课就可以。而 Tidy 则不然，需要更改成

``` r
> library(dplyr)
> thue2 <- thuesen %>% filter(blood.glucose < 7)
```

教员首先要讲授管道操作符 `%>%`，又一份额外的复杂性。在做这件事情的时候，教员很可能要强调管道是“从左到右”的流，然而学生会感到困惑，因为从左到右的流完成后，马上就又跟着一个从右到左的流 `<-`。（不管出于什么原因，Tidy 似乎并不使用 R 的 `->` 操作。）

又一次，Tidyverse 对于没有编程背景的学习 R 的人依然过于复杂，**拖慢了学习进度**。

### Tidyverse 倡导者们的提法

怀着为教学致力终生的热情，我强烈质疑 Tidyverse 倡导者们的提法，即使用 Tidy 对非程序员进行教学，而不使用 base-R。

（我认为 **dplyr** 和 **data.table** 都是高阶的课题；两者都不适合初学者。另一方面，指导初学者使用 **ggplot2** 则完全可行，当然要再次指出其并不是 Tidyverse 的一部分）

还没有关于倡导者们对 Tidy 可教学性的提法的研究。倡导者们通常会提供来自学生的赞誉，如

* “我用 Tidyverse 学习了 R，现在用 R 很有生产力”

* “我喜欢 Tidyverse 类似英文的自然用法”

* “我可以用 Tidyverse 做出漂亮的图”

* “Tidyverse 向我展现了数据的流动”

同时也是教员的倡导者们则会重复这些陈述并加以评论，诸如：

* “Base-R 适合专业程序员，但 Tidyverse 是只想进行数据分析的非技术人员学习 R 的最佳工具”

* “R 由统计学家创造，为统计学家使用。而我们是数据科学家，主要兴趣在于制作图表”

* “Tidyverse 是 **现代的** R，供我们其他人使用”

全部这些陈述要么具有误导性，要么和可教学性问题无关，或者是彻底的空话。关于 base-R 与 Tidy 间可教学性的比较，它们等于什么也没有讲。（讽刺的是，展示这些陈述的倡导者们是数据科学家，本应知道存在控制组的必要性。）

### Tidyverse 带来过多复杂性，让学习变得更难

与 Tidy 倡导者的提法正相反，我相信 Tidyverse 让之前没有编程背景的人更 *难* 学习。

**认知过载是很严重的问题**。Tidyverse 的学生要学习的材料相对多得多，这显然不是好的教育方法。在 [“Tidyverse 诅咒”](https://www.r-bloggers.com/the-tidyverse-curse)一文中，作者提到 *此外* 他还“仅仅”用到了 60 个Tidyverse 函数——60！Tidyverse 的“明星” **dplyr** 包含了 263 个函数。

尽管用户最开始只需要用到这些函数的一小部分，高度的复杂性依然明显存在。每当用户要使用一个操作的某种变体，都必须从几百个函数中筛选出正好是需要的那一个。

Tidy 倡导者说全部函数界面的统一性使学习变得更容易。统一的 *语法* 确实很好，但是实际情况是用户真正需要学习的是函数的 *语义*，即每个函数将进行何种操作。举例来说，**summarize()**、**summarize_each()**、**summarize_at()** 及 **summarize_if()** 区别何在？在何种情况下应该使用哪个函数？用户必须加以筛选。

关于 **dplyr**，**data.table** 的创造者 Matt Dowle [指出](https://twitter.com/MattDowle/status/1142001162230489088)

> 你要整合进管道的并不是一个函数 **mutate**。这一个函数可以是
> **mutate**、**mutate_**、**mutate_all**、**mutate_at**、**mutate_each**、
> **mutate_each_**、**mutate_if**、**transmute**、**transmute_**、
> **transmute_all**、**transmute_at** 和 **transmute_if**。
> 而你却告诉我 [因为用户界面都是一致的] 不需要参考手册就能学会这全部？

只是共用一套语法，并不能减轻让人昏头的复杂程度。

作为对比，只要用户学会了 base-R （不难），就可以用少数几个简单的操作处理各种情况。古话说得好：“授人以鱼，不如授之以渔。”

### Tidy 推广者不希望 R 初学者学习什么

Tidy 推广者提出避免使用 base-R 最基础的部分：

* `$` 操作符

* `[[ ]]`

* 循环

* **plot()** 以及相关的基础图形函数等

他们声称这能“简化”学习的过程，然而实际上却会迫使初学者采用一套更复杂、不直观且难以阅读的方案。

### 案例分析：tapply() 函数

**tapply()** 是在 R 语言里最常使用的函数之一。如下所示，不知出于什么原因，Tidy 倡导者不喜欢这个函数，然而这简直是 R 初学者 最好用的函数。

考虑 Tidyverse 教程里一个常见的例子，用到 R 的 **mtcars** 数据集。目标是找出一部车消耗每加仑燃料平均能行驶多少英里（miles per gallon, mpg），按汽缸个数进行分组。Tidy 给出的代码为

``` r
library(dplyr)
mtcars %>%
   group_by(cyl) %>%
   summarize(mean(mpg))
```

这是 base-R 版本：

``` r
tapply(mtcars$mpg, mtcars$cyl, mean)
```

两者都很简单。都不难为初学者所掌握。初学者看过几个例子后，把它们应用在同类别的新问题也不会有什么困难。Tidy 版本调用了两个函数，base-R 则是一个。无论如何，两个版本都不复杂，难分伯仲。但是这当然不能算作 Tidy 版本比较 *容易* 学习的例子。

如何从两个方面进行分组比较有指导意义：

``` r
> mtcars %>%
+ group_by(cyl, gear) %>%
+ summarize(mean(mpg))
# A tibble: 8 x 3
# Groups:   cyl [3]
    cyl  gear `mean(mpg)`
  <dbl> <dbl>       <dbl>
1     4     3        21.5
2     4     4        26.9
3     4     5        28.2
4     6     3        19.8
5     6     4        19.8
6     6     5        19.7
7     8     3        15.0
8     8     5        15.4
> tapply(mtcars$mpg, list(mtcars$cyl, mtcars$gear), mean)
      3      4    5
4 21.50 26.925 28.2
6 19.75 19.750 19.7
8 15.05     NA 15.4
```

必须告诉学生，**tapply()** 用于分组的变量数多于一个时，要把变量用 `list` 括起来。和前面一样，只要有一些例子，学生们这样用没有什么困难。

不过要看看输出形式：Tidy 版本输出一个 tibble，不易阅读，而 **tapply()** 输出一个 R 矩阵，以双向表的形式打印出来。后者的形式恰好是很多学生所需要的，比如应用到社会科学研究等。

检索过 **dplyr** 的几百个函数后，我没有找到如何把 Tidy 的输出转换为 **tapply()** 提供的更有信息量的表格样式。假使可以做到，既然没法轻易识别出这样的函数，也正好能体现我上述观点，Tidy 过于臃肿，不适合初学者。

此外，**tapply()** 的输出还有另一重含义，用户能够察觉没有8-汽缸、4-挡位的汽车，这又是在很多应用中非常有意义的一类信息。

实际上，可以对 Tidy 版本加以修改以显示空白组：

``` r
> mtcars$cyl <- as.factor(mtcars$cyl)
> mtcars$gear <- as.factor(mtcars$gear)
> mtcars %>%
+    group_by(cyl, gear, .drop=FALSE) %>%
+    summarize(mean(mpg))
# A tibble: 9 x 3
# Groups:   cyl [3]
  cyl   gear  `mean(mpg)`
  <fct> <fct>       <dbl>
1 4     3            21.5
2 4     4            26.9
3 4     5            28.2
4 6     3            19.8
5 6     4            19.8
6 6     5            19.7
7 8     3            15.0
8 8     4           NaN
9 8     5            15.4
```

注意需要格式转换，Tidy 文档没有提到。即使有文档，这对 R 初学者来说也是更加复杂了。

因此，说到晓畅程度和可学习性，在这个特定的例子里 Tidy 和 base-R 都不错，Tidy 也并没有更容易学习。至于可用性，我判 base-R 获胜。

### 对函数式编程的使用

Tidyverse 包中另一个特殊的库，面向 *函数式编程*（FP）的 **purrr**，有 177 个函数。关于复杂性的论点依然适用；我们再次遇到和上述 **dplyr** 同样的问题，“有太多函数要学”。

从入门的层次看，FP 就是调用 FP 函数以取代循环。R 的 **apply** 家族，再加上 **Reduce()**、**Map()** 和
**Filter()**，就属于 FP。在很多情况下，使用这些函数是正确的方案。但是按很多 Tidy 推广者提倡的，不加区分地使用 FP 替代 *所有* 循环，明显是过分了，还特别给初学者带来很多困难。

这个推断是 *先验* 的——**FP 涉及函数的编写，而多数初学者需要很长时间去掌握这项技能**。

值得注意的是，顶尖大学的计算机系在逐渐调整编程绪论课程，不再使用 FP 范式，而是采用更传统的 Python。他们认为 FP 更加抽象，更有挑战性。

关于这个话题，一个有趣的讨论见 [Charavarty 和 Keller](https://www-ps.informatik.uni-kiel.de/~mh/reports/fdpe02/papers/paper15.ps.gz)。其实他们支持在 CS 专业的编程绪论课堂中使用 FP，但两位作者的目标和学习 R 的人正好是对立的。作者们列出了三个目标，其中一个是讲授计算机科学理论，一般性的讲授 R 语言对此当然没有什么兴趣，更不要说教没有编写代码经验的人学习 R 语言。他们承认 FP 的一个关键概念 *递归* 是“显著的障碍”，即使是对 CS 学生来说。

如果说 FP 对 CS 学生就很难，那么就没有道理让学习 R 的非程序员学生去使用 FP。

甚至 Hadley 也在 *R for Data Science* 中说道：

> 把一个函数传递给另一个函数，这个想法十分强大，
> 也是使 R 可以成为函数式编程语言的行为之一。
> 你可能需要一些时间让你的头脑适应这个想法，
> 然而这种投入是值得的。

实际上，大多数非 FP 的语言也允许将一个函数传递给另一个，而且这也确实是个强大的工具，值得投入时间学习——*对于有经验的 R 程序员来说*。然而，不应当强迫学习 R 的非程序员“让他们的头脑适应” **purrr**。

### purrr 与 base-R 的对比

我们再次使用 **mtcars** 做例子，来自[在线教程](https://towardsdatascience.com/functional-programming-in-r-with-purrr-469e597d0229)。这里的目标是用车重去回归英里每加仑，计算每个汽缸组别的 R<sup>2</sup>。这是 Tidy 方案，来自 **map()** 的在线帮助页面：

``` r
library(purrr)
mtcars %>%
  split(.$cyl) %>%
  map(~ lm(mpg ~ wt, data = .)) %>%
  map(summary) %>%
  map_dbl("r.squared")

# output
4         6         8 
0.5086326 0.4645102 0.4229655
```

这里有几个主要的点需要注意：

* 针对这个特定的例子，学习 R 的人必须要学习两个不同的 map 函数，以及大量其它函数，只为了一个基础用法。这个例子很好地说明了 Tidy 认知过载的问题。实际上，**purrr** 有 52 个不同的 map 函数！（见下）

* 第一个 map 调用中的第一个 `~` 十分不直观，即使有经验的程序员也没法猜出其作用。这能有力反驳 Tidy 倡导者所声称 Tidy 更符合直觉、就像英语。

* Tidy 执着于避开使用 R 语言标准的 `$` 符号，导致了各种混乱与困惑。

* 不幸的学生自然要问：“表达式里的 ‘summary’ 是哪里来的？”看起来像是在调用 **map()** 的时候用了不存在的变量 **summary**。而在幕布背后，实际上是 base-R 的 **summary()** 函数被调用于前面的计算。这又是相当不直观的，在线帮助页面中也 **没有** 提到。

* 这个可怜的学生会对调用 **map_dbl()** 感到进一步困扰。那个 `r.squared` 从哪里来？再一次，Tidy 把事实隐藏了，**summary()** 会产生一个含有 **r.squared** 组件的 S3 对象。是的，有时候隐藏细节是有帮助的，但只是在不会让初学者感到困惑的时候。

实际上，**R 初学者最好还是从写一个循环开始，避开具有挑战性的 FP 概念**。即使教员认为初学者 *必须* 学习 FP，base-R 版本也要简单很多：

``` r
lmr2 <- function(mtcSubset) {
  lmout <- lm(mpg ~ wt, data=mtcSubset)
  summary(lmout)$r.squared
}
u <- split(mtcars, mtcars$cyl)
sapply(u, lmr2)
```

这里 **lmr2()** 有明确的定义，而不是 Tidy 版本里难以看透的 **map()** 调用和其中的 `~`。

在关于这个例子的[推特讨论](https://twitter.com/dgkeyes/status/1200532987000971264)中，一个 Tidy 倡导者提出异议说上面的 **purrr** 代码不适合学生用：

> 当然，不过我原本的推特是讲如何教导新人的。
> 你的例子其实是无关的，因为这是非常复杂的概念。

这就是我的观点！**新人应该用循环，而不是purrr**。然而 Tidy 推广者不愿让学生用循环。所以用 Tidy 的教员就得避免给学生用这样的例子，同样的例子用 base-R 的教员就很容易处理。

如上所述，Tidy 版本是对“有太多函数要学”这种认知过载的写照，我们更早在 **dplyr** 中也见到了这个问题。请看：

``` r
> ls('package:purrr', pattern='map*')
 [1] "as_mapper"      "imap"           "imap_chr"       "imap_dbl"      
 [5] "imap_dfc"       "imap_dfr"       "imap_int"       "imap_lgl"      
 [9] "imap_raw"       "invoke_map"     "invoke_map_chr" "invoke_map_dbl"
[13] "invoke_map_df"  "invoke_map_dfc" "invoke_map_dfr" "invoke_map_int"
[17] "invoke_map_lgl" "invoke_map_raw" "lmap"           "lmap_at"       
[21] "lmap_if"        "map"            "map_at"         "map_call"      
[25] "map_chr"        "map_dbl"        "map_depth"      "map_df"        
[29] "map_dfc"        "map_dfr"        "map_if"         "map_int"       
[33] "map_lgl"        "map_raw"        "map2"           "map2_chr"      
[37] "map2_dbl"       "map2_df"        "map2_dfc"       "map2_dfr"      
[41] "map2_int"       "map2_lgl"       "map2_raw"       "pmap"          
[45] "pmap_chr"       "pmap_dbl"       "pmap_df"        "pmap_dfc"      
[49] "pmap_dfr"       "pmap_int"       "pmap_lgl"       "pmap_raw"      
```

作为对比，base-R 版本中我们就只用到了 base-R！在 `apply` 家族中只有四个函数要学：**apply()**、**lapply()**、**sapply()** 和 **tapply()**。

### Tibbles

同样，迫使学生学习 tibbles 是糟糕的教学方法。这是更复杂的技术，还是数据框更简明。需要 tibbles 解决的情况应属于进阶课题，并不适宜没有编码背景的初学者。

这些高级的情况下，数据框里列或行的元素不是 *原子* 对象，即并非简单的数字、字符串或者逻辑值。**这是 Tidy 倡导者树立的“稻草人”**；R 初学者不大可能遇到这种类型的数据框。

### The English issue

Again, the point most emphasized by Tidyverse advocates is that the
Tidyverse is more teachable because of its "English-like" syntax. 

Below is a comparison of the "English" **dplyr** to the "non-English"
**data.table** (adapted from
[here](https://atrebas.github.io/post/2019-03-03-datatable-dplyr/)):
We'll again use R's built-in **mtcars** dataset.

``` r 
mtdt <- as.data.table(mtcars);  mtdt[cyl == 6]  # data.table syntax
mttb <- as_tibble(mtcars);  filter(mttb,cyl == 6)  # dplyr syntax 
``` 

Is there really any difference?  Can't beginners, even without
programming background, quickly adapt to either one after seeing a few
examples?  Even those who claim high teachability for **dplyr** do
readily agree that their students could also easily pick up
**data.table**, or for that matter my preference for beginners, base-R,
given some examples.

We saw earlier that the **purrr** example,

``` r
mtcars %>%
  split(.$cyl) %>%
  map(~ lm(mpg ~ wt, data = .)) %>%
  map(summary) %>%
  map_dbl("r.squared")
```

would be baffling even to experienced (but non-R) programmers, starkly
contradicting the claimed "English-like clarity" of Tidy.  And the
**dplyr** meaning of **mutate** is nowhere near its English meaning, and
again, would not be guessed even by a non-R professional programmer.

In other words, though students may say they like the "English" aspect
of Tidy, the benefit is illusory.  They could become more proficient in
R, **more quickly**, learning base-R than Tidy.

By the way, as noted below, the Tidy advocates don't like the many
base-R functions whose names *do* use English, e.g. **plot()**,
**lines()**,  **aggregate()** and **merge()**.  Clearly, then, English
is not the core issue.

### Pipes

The Tidyverse also makes heavy use of **magrittr** *pipes*, e.g. writing
the function composition **h(g(f(x)))** as

``` r
f(x) %>%  g() %>% h()
```

Again, the pitch made is that this is "English," in this case in the
sense of reading left-to-right.  But again, one might question just how
valuable that is, and in any event, I personally tend to write such code
left-to-right anyway, *without* using pipes:

``` r
a <- f(x)
b <- g(a)
h(b)
```

As a long-time teacher of programming languages (C, C++, Java, Pascal,
Python, R, assembly language, etc.), I find the promotion of pipes
troubling.  The piped version hides the fact that **g()** and **h()**
have an argument, which is invisible in the pipe expression.  

Or if **w()** say, were to have two arguments, the first one being used
in the pipe, that argument would be hidden, making it appear that there
is only one argument:

``` r
> w <- function(u,v) u+2*v
> 3 %>% w(5)
[1] 13
```

Here **w()** has 2 arguments, but it looks like 1.

And what if we want that 3 to play the role of **v**, not **u**?  Yes,
**magrittr** has a way to do that, the "dot" notation:

``` r
> 3 %>% w(5,.)
[1] 11
```

But that is yet another example of my point, that **Tidy is burdening
the R learner with extra, unnecessary complexity**.  Indeed, just as
**dplyr**, with 263 functions, is far too complex for beginners, so are
pipes.  There are so many variations to learn that Hadley's *R for Data
Science* book devotes a full chapter to pipes, 3415 words.  

As noted before, a beginner need learn only a small fraction of that
material at first, but the above example of the dot notation is
certainly not an advanced case.  Again, each time the beginner is
confronted with a new situation, she must sift through the myriad
variants, of **dplyr**, **purrr**, pipes or whatever.

Moreover, what if the function **h()** above has two arguments,
rather than just one, with each argument requiring functional
composition?  Pipes can't be used there.

And even more importantly, even advocates of pipes concede that pipes make
debugging more difficult; by contrast, my style above lends itself easily to
debugging.  And again, for large problems, piped code is slower.

The benefit of pipes claimed by the Tidyers is the "left to right"
execution.  They conceded that one can achieve this without pipes, but
stress that this comes at the expense of setting up variables for the
intermediate results.  That's a valid point, but is that small gain
worth the increased cognitive load on R learners, increased debugging
problems and so on?  To me it clearly is not.

### Code readability

The Tidyverse advocates also claim that the "English" in **dplyr** makes
the code easier to *read*, not just write.  To me, that is missing the
point; as any instructor of software engineering can tell you, the best
way to make code readable is to use REAL English, in good, meaningful
code comments.  And this is just as important, if not more so, for
nonprogrammers.

See my [R style guide](http://github.com/matloff/R-Style-Guide) for more on
readability issues.

### Summary:  the proper status of the Tidyverse in teaching

As I said earlier, in discussions with those who report success in using
the Tidyverse to teach beginning programmers, I ask whether their
students are incapable of learning just base-R.  They readily concede
that the answer is no.  Indeed, before the Tidyverse, throngs of people
were learning base-R without any prior programming background.

As also mentioned, the Tidyverse can be difficult to debug, and run very
slowly on large datasets.  The perceived benefit of being "English-like"
is illusory.

In short, in my view there is no advantage to teaching R through the
Tidyverse, and some significant disadvantages.  I think it is a mistake
to feature the Tidyverse in teaching R to beginners, for these reasons:

1.  Complexity and volume of the presented material.

2.  Difficulty in debugging.

3.  Inadequate generalizability.


## RECOMMENDATIONS

*Teaching:*

Courses in R, **especially those aimed an nonprogrammers**, should
develop a solid grounding in base-R as first priority.

The proper placement of Tidy in R courses should be:

* **dplyr:** Taught, along with **data.table**, at the Intermediate R
  level.

* **purrr:** Taught only at the Advanced level.

* pipes: Taught at the Intermediate level, and presented as an *option*
  that some students may find useful in some situations (as opposed to
being presented as *the* way one should work).

I am certainly not saying one should only use base R; on the
contrary, CRAN is a major advantage of R, which I use extensively,
and to which R beginners should definitely be exposed.

But the Tidyverse should be considered advanced R, not for beginners,
just as is the case for most complex CRAN packages, and should be
presented, as noted, as an *option*, not as *they* way.

*The role of RStudio:*

In my view, RStudio can easily remedy the problem.  It can take the
following actions to greatly ameliorate the "monopolistic" problems:

1.  Promote the teaching of base-R to beginners, treating the Tidyverse
    as an advanced topic.  The popular book, *R for Everyone: Advanced
Analytics and Graphics* (second ed.), by Jared Lander does exactly this!

2.  In the various RStudio Web pages on writing fast R code, give
    **data.table** equal time.
