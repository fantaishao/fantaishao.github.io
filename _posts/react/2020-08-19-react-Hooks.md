---
layout: post
#标题配置
title:  2019-08-19 React Hooks
#时间配置
date:   2019-08-19
#大类配置
categories: react
#小类配置
tag: React
---

* content
{:toc}


React Hooks 是React的一个新特性，在React 16.8版本中正式发布。

参照官方文档，动手写了一个小例子，先看效果截图，感觉很方便。直接可以在 react function里实现state的更新


了解一个新特性，先来了解它出现的动机，要解决什么问题？

1. hooks是什么
    他可以让你在react中不用写class就可以使用class才有的特性。
2. 动机 motivation

    2.1 组件之间的状态逻辑很难复用

    2.2 复杂的组件不易理解

    2.3 开发者和机器很难理解类

有些疑问
1.hooks之间怎么通信
像引入其他组件一样，import，然后传参
```
import { useFriendStatus } from './useFriendStatus';
const isRecipientOnline = useFriendStatus(recipientID)

```


2.hooks与class component 之间怎么通信
官方文档中有这样一句话，
> You can’t use Hooks inside of a class component。but you can definitely mix classes and function components with Hooks in a single tree.

Ps:后面一句话不是特别理解,目前的理解是class component中是无法使用hooks的

在google上搜到一篇文章[Using Hooks in  Classes](https://reacttraining.com/blog/using-hooks-in-classes/)
虽然我们不能在class component中直接使用Hooks，但是可以通过包装组件来使用。

```
// UsingHooksInClasses.js

function useDocumentTitle(title) {
    useeEffect(() => {
        document.title = title;
    },[title]);
}

export function DocumentTitle({title}) {
    useDocumentTitle(title);
    return null;
}
```

```
// app.js
    import { DocumentTitle } from './HOOKS/UsingHooksInClasses';

    <Fragment>
        <DocumentTitle title="Dashboard" />ß
    </Fragment>
```

