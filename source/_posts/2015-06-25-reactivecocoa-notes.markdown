---
layout: post
title: "ReactiveCocoa Notes"
date: 2015-06-25 15:10:35 +0800
comments: true
categories: 
---

##Background  
ReactiveCocoa (RAC) is an Objective-C framework inspired by Functional Reactive Programming. It provides APIs for composing and transforming streams of values.  
<!--more-->

##Structure
{% img center /images/rac/structure.png %}
Remember that any instance should be wrapped to NSObject in RAC.

##Feature
1. RAC provides signals (represented by RACSignal) that capture present and future values  
> subscribeNext  
> subscribeError  
> subscribeCompleted  

2. It provides a single, unified approach to dealing with asynchronous behaviors, including delegate methods, callback blocks, target-action mechanisms, notifications, and KVO.  

3. By chaining, combining, and reacting to signals, software can be written declaratively, without the need for code that continually observes and updates values.
{% img center /images/rac/enable.png %}

##Macros
RAC(Object, keypath): It performs a one-way binding of the right-hand value of the expression to the key path in question. Values must be NSObjects
RACObserve(Object, keypath)

##Functions

map: takes a list and return it into another list of the same length, "mapping" each value in the original list into a new value in the resulting list.    

reduceEach: Unpacks each RACTuple in the receiver and maps the values to a new value  

filter: Filtering a list just returns a new list containing all of the original entries, minus the entries that didn't return true from a test.  
  
flattenMap:Maps `block` across the values in the receiver and flattens the result.

##RACCommend
1. Create and subscribe to a signal in response to some action. Usually the action trigging a command is UI-driven, like when a button is clicked. 
2. Command can be automatically disabled based on a signal, and this disabled state can be represented in a UI by disabling any controls associated with the command

Cold Signal: Signals are typically lazy, meaning that they only do work and send signals when someone has subscribed to them. With each additional subscription, work is re-done. For trivial operations, this is acceptable, and in fect, desirable. 

Hot Signal : Sometimes we want work to be done immediately. This type of signal is called a hot signal. It's very rare to use a hot signal.
Signals by default are cold

Multicasting:
1. Signal: each new time a subscriber is added, its work is performed.
2. Multicast connection: subscribe to the signal that it's created with and when it's passed new values, sends those values through to the signal(which is exposed as a public property). You can subscribe to this signal as many as you want, and the work performed upon subscription is only done once.

RACScheduler: used to control when and where work is performed

Subscriptions: made on signals. when you want to be notified that a new value is sent(either next, error or completion).




