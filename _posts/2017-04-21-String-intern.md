---
layout: post
title:  "String的intern方法"
date:   2017-04-21 10:47:04 +0800
categories: JavaSE
---

### 1. 介绍
String对象的intern方法会得到字符串对象在常量池中对应的版本的引用（如果常量池中有一个字符串与String对象的equals结果是true），如果常量池中没有对应的字符串，则该字符串将被添加到常量池中，然后返回常量池中字符串的引用。

intern译为“扣留”，简单点说，就是将一个运行时创建的字符串（在堆中保存）扣留在常量区。

### 2. 实例
（说明：以下实例均采用jdk7进行编译运行）  

*样例如下：*

{% highlight java linenos %}
String a = "a";
String b = "b";
String ab = (a + b).intern();
System.out.println("ab" == ab);

String c = "c";
String d = "d";
String cd = c + d;
System.out.println("cd" == cd);
{% endhighlight %}

第一个`"ab" == ab`返回为true，虽然a+b在编译时转化为了StringBuilder执行，但调用intern()将会现在常量池中查找"ab"，没有则将新创建的字符串对象放入，有的话就返回常量池中"ab"的引用。而第二个`"cd" == cd`则直接比较两个不同的引用（"cd"在常量池中，而cd在堆中），所以结果为false。


*再来看一个经典的题目：*

{% highlight java linenos %}
String s1 = "Programming"; // 编译时放在静态区
String s2 = new String("Programming"); // 运行时放在堆中
String s3 = "Program"; // 静态区
String s4 = "ming"; // 静态区
String s5 = "Program" + "ming"; // 编译时直接拼接，恰巧为静态区的"Programming"
String s6 = s3 + s4; // 运行时调用StringBuilder拼接 new StringBuilder(s3).append(s4).toString();

System.out.println(s1 == s2); // false s1和s2的引用没有指向同一个地方
System.out.println(s1 == s5); // true s1和s5同指向静态区中的"Programming"
System.out.println(s1 == s6); // false s1和s6指向不同的位置
System.out.println(s2 == s6); // false s2和s6同在堆中，但产生方式不同，引用不同
System.out.println(s1 == s6.intern()); // true s1在编译期间放入常量池，s6通过intern方法可以获取到。
System.out.println(s2 == s2.intern()); // false s2.intern()为s1，与s2不等
{% endhighlight %}

### 3. 功能
调用intern方法会将字符串交由常量池统一管理，在某一个字符串频繁出现的时候，intern可以节约省内存，提高系统运行效率。
