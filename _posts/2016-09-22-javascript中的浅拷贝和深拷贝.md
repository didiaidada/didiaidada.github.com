---
layout: post
title:  JavaScript中的浅拷贝和深拷贝
subtitle: 
author: danX
date: 2016-09-22 09:44:03 +0800
categories: 
tag: 
---

### 1. 什么是浅拷贝

---

因为JS存储对象都是存地址的,浅拷贝会导致指向同一个地址.简单的赋值就是浅拷贝.因为对象和数组在赋值的时候都是引用传递.赋值的时候只是传递一个指针.

```
var a = [1,2];
var b = a;
console.log(a); //[1,2]
console.log(b); //[1,2]
b[0] = 2;
console.log(a); //[2,2]
console.log(b); //[2,2]

```

### 2. 什么是深拷贝

---

深拷贝是开辟一个新的内存地址,将原来对象的各个属性一一复制.


### 3. 实现深拷贝的方法

---

#### 3.1 通过jQuery实现深拷贝

```
//$.extend(true, {}, ...)
var x = {
    a: 1,
    b: { f: { g: 1 } },
    c: [ 1, 2, 3 ]
};

var y = $.extend({}, x),          //shallow copy
    z = $.extend(true, {}, x);    //deep copy

y.b.f === x.b.f       // true
z.b.f === x.b.f       // false
```

#### 3.2 借助JSON全局对象

它能正确处理的对象只有 Number, String, Boolean, Array, 扁平对象，即那些能够被 json 直接表示的数据结构。

```
function jsonClone(obj){
    return JSON.parse(JSON.stringify(obj));
}

```


