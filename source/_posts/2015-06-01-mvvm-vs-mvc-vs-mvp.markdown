---
layout: post
title: "MVVM VS MVC VS MVP"
date: 2015-06-01 17:58:28 +0800
comments: true
categories: 
---

##Background
MVC作为提倡的代码结构已经被广泛使用。但是随着使用越来越多，它的弊端也越来越明显。比如：Model管理数据，View管理UI相关，Controller协调Model和View。Controller因此包含了太多的property和Protocol的执行代码，这导致Controller职责太大，代码量也太大。 MVC已经不是Model-View-Controller， 而成为了Massive-View-Controller。
  
其次，我们应该把网络层相关code放到哪里？Model？网络请求通常都是异步的，如果网络请求的生命周期不完全属于这个Model呢？很明显我们也不能把网络代码放在View中。那么只能放到Controller中，这又进一步使MVC成了Massive-View-Controller。
<!--more-->

##Element
###Model
包含数据对象以及外部对数据操作的接口。

###View
包含所有的UI显示及用户交互。为了提高重用性，工程里需要将相同的UI作为一个单独的View。

##MVC (Model-View-Controller)

{% img  center /images/mvc_mvvm/mvc.png %}

Controller或者将UI事件传递给Model层，引起Model的数据改变或显示相应的View，或者选择显示下一个View。
Model通过Observer模式update View。  

1. 一个Controller对应多个View；  

2. Model的数据更新不通过Controller直接通知View。  

Disadvantage：  

难于进行UT测试。如何从View角度评估Controller对数据的操作的结果？例如：用户点击的按钮，然后点击事件被传递给了Controller，Controller更新了Model的数据。Model通过Observer模式更新了View中的font size/color。 


##MVP（Model-View-Presenter）
1. Objective-C中涉及的MVC等同于MVP；
2. 一个Presenter只对应一个View；
3. 与Controller有相同的地方，接收UI事件传递给Model层，update Model，但是Model的更新不会直接通知View，而是先通知Presenter，然后Presenter再通知View更新；

##MVVM (Model-View-ViewModel)

{% img  center /images/mvc_mvvm/mvvm.png %}

1. ViewModel不同Model，可以理解为view的model，即包含View的一些属性和操作的Model;
2. View和ViewModel的通知是双向的，View的变化会直接作用于ViewModel，ViewModel的变化也会直接作用于View；
3. 一个ViewModel对应一个View;
4. View包含View和ViewController, MVVM架构下，View应该足够简单，它应该只被用来显示当前UI的状态.


##Summary
几种模式主要区别在于粘合Model和View的方式以及实现用户交互操作机变更通知的方式。但是他们并没有太明确的界限，我们的最终目的是模块解耦，使每个模块都更轻量化，UT更容易。实际工作中经常不经意间融合几种模式在一起，不必太纠结。

##Reference
1. http://joel.inpointform.net/software-development/mvvm-vs-mvp-vs-mvc-the-differences-explained/
2. http://www.teehanlax.com/blog/model-view-viewmodel-for-ios/
