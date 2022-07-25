---
title: HTML入门
date: 2022-1-22
---

# **HTML 入门**

**核心**

- 域名知识
- http 知识
- html 知识
- 其他

互联网就是互联网，指基于 ip 的网络

万维网是指 www 的网

html 由 Tim Berners-Lee 发明的

html 排错

- html 代码验证器，可以搜索 w3c 验证器安装命令行工具
- vscode 颜色提示
- webstorm 的提示

如果遇到不会的，直接 Google MDN + 关键词

## 章节标签

标题： h1~h6 ， 默认黑体，表示标题

章节： section ， 表示章节

文章： article ？？？

段落： p 表示章节里的内容

头部： header ， 表示文章结构的头部

脚部: footer， 表示文章的末尾部分

主要内容： main, 表示主体

旁支： aside ， 表示非主体内容

划分： div 划分网页内容

## 全局属性: 所有标签都有的属性

class ： 用来表示样式的

contenteditable： 可以使得内容可编辑

hidden： 使内容不显示

id： 与 class 类似， 不过不建议使用， 使用时需要注意保留字

style: 样式

tabindex： 表示当前内容的 tab 值，用来用 tab 键位操作

1-n，数字越小优先级越低

0，优先级最低

-1，表示 tab 不会索引到这里

title：表示鼠标摸上去的时候，黄色背景的内容

## 默认样式

elements→ style→ user agent stylesheet

最开始写的时候，需要把默认样式去掉，然后写的是时候自己加样式

## 内容标签

ol+ li ： ordered list ， listitem

有顺序的 list，用“1. 2.”这种表示，只能放在内容只能放在 li 里

ul+li ： unordered list

和上面一样，但是没有数字标识

dl+dt+dd ： dt 为 term， dd 为 description， 描述这个 item

pre：保留空格回车 tab 等，包起来即可

code： code 里的内容默认等宽的，可以使用 pre+code 写代码

hr：分割线

br：换行 - break

a：一般是超链接用

em：强调， emphasis ， 默认样式是斜体，语气的强调

strong：强调，本质的强调

quote：行内引用

blockquote：换行的引用
