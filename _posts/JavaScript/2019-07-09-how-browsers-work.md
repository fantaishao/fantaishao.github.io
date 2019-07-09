---
layout: post
#标题配置
title:  how browsers work
#时间配置
date:   2019-07-07 9:00 am
#大类配置
categories: front-end
#小类配置
tag: JavaScript
---

* content
{:toc}


#### 在讨论浏览器如何工作之前，我们先来了解下浏览器的结构
##### 浏览器的主要组件分为以下几个
	1. 用户界面
	包括地址栏，前进后退按钮，书签菜单等。除了浏览器的主窗口显示的您请求的页面外，其他显示的各个部分都属于用户界面
	2. 浏览器引擎
	在用户界面和渲染引擎之间传送指令
	3. 渲染引擎
	对请求的内容作出响应。比如，用户请求的内容是html，渲染引擎会去解析html和css，然后将解析好的内容呈现在屏幕上
	4. 网络
	网络请求，比如http请求，其接口与平台无关，并为所有平台提供底层实现
	5. 用户界面后端
	用于绘制基本的窗口小部件，比如组合框和窗口。其公开了与平台无关的通用接口，而在底层使用操作系统的用户界面方法
	6. JavaScript解释器
	用于解释和执行JavaScript代码
	7. 数据存储
	这是持久层。浏览器需要在硬盘上保存各种数据，例如cookie。新的html规范（html5）定义了‘网络数据库’，这是一个完整且轻便的浏览器内数据库。
	
	浏览器的主要组件组成			{#browser-main-components}
---------------------

![/styles/images/browser-main-components.jpg]({{ '/styles/images/browser-main-components.jpg' | prepend: site.baseurl  }})



#### 渲染引擎渲染基本流程
1. 渲染引擎先将html文档解析成dom节点，组织成dom树；然后解析样式文件。html中这些带有视觉指令的样式信息将用于创建另一个树结构，渲染树。
渲染树包含多个带有视觉属性（如颜色和尺寸）的矩形。这些矩形的排列顺序就是他们将在屏幕上显示的顺序



#### 浏览器渲染基本流程(webkit)			{#render-engine-basic-flow}
---------------------

![/styles/images/render-engine-basic-flow.jpg]({{ '/styles/images/render-engine-basic-flow.jpg' | prepend: site.baseurl  }})

#### WebKit主流程		{#main-flow}
---------------------

![/styles/images/how-browsers-work.png]({{ '/styles/images/how-browsers-work.png' | prepend: site.baseurl  }})
