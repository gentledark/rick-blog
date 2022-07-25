---
title: BFC 是什么?
date: 2022-6-12
---

#### BFC 是什么?

BFC 是 block formatting context，块级格式化上下文

主要作用就是用来创建一个**不会被外界影响**的 css 区域

##### 如何创建一个 BFC？

https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context

所有的触发方式如上，常用如下列表：

1. float 不是 none 的
2. position 为 fixed 或者 absolute 的
3. inline-block 元素，行内块元素
4. overflow 不是 visible 的元素
5. display 为 flex 或者 inline-flex 的直接子元素

##### 解决的问题/常用方法：

由于创建了一个**不会被影响**的区域，所以可以实现以下效果

1. 清除浮动（clearfix 也可以清除浮动）

   ```html
   <div class="container">
     <div class="box1"></div>
     <div class="box2"></div>
   </div>
   ```

   ```css
   .container {
     background: red;
   }
   .box1 {
     float: left; /*由于box1 float了，所以container的高度会塌陷*/
     width: 200px;
     height: 200px;
     background-color: blue;
   }
   .box2 {
     width: 400px;
     height: 100px;
     background: cyan;
   }
   ```

   ```css
   .container {
     overflow: auto; /*对container触发bfc，上面的塌陷就会消除*/
   }
   ```

2. 防止 margin 合并

   ```html
   <div class="div1"></div>
   <div class="div2"></div>
   ```

   ```css
   .div1 {
     width: 100px;
     height: 100px;
     background-color: green;
     margin-bottom: 10px;
   }
   /*这个时候由于外边距重叠，那么上下的距离是20px*/
   .div2 {
     width: 100px;
     height: 100px;
     background-color: red;
     margin-top: 20px;
   }
   ```

   ```html
   <div class="wrapper">
     <!-- 通过创建一个wrapper，再对wrapper创建bfc即可分离margin-->
     <div class="div1"></div>
   </div>
   <div class="div2"></div>
   ```

   ```css
   .wrapper {
     /* 开启BFC */
     overflow: hidden;
   }
   .div1 {
     width: 100px;
     height: 100px;
     background-color: green;
     margin-bottom: 10px;
   }
   .div2 {
     width: 100px;
     height: 100px;
     background-color: red;
     margin-top: 20px;
   }
   ```

3. 制作两栏布局

   ```html
   <div class="left"></div>
   <div class="right"></div>
   ```

   ```css
   .left {
     width: 200px;
     height: 100px;
     background-color: green;
     float: left;
   }
   /*BFC的区域不会与浮动的元素区域重叠，所以right是自适应的，left是左侧固定宽度*/
   .right {
     height: 100px;
     background-color: red;
     overflow: hidden; /* 创建BFC */
   }
   ```
