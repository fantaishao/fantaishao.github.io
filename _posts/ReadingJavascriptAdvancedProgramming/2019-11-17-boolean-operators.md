---
layout: post
#标题配置
title:  JavaScript逻辑运算符
#时间配置
date:   2019-11-17
#大类配置
categories: JavaScript
#小类配置
tag: JavaScript
---

* content
{:toc}


1. **逻辑与**
	
```
var a = 1;
var b = 2;

a===1 && b === 2
```

短路写法，即如果第一个操作数能够决定结果，那么就不会对第二个操作数求值。
* 前面是一个判断，后面是一个表达式

逻辑与不一定返回布尔值。此时，它遵循以下规则
* 如果第一个操作数是对象，则返回第二个操作数

![/styles/images/8.png]({{ '/styles/images/17.png' | prepend: site.baseurl  }})

* 如果第二个操作数是对象，则只有第一个操作数的求值结果为true的情况下才返回该对象

![/styles/images/8.png]({{ '/styles/images/18.png' | prepend: site.baseurl  }})

* 如果两个操作数都是对象，则返回第二个操作数

![/styles/images/8.png]({{ '/styles/images/19.png' | prepend: site.baseurl  }})

* 如果第一个操作数是null， 则返回null
* 如果第一个操作数是NaN， 则返回NaN
* 如果第一个操作数是undefined，则返回undefined

![/styles/images/8.png]({{ '/styles/images/20.png' | prepend: site.baseurl  }})


2. **逻辑或**

```
var a = 1
var b = 2
a == 2 || b == 2
```
逻辑或不一定返回布尔值。此时，它遵循以下规则
* 如果第一个操作数是对象，则返回第一个操作数
* 如果第一个操作数的求值结果是false， 则返回第二个操作数
* 如果两个操作数都是对象，则返回第一个操作数
* 如果两个操作数都是null， 则返回null
* 如果两个操作数都是NaN,则返回NaN
* 如果两个操作数都是undefined，则返回undefined
逻辑或与逻辑与都是短路操作，如果两个写在一起会发生什么呢？

```
a && b || c
上面这个相当于三目运算符 a?b:c
```

那么问题来了
* 如果逻辑与中，第一个是false，第二个操作数还会计算么
答案是不会计算的。
只有在逻辑非中，如果第一个是false，它会继续计算第二个，如果第一个是true， 后面的不会计算

