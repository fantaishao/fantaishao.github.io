---
layout: post
#标题配置
title:  JavaScript事件
#时间配置
date:   2020-05-01
#大类配置
categories: JavaScript
#小类配置
tag: JavaScript基础知识整理
---

* content
{:toc}


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

##### DOM0事件(属性事件)

这个是通过JavaScript指定事件处理程序的传统方式，将一个函数赋值给一个事件处理程序属性

```
var btn = document.getElementById('btn');

​    btn.onclick = function(){}
```

使用DOM0级方法指定的事件处理程序被认为是元素的方法。因此，这时候的事件处理程序是在元素的作用域中运行；换句话说，程序中的this引用当前元素。来看一个例子

```
var btn = document.getElementById('btn');

​    btn.onclick = function(){

​      console.log(this.id);*// btn*

​    }
```

以这种方式添加的事件处理程序会在事件流的冒泡阶段被处理，如果需要删除事件，直接将属性的值设为null即可。

  DOM0如何触发事件呢？

先获取要触发的元素

主要是指鼠标键盘事件

##### DOM2事件(监听事件)

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

  var passiveSupported = false;

  ​    try {

  ​     var options = Object.defineProperty({}, 'passive', {

  ​       get: function() {

  ​         passiveSupported = true;

  ​       }

  ​     });

  ​     window.addEventListener('test', null, options)

  ​    } catch(err) {}

   因为在旧版本的浏览器中，第三个属性仍然是一个布尔值，所以你需要编写一些代码来有效的监测你的浏览  器是否支持对象中的属性

第三个函数可选

```
function getData() {

​      *// do something*

​    }

​    window.addEventListener('click', getdata, false);

​    window.removeEventListener('click', getdata, false)
```

添加和移出的函数必须是统一函数，所以如果你需要移除绑定的函数，就不能使用匿名函数

`window.addEventListener('click', function(){}, false);`

> 大多数情况都是将事件处理程序添加到事件流的冒泡阶段，这样可以最大限度地兼容各种浏览器。

1. DOM3事件

DOM3里新定义了自定义事件

```
function customEvent() {

​      var div = document.getElementById('div');

​      var event = document.createEvent('click', document);

​      div.dispatchEvent(event)

​    }
```

目前只有火狐浏览器支持

> 为什么没有DOM1事件？因为DOM1中没有定义事件相关的内容

##### IE事件处理程序

IE实现了与DOM中类似的两个方法，attachEvent和detachEvent。

这两个方法接受相同的两个参数: 事件处理程序名称与事件处理程序函数。由于IE8及更早的版本只支持事件冒泡，所以通过attachEvent()添加的事件处理程序都会被添加到冒泡阶段。

```
var btn = document.getElementById('btn');

​    btn.attachEvent('onclick', function(){})
```



> 在IE中使用attachEvent()与使用DOM0级方法的主要区别在于事件处理程序的作用域。在使用DOM0级方法的情况下，事件处理程序会在其所属元素的作用域内运行；在使用attachEvent()方法的情况下，事件处理程序会在全局作用域中运行，因此this等于window

与addEventListener()类似，attachEvent()方法也可以用来为一个元素添加多个事件处理程序

```
var btn = document.getElementById('btn');

​    btn.attachEvent('onclick', function(){console.log(123)})

​    btn.attachEvent('onclick', function(){console.log(456)})
```

与DOM方法不同的是，这些事件处理程序不是按照他们添加的顺序执行的，而是以相反的顺序被触发

[DOM其他信息]: https://www.w3.org/DOM/DOMTR

##### 事件类型

DOM3级事件类型

* UI事件，当用户与页面的元素交互时触发， load，unload，abort，error，select，resize，scroll

* 焦点事件，当元素获得或失去焦点时触发, blur,DOMFocusIn,DOMFocusOut,focus,focusin,focusout

* 鼠标事件，当用户通过鼠标在页面上执行操作时触发

* 滚轮事件，当使用鼠标滚轮(或类似设备)时触发 鼠标滚轮事件：click,dbclick,mousedown,mouseenter,mouseleave,mousemove,mouseout,mouseover,mouseup，mousewheel

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

在触发DOM上的某个事件时，会有一个事件对象event，这个对象中包含着所有与事件有关的信息。包括导致事件的元素，事件的类型以及其他与特定事件相关的信息。

