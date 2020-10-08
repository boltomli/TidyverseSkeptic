# TidyverseSkeptic

从另一种视角看 R 语言的 Tidyverse “方言”，以及 RStudio 对 Tidyverse 的提倡。

## Norm Matloff, Prof. of Computer Science, UC Davis (former Prof. of Statistics at UCD)

作者 Norm Matloff 为 UC Davis 计算机科学教授（曾任 UCD 统计学教授）。本中文翻译经过作者[同意](https://github.com/matloff/TidyverseSkeptic/issues/22)。文中的“我”为作者视角，但译文中存在的任何不妥之处当然很可能是由译者引入的，还望读者不吝[赐教](https://github.com/boltomli/TidyverseSkeptic/issues/new)。

## 注意：此为简版

在我看来，Tidyverse 的主要问题在于其不利于教学。我相信使用 Tidyverse 而非 base-R 实际上会**阻碍**对没有编写代码背景的初学者进行教学。这个简洁的版本仅保留了 TidyverseSkeptic 文中关于教学的部分。我在完整的文档中还谈及了其它问题，详见[英文原文全文](READMEFull.md)。

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

* RStudio 作了可敬的工作，让更多女性及未被充分代表的少数群体能接触到 R。然而，由于被限制在复杂的 Tidyverse 系统中，这些群体将很难为 R 语言作出更多贡献，诸如编写 CRAN 包、撰写书籍等等。这些工作需要相当熟悉 base-R 的使用，即使代码本身仍然可以主要由 Tidyverse 写就。

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
> ggplot(dn) + geom_histogram(aes(Nile),dn)
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
> thue2 <- subset(thuesen,blood.glucose < 7)
```

基于 base-R 的话，这第二课可以轻松讲到，说不定第一课就可以。而 Tidy 则不然，需要更改成

``` r
> library(dplyr)
> thue2 <- thue2 %>% filter(blood.glucose < 7)
```

教员首先要讲授管道操作符 `%>%`，又一份额外的复杂性。在做这件事情的时候，教员很可能要强调管道是“从左到右”的流，然而学生会感到困惑，因为从左到右的流完成后，马上就又跟着一个从右到左的流 `<-`。（不管出于什么原因，Tidy 似乎并不使用 R 的 `->` 操作。）

又一次，Tidyverse 对于没有编程背景的学习 R 的人依然过于复杂，**拖慢了学习进度**。

### The Tidyverse advocates' claims

As a lifelong passionate teacher, I strongly question the claim made by
Tidyverse advocates that it facilitates the teaching of R to
non-programmers, as opposed to teaching them base-R.  

(I regard both **dplyr** and **data.table** as advanced topics; neither
is suitable for beginners.  On the other hand, I think teaching
beginners **ggplot2** is fine, but point out again that it is not part
of the Tidyverse.)

There has been no study of Tidy advocates' teachability claim.
Advocates often provide testimonials from students like 

* "I learned R using Tidyverse, and now am productive in R" 

* "I like the English-like nature of the Tidyverse"

* "I can make beautiful graphics with the Tidyverse"

* "Tidyverse showed me the fluidity of data"

Advocates who are instructors will echo those statements, and add, e.g.

* "Base-R is good for professional programmers, but the Tidyverse is the
  best R learning tool for non-techies who just want to do data
analysis"

* "R was created by statisticians, for statisticians.  But we are data
  scientists, mainly interested in producing graphs and tables"

* "The Tidyverse is **modern** R, for the rest of us"

All of these statements are either misleading, irrelevant to the
teachability issue, or downright meaningless.  They say nothing at all
about the teachability of base-R in comparison to Tidy.  (It is ironic
that advocates who present such statements are data scientists, who
ought to know the need for a control group.)

### Tidyverse makes learning harder, due to adding much complexity 

Contrary to the Tidy advocates' claim, I believe using the Tidyverse
makes things more *difficult* for learners without prior programming
background.  

**There is a serious problem of cognitive overload.** Tidyverse students
are being asked to learn a much larger volume of material, which is
clearly bad pedagogy.  See ["The Tidyverse
Curse"](https://www.r-bloggers.com/the-tidyverse-curse), in which the
author says *inter alia* that he uses "only" 60 Tidyverse functions --
60!  The "star" of the Tidyverse, **dplyr**, consists of 263 functions. 

While a user initially need not use more than a small fraction of those
functions, the high complexity is clear.  Every time a user needs some
variant of an operation, she must sift through those hundreds of
functions for one suited to her current need.  

Tidy advocates say the uniformity of interface in all those functions
makes learning them easier.  Uniform *syntax* is nice, yes, but the fact
remains that users must learn the *semantics* of the functions, i.e.
what operations they perform.  What, for example, is the difference
between **summarize()**, **summarize_each()**, **summarize_at()** and
**summarize_if()**?  Under which circumstances should each be used?  The
user must sift through this.

As Matt Dowle, creator of **data.table**, [pointed
out](https://twitter.com/MattDowle/status/1142001162230489088) about
**dplyr**,

> It isn't one function **mutate** that you combine in a pipe.  It's
> **mutate**, **mutate_**, **mutate_all**, **mutate_at**, **mutate_each**,
> **mutate_each_**, **mutate_if**, **transmute**, **transmute_**,
> **transmute_all**, **transmute_at** and **transmute_if**.  And you're
> telling me [because of consistency of the user
> interfaces] you don't need a manual to learn all those?

Having a common syntax thus does not compensate for this dizzying
complexity. 
 
By contrast, if the user knows base-R (not difficult), she can handle
any situation with just a few simple operations.  The old adage applies:
"Give a man a fish, and he can eat for a day. Teach him how to fish, and
he can eat for a lifetime."  

### What Tidy promoters want R beginners NOT to learn

The Tidyers make a point of avoiding the most basic parts of base-R:

* the '$' operator

* '[[ ]]'

* loops

* **plot()** and the associated basic graphics functions

They would argue that this "simplifies" the learning process, but
actually it forces beginners to come up with more complex, less
intuitive and harder-to-read solutions.

### Case Study: the tapply() Function

One of the most commonly-used functions in R is **tapply()**.  As
noted below, for some reason Tidy advocates hate this function, but
arguably it is perfect for R beginners.

Consider a common example in tutorials on the Tidyverse, involving R's
**mtcars** dataset.  The goal is to find mean miles per gallon, grouped
by number of cylinders.  The Tidy code offered is

``` r
mtcars %>%
   group_by(cyl) %>% 
   summarize(mean(mpg))
```

Here is the base-R version:

``` r
tapply(mtcars$mpg,mtcars$cyl,mean)
```

Both are simple.  Both are easily grasped by beginners. After being
presented with some examples, beginners have no trouble using them in a
new setting of similar type.  The Tidy version requires two function
calls rather than one for base-R.  But again, both versions are simple,
so let's call it a tie.  But is it certainly not the case that the Tidy
version is *easier* to learn.

It's instructive to look at what happens when one groups by two aspects:

``` r
> mtcars %>%
+ group_by(cyl,gear) %>%
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
> tapply(mtcars$mpg,list(mtcars$cyl,mtcars$gear),mean)
      3      4    5
4 21.50 26.925 28.2
6 19.75 19.750 19.7
8 15.05     NA 15.4
```

With **tapply()**, students do have to be told that in the case of more
than one grouping variable, they need to surround the variables with
'list'.  Again, once they are given examples, students have no trouble
with this.

But look at the form of the output:  The Tidy version outputs a tibble,
rather hard to read, while **tapply()** outputs an R matrix, printed out
as a two-way table.  The latter form is exactly what many students need
in their applications, e.g.  social science research.  

In searching through the hundreds of functions in **dplyr**, it is not
clear to me which one, if any, can convert that Tidy output to the very
informative tabular view that **tapply()** provides.  If there is one,
the fact that one is not easily identifiable illustrates my point above
that Tidy is actually very bloated, not suitable for beginners.

Moreover, the **tapply()** output is more informative in a second sense,
letting the user know that there were no 8-cyliner, 4-speed cars, again
the kind of thing that is quite meaningful in many applications.  

Actually, the Tidy version can be modified in order to notice that empty
group:

``` r
> mtcars$cyl <- as.factor(mtcars$cyl)
> mtcars$gear <- as.factor(mtcars$gear)
> mtcars %>% 
+    group_by(cyl,gear,.drop=FALSE) %>% 
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

Note the need to convert to factors, something not mentioned in the
Tidy documentation, and which would further complicate things for R
beginners even if it were documented.

So, in terms of clarity and learnability, the Tidy and base-R versions
in this paricular example are both good, again showing that Tidy is not
easier to learn.  And In terms of usability, I'd give base-R the win
here. 

### Use of functional programming

Another featured Tidyverse package, the *functional programming*
(FP)-oriented library **purrr**, has 177 functions.  Again the point
about complexity applies;  we again have the "too many functions to
learn" problem as we saw with **dplyr** above.  

At the basic level, FP is merely replacing loops by calls to FP
functions.  R's **apply** family, plus **Reduce()**, **Map()** and
**Filter()** should be considered FP.  In many cases, using such
functions is the right solution.  But the indiscriminate use of FP,
advocated by many Tidyers, to replace *all* loops is clearly overdoing
it, and makes things especially difficult for beginners.

This is clear *a priori* -- **FP involves writing functions, a skill that
most beginners take a long time to develop well.**

It is worth noting that top university Computer Science Departments have
shifted away from teaching their introductory programming courses using
the FP paradigm, in favor of the more traditional Python, as they deem
FP to be more abstract and challenging.  

An interesting discussion of the topic is in [Charavarty and
Keller](https://www-ps.informatik.uni-kiel.de/~mh/reports/fdpe02/papers/paper15.ps.gz).
Though they support using FP in introductory programming classes for CS
majors,  the authors' goals are antithetical to those of R learners.
The authors list three goals, one of which is to teach theoretical
computer science, certainly not desirable for teaching R in general, let
alone for teaching R to those with no coding experience.  They also
concede that a key concept in FP, *recursion*, is a "signficant
obstacle" even for CS students.  

If FP is tough for CS students, it makes no sense to have nonprogrammer
learners of R use it.

Even Hadley, in *R for Data Science*, says:

> The idea of passing a function to another function is extremely powerful
> idea, and it’s one of the behaviours that makes R a functional
> programming language. It might take you a while to wrap your head around
> the idea, but it’s worth the investment. 

Actually, most non-FP languages allow passing one function to another,
but yes it is a powerful tool, worth the investment of time -- *for the
experienced R programmer*.  But again, it's wrong to foce nonprogrammer
learners of R to "wrap their heads around" **purrr**.

### purrr vs. base-R example 

Again, let's use an **mtcars** example taken from
[an online tutorial](https://towardsdatascience.com/functional-programming-in-r-with-purrr-469e597d0229).  Here the goal is to regress miles per gallon against weight, calculating R<sup>2</sup> for each cylinder group.  Here's the Tidy
solution, from the online help page for **map()**:

``` r
mtcars %>%
  split(.$cyl) %>%
  map(~ lm(mpg ~ wt, data = .)) %>%
  map(summary) %>%
  map_dbl("r.squared")

# output
4         6         8 
0.5086326 0.4645102 0.4229655
```

There are several major points to note here:

* The R learner here must learn two different map functions for this
  particular example, and a dozen others for even basic use. This is an
excellent example of Tidy's cognitive overload problem.  Actually,
**purrr** has 52 different map functions!  (See below.)

* The first '~' in that first map call is highly nonintuitive.  Even
  experienced programmers would not be able to guess what it does. This
is starkly counter to the Tidyers' claim that Tidy is more intuitive and
English-like.

* Tidy, in its obsession to avoid R's standard '$' symbol, is causing
  all kinds of chaos and confusion here.

    The hapless student would naturally ask, "Where does that expression
'summary' come from?"  It would appear that **map()** is being called on
a nonexistent variable, **summary**.  In actuality, base-R's
**summary()** function is being called on the previous computation
behind the scenes.  Again, highly nonintuitive, and NOT stated in the
online help page.

    The poor student is further baffled by the call to **map_dbl()**.
Where did that 'r.squared' come from?  Again, Tidy is hiding the
fact that **summary()** yields an S3 object with component
**r.squared**.  Yes, sometimes it is helpful to hide the details, but
not if it confuses beginners.

The fact is, **R beginners would be much better off writing a loop here,
avoiding the conceptually more challenging FP.** But even if the
instructor believes the beginner *must* learn FP, the base-R version is
far easier:

``` r
lmr2 <- function(mtcSubset) {
   lmout <- lm(mpg ~ wt,data=mtcSubset)
   summary(lmout)$r.squared
}
u <- split(mtcars,mtcars$cyl)
sapply(u,lmr2)
```

Here **lmr2()** is defined explicitly, as opposed to the Tidy version, with
its inscrutable '~' within the **map()** call.

In a [Twitter discussion](https://twitter.com/dgkeyes/status/1200532987000971264)
of the above example, a Tidy advocate protested that the above **purrr** code was not 
appropriate for learners:

> Sure, but my original tweet was about teaching newbies. Your example is
> not really relevant to that because it's about a VERY complex concept.

Exactly my point!  **Newbies should write this as a loop, NOT using
purrr**.  But the Tidy promoters don't want learners to use loops.
So the instructor using Tidy simply would avoid giving students such an
example, whereas it would be easy for the base-R instructor to do so.

As noted, the Tidy version shown earlier  is an illustration of the "too
many functions to learn," cognitive overload, problem we saw earlier
with **dplyr**.  Behold:

``` r
> ls(package:purrr,pattern='map*')
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

By contrast, in the base-R version, we indeed stuck to base-R!  There
are only four main functions to learn in the 'apply' family:  **apply()**,
**lapply()**, **sapply()** and **tapply()**.

### Tibbles

Similarly, it is bad pedagogy to force students to learn tibbles, a
more complex technology, instead of data frames, a simpler one.  The
types of situations that tibbles are meant to address should be an
advanced topic, not for beginners with no coding background.

Those advanced situations involve data frames in which row/column
elements are not *atomic* objects, i.e.\ not simple numbers, character
strings or logical values.  **This is a "straw man" set up by the Tidy
advocates'**; R beginners are very unlikely to encounter data frames of
this type.

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
