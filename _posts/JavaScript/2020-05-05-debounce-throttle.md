---

layout: post
#标题配置
title:  JavaScript 防抖动和节流
#时间配置
date:   2020-05-05
#大类配置
categories: front-end
#小类配置
tag: JavaScript
---

##### 什么是防抖动函数

防抖动函数就是当你连续触发一个事件的时候，它只会在一定的时间之后执行最后一次事件。

比方说，你监听一个鼠标事件，当你鼠标移动的时候，它可能会在一秒或者更短的事件内，连续触发几十次甚至几百次事件，这会很影响页面的性能。

它能用在很多方面，比方说你页面滚动触发事件，页面缩放，监听鼠标事件等等

监听鼠标移动事件，使用debounce函数和不使用的对比。

<iframe
     src="https://codesandbox.io/embed/nifty-kilby-1tuij?fontsize=14&hidenavigation=1&theme=dark"
     style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
     title="nifty-kilby-1tuij"
     allow="accelerometer; ambient-light-sensor; camera; encrypted-media; geolocation; gyroscope; hid; microphone; midi; payment; usb; vr"
     sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
   ></iframe>

监听滚动条事件，使用debounce函数和不使用的对比。



##### 什么是节流函数



参考文章

[MDN window.requestAnimationFrame]: https://developer.mozilla.org/zh-CN/docs/Web/API/Window/requestAnimationFrame
[Debouncing and Throttling Explained Through Examples]: https://css-tricks.com/debouncing-throttling-explained-examples/

###### [Can someone explain the “debounce” function in Javascript](https://stackoverflow.com/questions/24004791/can-someone-explain-the-debounce-function-in-javascript)