触发的事件类型不一样，可用的属性和方法也不一样。不过，所有的事件都会有下表中的属性和方法。

| 属性/方法                  | 类型         | 读/写 | 说明                                                         |
| -------------------------- | ------------ | ----- | ------------------------------------------------------------ |
| bubbles                    | Boolean      | 只读  | 表示事件是否冒泡                                             |
| cancelable                 | Boolean      | 只读  | 是否可以取消事件的默认行为                                   |
| currentTarget              | Element      | 只读  | 当前事件处理程序正在处理的元素                               |
| defaultPrevented           | Boolean      | 只读  | 为true表示已经调用了preventDefault()                         |
| detail                     | Integer      | 只读  | 与事件相关的信息                                             |
| eventPhase                 | Integer      | 只读  | 调用事件处理程序的阶段，1表示捕获阶段，2表示目标阶段，3表示冒泡阶段 |
| preventDefault()           | Function     | 只读  | 取消事件默认行为，如果cancelable为true，才可以调用           |
| stopImmediatePropagation() | Function     | 只读  | 取消事件的进一步捕获或冒泡，同时阻止任何事件处理程序被调用(DOM3级事件中新增) |
| stopPropagation()          | Function     | 只读  | 取消事件的进一步捕获或冒泡，如果bubbles为true，才可以调用    |
| target                     | Element      | 只读  | 事件的目标                                                   |
| trusted                    | Boolean      | 只读  | 为true表示是浏览器生成，为false表示由开发人员通过JavaScript创建的(DOM3级事件中新增) |
| type                       | sting        | 只读  | 被触发的事件类型                                             |
| view                       | AbstractView | 只读  | 与事件关联的抽象视图。等同于发生事件的window对象。PS:这个很少用，一般直接用window对象了 |

> currentTarget表示当前事件发生在哪个元素上，target表示当前事件目标元素是什么
>
> 我们点击了内层div，比方说这个时候target指向的是内层div，这个时候currentTarget不一定指向内层div，要看你当前事件处理程序是处在哪个阶段，如果是在外层div的捕获阶段，这个时候target指向内层div，currentTarget指向外层div。
>
> currentTarget和this指向同一个东西，target指向触发事件的目标对象。
>
> 如果是处于目标阶段，eventPhase等于2，currentTarget，target，this这三者的指向是一样的

> stopPropagation()阻止事件的传播，不会阻止事件的默认行为；currentTarget()阻止事件的默认行为，不会阻止事件的传播

> stopPropagation()虽然事件不会继续传播，但是当前节点绑定的函数仍然会执行

> stopImmediatePropagation()与stopPropagation()的区别
>
> 只有当前节点绑定了两个或者以上的事件才有区别
>
> stopImmediatePropagation()阻止了事件的传播，绑定他之后的函数不会继续执行

event对象总的来说可以分为三类，和位置相关，和键盘相关，和鼠标的按键相关

和位置相关，一共有六个属性，每个对应两个方向，一个x轴，一个y轴

* screenX：相对于整个电脑屏幕的位置

* clientX：以内容区域为参考

* pageX：页面本身的位置，如果有滚动 还是要加上滚动的距离, 相对于整个文档 ps：IE8及更早的版本不支持pageX

  > 举个例子，如果页面向右滚动 200px 并出现了滚动条，这部分在窗口之外，然后鼠标点击距离窗口左边 100px 的位置，pageX 所返回的值将是 300。

* layerX：以body为参考点，获取触发点相对于offsetParent元素左上角的距离(确切的说是边框外界的距离)，包括中间所有元素的padding、margin、border及元素宽度值之和， IE9以上可用

>  offsetParent元素
>
> 如果当前元素的祖先元素没有进行css定位(position为absolute或relative)，offsetParent为body
>
> 如果当前元素的祖先元素(包括当前元素)中有css定位(position为absolute或relative),offsetParent取最近的那个祖先元素(包括当前元素)

* offsetX：当前元素左上角相对于节点的左边界的像素值，以content为参考点

* movementX：两个连续移动事件之间的距离

  `currentEvent.movementX = currentEvent.screenX - previousEvent.screenX`.

![/styles/images/mouseevent.png]({{ '/styles/images/mouseevent.png' | prepend: site.baseurl  }})

和键盘相关的事件

