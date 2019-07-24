---
layout: post
#标题配置
title:  2019-07-15 一周热词第二期
#时间配置
date:   2019-07-15
#大类配置
categories: daily
#小类配置
tag: hot-words
---

* content
{:toc}


#### 一周热词
#### 1. [伪类，伪元素](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Pseudo-classes_and_pseudo-elements)
====================================
    1.1伪类 pseudo class

    添加在选择器后面，以:开始，用于对特别指出的元素应用样式

    比方说，我们经常用的 :hover :first-child :last-child 

    1.2 伪元素 pseudo element

    添加在选择器后面，以::开始，用于在特定的元素后面添加一个元素
    
    比方说，我们经常用的 ::before  ::after

#### 2. Object.freeze
====================================
#### 3. js严格模式与正常模式的区别
====================================
	之前在写angularjs的时候，经常在页面的顶部，显示调用严格模式 use strict;

	严格模式是在ECMAscript5中添加的，顾名思义，就是是的JavaScript再更严格的条件下运行

	设立严格模式主要有以下几个目的

	①消除JavaScript语法的一些不合理，不严谨之处，减少一些怪异行为；

	②消除代码运行的一些不安全之处，保证代码运行的安全

	③提高编译器效率，增加运行速度

	④为未来新版本的JavaScript做好铺垫

	
	现代浏览器都已经支持严格模式，框架中也支持。

    PS：老版本的浏览器会把严格模式的调用当做一行字符串，忽略。
	
	调用严格模式只需要协商“use strict”；即可

	严格模式有两种调用方法，作用范围不同

	①针对整个脚本文件

	在脚本第一行写上“use strict”；，必须写在第一行，否则无效，将以正常模式调用
	``<script>
	"use strict";
	
	// doing something
	function func() {
	    
	}
	</script>``

	在现代开发过程中，线上部署的时候，我们通常将会把所有的js文件合并成一个js，这种写法可能不利于合并，我们可以把整个脚本文件放在一个立即执行的匿名函数中
	``()(function() {
	    "use strict";
	
	// doing something
	})()``

	ps：之前在angularjs中，采用的就是这种写法

	②针对单个函数

	在函数体的第一行写上“use strict”；

	``function func() {
	    use strict”；
	  
	// doing something
	}``

	在具体的代码过程中，究竟有哪些影响呢？

	① 变量必须先显示声明再使用，否则报错

	②静态绑定 

	JavaScript有一个特点就是允许“动态绑定”，即某些属性和方法属于哪一个对象是在运行时确定的，在严格模式下，再编译阶段就确定，这样做有利于编译效率的提高，代码易读。

	具体如下 
    1. 禁止使用with语句
	2. 创设eval作用域  


	③加强了一些安全措施  
    
	1. 禁止this关键字指向全局对象
	2. 禁止在函数内部遍历调用栈

	④禁止删除变量，只有configurable设置为true的对象属性，才能被删除
	``"use strict";
	var x;
	delete x; // 语法错误
	var o = Object.create(null, {'x': {
	value: 1,
	configurable: true
	}});
	delete o.x; // 删除成功``
	
	⑤显示报错
	1. 正常模式下，对一个对象的只读属性赋值，不会报错，会默默地失败。严格模式下，将报错
	2. 严格模式下，对getter方法赋值，会报错
	3. 严格模式下，对禁止扩展的对象添加新属性，会报错
	"use strict";
	var o = {};
	Object.preventExtensions(o);
	o.v = 1; // 报错
	
	4.严格模式下，删除一个不可删除的属性，会报错
	"use strict";
	delete Object.prototype; // 报错
	
	⑥重名错误，函数，变量名，对象属性都不能有重复的，否则会报错
	⑦禁止八进制
	``"use strict";
	var n = 0100; // 语法错误``

	⑧arguments对象的显示

	1. 不允许对arguments赋值
	``"use strict";
	arguments++; // 语法错误``
	
	2. arguments不再追踪参数的变化

	3. 禁止使用arguments.callee
	    ``"use strict";
	    var f = function() { return arguments.callee; };
	    f(); // 报错``
	
	⑨函数必须生命再顶层，不允许在非函数的代码块内生命函数
	``"use strict";
	if () {
	function f() { } // 语法错误
	}
	for () {
	function f2() { } // 语法错误
	}``
	
	⑩添加了一些保留字，
	implements, interface, let, package, private, protected, public, static, yield。 

	
	参考文章
	1. http://www.ruanyifeng.com/blog/2013/01/javascript_strict_mode.html
    2. https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode

#### 4. 逻辑运算符 && 和 \|\| 不一定返回布尔值
====================================


##### 相关链接：
[&& 和||不一定返回布尔值](https://tc39.es/ecma262/#prod-LogicalORExpression)
