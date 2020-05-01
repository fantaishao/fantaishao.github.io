layout: post
#标题配置
title:  JavaScript中的事件
#时间配置
date:   2020-05-01
#大类配置
categories: JavaScript
#小类配置
tag: JavaScript基础知识整理



##### 事件的基本概念

事件就是用户或浏览器自身执行的某种动作。

事件对象，比方说你说表点击的事件包含的信息

事件流：描述页面接收事件的顺序

> 当浏览器发展到第四代时(IE4及Netscape Communicator4)，浏览器开发团队遇到了一个很有意思的问题: 页面的哪一部分会拥有某一个特定的事件?要明白这个问题问的是什么，可以想象画在一张纸上的一组同心圆。如果你把手指放在圆心上，那么你的手指指向的不是一个圆，而是纸上的所有圆。两家浏览器的开发团队在看待浏览器事件方面还是一致的。如果你单击了某个按钮，他们都认为单击事件不仅仅发生在按钮上。换句话说，在单击按钮的同时，你也单击了按钮的容器元素，甚至是整个页面。
>
> 不过他们提出了完全相反的事件流的概念。IE的事件流是事件冒泡流，而Netscape的事件流是事件捕获流

事件冒泡：事件开始时由最具体的元素接收(文档中嵌套层次最深的那个节点)，然后逐级向上传播到较为不具体的节点

事件捕获：不太具体的节点最早接收到事件，而最具体的节点应该最后接收到事件

##### 事件的触发方式

HTML触发

属性触发

事件监听回调

JavaScript事件分为

##### HTML事件

  在html元素中添加事件 

定义方式：on+事件名称

`<button onclick="alert(1)"></button>`

html中直接写元素有三个弊端就是，第一个时间差的问题，我们一般会把js写在页面的最底部，html会首先加载，如果页面出现的时候，用户去点击这个button，html里面对应的处理函数的js还没加载完，就会报错。

当然这里是有处理方法的将它包裹再try...catch语句中，只不过这种用法几乎没人使用

`<button onclick="try{alert(1)}catch(err){}"></button>`

所以后面又有的DOM事件

>  JavaScript中的所有事件只会发生在两个地方，dom元素，ducument对象和window对象上

第二个问题，html事件的作用域是全局，有些事件的定义是有他自己的作用域的。

第三个是代码耦合度的问题，如果页面里面有大量的这样的代码，如果之后需要改动，至少要改动两处，那将会是非常麻烦的。

HTML事件写法，适合小型项目。

##### DOM0事件

这个是通过JavaScript指定事件处理程序的传统方式，将一个函数赋值给一个事件处理程序属性

`var btn = document.getElementById('btn');

​    btn.onclick = function(){}`

使用DOM0级方法指定的事件处理程序被认为是元素的方法。因此，这时候的事件处理程序是在元素的作用域中运行；换句话说，程序中的this引用当前元素。来看一个例子

`var btn = document.getElementById('btn');

​    btn.onclick = function(){

​      console.log(this.id);*// btn*

​    }`

以这种方式添加的事件处理程序会在事件流的冒泡阶段被处理，如果需要删除事件，直接将属性的值设为null即可。

  DOM0如何触发事件呢？

先获取要触发的元素

主要是指鼠标键盘事件

##### DOM2事件

DOM2级的事件流包括三个阶段，事件捕获阶段，处于目标阶段，和事件冒泡阶段

两个事件

addEventListener()

removeEventListener()

这两个事件接受三个参数

* 事件名称(类型)，

* 运行函数，