* shiftKey：是否按下shift键
* ctrlKey：是否按下ctrl键
* altKey：是否按下alt键
* metaKey：是否按下meta键

和鼠标的按键相关

* button：返回一个值，代表用户按下并触发了事件的鼠标按键。 -1没有按键，0表示主鼠标按钮，1辅助按键被按下，通常指鼠标右键，2次键被按下，通常指鼠标右键，3第四个按钮被按下，通常指浏览器后退按钮，4第五个按钮被按下，通常指浏览器的前进按钮。ps：如果配置为左手使用鼠标，刚好相反。此种情况下，从右至左读取数据
* buttons：指事件触发时哪些鼠标按键被按下。如果同时按下多个键，buttons的值为各键对应值做加计算。例如，如果右键(2)和滚轮键(4)被同时按下，buttons的值为2+4=6



##### HTML5事件

* contextmenu：表示何时应该显示上下文菜单，以便开发人员能够取消默认的上下文菜单而提供自定义的
* beforeunload：取消页面卸载并继续使用原有页面，会在浏览器卸载页面之前触发，但是不能彻底取消这个页面，因为那就相当于用户无法离开这个页面了。这个事件的真正用途，是将控制权交给用户。显示的消息会告知用户页面将被卸载，（出现一个弹框）询问用户是否真的要关闭这个页面还是希望继续留下来
* DOMContentLoaded：在形成完整的DOM树之后就会触发。正常的window的load事件会在页面中的一切加载完毕时触发
* readystatechange：提供与文档或元素的加载状态相关信息
* pageshow和pagehide：页面显示和卸载时触发
* hashchange：url参数列表发生变化时触发

我们在平常的用的比较多的是鼠标点击事件。

一个完整dbclick事件触发事件的顺序如下

1. mousedown
2. mouseup
3. click
4. mousedown
5. mouseup
6. click
7. dbclick

IE8及之前的版本有一个小bug，在双击事件中会掉过第二个mousedown和click事件，其顺序如下：

1. mousedown
2. mouseup
3. click
4. mouseup
5. dbclick

IE9修复了这个bug，之后顺序就正确了。

鼠标的移入事件有两个，mouseenter和mouseover

它们两者的区别是mouseenter**不会冒泡**，在鼠标光标从元素外部首次移动到元素范围之内时触发，因为不会冒泡，所以在元素移动到后代元素上不会触发；mouseover，在鼠标指针位于一个元素外部，然后用户将其首次移入另一个元素边界之内时触发，每次在子节点上移动，因为该事件会冒泡，也会被触发。

鼠标的移开事件有两个，mouseleave和mouseout

它们两者的区别是mouseleave**不会冒泡**，在位于元素上方的鼠标光标移动到元素范围之外时触发，因为不会冒泡，在光标移动到后代元素上时不会触发；mouseout，在鼠标指针位于一个元素上方，然后用户将其移入另一个元素时触发。又移入的另一个元素可能位于前一个元素的外部，也可能是这个元素的子元素。

另外一个是焦点事件

当焦点从页面中的一个元素移动到另一个元素，会依次触发下列事件：

1. focusout在失去焦点的元素上触发
2. focusin在获得焦点的元素上触发
3. blur在失去焦点的元素上触发
4. DOMFocusOut在失去焦点的元素上触发
5. focus在获得焦点的元素上触发
6. DOMFocusIn在获得焦点的元素上触发

其中，blur、DOMFocusOut和focus的事件目标是失去焦点的元素；而focus、DOMFocusIn和focusin的事件目标是获得焦点的元素

鼠标滚轮事件mousewheel

滚动事件的一些问题总结

1. 滚动事件，每个浏览器支持的不一样，根据你项目需要支持的浏览器做实际的坚持

2. wheelDelta滚轮不一样是120的倍数，这个跟设备，比方说你用的鼠标不一样，有一种叫线性滚轮鼠标；另外mac的触摸板就可以模拟滚轮，滚动值就不一样，wheelDelta是3的倍数，不是120的倍数。你划一下，可以一下子滚动几十倍次，wheelDetlta先上涨再下降，是一个抛物线的性质

3. 只要滚轮停止滚动，滚动事件就直接停止；但是对于mac的触摸板而言，如果你的手不离开触摸板，触摸也停止了，你的手碰一下，又离开了

4. wheelMeta可能出现连续的振动，

