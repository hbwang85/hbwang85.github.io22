---
layout: post
title: "ReactiveCocoa Notes"
date: 2015-06-25 15:10:35 +0800
comments: true
categories: 
---

##ReactiveCocoa试图解决什么问题

经过一段时间的研究，我认为ReactiveCocoa试图解决以下3个问题：

1. 传统iOS开发过程中，状态以及状态之间依赖过多的问题
2. 传统MVC架构的问题：Controller比较复杂，可测试性差
3. 提供统一的消息传递机制

RAC在应用中大量使用了block，由于Objective-C语言的内存管理是基于引用计数的，为了避免循环引用问题，在block中如果要引用self，需要使用@weakify(self)和@strongify(self)来避免强引用。另外，在使用时应该注意block的嵌套层数，不恰当的滥用多层嵌套block可能给程序的可维护性带来灾难

1. RAC provides signals (represented by RACSignal) that capture present and future values  
2. By chaining, combining, and reacting to signals, software can be written declaratively, without the need for code that continually observes and updates values.
3. It provides a single, unified approach to dealing with asynchronous behaviors, including delegate methods, callback blocks, target-action mechanisms, notifications, and KVO  


Signals can also represent asynchronous operations, much like futures and promises. This greatly simplifies asynchronous software, including networking code


unlike KVO notifications, signals can be chained together and operated on (pipeline)

Signal Commend


Signal cold  hot: 
cold signal : it will not do any work until subscription

reduceEach: Unpacks each RACTuple in the receiver and maps the values to a new value   n-->1

Map: takes a list and return it into another list of the same length, "mapping" each value in the original list into a new value in the resulting list.       1-->1

Filter: Filtering a list just returns a new list containing all of the original entries, minus the entries that didn't return true from a test.

Fold: combines each entry in a list down to a single value. It's often referred to as "combine".

RACScheduler: used to control when and where work is performed

Subscriptions: made on signals. when you want to be notified that a new value is sent(either next, error or completion).

Macros
RAC(Object, keypath): It performs a one-way binding of the right-hand value of the expression to the key path in question. Values must be NSObjects
RACObserve(Object, keypath)

RACCommend : 
1. Create and subscribe to a signal in response to some action. Usually the action trigging a command is UI-driven, like when a button is clicked. 
2. Command can be automatically disabled based on a signal, and this disabled state can be represented in a UI by disabling any controls associated with the command

Cold Signal: Signals are typically lazy, meaning that they only do work and send signals when someone has subscribed to them. With each additional subscription, work is re-done. For trivial operations, this is acceptable, and in fect, desirable. 
Hot Signal : Sometimes we want work to be done immediately. This type of signal is called a hot signal. It's very rare to use a hot signal.
Signals by default are cold

Multicasting:
1. Signal: each new time a subscriber is added, its work is performed.
2. Multicast connection: subscribe to the signal that it's created with and when it's passed new values, sends those values through to the signal(which is exposed as a public property). You can subscribe to this signal as many as you want, and the work performed upon subscription is only done once.






