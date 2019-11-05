---
layout: post
#标题配置
title:  React 组件生命周期
#时间配置
date:   2019-03-22
#大类配置
categories: react
#小类配置
tag: 总结
---

* content
{:toc}


浅析React 组件生命周期

React的生命周期是理解React中比较重要的一环。

React的生命周期分为三个部分
1. Mounting

   1.1 construtor()
   这个函数用来初始化state对象和给函数绑定this作用域

   1.2 getDerivedStateFromProps()
   获取props的变化来更新state

   1.3 render()
   当state有变化时，会调用render函数，重新渲染组件树

   1.4 componentDidMount()
   当render执行完成后，会调用componentDidMount(),这个函数只会在初始化完成后，调用一次

2. Update
   当props或者state变化时，会引发更新
   2.1 getDerivedStateFromProps()
   当用户状态更新时，getDerivedStateFromProps()会捕捉到props或者state的变化

   2.2 shouldComponentUpdate()
   如果有些情况你不想重新渲染组件树，可以再shouldComponentUpdate中进行判断，返回true代表需要更新，false则不需要更新

   2.3 render()
   当有状态更新时，render函数会重新渲染组件树

   2.4 getSnapshotBeforeUpdate()
   
   2.5 componentDidUpdate()
   更新完成后，会调用componentDidUpdate(),在组件初始化的时候，不会调用此函数

3. Unmount

   3.1 componentWillUnmount()
   组件卸载的之后会调用此函数