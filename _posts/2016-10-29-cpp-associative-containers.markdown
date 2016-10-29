---
layout:     post
title:      "C++ STL容器在面向对象编程时的用法"
subtitle:   "C++ STL Associative containers/Unordered associative containers"
date:       2016/10/29 20:04:27 
author:     "率怀一"
header-img: "img/in-post/2016-10-29-cpp-associative-containers/post-bg.jpg"
catalog: true
tags:
    - C/C++
    - 面向对象
    - 学习笔记
---

## 前言 ##

作为最接近硬件底层的编程语言，C一直以其它高级语言难以望其项背的执行速度闻名于世。然而正因为C偏向底层的的特点，我们在使用它的时候会有很多不方便之处，比如不支持面向对象，复杂的数据结构全部需要自行编写等等，使编程工作者不得不把大把的时间放在基础语言的完善上。所幸后来有了C++，支持面向对象、函数重载等诸多高级特性，还有官方自带的STL库，实现了动态数组、链表、集合、映射等多种数据结构和很多常用算法，大大方便了程序员的使用。不过C++终究还是针对C的拓展，设计重点依然是运行效率，它的STL容器很多时候并不能像其他语言中的数据结构一样直接使用，初学者很容易在使用的时候出现问题。

本文以分别以`set`和`unordered_set`为例，分别介绍C++ STL容器库中的关联容器和无序关联容器在一个较复杂的应用场景下（使用这些容器保存自定义类实例）的使用方法。

## 关联容器 ##

C++ STL中定义的关联容器有`set`, `map`, `multiset`, `multimap` 四种。它们都通过二叉搜索树（及其变型）实现，因此用法也都大同小异。这里仅仅说明`set`在保存自定义类的实例时的用法。

让我们写一个很简单的`Student`类

```c++
class Student
{
public:
	int stuID;
};
```

然后将它的实例插入`set`中

```c++
#include <set>

using namespace std;

class Student
{
public:
	int stuID;
};

int main()
{
	Student st;
	set<Student> s;
	for (int i = 0; i < 10; i++)
	{
		st.stuID = i;
		s.insert(st);
	}
	return 0;
}
```

我们都知道`set`的`insert`方法插入的是值，每次执行`s.insert(st);`语句时都会插入一个`Student`类的新实例。这个类非常的简单，也不会有浅拷贝问题。这个代码看似毫无问题，然而实际执行时却会发现，这个代码根本无法编译，会有报错：`error C2676: 二进制“<”:“const Student”不定义该运算符或到预定义运算符可接收的类型的转换`。这是为什么呢？

如前文所言，C++ STL容器库中的关联容器本质上是以二叉搜索树保存的。通过不同方法实现的二叉搜索树的构造过程虽然各有不同，但一个共性的地方是确定的，那就是**构造过程中必然会有比较**。那么问题来了，对于这个`Student`类，C++应该如何比较大小呢？

答案是C++自己不知道应该怎样比较大小，我们必须为自己定义的类重载一个`operator <`方法，然后C++才能根据这个方法构造二叉搜索树。就像这样：

```c++
class Student
{
public:
	int stuID;
	bool operator < (const Student &c) const
	{
		return stuID < c.stuID;
	}
};
```

当把Student类改成这样之后，程序就可以正常编译运行了。

需要注意的是：我们只需要重载一个`operator <`方法，C++就可以完成二叉树的构造，而不必重载`operator ==`，因为C++ STL库中的关联容器会只使用`<`来判定两个元素是否相等。**假如两个元素a和b满足`!(a < b) && !(b < a)`，则将这两个元素判断为相同**。这就使得我们的`operator <`方法并不能随便定义。在上面的例子中`operator <`方法定义成这样没有任何问题，但是在对复杂的类进行`operator <`的定义的时候可能非常困难，甚至根本不能实现。读者可以自己思考一下，如果在`Student`类中新增一个`string name`成员，那么`operator <`方法如何实现才能满足条件？在这个时候我们要么自己实现一个直接通过`==`判断相等的关联容器，要么使用下面要介绍的无序关联容器。

## 无序关联容器 ##

与关联容器对应，C++ STL容器库中定义的无序关联容器有`unordered_set`, `unordered_map`, `unordered_multiset`, `unordered_multimap`四种。它们都使用哈希法实现，比起关联容器，它们遍历时的效率较低，但是基于主键查找时的效率较高。

我们同样使用Student类，对`unordered_set`进行测试：

```c++
#include <unordered_set>

using namespace std;

class Student
{
public:
	int stuID;
};

int main()
{
	Student st;
	unordered_set<Student> s;
	for (int i = 0; i < 10; i++)
	{
		st.stuID = i;
		s.insert(st);
	}
	return 0;
}
```

如果你看懂了前面一部分，那么估计你已经猜到了我想要说什么。实现哈希查找需要hash值，得到hash值需要hash函数。hash值相等两个元素并不一定相同，所以还需要`operator ==`方法。按照C++的尿性，它多半不会提供这些函数。事实正是如此，上面的代码在编译时会出错。

那么我们只要提供hash函数和`operator ==`方法就好啦，这次并没有跟关联容器一样弱智的相等判断机制挡在我们面前。

什么？你问我怎样为自定义类提供hash方法？看这里→[http://en.cppreference.com/w/cpp/utility/hash](http://en.cppreference.com/w/cpp/utility/hash "std::hash")

## 参考阅读 ##

1. [C++ 标准文档](http://www.open-std.org/jtc1/sc22/wg21/)
2. http://en.cppreference.com/
3. http://www.cplusplus.com/