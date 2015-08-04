---
layout: post
title: "KVC"
date: 2015-07-20 15:10:25 +0800
comments: true
categories: 
---

##Background

KVC is a fundamental technology when working with key-value observing, Cocoa bindings, Core Data and making your application AppleScript-able. It's really powerful, But few know about the detail. Especially for the collection operators. As part of KVC, collection operators help make many routine tasks simple.
<!--more--> 

##KVC Fundament  

Key-Value Coding is a mechanism for accessing an object's properties indirectly, using strings to identify properties, rather than through invocation of an accessor method or accessing them directly through instance variable. It is a fundamental technology when working with key-value observing, Cocoa bindings, Core Data and making your application AppleScript-able.  

Simply We can get the value by invoking valueForKey:(valueForKeyPath). If there is no accessor or instance variable for the specified key, then the receiver sends itself a valueForUndefinedKey: message, and the default implementation of that message raises an NSUndefinedKeyException.  

On the other hand, we can set the value of the specified key by invoking setValue: forKey:. If the specified key doesn't exist, the reveiver is sent a setValue:forUndefinedKey: message, and the message will raise an NSUndefinedKeyException.  

The essential methods for key-value coding are declared in the NSKeyValueCoding Objective-C informal protocol and default implementations are provided by NSObject.  

Key-value coding supports properties with object values, as well as the scalar types and structs. Non-object parameters and return types are detected and automatically wrapped, and unwrapped.   

For scalar types, the instances will be wrapped to NSNumber instances，
{% img center /images/kvc/scalar1.png %}
{% img center /images/kvc/scalar2.png %}  
  
For Struct，the instances will be wrapped as NSValue instances. Remember that NSValue and NSNumber both are inheritated from NSObject.  
{% img center /images/kvc/struct.png %}

when you access a property using the dot syntax, you invoke the receiver's standard accessor methods.  

##Collection Operators  

Collection operators allow actions to be performed on the items of a collection using key path notation and an action operator. This article describes the available collection operators, example key paths, and the results they’d produce. The format is as below:

{% img center /images/kvc/collection_operators_format.png %}


Collection operators are specialized key paths that are passed as the parameter to the valueForKeyPath: method. The operator is specified by a string preceded by an at sign (@). The key path on the left side of the collection operator, if present, determines the array or set, relative to the receiver, that is used in the operation. The key path on the right side of the operator specifies the property of the collection that the operator uses. Figure 1 illustrates the operator key path format.  

We can use it as below:  
```  
[object valueForKeyPath:@"<keypathToCollection>.<@collectionOperator>.<keypathToProperty>"];
```

This is the same as :
```
[[object valueForKeyPath:@"<keypathToCollection>"] valueForKeyPath:@"<@collectionOperators>.<keypathToProperty>"];

```

The obvious advantage is their consicion, but the big disadvantage is that we don’t get compile-time errors when we misuse them and nor do we get code-completion  

Collection Operators can be devided to 3 kinds:

###Simple Colletion Operators
> @avg    
> @max  
> @min   
> @sum  
> @count

Note:  
1. If you'd like to call @max or @min, the compared property objects must support comparison with each other;  
2. For the @count, the keypath to the right of the operator is ignored. And the difference between @count and count method are as below:  
```
[@[@"a",@"b"] count]
    // -> 2
[@[@"a",@"b"] valueForKey:@"@count"]
    // -> @(2)

```  

###Object Operators  
> @distinctUnionOfObjects  
> @unionOfObjects

Note:  
1. @unionOfObjects, is basically useless,   
```
[object valueForKeypath:@"@unionOfObjects.<keypathToProperty>"];  
```
is exactly the same as :  
```
[object valueForKey:@"<keypathToProperty>"];
```

###Array and Set Operators
> @unionOfArray  
> @distinctUnionOfArrays  
> @distinctUnionOfSet

###KVC + self = perfect  
You can use self as the <keypathToProperty>. for example, if you'd like to flatten a array as below:
```
[@[@[@(1),@(2),@(3)]] valueForKeyPath:@"@unionOfArray.self"];
       // @[@(1),@(2),@(3)]
``` 
If the wrap lever is more than one, e.g. 2, you can flatten it as below:  
```
[@[@[@[@(1),@(2),@(3)]]] valueForKeyPath:@"@unionOfArray.self.@unionOfArray.self"];
       // @[@(1),@(2),@(3)]
       // the first "@unionOfArray.self" is used as <keypathToCollection>
```

##Reference
1. Key-Value Coding Programming Guide  
2. http://bou.io/KVCCustomOperators.html  
