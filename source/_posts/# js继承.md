---
title: js继承
date: 2022-3-10
---

# js 继承

1. 基于原型的继承

```javascript
function Person(name, age, gender) {
  this.name = name;
  this.age = age;
  this.gender = gender;
} //Person函数主要用来添加新对象的自身属性
Person.prototype.sayHi = function () {
  console.log("hi, I am " + this.name);
};
Person.prototype.study = function () {
  console.log(this.name + "is studying");
};
//prototype下主要添加新对象的共有属性
let rick = new Person("rick", 18, "male");
let ricky = new Person("ricky", 20, "female");
rick.sayHi.call(rick);
rick.sayHi.call(ricky); //注意call的用法
rick.name;

rick.__proto__ === Person.prototype; //true
rick.__proto__.__proto__ === {}.__proto__; //true
```

以上代码表示以 Person 为原型构造了对象 rick 和 ricky。
rick.**proto**里面包含了 sayHi 和 study 函数，并且还有 constructor = Person（）
并且还有 Object.prototype，所以 rick 也具有 object 的属性

2. 基于 class 的继承

```javascript
class Person {
  constructor(name, age, gender) {
    this.name = name;
    this.age = age;
    this.gender = gender;
  }
  sayHi() {
    console.log("hi, I am " + this.name);
  }
  study() {
    console.log(this.name + "is studying");
  }
} //Person函数主要用来添加新对象的自身属性
//再次继承
class ForeignPerson {
  constructor() {}
  printCountry() {}
}
```

以上代码表示了构造 class 的继承，写法不用，但是和基于原型的继承作用相同
