---
layout:     post
title:      "几个Struts2有用的插件"
subtitle:   "Struts2 plugins"
date:       2016/12/16
author:     "率怀一"
header-img: "img/in-post/2016-11-07-struts2-summary/post-bg.jpg"
catalog: true
tags:
    - Java
    - web开发
    - 学习笔记
    - Struts2
---

## 前言 ##

最近几天为了完成软工项目，一直都没有更新博客。现在项目终于成功验收，我也有时间来写几篇日志了。首先介绍一下项目开发过程中发现的几个好用的struts插件——JSON插件，JQuery插件和Bootstrap插件。

## struts的核心库文件 ##

在介绍这些插件之前，首先介绍一下struts的几个核心库文件，防止出现无法使用的问题。这些文件基本是使用struts框架所必须的，一般都会拷贝。

本文基于Struts2.3版本，版本变更之后可能出现不同之处，恕不一一列明。

![库文件](\img\in-post\2016-12-16-struts-plugins\libs.jpg)

## JSON插件 ##

#### 安装 ####

Struts JSON插件是Struts官方维护的插件，在你下载的Struts完整压缩包的lib目录下可以找到一个名为
`struts2-json-plugin-2.3.31.jar`的文件，如果你已经拷贝了上文所述的核心库文件，那么只需将这个文件放入你项目的构建库中即可。注意版本的一致，如果你使用的是2.5版本的Struts，那么请使用2.5版本的插件。

除此之外，对于使用IntelliJ IDEA的用户，使用这个插件之前必须将插件jar包根目录下的`struts-plugin.xml`加入项目的Project Structure->Facets->Struts2的file set中，对于Eclipse这一步是否需要我也不是很清楚。

![idea配置](\img\in-post\2016-12-16-struts-plugins\QQ截图20161216211536.jpg)

#### 使用 ####

这个插件使用起来十分简单，在`struts.xml`中，令包含需要返回JSON结果的Action的package的`extends`属性为`"json-default"`，然后将Action的结果类型定为`"json"`即可。这时访问这个Action，如果一切正常，服务器应当返回一个JSON对象，其中包含了Action中所有可读属性。

如果想要对返回的JSON对象进行更细节的控制，可以通过参数来解决。详情请参阅官方文档：[https://struts.apache.org/docs/json-plugin.html](https://struts.apache.org/docs/json-plugin.html)

## JQuery插件 ##

这个插件提供了一个taglib，可以用于处理JQuery的一些使用场景，可以大大减少前端工程师的代码工作量。例如，使用`<sj:head>`标签可以直接引入JQuery和JQuery UI，`<sj:a>`可以直接生产ajax代码等等。

不过学会了JQuery的语法到哪都能用，学会了这个插件只有struts项目能用，读者可以自行权衡是否投入精力去学习。

插件的官方网站：[https://github.com/struts-community-plugins/struts2-jquery](https://github.com/struts-community-plugins/struts2-jquery)，下载和详细的文档都可以在这里找到。

## Bootstrap插件 ##

与JQuery插件插件类似，`<sb:head>`可以引入bootstrap的css和js文件，这个插件还提供了bootstrap的主题，可以作为struts主题使用。

项目主页：[https://github.com/struts-community-plugins/struts2-bootstrap](https://github.com/struts-community-plugins/struts2-bootstrap)