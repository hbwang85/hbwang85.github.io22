---
layout: post
title: "KVC &amp; KVO"
date: 2015-07-20 15:10:25 +0800
comments: true
categories: 
---

Key-Value Coding is a mechanism for accessing an object's properties indirectly, useing strings to identify properties, rather than through invocation of an accessor method or accessing them directly through instnce variable.

There are two basic forms of ccessor: get accessors and set accessors.

The essential methods for key-value coding are declared in the NSKeyValueCoding informal protocol and default implementations are provided by NSObject.

Key-value coding can be used to access three different types of object values:atrributes, to-one relationships and tomany relationships.The term property refers to any of these types of values.

We can get the value by invoking valueForKey:(valueForKeyPath). If there is no accessor or instance variable for the specified key, then the receiver sends itself a valueForUndefinedKey: message, and the default implementation of that message raises an NSUndefinedKeyException.

On the other hand, we can set the value of the specified key by invoking setValue: forKey:. If the specified key doesn't exist, the reveiver is sent a setValue:forUndefinedKey: message, and the message will raise an NSUndefinedKeyException.

Dot syntax and key-value coding: Using the dot syntax when you access a property; using key-value coding when you set a property.

Commonly used accessor method including: -<key>, set<Key>:
accessor methods for collection including: -countOf<key>, -objectIn<Key>AtIndex:; -insert<Key>:.