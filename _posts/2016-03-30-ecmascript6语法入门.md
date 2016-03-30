---
layout: post
title: ECMAScript6  语法入门
subtitle: 
author: danX
date: 2016-03-30 11:32:30 +0800
categories: ECMAScript6
tag: 
---

ECMAScript6是JavaScript的下一代标准。我得了解基本的语法。

<br>

--------

<br>


> let和const命令

JS没有块级作用域，let类似于var，用于声明变量。
不同之处是：

1. let声明的变量只在代码块内有效。for循环的计数器很适合let。
2. let没有『变量提升』现象。
3. let在一个作用域内不可重复声明同一个变量。

const类似于let，不同之处是用于常量的声明并且不可改变。

<br>

-----

<br>

> 变量的解构赋值

ES6允许按照一定的模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。
用法解释:

1. 注意『模式匹配』，即等号两边的模式相同。
2. 若解构不成功，变量的值就为undefined。
3. 数组元素匹配时，变量的取值由它的位置决定；对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
4. 数组和对象的解构都可以指定默认值。

<br>

-----

<br>
-------

> 字符串的扩展

JS内部字符以UTF-16的格式存储，每个字符固定为2个字节。（汉字为4个字节）

1. ES6提供了codePointAt方法，能够正确处理4个字节储存的字符，返回一个字符的码点。ES6提供了String.fromCodePoint方法，可以识别0xFFFF的字符，弥补了String.fromCharCode方法的不足。在作用上，正好与codePointAt方法相反。
   
   
   ```
    String.fromCodePoint(0x20BB7) 
    // "吉"
   
   var s = "吉a";
    
   s.codePointAt(0) // 134071 即16进制0x20BB7
   s.codePointAt(1) // 57271
    
   ```

2.  ES6对正则表达式添加了u修饰符，用来正确处理大于\uFFFF的Unicode字符（可以处理汉字）。

    ```
    var s = "吉";
    
    /^.$/.test(s) // false
    /^.$/u.test(s) // true
    
    ```

3.  函数名|用法
     :---|:-----
     contains()|返回布尔值，表示是否找到参数字符串
     startWith()|返回布尔值，表示参数字符串是否在源字符串的头部
     endWith()|返回布尔值，表示参数字符串是否在源字符串的尾部
     repeat(n)|将原字符串重复n次返回
     
     
4.  ES6还为正则表达式添加了y修饰符，叫做“粘连”（sticky）修饰符。<br>
    它的作用与g修饰符类似，也是全局匹配，后一次匹配都从上一次匹配成功的下一个位置开始。<br>
    不同之处在于：<br>
    g修饰符只确保剩余位置中存在匹配，而y修饰符确保匹配必须从剩余的第一个位置开始，这也就是“粘连”的涵义。进一步说，y修饰符号隐含了头部匹配的标志ˆ。ES6的正则对象多了sticky属性，表示是否设置了y修饰符。
                                                                                     

    
    ```
    var s = "aaa_aa_a";
    var r1 = /a+/g;
    var r2 = /a+/y;
    
    r1.exec(s) // ["aaa"]
    r2.exec(s) // ["aaa"]
    
    r1.exec(s) // ["aa"]
    r2.exec(s) // null
    ```
   
5.  模板字符串

模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

<br>

-----

<br>


> 数组的扩展

1. Array.from(),用于将两类伪数组转换为真正的数组，就可以使用数组的方法。
2. Array.of(),用于将一组值转换为数组。
3. find(),数组实例的find()用于找出第一个符合条件的数组元素。它的参数是一个回调函数，所有数组元素依次遍历该回调函数，直到找出第一个返回值为true的元素，然后返回该元素，否则返回undefined。回调函数接受三个参数，依次为当前的值、当前的位置和原数组。
4. findIndex(),与find()用法类似，不同之处是返回的值是第一个符合条件的数组元素的位置，若没有找到则返回-1。
5. fill(n, firstIndex, endIndex),后面两个参数可选，在满足条件的位置用n填充数组。
6. entries()，keys()和values()——用于遍历数组。它们都返回一个遍历器，可以用for...of循环进行遍历，唯一的区别是keys()是对键名的遍历、values()是对键值的遍历，entries()是对键值对的遍历。
7. 数组推导，ES6提供简洁写法，允许直接通过现有数组生成新数组，这被称为数组推导（array comprehension）。
8. Array.observe()，Array.unobserve()。这两个方法用于监听（取消监听）数组的变化，指定回调函数。

