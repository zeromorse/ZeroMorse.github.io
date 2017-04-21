---
layout: post
title:  "Java中assert的使用"
date:   2017-04-20 22:40:03 +0800
categories: JavaSE
---

### 1. 简介

编写代码时，我们总是会做出一些假设，断言就是用于在代码中捕捉这些假设，可以将断言看作是异常处理的一种高级形式。在Java中通过`assert`关键字来实现。

### 2. 基本语法
> assert expression1;  
> assert expression1: expression2;

*解释：*  
 **experssion1** 为要检查的布尔表达式，如果表达式的结果为`true`，则说明假设为真，则程序继续向下执行；如果表达式的值为`false`，系统会抛出`java.lang.AssertionError`异常并退出程序，若 **expression2** 存在，则还会将expression2作为异常的附加信息输出。

### 3. 使用方法
一般来说，`assert`用于保证程序最基本、关键的正确性。`assert`检查通常在开发和测试时开启。为了提高性能，在软件发布后，`assert`检查通常是关闭的，所以需要设置VM参数 `-ea`（应该是 enable assert的缩写）开启断言功能。然后编译运行含有断言的代码即可。

### 4. 样例
Java代码：

{% highlight java linenos %}
public class Main {
    public static void main(String[] args) {
        assert 1 == 2 : "hello assert";
    }
}
{% endhighlight %}

输出结果：
> Exception in thread "main" java.lang.AssertionError: hello assert  
	at Main.main(Main.java:3)

### 5. 参考文章
1. [java assert的用法简介](http://www.cnblogs.com/wardensky/p/4307848.html)
2. [百度百科-assert](http://baike.baidu.com/link?url=FzaLXQY2AhC4gPLmuqC94JQcdDq1vxGZV9oH1oqmRs-CzZVe5OwNqfsNGvODfMWiPR5wsV70ZUbgSNj-h-GNUK)
