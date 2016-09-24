---
layout:     post
title:      "Java中有趣的相等"
subtitle:   "==,equals(),and contains() in Java"
date:       2016/9/24 14:46:12 
author:     "率怀一"
header-img: "img/in-post/2016-09-24-Java-equal/post-bg.jpg"
catalog: true
tags:
    - Java
    - 学习笔记
---

# 前言 #

最近为了完成项目，疯狂自学Java。其实有了C++做基础，学Java并不算非常困难。然而Java中一个非常令人不适应的地方就是Java没有指针。一个没有指针的语言，很多数据结构都难以实现，自然是算不上一个成熟的语言的。Java中自然有代替指针的玩意——引用。就我对引用的浅显理解，似乎所有对象的变量名在Java中都代表的是这一对象在内存中的地址，也就等效于C++中的指针。而这一点正好在Java中判断两个对象相等时，会产生很有趣的效果。

# ==与equals() #

众所周知，字符串不管在C++还是在Java中都是一个类。在C++中，关系运算符`==`可以被很好的执行，如图所示：

![C++==test](/img/in-post/2016-09-24-Java-equal/C++==test.png)

然而同样的代码到了Java就会出现玄学现象：

![Java==test](/img/in-post/2016-09-24-Java-equal/Java==test.png)

这是为什么呢？难道说Java出bug了吗？这当然不可能了。让我们仔细分析一下这些代码。测试用的两个代码首先都新建了两个内容为`"123"`的字符串对象，然后将这两个对象用`==`进行比较，相同则输出`1`或`true`，不同则输出`0`或`false`。在C++环境下，二者比对的结果是相等；而在Java环境下，二者比对的结果是不相等。这个结果令人十分诧异，都是`"123"`，为什么Java会认为两者不相等呢？原因就在于Java中对对象用`==`进行对比时，进行的操作实际上是对两个对象的地址进行对比，即判断这两个对象是不是同一个对象。在我们的代码中对象`a`与对象`b`很明显不是同一个对象，所以耿直的Java就会返回false。

实际上在C++中对象的标识符代表的也是这个对象的地址，只不过C++对针对对象的运算符进行了严谨的重载。在对两个对象进行`==`运算时，C++会调用库中的函数，对二者的值进行比较。然而不知道为什么，Java却不会这么做，因此我们在编写Java程序时一定要注意这一点，否则就有很高可能发生语义错误。

那么我们在处理值相等时改怎么做呢？答案是使用自带的或自己编写的`equals()`方法。如图所示

![Javaequalstest](/img/in-post/2016-09-24-Java-equal/Javaequalstest.png)

# contains() #

知道了上面所说的现象之后，我们不妨深入的想一下。我们都知道Java中的集合有`contains()`方法，映射有`containsKey()`和`containsValue()`方法。那么当这些高级数据结构中的元素是对象的时候，这些方法能不能正常工作呢？让我们测试一下。

![Javacontainstest](/img/in-post/2016-09-24-Java-equal/Javacontainstest.png)

好吧，看来至少对于String类来讲，`contains()`方法还是没有任何问题的。那么对于自定义类是不是这样呢？

![Javacontainstest2](/img/in-post/2016-09-24-Java-equal/Javacontainstest2.png)

结果返回了false。
。
。
。
这就很尴尬了，为什么会这样呢？原因在Java源码中可以找到。

```java
public boolean contains(Object o) {
        return map.containsKey(o);
    }
public boolean containsKey(Object key) {
        return getNode(hash(key), key) != null;
    }
static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
final Node<K,V> getNode(int hash, Object key) {
        Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
        if ((tab = table) != null && (n = tab.length) > 0 &&
            (first = tab[(n - 1) & hash]) != null) {
            if (first.hash == hash && // always check first node
                ((k = first.key) == key || (key != null && key.equals(k))))
                return first;
            if ((e = first.next) != null) {
                if (first instanceof TreeNode)
                    return ((TreeNode<K,V>)first).getTreeNode(hash, key);
                do {
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        return e;
                } while ((e = e.next) != null);
            }
        }
        return null;
    }
```

`contains()`对元素的判断基于元素的`hashcode()`和`equals()`两个方法，如果要对自定义类进行`contains()`操作，必须先将这两个方法定义。总而言之不建议对自定义类使用`contains()`就是了。

# 附录：源代码 #

#### C++运算符测试 ####

```C++
#include <iostream>
using namespace std;

int main()
{
	string a("123");
	string b("123");
   	cout << (a==b);
   	return 0;
}
```

#### Java运算符测试 ####

```Java
public class HelloWorld {
    public static void main(String []args) {
		String a = new String("123");
		String b = new String("123");
       	System.out.println(a==b);
    }
}
```

#### Java equals()测试 ####

```Java
public class HelloWorld {
    public static void main(String []args) {
		String a = new String("123");
		String b = new String("123");
       	System.out.println(a.equals(b));
    }
}
```
#### Java contains()测试 ####

```Java
import java.util.HashSet;
public class HelloWorld {
    public static void main(String []args) {
		
		String a = new String("123");
		String b = new String("123");
		HashSet <String> c = new HashSet <String>();
		c.add(a);
       	System.out.println(c.contains(b));
    }
}
```

#### Java 自定义类contains()测试 ####

```java
package HelloWorld;
import java.util.HashSet;
public class HelloWorld {
	static class Name {  
    	String first;   
    	String last;   
    	Name(String first, String last) {   
        	this.first = first;   
        	this.last = last;   
    	}
	}
    public static void main(String []args) {
		Name a = new Name("123","456");
		Name b = new Name("123","456");
		HashSet <Name> c = new HashSet <Name>();
		c.add(a);
       	System.out.println(c.contains(b));
    }
}
```