---
title: AJAX Fetch
date: 2022-5-29
---

### AJAX Fetch

**AJAX**是 Asynchronous JavaScript And XML，是异步请求的一种概念，XHR 是一种实现 ajax 的方式

ajax 一共分为四步，如下

```js
const ajax = (method, url, successfunction, failfunction) => {
  const xhr = new XMLHttpRequest(); //第一步：创建对象
  xhr.open(method, url); //第二步：初始化请求方式和url
  xhr.onreadystatechange = function () {
    //第三步：检查请求状态和执行对应函数
    if (readyState === 4)
      if ((xhr.status >= 200 && xhr.status < 300) || xhr.status === 304) {
        successfunction(xhr.response);
      } else {
        failfunction(xhr.response);
      }
  };
  xhr.send(); //第四步：发送请求
};
```

**Fetch**是一个网络请求 api，会返回一个 promuise，并且请求被响应之后会被 resolve，并传回 response 对象

```js
fetch('http://example.com/movies.json')
  .then(response => response.json())
  .then(data => console.log(data));
	.catch(err=>console.log(err))

//fetch也支持第二个参数
fetch('https://example.com/profile/avatar', {
  method: 'PUT',
  body: formData
})
.then(response => response.json())
.then(result => {
  console.log('Success:', result);
})
.catch(error => {
  console.error('Error:', error);
});
```
