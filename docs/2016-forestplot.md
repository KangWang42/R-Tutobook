# R语言绘制森林图详细教程-forestplot



> 本期主要介绍如何使用forestplot包绘制森林图，常用于meta分析的可视化
>
> 根据我的教程书写体验来看forestplot包**还很不好用**，基于gpar包来设置样式，使用体验极不好，不过写都写了，发一点东西
> 
> 根据实际体验来看还是**forestploter包绘制森林图更好看**，代码更合理，样式也更好看，之后会介绍
> 
> 这期不建议看，这个**包也不建议用**，连教程文档很多都跑不动
> 

## R包介绍

forestplot包是R语言中用于绘制森林图的包，其主要功能是将数据整理成适合绘制森林图的格式，并提供了丰富的绘图选项，使得用户可以轻松地绘制出各种类型的森林图。

[更多教程](https://cran.r-project.org/web//packages/forestplot/vignettes/forestplot.html)

## R包安装


``` r
install.packages("forestplot")
```

## R包教程

### 载入包


``` r
library(forestplot)
library(dplyr)
```

### 导入数据

- mean: OR区间的平均值
- lower/upper：置信区间上下限
- study：标签


``` r
data <- tibble::tibble(
  mean = c(0.578, 0.165, 0.246, 0.700, 0.348, 0.139, 1.017),
  lower = c(0.372, 0.018, 0.072, 0.333, 0.083, 0.016, 0.365),
  upper = c(0.898, 1.517, 0.833, 1.474, 1.455, 1.209, 2.831),
  study = c(
    "Auckland", "Block", "Doran", "Gamsu",
    "Morrison", "Papageorgiou", "Tauesch"
  ),
  deaths_steroid = c("36", "1", "4", "14", "3", "1", "8"),
  deaths_placebo = c("60", "5", "11", "20", "7", "7", "10"),
  OR = c("0.58", "0.16", "0.25", "0.70", "0.35", "0.14", "1.02")
)
```

### 基础绘图

可以看出forestplot包绘制森林图主体为`forestplot`函数，后续增加`fp_xxx`函数来完善内容

- fp_set_style：设置样式
- fp_add_header：添加表头
- fp_append_row：额外添加行


``` r
data |>
  forestplot(
    labeltext = c(study, deaths_steroid, deaths_placebo, OR),
    clip = c(0.1, 2.5),
    xlog = TRUE
  ) |>
  fp_set_style(
    box = "royalblue",
    line = "darkblue",
    summary = "royalblue"
  ) |>
  fp_add_header(
    study = c("", "Study"),
    deaths_steroid = c("Deaths", "(steroid)"),
    deaths_placebo = c("Deaths", "(placebo)"),
    OR = c("", "OR")
  ) |>
  fp_append_row(
    mean = 0.531,
    lower = 0.386,
    upper = 0.731,
    study = "Summary",
    OR = "0.53",
    is.summary = TRUE
  ) |>
  fp_set_zebra_style("#EFEFEF")
```

<img src="2016-forestplot_files/figure-html/unnamed-chunk-4-1.png" width="672" />

## 样式美化

### 修改样式

- 使用`fp_set_style`来修改各内容的样式
- 使用`fp_add_lines`来添加线条
- 更多参数大家需要多看help文档

![](https://pic-go-42.oss-cn-guangzhou.aliyuncs.com/img/202410280846517.webp)

主要参考的是设置是`gpar`包样式
 

``` r
data |>
  forestplot(
    labeltext = c(study, deaths_steroid, deaths_placebo, OR),
    clip = c(0.1, 2.5),
    xlog = TRUE
  ) |>
  fp_add_lines() |>
  fp_set_style(
    box = "royalblue",
    line = "darkblue",
    summary = "royalblue",
    align = "lrrr",
    hrz_lines = "#999999"
  ) |>
  fp_add_header(
    study = c("", "Study"),
    deaths_steroid = c("Deaths", "(steroid)") |>
      fp_align_center(),
    deaths_placebo = c("Deaths", "(placebo)") |>
      fp_align_center(),
    OR = c("", fp_align_center("OR"))
  ) |>
  fp_append_row(
    mean = 0.531,
    lower = 0.386,
    upper = 0.731,
    study = "Summary",
    OR = "0.53",
    is.summary = TRUE
  )
```

<img src="2016-forestplot_files/figure-html/unnamed-chunk-5-1.png" width="672" />

### 对线条自定义

使用fp_add_lines来添加辅助线，lty是线形，lwd是线宽，col是颜色

f_n代表对第几列添加线条，columns设置线条有多宽


``` r
data |>
  forestplot(
    labeltext = c(study, deaths_steroid, deaths_placebo, OR),
    clip = c(0.1, 2.5),
    vertices = TRUE,
    xlog = TRUE
  ) |>
  fp_add_lines(
    h_3 = gpar(lty = 2),
    h_11 = gpar(lwd = 1, columns = 1:4, col = "#000044")
  ) |>
  fp_set_style(
    box = "royalblue",
    line = "darkblue",
    summary = "royalblue",
    align = "lrrr",
    hrz_lines = "#999999"
  ) |>
  fp_add_header(
    study = c("", "Study"),
    deaths_steroid = c("Deaths", "(steroid)") |>
      fp_align_center(),
    deaths_placebo = c("Deaths", "(placebo)") |>
      fp_align_center(),
    OR = c("", fp_align_center("OR"))
  ) |>
  fp_append_row(
    mean = 0.531,
    lower = 0.386,
    upper = 0.731,
    study = "Summary",
    OR = "0.53",
    is.summary = TRUE
  )
```

<img src="2016-forestplot_files/figure-html/unnamed-chunk-6-1.png" width="672" />

### 减小固定box（就是平均值的那个盒子）大小

强制boxsize的大小，使用函数forestplot的参数`boxsize`,但是设置之后大小也不会随着OR增大而增大


``` r
data |>
  forestplot(
    labeltext = c(study, deaths_steroid, deaths_placebo, OR),
    clip = c(0.1, 2.5),
    vertices = TRUE,
    boxsize = 0.2,
    xlog = TRUE
  ) |>
  fp_add_lines(
    h_3 = gpar(lty = 2),
    h_11 = gpar(lwd = 1, columns = 1:4, col = "#000044")
  ) |>
  fp_set_style(
    box = "royalblue",
    line = "darkblue",
    summary = "royalblue",
    align = "lrrr",
    hrz_lines = "#999999"
  ) |>
  fp_add_header(
    study = c("", "Study"),
    deaths_steroid = c("Deaths", "(steroid)") |>
      fp_align_center(),
    deaths_placebo = c("Deaths", "(placebo)") |>
      fp_align_center(),
    OR = c("", fp_align_center("OR"))
  ) |>
  fp_append_row(
    mean = 0.531,
    lower = 0.386,
    upper = 0.731,
    study = "Summary",
    OR = "0.53",
    is.summary = TRUE
  )
```

<img src="2016-forestplot_files/figure-html/unnamed-chunk-7-1.png" width="672" />

### 分组OR

垃圾包，已经跑不了分组了，应该是groupby更新后没适配上。浪费我一个小时


``` r
data(dfHRQoL)

dfHRQoL  |> group_by(group)|>
  forestplot(
    labeltext = c(labeltext),
    boxsize = 0.1,
    lineheight = "lines",
    xlab = "EQ-5D index"
  ) |>
  fp_add_lines("steelblue") |>
  fp_add_header("Variable") 

  |>
  fp_set_style(
    box = c("blue", "darkred") |>
      lapply(function(x) gpar(fill = x, col = "#555555")),
    default = gpar(vertices = TRUE)
  )
```