* 在捕获阶段还是冒泡阶段执行(boolean，true:冒泡阶段，false:捕获阶段，默认false)

  第三个属性也可以是一个对象，它有三个属性，都是boolean类型, 分别是，

  * capture ： true代表捕获，false代表冒泡
  * once： 如果指定true，代表只调用一次
  * passive：设置为true时，表示函数永远不会调用preventDefault().如果listener仍然调用了整函数，客户端将会忽略它并抛出一个控制台警告

  如果你想检测 `passive` 值可以参考下面这个例子：

  ` 

  var passiveSupported = false;

  ​    try {

  ​     var options = Object.defineProperty({}, 'passive', {

  ​       get: function() {

  ​         passiveSupported = true;

  ​       }

  ​     });

  ​     window.addEventListener('test', null, options)

  ​    } catch(err) {}

  `

  

   因为在旧版本的浏览器中，第三个属性仍然是一个布尔值，所以你需要编写一些代码来有效的监测你的浏览  器是否支持对象中的属性

第三个函数可选

`function getData() {

​      *// do something*

​    }

​    window.addEventListener('click', getdata, false);

​    window.removeEventListener('click', getdata, false)`

添加和移出的函数必须是统一函数，所以如果你需要移除绑定的函数，就不能使用匿名函数

`window.addEventListener('click', function(){}, false);`

> 大多数情况都是将事件处理程序添加到事件流的冒泡阶段，这样可以最大限度地兼容各种浏览器。

1. DOM3事件

DOM3里新定义了自定义事件

`function customEvent() {

​      var div = document.getElementById('div');

​      var event = document.createEvent('click', document);

​      div.dispatchEvent(event)

​    }`

目前只有火狐浏览器支持

> 为什么没有DOM1事件？因为DOM1中没有定义事件相关的内容

##### IE事件处理程序

IE实现了与DOM中类似的两个方法，attachEvent和detachEvent。

这两个方法接受相同的两个参数: 事件处理程序名称与事件处理程序函数。由于IE8及更早的版本只支持事件冒泡，所以通过attachEvent()添加的事件处理程序都会被添加到冒泡阶段。

`var btn = document.getElementById('btn');

​    btn.attachEvent('onclick', function(){})`

> 在IE中使用attachEvent()与使用DOM0级方法的主要区别在于事件处理程序的作用域。在使用DOM0级方法的情况下，事件处理程序会在其所属元素的作用域内运行；在使用attachEvent()方法的情况下，事件处理程序会在全局作用域中运行，因此this等于window

与addEventListener()类似，attachEvent()方法也可以用来为一个元素添加多个事件处理程序

`var btn = document.getElementById('btn');

​    btn.attachEvent('onclick', function(){console.log(123)})

​    btn.attachEvent('onclick', function(){console.log(456)})`

与DOM方法不同的是，这些事件处理程序不是按照他们添加的顺序执行的，而是以相反的顺序被触发

##### 事件类型

DOM3级事件类型

* UI事件，当用户与页面的元素交互时触发， load，unload，abort，error，select，resize，scroll

* 焦点事件，当元素获得或失去焦点时触发, blur,DOMFocusIn,DOMFocusOut,focus,focusin,focusout

* 鼠标事件，当用户通过鼠标在页面上执行操作时触发

* 滚轮事件，当使用鼠标滚轮(或类似设备)时触发 鼠标滚轮事件：click,dbclick,mousedown,mouseenter,mouseleave,mousemove,mouseout,mouseover,mouseup

* 文本事件，当在文档中输入文本时触发

* 键盘事件，当用户通过键盘在页面执行操作时触发 键盘文本事件：keydown，keypress，keyup，textInput(DOM3级事件引入)

* 合成事件，当为IME(input method editor,输入法编辑器)输入字符时触发，DOM3新添加的事件

  * compositionstart：在IME的文本复合系统打开时触发，表示要开始输入了。
  * compositionupdate：在向输入字段插入新字符时触发。
  * compositionend: 在IME的文本复合系统关闭时触发，表示返回正常键盘输入状态

  > 合成事件跟文本事件很相似，在触发合成事件时，目标是接收文本的输入字段。但它比文本事件的实践对象多一个属性data

