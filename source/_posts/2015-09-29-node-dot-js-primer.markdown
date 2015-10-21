---
layout: post
title: "Node.js primer"
date: 2015-09-29 17:35:28 +0800
comments: true
categories: 
---

## The correct writing for Node.js
NodeJS、Nodejs都是错的，Node.js官网用Node或Node.js， Node.js更准确，后缀点出了Node的本意。  
  
##Node.js 是什么  
它并不是一个Javascript应用，它采用C++语言编写而成，是一个可以在后端运行Javascript的运行环境(平台)。  
Node.js的设计思路中以事件驱动为核心，它提供的绝大多数API都是基于事件的、异步的风格。

##Node.js核心词汇
###事件驱动、异步编程
Node.js以事件驱动为核心，注册相应的回调函数实现。

###快速构建Web服务器
网络编程比较便利，提供的模块开放了容易上手的API

###性能
单进程、单线程运行模式

###异步IO
为了充分利用CPU,和使I/O可以并行,目前有两种方式可以 达到目的:
多线程单进程 
多线程的设计之处就是为了在共享的程序空间中,实现并行处理任 务,从而达到充分利用CPU的效果。多线程的缺点在于执行时上下文 交换的开销较大,和状态同步(锁)的问题。同样它也使得程序的编 写和调用复杂化。

单线程多进程 
为了避免多线程造成的使用不便问题,有的语言选择了单线程保持调 用简单化,采用启动多进程的方式来达到充分利用CPU和提升总体的 并行处理能力。 它的缺点在于业务逻辑复杂时(涉及多个I/O调用), 因为业务逻辑不能分布到多个进程之间,事务处理时长要远远大于多线程模式。

￼


??Javascript的匿名函数和闭包特性


##CommonJS 规范


##简单模块的定义和使用
```
var PI = Math.PI; 

exports.area = function (r) {
	return PI * r * r; 
};

exports.circumference = function (r) { 
	return 2 * PI * r;
};

```

将这个文件存为circle.js,并新建一个app.js文件,并写入以下代码
```
var circle = require('./circle.js');
console.log( 'The area of a circle of radius 4 is
' + circle.area(4));

```

Node.js模块分为两类，一类为原生（核心）模块，一类是文件模块。

一个符合CommonJS规范的包应该是如下这种结构:
1. 一个package.json文件应该存在于包顶级目录下 
2. 二进制文件应该包含在bin目录下
3. JavaScript代码应该包含在lib目录下
4. 文档应该在doc目录下
5. 单元测试应该在test目录下。


package.json文件定义了如下 一些必须的字段:
name: 包名,需要在NPM上是唯一的。不能带有空格。 
description: 包简介。通常会显示在一些列表中。 
version: 版本号。一个语义化的版本号(http://semver.org/ ),通常 为x.y.z。该版本号十分重要,常常用于一些版本控制的场合。 
keyword: 关键字数组。用于NPM中的分类搜索。 
maintainers: 包维护者的数组。数组元素是一个包含name、email、 web三个属性的JSON对象。 
contributors: 包贡献者的数组。第一个就是包的作者本人。在开源社区,如果提交的patch被merge进master分支的话,就应当加上这个贡献patch的人。格式包含name和email。如:
```
"contributors": [{
	"name": "Jackson Tian", 
	"email": "mail @gmail.com"
}, {
	"name": "fengmk2", 
	"email": "mail2@gmail.com"
}],
```

bugs:一个可以提交bug的URL地址。可以是邮件地址 (mailto:mailxx@domain),也可以是网页地址(http://url)。
licenses: 包所使用的许可证。例如:
```
￼"licenses": [{ "type": "GPLv2",
"url": "http://www.example.com/licenses/gpl.h tml",
}]
```
repositories: 托管源代码的地址数组。
dependencies: 当前包需要的依赖。这个属性十分重要,NPM会通过 这个属性,帮你自动加载依赖的包。




