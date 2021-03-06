---

layout: post
#标题配置
title:  JavaScript数组的去重
#时间配置
date:   2020-05-04
#大类配置
categories: JavaScript
#小类配置
tag: JavaScript基础知识整理
---

##### 数组的去重

定义一个空数组，将原来的数组遍历，然后去空数组中比较，如果没有就push进去

```
<script>
       var array = [6, 2, 6,3, 8, 1, 9,];
       var tmp = []
       for(var i = 0;i<array.length;i++) {
           if(i === 0) tmp.push(array[i])
           var isPush = true;
           for(var k = 0;k< tmp.length; k++) {
               if(array[i] === tmp[k]) {
                 isPush = false;
                 break;
               }
           }
           if(isPush) tmp.push(array[i]);
       }
       console.log(tmp) //  [1, 2, 6, 3, 8, 9]s
</script>
```

定义一个空数组，遍历原数组数组，将数组的当前项与其他项对比，如果没有则push进去

```
var tmp2 = [];
       for(var i = 0; i < array.length; i++) {
           for(var k = i+1; k< array.length; k++) {
                if(array[i] === array[k]) {
                    k = ++i;
                }
           }
           tmp2.push(array[i]);
        }
       console.log(tmp2)// [2, 6, 3, 8, 1, 9]
```

遍历原来的数组，当前项与剩下的项一一比较，如果发现相同，则将原来的项删除，可以运用splice方法

```
var array1 = [6, 2, 6,3, 8, 1, 9];
       var len = array1.length;
       for(var i = 0; i < len; i++) {
           for(var k = i+1; k< len; k++) {
                if(array[i] === array[k]) {
                    array1.splice(k,1)
                    len--;
                }
           }
        }
        console.log(array1)// [6, 2, 3, 8, 1, 9]

```

根据对象的特性来，对象里面属性的名称是不能重复的，遍历数组，将每个值作为对象的属性，先检测对象的属性是否存在，如果存在，将属性值设置为true，否则push到空数组中

```
var array2 = [6, 2, 6,3, 8, 1, 9];
        var tmp = []
        var obj = {};
        for(var i = 0;i < array2.length;i++) {
           if(obj[array2[i]] === undefined) {
              tmp.push(array2[i]);
              obj[array2[i]] = true;
           }
        }
        console.log(tmp);// [6, 2, 3, 8, 1, 9]
```

将数组先排序，然后任意取一项，跟前面或者后面的对比，如果发现相同，则移除比较项

```
var array3 = array2.sort(function(a,b){
            return a-b;
        })
        for(var i = 0;i < array3.length;i++) {
           if(array3[i] === array3[i+1]) {
              array3.splice(i,1)
           }
        }
        console.log(array3);// [1, 2, 3, 6, 8, 9]
```

利用数组的indexOf方法, 它可以接收两个参数，第一个是查找值，第二个是查找的起点位置，如果返回-1，可以将它push进新数组

```
var tmp = [];
        var array4 = [6, 2, 6,3, 8, 1, 9];
        for(var i = 0;i < array4.length;i++) {
           var index = tmp.indexOf(array4[i])
           if(index === -1) {
               tmp.push(array4[i])
           }
        }
        console.log(tmp);// [6, 2, 3, 8, 1, 9]
```

利用ES6中的set对象，set对象中的每个值都是唯一的

```
var array = [1,2,3,4,4]
var tmp = Array.from(new Set(array));
console.log(tmp) // [1,2,3,4]
```

> `Array.from`方法用于将两类对象转为真正的数组：类似数组的对象（array-like object）和可遍历（iterable）的对象（包括 ES6 新增的数据结构 Set 和 Map）

利用ES6中的拓展运算符

```
var array = [1,2,3,4,4];
var tmp = [...new Set(array)];
console.log(tmp) // [1,2,3,4]
```