5. 鼠标的滚动事件和页面滚动事件是两个完全不一样的。键盘和鼠标滚轮会触发鼠标滚动事件，滑动页面的滚动条是不会触发鼠标的滚动事件

6. 鼠标的滚轮事件跟页面的滚动条到底部和顶部是没关系的。即使你页面滚动到顶部，你继续操作鼠标滚轮，鼠标滚轮事件还是在触发， 只是你的页面没有显示出来而已。mac和安卓设备上，用手指去放大缩小的时候是会触发鼠标事件的

7. 对于鼠标滚动或者移动，是一个高频事件，会连续发生好多事件，如果你的事件执行的比较慢，那么页面就会比较卡，严重影响性能。这里就会有两个函数，节流和防抖函数。

   举个例子

   网页懒加载，比方说网页有很多屏，刚打开页面的时候，用户只能看到第一屏，当页面滚动页面的时候，才会去动态加载接下来的页面。那么什么时候需要加载页面呢？首先要去检测页面发生了滚动事件，遍历已经加载的DOM节点，然后加载接下来的页面。但是这样会非常耗时，每次滚动都需要遍历节点。我们可以用户停止滚动的时候，去遍历检查页面。我们可以在一定的事件的内，比方说两秒内，已经执行过对应的事件处理程序，那么就不执行。这个是防抖函数，就是设置一个时间戳，如果在这个时间内执行过，就推迟执行这个函数；节流函数，就是固定时间间隔执行函数。

   我们平常在连续高频的执行事件都会用到防抖节流函数，比方说，滚轮，鼠标移动，窗口缩放，拖拽，滑动的touchmove，都会涉及到防抖节流函数。

   

##### 事件的优先级

```
<body>
        <div id="parent" style="width:100px;height:50px;background: yellow;color:white;">
            <div id="child" style="width:50px;height:30px;background: red;color:white;">点击我</div>
        </div>
    </body>
```



```
// 事件优先级
        var parent = document.getElementById('parent');
        var child = document.getElementById('child');
        // DOM2级事件
        function bodyClick1(){console.log('DOM2 click body and 捕获阶段')}
        function bodyClick2(){console.log('DOM2 click body and 冒泡阶段')}
        function parentClick1(){console.log('DOM2 click parent and 捕获阶段')}
        function parentClick2(){console.log('DOM2 click parent and 冒泡阶段')}
        function childClick1(){console.log('DOM2 click child and 捕获阶段')}
        function childClick2(){console.log('DOM2 click child and 冒泡阶段')}
        document.body.addEventListener('click', bodyClick1, true);// 捕获阶段调用
        document.body.addEventListener('click', bodyClick2, false);// 冒泡阶段调用
        parent.addEventListener('click', parentClick1, true);
        parent.addEventListener('click', parentClick2, false);
        child.addEventListener('click', childClick1, true);
        child.addEventListener('click', childClick2, false);
        // DOM0级事件
        document.body.onclick = function(){console.log('DOM0 click body')}
        parent.onclick = function(){console.log('DOM0 click parent')}
        child.onclick = function(){console.log('DOM0 click child')}
```

浏览器输出结果

![/styles/images/image-20200502101846924.png]({{ '/styles/images/image-20200502101846924.png' | prepend: site.baseurl  }})

针对DOM0或者DOM2级别的事件，只会在冒泡阶段

如果一个事件发生在目标阶段和冒泡阶段，事件执行的顺序是按照你绑定的顺序来执行的。

当冒泡到外层div，触发顺序也是根据绑定顺序来执行的。

我们改动下顺序

```
<script>
        // 事件优先级
        var parent = document.getElementById('parent');
        var child = document.getElementById('child');
        // DOM0级事件
        document.body.onclick = function(){console.log('DOM0 click body')}
        parent.onclick = function(){console.log('DOM0 click parent')}
        child.onclick = function(){console.log('DOM0 click child')}
        // DOM2级事件
        function bodyClick1(){console.log('DOM2 click body and 捕获阶段')}
        function bodyClick2(){console.log('DOM2 click body and 冒泡阶段')}
        function parentClick1(){console.log('DOM2 click parent and 捕获阶段')}
        function parentClick2(){console.log('DOM2 click parent and 冒泡阶段')}
        function childClick1(){console.log('DOM2 click child and 捕获阶段')}
        function childClick2(){console.log('DOM2 click child and 冒泡阶段')}
        document.body.addEventListener('click', bodyClick1, true);// 捕获阶段调用
        document.body.addEventListener('click', bodyClick2, false);// 冒泡阶段调用
        parent.addEventListener('click', parentClick1, true);
        parent.addEventListener('click', parentClick2, false);
        child.addEventListener('click', childClick2, false);
        child.addEventListener('click', childClick1, true);
    </script>
```

