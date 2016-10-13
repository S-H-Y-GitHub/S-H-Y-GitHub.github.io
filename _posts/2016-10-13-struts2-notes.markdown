---
layout:     post
title:      "Struts2学习笔记"
subtitle:   "Struts2 notes"
date:       2016/10/13
author:     "率怀一"
header-img: "img/in-post/2016-10-13-struts2-notes/post-bg.png"
catalog: true
tags:
    - Struts2
    - 学习笔记
---

## 前言 ##

最近用Struts2完成了一个项目，工作量还算挺大的。在这里把一些值得记录的东西记下来。

## 安装 ##

安装方面比较简单，将Struts2的库放入项目的构建路径中，然后在你项目的`web.xml`中规定正确的filter即可。经过博主验证，官网下载的最新的Struts2.5版本很容易产生一些玄学错误，这里建议使用2.3版本。

#### 2.3版本 ####

必须的jar资源包：

```
asm.jar
asm-commons.jar
asm-tree.jar
commons-fileupload.jar
commons-io.jar
commons-lang.jar
freemarker.jar
javassist.jar
ognl.jar
struts2-core.jar
xwork-core.jar
```

web.xml配置：

```xml
<filter>
	<filter-name>struts2</filter-name>
	<filter-class>org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter</filter-class>
</filter>
<filter-mapping>
	<filter-name>struts2</filter-name>
	<url-pattern>/*</url-pattern>
</filter-mapping>
```

#### 2.5版本 ####

> 2.5不是我做项目时主要使用的版本，下面的内容可能有不准确之处，欢迎在评论中指出。

必须的jar资源包：

```
asm-3.3.jar
asm-commons-3.3.jar
asm-tree-3.3.jar
commons-fileupload-1.3.2.jar
commons-io-2.4.jar
commons-lang3-3.4.jar
commons-logging-1.1.3.jar
freemarker-2.3.23.jar
javassist-3.20.0-GA.jar
log4j-api-2.5.jar
ognl-3.1.10.jar
struts2-core-2.5.2.jar
```

web.xml配置：

```xml
<filter>
	<filter-name>struts-prepare</filter-name>
	<filter-class>org.apache.struts2.dispatcher.filter.StrutsPrepareFilter</filter-class>
</filter>
<filter>
	<filter-name>struts-execute</filter-name>
	<filter-class>org.apache.struts2.dispatcher.filter.StrutsExecuteFilter</filter-class>
</filter>
<filter-mapping>
	<filter-name>struts-prepare</filter-name>
	<url-pattern>/*</url-pattern>
</filter-mapping>
<filter-mapping>
	<filter-name>struts-execute</filter-name>
	<url-pattern>/*</url-pattern>
</filter-mapping>
```

也有说将prepare和execute合并的写法，我没有测试过，并不清楚效果如何。

```xml
<filter>
	<filter-name>struts2</filter-name>
	<filter-class>org.apache.struts2.dispatcher.filter.StrutsPrepareAndExecuteFilter</filter-class>
</filter>
<filter-mapping>
	<filter-name>struts2</filter-name>
	<url-pattern>/*</url-pattern>
</filter-mapping>
```

## 标签 ##

标签是Struts框架的重要组成。要使用标签，首先必须在JSP文件的头部引入标签库

```jsp
<%@taglib prefix="s" uri="/struts-tags" %>
```

然后就可以使用Struts2标签的强大功能了。详细信息请参阅<a href = "#ref">参考文档</a>一节。

## OGNL ##

> 对象导航图语言（Object Graph Navigation Language），简称OGNL，是应用于Java中的一个开源的表达式语言（Expression Language），它被集成在Struts2等框架中，作用是对数据进行访问，它拥有类型转换、访问对象方法、操作集合对象等功能。   
> <div class = 'text-right'>——[维基百科](https://zh.wikipedia.org/wiki/%E5%AF%B9%E8%B1%A1%E5%AF%BC%E8%88%AA%E5%9B%BE%E8%AF%AD%E8%A8%80) </div>

在使用Struts时，想要使用一些比较高级的功能，OGNL是必不可少的。详细信息请参阅<a href = "#ref">参考文档</a>一节。

<div id = "ref"></div>

## 参考文档及扩展阅读 ##

1. [Struts2官网](http://struts.apache.org/)
2. [Struts2官方文档](http://struts.apache.org/docs/home.html)
3. [OGNL官网](https://commons.apache.org/proper/commons-ognl/)
4. [OGNL语言介绍](https://commons.apache.org/proper/commons-ognl/language-guide.html)
5. [Struts2Eclipse项目开发中文指导（较简略）](http://www.blogjava.net/max/category/16130.html)