* 变动(mutation)事件，当底层DOM结构发生变化时触发

  DOM2级的变动事件能再DOM中的某一部分发生变化时给出提示。变动事件是为XML或HTML DOM设计的，并不特定于某种语言

  * DOMSubtreeModified: 在DOM结构发生任何变化时触发。这个事件在任何其他事件触发后都会触发

  * DOMNodeInserted：在一个节点作为子节点被插入到另一个节点中时触发

  * DOMNodeRemoved：在节点从其父节点中移除时触发

  * DOMNodeInsertedIntoDocument：在一个节点被直接插入文档或通过子树子树间接插入文档之后触发。这个事件在DOMNodeRemoved之后触发

  * DOMNodeRemovedFromDocument：在一个节点被直接从文档中移除或通过子树间接从文档中移除之前触发。这个事件在DOMNodeRemoved之后触发

  * DOMAttrModified：在特性被修改之后触发

  * DOMChracterModified：在文本的节点发生变化时触发

    DOM3级事件

    * removeChild()或replaceChild()
    * appendChild()或replaceChild()或insertBefore()

  除了这些事件外，HTML5也定义了一组事件，而有些浏览器还会专门在DOM和BOM中实现其他专有事件

##### 事件对象

在触发DOM上的某个事件时，会禅城一个事件对象event，这个对象中包含着所有与事件有关的信息。包括导致事件的元素，事件的类型以及其他与特定事件相关的信息。

* bubbles

##### HTML5事件

* contextmenu：表示何时应该显示上下文菜单，以便开发人员能够取消默认的上下文菜单而提供自定义的

* beforeunload：取消页面卸载并继续使用原有页面，会在浏览器卸载页面之前触发，但是不能彻底取消这个页面，因为那就相当于用户无法离开这个页面了。这个事件的真正用途，是将控制权交给用户。显示的消息会告知用户页面将被卸载，（出现一个弹框）询问用户是否真的要关闭这个页面还是希望继续留下来

* DOMContentLoaded：在形成完整的DOM树之后就会触发。正常的window的load事件会在页面中的一切加载完毕时触发

* readystatechange：提供与文档或元素的加载状态相关信息

* pageshow和pagehide：页面显示和卸载时触发

* hashchange：url参数列表发生变化时触发

  

##### 事件的性能和内存

在我们使用事件的过程中，需要注意性能与内存。

函数也是一个对象，储存在内存空间中。

如果你在代码中定义太多的事件，就会占用太多的内存。

我们在使用innerHTML的时候会碰到一些问题。

你定义的事件与事件触发之间会建立一个联系。你先定义了一个事件，然后将这个事件用innerHTML更改他的文字。虽然事件不触发了，但是他们之间的联系还在，内存并没有得到释放。

这个时候，我们可以手动释放，将事件重新赋值为null

`function printMessage() {

​      console.log(123)

​    }

​    var btn = document.getElementById('btn');

​    btn.onclick = printMessage;

​    btn.onclick = null;

​    btn.innerHTML('print this message');`

另外一种办法是， 我们可以使用<strong>事件委托</strong>

`document.addEventListener('click', function() {

​      switch(type){

​        case 'delete':

​        *// do something*

​        break;

​        case 'add':

​        *// do something*

​        breask;

​        default:;

​      }

​    })`

我们可以一起处理一类事件，避免占用过的的内存。

##### 移动端

移动设备上是没有点击事件的，都是touch事件。

touch事件分为三个阶段，touchstart，touchmove，touchend。

click事件也是通过touch事件来模拟的。

> click事件在移动设备上是有300ms延迟的，touch事件是没有的。
>
> 如果你弹窗关闭的过程在300ms内完成了，那么touch事件就会从当前位置穿透下一层，你点击的就好像是下一层div。
>
> 处理方式，把这个300ms的过程处理掉，比方说让弹窗的消失过程持续300ms
>
> 可以了解js事件穿透