![/styles/images/image-20200502105734943.png]({{ '/styles/images/image-20200502105734943.png' | prepend: site.baseurl  }})

##### 事件的传递和css有关系么

这里面有个例外，如果你绑定了html事件，它是最先执行的，只不过它被JavaScript绑定的属性事件给覆盖了。

>  PS：因为事件是浏览器绑定的，HTML代码是最先渲染的

调整下上面代码，去掉属性事件，添加HTML事件

```
<body>
        <div id="parent" style="width:100px;height:50px;background: yellow;color:white;" onclick="parentHTML()">
            <div id="child" style="width:50px;height:30px;background: red;color:white;" >点击我</div>
        </div>
    </body>
```

```
<script>
        // 事件优先级
        function parentHTML() {
            console.log('HMTL事件 parent')
        }
        var parent = document.getElementById('parent');
        var child = document.getElementById('child');
        // DOM0级事件
        document.body.onclick = function(){console.log('DOM0 click body')}
        // parent.onclick = function(){console.log('DOM0 click parent')}
        child.onclick = function(){console.log('DOM0 click child')}
        // DOM2级事件
        function bodyClick1(){console.log('DOM2 click body and 捕获阶段')}
        function bodyClick2(){console.log('DOM2 click body and 冒泡阶段')}
        function parentClick1(){console.log('DOM2 click parent and 捕获阶段')}
        function parentClick2(){console.log('DOM2 click parent and 冒泡阶段')}
        function childClick1(){console.log('DOM2 click child and 捕获阶段')}
        function childClick2(){console.log('DOM2 click child and 冒泡阶段')}
        document.body.addEventListener('click', bodyClick1, true);// 捕获阶段调用
        document.body.addEventListener('click', bodyClick2, false);// 冒泡阶段调用
        // parent.addEventListener('click', parentClick1, true);
        // parent.addEventListener('click', parentClick2, false);
        child.addEventListener('click', childClick2, false);
        child.addEventListener('click', childClick1, true);
    </script>
```

![/styles/images/image-20200502111156477.png]({{ '/styles/images/image-20200502111156477.png' | prepend: site.baseurl  }})

##### 事件的传递和css有关系么

不会。

事件的传播是按照HTML结构来传播的。事件的绑定是浏览器根据你的HTML结构来绑定的。

如果你用css绝对定位来改变元素的位置，它还是按照原来的绑定顺序来触发的。

但是有一种例外，事件穿透。

在移动端click事件是有300ms的延迟的，touch事件是没有，比方说有一个弹窗，你在300ms内关闭它，那么事件就会穿透到里面的div层，好像点到了里面的div层。

可以将关闭动画延长至300ms或者在弹窗后面添加一层遮罩，穿透后点击到添加的那层遮罩。弹窗关闭后处理掉那层遮罩即可。

##### 事件的内存和性能

在我们使用事件的过程中，需要注意性能与内存。

函数也是一个对象，储存在内存空间中。

如果你在代码中定义太多的事件，就会占用太多的内存。

我们在使用innerHTML的时候会碰到一些问题。

你定义的事件与事件触发之间会建立一个联系。你先定义了一个事件，然后将这个事件用innerHTML更改他的文字。虽然事件不触发了，但是他们之间的联系还在，内存并没有得到释放。

这个时候，我们可以手动释放，将事件重新赋值为null

```
function printMessage() {

​      console.log(123)

​    }

​    var btn = document.getElementById('btn');

​    btn.onclick = printMessage;

​    btn.onclick = null;

​    btn.innerHTML('print this message');
```

另外一种办法是， 我们可以使用<strong>事件委托</strong>

```
document.addEventListener('click', function() {

​      switch(type){

​        case 'delete':

​        *// do something*

​        break;

​        case 'add':

​        *// do something*

​        breask;

​        default:;

​      }

​    })
```

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

