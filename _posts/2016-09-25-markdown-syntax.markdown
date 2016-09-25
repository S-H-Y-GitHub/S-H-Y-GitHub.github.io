---
layout:     post
title:      "markdown语法简明手册"
subtitle:   "markdown syntax"
date:       2016/9/25 12:07:31 
author:     "率怀一"
header-img: "img/in-post/2016-09-25-markdown-syntax/post-bg.png"
catalog: true
tags:
    - markdown
    - 学习笔记
---

# Markdown 概述

Markdown 是一种轻量级标记语言，它允许人们使用易读易写的纯文本格式编写文档，然后转换成格式丰富的HTML页面。 
—— [维基百科](https://zh.wikipedia.org/wiki/Markdown)

Markdown 语法是对纯文本格式的强化，能使文本显示得更清晰、有条理。但它依旧算是简单的文本，很容易修改和扩展，常用于快速写作中。

所见即所得。不少 MD 编辑器有极强的实时预览渲染，可以让写作者及时看到自己写作的内容显示效果并对此做出调整。

Markdown 格式的简洁特性、兼容扩展性颇佳，使之能快速转换为各种互联网上的常用格式，比如 HTML、Word、PDF 等。目前，越来越多的人开始接受和使用它。

# Markdown 编辑器

常见及常用的 Markdown 编辑器很多，比如：

* [MacDown](http://macdown.uranusjr.com/)
* [Typora](http://typora.io/)  

此外还有（收费为主）：

* [MarkdownPad](http://markdownpad.com/)
* [Scrivener](http://www.literatureandlatte.com/scrivener.php)
* [Typed](http://realmacsoftware.com/typed/)
* [iA Writer](https://ia.net/writer/mac/)
* [Byword](http://bywordapp.com/)
* [Marked 2](http://marked2app.com/)
* [Ulysses](http://www.ulyssesapp.com/)
* [Marboo](http://marboo.io/) 
* [Mou](http://25.io/mou/)

以及支持 Markdown 的优质在线编辑器：

* [马克飞象](http://maxiang.info/)
* [Dillinger](http://dillinger.io/)
* [StackEdit](https://stackedit.io/)
* [Markable](http://markable.in/editor/)

入门编辑器推荐第一序列的 MacDown，其它编辑器可以等熟悉 Markdown 之后再自行探索。
 


# Markdown 语法

关于 Markdown 的基本语法，这里将逐一说明。对于一些写作中一般不算常用（不好用）的表格及代码展示，不多说明。

基本所有以下涉及的标点都以在英文输入状态下的为准。不然会导致语法失效。**由于博客使用的是kramdown解释器，一些显示效果可能与Github官方不同，在博文中能够看到的效果经供参考。**

关于语法，让我们先从在文中起到分清区块、梳理逻辑关系的标题说起：

## 标题

    # 一级标题
    ## 二级标题
    ### 三级标题
    #### 四级标题
    ##### 五级标题

显示效果如下：

# 这是一级标题  
## 俺，二级标题  
### 我是三级标题  
#### 人家只是个四级标题……  
##### 更小的我，五级标题 XD 
###### Github 可以支持的最小的我（哪里冒出来的）

## 换行

Markdown 语法下，换行的方式有：

1. 隔行换行。连续敲击两下「Enter」键，再开始写下一段；
2. 在行末添加两个空格符，而后「Enter」（为了显示清晰），开始写下一段。

## 强调标记
    
    *斜体* 斜体
    _斜体_
    
    **加粗** 加粗
    __粗体__

对于强调符号，需要注意的就是，以什么开始，以什么结尾，数量也保持一致，相应的语法才能生效。

显示效果如下：

这是 *斜体*

这是 **强调**

## 分割线
    
    *** 加分割线
    * * * 加分割线
    ***** 或者这样？
    --- 还有另外的方式
    ___ 其实，还可以这样
    
以下就是一条分割线：

***

## 列表

列表分无序列表合有序列表两类，前者以「*」、「-」、「+」开头，后者以阿拉伯数字「1」开头。

三个注意点：

1. 如果前面有内容，在输入字符前，应先空一行；
2. 符号与内容之间，须隔一个空格符，列表模式才能生效；
3. 第一行内容输入完成，换行会自动补全下一行的开头符号（有序列表数字递增，无序列表符号不变），接下去只需继续输下一行内容，以此类推；
4. 多层级列表，为美观也为减少出错考虑，注意同级列表符号的统一和上下对齐。

无序列表：

    Unordered List:
    
    * English
    * Japanese
    * Chinese
    * ……

    Unordered List:
    
    - English
    - Japanese
    - Chinese
    - ……

显示效果均如下：

Country List：

* English
* Japanese
* Chinese
* ……


有序列表：

    Ordered List:
    
    1. Orange
    2. Apple
    3. Banana

My Favorite Fruit List:
    
1. Orange
2. Apple
3. Banana

多层级列表：

    两都名胜
    
    - 南京
      + 玄武湖
      + 中山陵
      + 鸡鸣寺
    - 杭州
      + 西湖
        * 苏堤
        * 湖心亭
        * 太子湾
      + 九溪
      + 灵隐

注：此处的几个符号作用都是一样的，不同层级符号有所区别只为显示美观。日常使用，请每一级的符号一致。

显示效果如下：
      
两都名胜
    
- 南京
    + 玄武湖
    + 中山陵
    + 鸡鸣寺
- 杭州
    + 西湖
      * 苏堤
      * 湖心亭
      * 太子湾
    + 九溪
    + 灵隐

*** 

## 引用

引用。使用「>」，添加在每行的开头。

两个注意点：

1. 「>」的上一行，必须为空行；
2. 「>」与其后紧跟的第一个字之间有无空格符不影响效果（不过建议加一个）。

显示效果如下：

詹姆斯·馬奇《馬奇論管理》：

> 堂吉诃德提醒我们，如果我們只在不被辜負時去信任，只在有所回報時去愛，只在學有所用時去學習，那麼我們就放棄了為人的特征——願意在自我理念的名義下行動，不管結果如何。

或者，你想要引用一首诗、一首歌：

    > 五月天《天使》
    
    > 像孩子依赖着肩膀 
    > 像眼泪依赖着脸庞 
    > 你就像天使一样 
    > 给我依赖 给我力量  

这儿也需要注意换行：每一行最后换行，添加两个空格符，不然内容会挤压在一块，变成一行。或者行与行之间，空一行。以下例子中，歌词部分输入时虽然都分列开，而实际显示时歌词都连成一句了。

> 五月天《天使》 
> 
> 像孩子依赖着肩膀 
> 像眼泪依赖着脸庞 
> 你就像天使一样 
> 给我依赖 给我力量 

每句歌词的行尾空两格之后，效果是这样的：
 
> 五月天《天使》 
>  
> 像孩子依赖着肩膀  
> 像眼泪依赖着脸庞  
> 你就像天使一样  
> 给我依赖 给我力量   

如果是想嵌套引用，像这样：

> 浙江  
>> 杭州  
>>> 西湖  
>>>> 湖心亭  

语法如下，每行多添加一个「>」符号，再输入文字内容即可（每行行尾记得添两个空格符）：

    > 浙江
    >> 杭州
    >>> 西湖
    >>>> 湖心亭


## 代码区

也就是 Blockquotes。

如果行尾不空格呢有没其它解决方法呢？如果是这样——
 
    风吹柳絮
    
    《麦兜当当伴我心》插曲

    风吹柳絮 茫茫难聚  
    随着风吹 飘来飘去  
    我若能够携你随风去  

    我愿像一块扣肉  
    我愿像一块扣肉  
    我愿像一块扣肉  
    扣住你梅菜扣住你手  

    我愿像一块扣肉  
    我愿像一块扣肉  
    我是你一块扣肉  
    你是那梅菜扣住你手  

这里的方法是首行开头缩进四个空格符，或敲一下 tab 键（制表符键）。

还有一个方法。连续三个反引号「`」组成的前后两行，将内容包裹起来。


显示效果如下：

```
这是另一个代码区块
```

在代码区块中，Markdown 语法不会被转换，这也是为什么前面很多 Markdown 语法的例子能在代码区展示出来的缘故。不然这样一篇以 Markdown 语法解释 Markdown 语法的说明也无从谈起了。

嗯...嗯？

反引号的输入：英文输入模式下，点击键盘左上角的「~」键。


## 标记

标记小段代码（文字）。为着重强调的内容添加深色背景框，在内容前后各添一个反引号「`」，将代码段或文字夹在中间即可实现。

显示效果如下：

1. Use the `printf()` function.
2. 这是加深背景色框的`字符`。

*** 

## 网址链接

### 自动链接

使用「<」、「>」这样的尖角符号，url/email 在 Markdown 下可自动实现可点击链接的效果。

    <http://www.google.com>

显示效果如下：

<http://www.google.com>

### 网址链接

至于网址链接的基本格式，应该是这样：

    [Link Name](Link) 

构成为：

* 一个方括号，添加图片的描述文字
* 一个括号，添加图片网址

以下为一个网址的栗子：

    [Welcome to my blog](https://s-h-y-github.github.io/)

显示效果如下：

[Welcome to my blog](https://s-h-y-github.github.io/)

### 索引链接

内容描述后添加定义链接（以数字/英文/符号为主），在文字段落外关联具体网址，实现可跳转效果。

    [Click Google Search][Tags]

    [Tags]: http://www.google.com "Google"

显示效果如下：

[Click Google Search][Tags]

[Tags]: http://www.google.com "Google"

## 添加图片

插入图片的语法：

    ![Pic name](Pic link)  
    ![Instagram Pic](http://i.imgur.com/UKhrRrK.jpg)

* 一个英文输入下的惊叹号「!」；
* 一个方括号，添加图片的描述文字；
* 一个括号，添加图片网址。

相比插入网址链接，多了一个开头的惊叹号。

显示效果如下：

![Instagram Pic](http://i.imgur.com/UKhrRrK.jpg)

## 添加表格

	|Title |Title 1|Title 2|Title 3|
	|---|---:|:---:|---:|
	| A|B|C|D|

显示效果如下：

|Province | ZJ 浙江省 | FJ 福建省 | YN 云南省 |
|---|:-----|:-----:|-----:|
|省会|杭州|厦门|昆明|

一般的表格由「|」与「-」两种符号（英文半角字符）构成。第一、三及其后的行都由「|」组成。依数据的列数确定数量（列数据量 +1）。  
第二行为中间为连续的「-」组成的隔断，数量不限，更多是让文本显得美观（和预览无关）。

第二行中出现的冒号作用是设定表格内数据的对齐方式，不是必须使用的。具体意义如下：

1. `:–--` 冒号在左，左对齐
2. `--–：` 冒号在右，右对齐
3. `：--–：` 左右两侧都出现冒号，居中对齐

## 转义符

如何在 MD 文档中输出被用于转换格式的符号本身？这里就需要转义符，也就是反斜线「\」来协助。

如果要显示「*」，则可以用如下的方式：

	表示强调的符号这样用： \*Emphasize\*

显示效果如下：

表示强调的符号这样用： \*Emphasize\*

支持转义的 MD 符号包括：

    \   反斜线
    `   反引号
    \*   星号
    \_   下划线
    {}  花括号
    []  方括号
    ()  圆括号
    #   井号
    +   加号
    -   减号（连字符）
    .   句点
    !   感叹号

*** 
## 扩展阅读

基于 Markdown 的 HTML 语言运用。

HTML 可以契合 MD 语法，而通过利用前者，可以实现一些单纯依靠 MD 语法暂时无法实现的功能和页面显示效果。

### 网址链接

页面内跳转链接。利用 HTML <img> 语法制作 Markdown 长文的可跳转目录。分两部分，前为具体条目信息，后边则指向内容的位置（代码段放在页面的哪里，点击索引条目后就跳转到哪里）。

范例语法如下：

    [Line](#A)

	<a name="A"></a>

[Line](#A)

<a name="A"></a>


## 参考文档及扩展阅读

1. [献给写作者的 Markdown 新手指南_简书](http://www.jianshu.com/p/q81RER)  
2. [Markdown 语法说明_WowUbuntu](http://wowubuntu.com/markdown/#editor)  
3. [Markdown 语法说明（详解版）_图灵社区](http://www.ituring.com.cn/article/504)  
4. [Mastering Markdown · GitHub Guides](https://guides.github.com/features/mastering-markdown/)
5. [Markdown - Wikiwand](https://www.wikiwand.com/zh/Markdown)
6. [Markdown 写作浅谈 - 阳志平的网志](http://www.yangzhiping.com/tech/r-markdown-knitr.html)
7. [Markdown语法进阶指南](https://michelf.ca/projects/php-markdown/extra/#fenced-code-blocks)
8. [Markdown语法官方说明](http://daringfireball.net/projects/markdown/syntax)
9. [Github版Markdown说明](https://help.github.com/categories/writing-on-github/)