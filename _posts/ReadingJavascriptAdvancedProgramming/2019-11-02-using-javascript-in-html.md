---
layout: post
#标题配置
title:  在html中使用JavaScript
#时间配置
date:   2019-11-02
#大类配置
categories: JavaScript
#小类配置
tag: JavaScript
---

* content
{:toc}



#### 本章内容
1. 使用\<script\>标签
2. 外部脚本和内部脚本
3. 文档模式对JavaScript的影响
	


#### 1. 使用\<script\>标签
向html中插入JavaScript的主要方法，就是使用\<script\>标签。

Html4.01为\<script\>定义了6个属性

这里用了一个词主要方法，还可以直接将JavaScript代码直接放在元素内部即可。

* async：可选。异步下载，表示应该立即下载脚本，但不应该妨碍页面中的其他操作。只对外部脚本有效。
计算中的同步和异步，与现实世界中是相反的。
计算机中同步代表事情一件一件执行，异步是代表同时执行。
* charset：可选。表示通过src属性置顶的代码的字符集。由于大多数浏览器会忽略它的值，因此这个属性很少有人使用。
使用场景：
出现乱码，比方说有中文，其他国家的语言，可能会用的上。但是用的也特别少。
* defer：可选。延迟执行。表示脚本可以延迟到文档完全被解析和现实之后执行。只对外部文件有效。
* language：已废弃。原来用于表示编写代码使用的脚本语言（如JavaScript，JavaScript1.2，VBScript）。大多数浏览器会忽略这个属性。
* src： 可选。表示要执行代码的外部文件。
src属性还可以引用来自外部域的JavaScript标签

```
 <script src="http://www.baidu.com/home.js"></script>
```

这个特点让它很强大，也不安全，如果引用的js包含恶意代码就很危险。所以引用外部域的代码可以选择你是作者，或者大公司的
* type：可选。可以看成是language的代替属性。表示编写代码使用的脚本语言的内容类型（也称为MIME类型 multipurpose internet mail extensions）。我们平常使用比较多的是text/javascript。实际上，服务器上传送JavaScript文件时使用的MIME类型通常是，application/x-javascript,但是在type中设置这个值，可能会导致脚本被忽略。
	
按照惯例，外部的JavaScript文件带有.js扩展名，但是这个扩展名不是必须的，因为浏览器不会检查包含JavaScript的文件的扩展名。这样一来，使用jsp，php或其他服务器端语言动态生成JavaScript代码也就成为了可能。但是，服务器通常还是需要看扩展名决定为响应那种mime类型。如果不使用.js扩展名，请确保服务器能返回正确的MIME类型。

```
<script>
   function sayScript() {
       alert("<\/script>");
   }
</script>
```

包含在\<script\>元素内部的JavaScript代码将被从上到下依次解释。
这个解释两个字有坑，在开发或者面试中都可能碰到。
这里的解释虽然只有一个词，但是它是分为两个过程的，预处理和执行。
预处理完了才开始执行，这两个过程组成解释。

就拿上面的例子来讲，解释器会解释一个函数的定义，然后将该定义保存在自己的环境中。在解释器对<script>元素内部的所有代码求值完比以前，页面中的其余内容都不会被浏览器加载或显示。
因为JavaScript是一种阻断式语言，js在运行的过程中，所有其他的事情全部停止。

> 总的来说就是: JavaScript解释的过程是预处理加执行，这个过程是一个阻断式的行为

在使用JavaScript中的时候，不要在代码中使用\</script\>字符串，浏览器会认为那是结束的标签。通过转义字符‘\‘解决这个问题。

在html中使用scrit标签时，要使用结束的\</script\>标签。
在xhmtl中可以使用自闭和标签\</script\>。
但是在html中是不能使用这种语法。因为这种语法不符合html规范，而且也得不到某些浏览器的正确解析，尤其是ie。

```
<script src="../home.js">
   function sayScript() {
       alert("</script>");
   }
</script>
```

> 需要值得注意的是，带有src属性的标签，不应该在\<script\>和\</script\> 之间在包含额外的JavaScript代码。如果有，只会执行外部js，嵌入的代码会被忽略。

#### 1.1.1标签的位置
在平常的正常开发中，会把\<script\>放在body标签的最后面，这样，在解析js代码之前，页面的内容将完全呈现在浏览器中，用户不会觉得页面卡顿。
如果将\<script\>放在<head>标签中，意味着必须等到全部JavaScript代码都被下载、解析、执行完成以后，才能开始呈现页面（浏览器遇到<body>标签才开始呈现内容）。如果一个网站的js比较多，会导致浏览器在呈现页面时出现延迟，用户会看到一片空白。非常影响用户体验。

当然也有情况，js必须放在顶部
1.需要在页面渲染之前执行js，
比方说你用某些库的时候，或者说和css相关的一些js，他会在html的根节点上创建一个class，把浏览器支持和不支持的属性都给列出来。
或者在做移动开发，使用rem单位的时候，需要根据根节点的字体大小来渲染其余内容的字体大小

#### 1.1.2延迟脚本和异步脚步

```
<html lang="en">
    <head>
        <title></title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="css/style.css" rel="stylesheet">
        <script defer="defer" src="main.js"></script>
        <script defer="defer" src="main2.js"></script>
    </head>
    <body>
    </body>
</html>
```

在这个例子中，虽然我们把\<script\>元素放在了<head>元素中，但其中包含的脚本将延迟到浏览器遇到</html>标签后再执行。Html5规范要求脚本按照他们出现的先后顺序执行。因此第一个延迟脚本会先于第二个延迟脚本执行，而这两个脚本会先于DOMContentLoaded事件执行。在现实当中，延迟脚本不一定会按照顺序执行，也不一定会在DOMContentLoaded事件触发前执行，因为最好只包含一个延迟脚本。

```
 <html lang="en">
        <head>
            <title></title>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1">
            <link href="css/style.css" rel="stylesheet">
            <script async src="main.js"></script>
            <script async src="main2.js"></script>
        </head>
        <body>
        </body>
    </html>
```

在上面这个例子中，async与defer不同的是，它并不保证按照指定他们的先后顺序执行。第二个文件有可能比第一个先执行。因此确保两者之间不互相依赖很重要。指定async属性的目的是不让页面等待两个脚本下载和执行，从而异步加载页面其他内容。因为建议异步脚本不要在加载期间修改DOM.
异步脚本一定会在页面的load事件之前执行，但可能会在DOMContentLoaded事件触发之前或者之后执行。
所以以上两种属性尽量少使用。

#### 2. 外部脚本和内部脚本
内部文件性能好，不用产生一次请求。这种性能在手机上特别明显，手机上请求开销比较大。
外部文件可以重复利用，可以缓存，如果有两个页面使用了同一个js，浏览器只会下载一次，可以提高页面加载速度

#### 3. 文档模式对JavaScript的影响
混杂模式(quirks mode)和标准模式(standards mode)。
虽然这两种模式主要影响css内容的呈现，但在某些情况下也会影响到JavaScript的解释执行。


#### 总结
1. \<script\>标签有六个属性，最常用的是src
2. \<script\>使用位置在<body>底部或者放在<head>标签里，因为js是一种阻断式语言，建议放在<body>底部
3. \<script\>有内部文件和外部文件，内部文件性能较好，外部文件可以缓存，容易维护
4. 延迟脚本defer和异步脚本async属性，实际开发中使用比较少

