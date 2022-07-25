---
title: Promise
date: 2022-4-5
---

# Promise

Promise 对象代表了一个异步操作的成功或失败
用于当某个操作（eg.加载 xml）完成或者失败后执行相应的操作
**如何创建 Promise： **

```javascript
//让函数拥有promise功能
//当异步代码执行成功时，我们才会调用resolve(...), 当异步代码失败时就会调用reject(...)
function myPromise(url) {
  return new Promise((resolve, reject) => {
    //重要！
    const request = new XMLHttpRequest();
    request.open("GET", url);
    request.onreadystatechange = () => {
      if (request.readyState === 4 && request.status === 200) {
        resolve.call(null, request.response);
        console.log("success");
      } else {
        reject.call(null, request);
      }
    };
    request.send();
  });
}
myPromise(www.baidu.com).then(function (result) {
  console.log(result);
});
//创建promise对象
let myFirstPromise = new Promise(function (resolve, reject) {
  //在本例中，我们使用setTimeout(...)来模拟异步代码，实际编码时可能是XHR请求或是HTML5的一些API方法.
  setTimeout(function () {
    resolve("成功!"); //代码正常执行！
  }, 250);
});

myFirstPromise.then(function (successMessage) {
  //successMessage的值是上面调用resolve(...)方法传入的值.
  //successMessage参数不一定非要是字符串类型，这里只是举个例子
  console.log("Yay! " + successMessage);
});
```

**Promise.prototype.then **
因为 Promise.prototype.then 和 Promise.prototype.catch 方法返回的是 promise， 所以它们可以被链式调用。也就是说每次的 then 返回的都是一个新的 Promise
于是我们可以写出以下的代码

```javascript
new Promise(function (resolve, reject) {
  setTimeout(() => resolve(1), 1000); // (*)
})
  .then(function (result) {
    // (**)

    alert(result); // 1
    return result * 2;
  })
  .then(function (result) {
    // (***)

    alert(result); // 2
    return result * 2;
  })
  .then(function (result) {
    alert(result); // 4
    throw 'error'
    return result * 2;
  }).catch(function(3){
  	console.log(e)//‘error’
  	});
```

上述所有操作都是按顺序进行的，只有当上一个异步操作完成之后才会进行下一步，并且异步操作的结果是每一步更新的

**Promise.all() **
Promise.all() 方法接收一个 promise 的 iterable 类型（注：Array，Map，Set 都属于 ES6 的 iterable 类型）的输入，并且只返回一个 Promise 实例， 那个输入的所有 promise 的 resolve 回调的结果是一个数组。这个 Promise 的 resolve 回调执行是在所有输入的 promise 的 resolve 回调都结束，或者输入的 iterable 里没有 promise 了的时候。它的 reject 回调执行是，只要任何一个输入的 promise 的 reject 回调执行或者输入不合法的 promise 就会立即抛出错误，并且 reject 的是第一个抛出的错误信息。

```javascript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, "foo");
});

Promise.all([promise1, promise2, promise3]).then((values) => {
  console.log(values);
});
// 输出: Array [3, 42, "foo"]
```

**promise.race() **
Promise.race(iterable) 方法返回一个 promise，一旦迭代器中的某个 promise 解决或拒绝，返回的 promise 就会解决或拒绝。

```javascript
let p3 = new Promise(function (resolve, reject) {
  setTimeout(resolve, 100, "three");
});
let p4 = new Promise(function (resolve, reject) {
  setTimeout(reject, 500, "four");
});

Promise.race([p3, p4]).then(
  function (value) {
    console.log(value); // "three"
    // p3 更快，所以它完成了
  },
  function (reason) {
    // 未被调用
  }
);
```