<br>

-----

<br>

> 对象的扩展

1. 属性的简洁表示法。ES6允许直接写入变量和函数，作为对象的属性和方法。

2. Object.is()用来比较两个值是否严格相等。它与严格比较运算符（===）的行为基本一致，不同之处只有两个：一是+0不等于-0，二是NaN等于自身。

3. Object.assign(target, source1,...),将源对象(source)的所以可枚举属性复制到目标对象(target)。

4. proto属性，Object.setPrototypeOf()，Object.getPrototypeOf()
5. ES6引入了一种新的原始数据类型Symbol，表示独一无二的ID。它通过Symbol函数生成。
6. Proxy用于修改某些操作的默认行为，等同于在语言层面做出修改，所以属于一种“元编程”（meta programming），即对编程语言进行编程。
7. Object.observe()，Object.unobserve()，用来监听对象（以及数组）的变化。一旦监听对象发生变化，就会触发回调函数。这两个方法不属于ES6，而是属于ES7的一部分。
                                     
<br>

-----

<br>

> 函数的扩展

1. 函数的参数可以设置默认值
2. ES6引入rest参数(...变量名)，rest参数搭配的变量是一个数组，该变量将多余的参数放入数组中。
3. 扩展运算符(...)，它好比rest参数的逆运算。
4. ES6允许使用“箭头”（=>）定义函数。“箭头”前的为函数的输入，“箭头”后为函数的输出。

    ```
    var f = () => 5; 
    // 等同于
    var f = function (){ return 5 };
    
    var sum = (num1, num2) => num1 + num2;
    // 等同于
    var sum = function(num1, num2) {
        return num1 + num2;
    };

    ```
                                     
<br>

-----

<br>

> Set和Map数据结构

ES6提供了新的数据结构Set。它类似于数组，但是成员的值都是唯一的，没有重复。
Set结构有以下属性。

* Set.prototype.constructor：构造函数，默认就是Set函数。
* Set.prototype.size：返回Set的成员总数。

 Set数据结构有以下方法。

* add(value)：添加某个值，返回Set结构本身。
* delete(value)：删除某个值，返回一个布尔值，表示删除是否成功。
* has(value)：返回一个布尔值，表示该值是否为Set的成员。
* clear()：清除所有成员，没有返回值。
* values():返回一个遍历器。
* foreach(键值，键名，集合本身)：用于对每个成员执行某种操作，返回修改后的Set结构。
* 为了与Map结构保持一致，Set结构也有keys和entries方法，这时每个值的键名就是键值。

<br>

ES6提供了map数据结构，它类似于对象，也是键值对的集合，但“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object结构提供了“字符串—值”的对应，Map结构提供了“值—值”的对应。
                                                               
    注意，只有对同一个对象的引用，Map结构才将其视为同一个键。
  
<br> 
Map数据结构有以下属性和方法。

* size：返回成员总数。
* set(key, value)：设置key所对应的键值，然后返回整个Map结构。如果key已经有值，则键值会被更新，否则就新生成该键。
* get(key)：读取key对应的键值，如果找不到key，返回undefined。
* has(key)：返回一个布尔值，表示某个键是否在Map数据结构中。
* delete(key)：删除某个键，返回true。如果删除失败，返回false。
* clear()：清除所有成员，没有返回值。

<br>
Map原生提供三个遍历器。

* keys()：返回键名的遍历器。
* values()：返回键值的遍历器。
* entries()：返回所有成员的遍历器。

<br> 

-----

<br>

> Iterator和for...in循环

---未完









