---
title: this是什么？ call apply bind
date: 2022-2-115
---

# this 是什么？ call apply bind

参考https://zhuanlan.zhihu.com/p/23804247

编程中有一种情况，就是当前不知道未来使用这个函数的对象是谁，所以**用 this 指代未来使用的对象**

而 call 解释了 this 究竟是什么，**this 是 call 的第一个参数**

```javascript
class Person {
  constructor(name) {
    this.name = name;
    // this 是new强制制定的
  }
  sayHi() {
    console.log("无法引用name");
  }
}
```

如上所示，上面的 sayHi（）是无法引用 name 变量的。
但是我们知道，用户是一定会用如下两句来引用函数

```javascript
let person = new Person("rick");
person.sayHi();
```

那么是不是可以再引用函数的时候来指定一个形式参数呢
为了解决这个问题，js 采用了 this 和 call

### call 用法

```javascript
//第一种,当a.sayHi（）执行的时候，将person=this作为默认的输入，这样，this.name就变成了a.name
person.sayHi（）
//第二种，当执行函数的时候，由用户手动的指定this
person.sayHi.call（a）
//实际上两种情况是相等的，但一般建议用第二种，可以直观的看到this是什么
```

所以确定 this 就是将函数的使用改写成 call 的形式

```js
function func() {
  console.log(this);
}
func();

function func() {
  console.log(this);
}

func.call(undefined); // 可以简写为 func.call()
//浏览器可能修改默认的this为window，如果不想浏览器修改，可以在函数中加入'use strict'
```

另一个例子

```js
var obj = {
  foo: function () {
    console.log(this);
  },
};
obj.foo();
//转换代码
obj.foo.call(obj); //this是obj
```

### apply

上面的 call 对 js 来说是隐式的传输，apply 是显式传输

```javascript
//a.sayHi.call（a）
//现在假设sayHi（）函数接受三个变量
sayHi（a,b,c）{
		console.log(a+b+c)
}
//当用call用法时
person.sayHi.call（person,1,2,3）
//当用apply时
person.sayHi.call(person,[1,2,3])
//实际上就是将实参用[]括起来，在参数数量未知的情况下是很有用的
```

### bind

bind 就是将 call 或者参数锁定

```javascript
let fn（） = person.sayHi.call（{name:'rick'}）
//这样执行fn的时候this一定是{name:'rick'}
//或者
let fn1() = person.sayHi.all({name:'rick'},1)
//以上指定了第一个参数和this，使用fn1的时候只用指定后两个参数即可
```
