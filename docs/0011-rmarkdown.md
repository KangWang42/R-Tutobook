# rmarkdown教程-初学r语言推荐



## rmarkdown介绍

rmarkdown是一种将r语言代码和markdown语法整合在一起的工具，它可以将r语言代码的执行结果和文字、图片、表格等内容整合在一起，形成一个完整的文档。rmarkdown的文档可以导出为html、pdf、word等格式的文档。rmarkdown的文档可以在github上免费发布，也可以在rstudio上免费发布。rmarkdown的文档可以在

rmarkdown主要用于**逐段运行代码并展示结果，生成演示文档，生成html用于其它平台发布，搭配bookdown搭建网页教程**

刚学习r语言的同学可以使用rmarkdown来学习r语言，不仅可以在段落中间穿插个人说明，同时用markdown的大纲符号“#”可以让**代码结构清晰**

## rmarkdown使用

在工具栏新建rmarkdown文档，会生成模板文件，在模板文件的基础上增删修改

![](https://vip.123pan.cn/1813062489//7%20pic/202410200846060.png)


## rmarkdown界面

![](https://vip.123pan.cn/1813062489//7%20pic/202410200851433.png)

- 先把yaml里的文档原属性进行修改，作者标题修改一下，后期如果要发布展示会显示在页面最上方
- 用markdown语法新建大纲标题，用“#”符号，“#”符号越多，标题字号越小
- 用快捷键“ctrl+alt+i”可以在当前位置插入代码块，用“ctrl+alt+o”可以在当前位置插入输出块
- 尝试运行自己的代码吧

## rticles包-rmarkdown模板

安装rticles包之后，**在新建rmd文件处就能看到不同的模板，选择一个模板，就可以生成一个模板文件**，模板文件的内容和模板的内容是一样的，但是模板文件的内容更加完善，模板文件的内容可以直接运行，模板文件的内容可以导出为html、pdf、word等格式的文档，模板文件的内容可以在github上免费发布，也可以在rstudio上免费发布

安装prettydoc包也是一样的效果


![](https://vip.123pan.cn/1813062489//7%20pic/202410200856148.png)

## rmarkdown编译

代码完成后即可点击rstudio的“knit”按钮，即可编译，编译后会生成一个html文件，在html文件中可以看到代码的运行结果，同时也可以导出为pdf、word等格式的文档，导出的文档可以在github上免费发布，也可以在rstudio上免费发布

![](https://vip.123pan.cn/1813062489//7%20pic/202410200950363.png)

## rmarkdown的块设置

rmarkdown主要是用于代码导出结果展示的包，同时在导出时我们会有侧重的设置某些代码块的运行。例如：设置一些块不运行，一些块运行但是不显示信息，一些块运行但是不报错，一些块运行但是不显示结果。

rmd的块设置共有7种，**Code evaluation、Results、Code Decoration、Chunks、Cache、Animation、Plots**。看起来复杂，其实实际使用到的也就几个，大家先过一遍，以后慢慢熟悉。

### 如何添加块设置

在块头处和r用空格隔开，不同设置间用“,”隔开

![](https://vip.123pan.cn/1813062489//7%20pic/202410200918995.png)


### Code evaluation-设置块是否运行

#### eval参数  示例：“eval=F”

**可设置不运行代码,注意这里不运行代码**


``` r
print('这是运行结果')
```


#### include参数 示例：“include=F”

**这里其实是有代码的，但是带着输出被一起隐藏了（占位符）**



#### Results参数,设置结果输出



``` r
print("这是设置 result = 'hide'的运行结果,虽然运行了，但是不显示")
```



#### collapse参数 ,为T表示代码和结果一起输出

下方设置为F效果


``` r
print('这是运行结果')
```

```
## [1] "这是运行结果"
```


### echo参数，输出文档是否显示代码

**设置为F之后，运行代码，但是只显示结果不显示代码**


```
## [1] "这是运行结果"
```


### error、warning、message为同一类参数，当代码中有警告或者错误信息时是否展示，如果为F时即不展示。


``` r
print('这是运行结果')
```

```
## [1] "这是运行结果"
```

## 更多教程

中间介绍了几个我常用的，更多的rmd教程可直接阅读官方的[使用手册](https://bookdown.org/yihui/rmarkdown/)
