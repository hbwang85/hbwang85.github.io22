---
layout: post
title: "Test Driven Development"
date: 2015-07-19 07:49:13 +0800
comments: true
categories: 
---

可运行的简洁代码是关于“测试驱动开发”（TDD）目标的精辟概括。 TDD带给我们前所未有的好处：
1. 仅当自动化测试失败的时候才需要编写新的代码；
2. 可以以TDD为依据进行重构，去掉重复的代码；
3. 自动化测试可以作为help manual， 代码中不再需要过多的注释。

当然，它也有弊端：
1. 必须developer自己写测试；
2. 我们的设计必须遵循高内聚、低耦合的原则，否则不便于测试；
3. 快速响应，实时的维护自动化测试；

TDD的经典三部曲
1. 红色指示条：根据需求编写一个测试，当然此时这个测试无法通过编译；
2. 绿色指示条：编写代码，使测试通过，这个过程可谓想方设法，可谓不择手段；
3. 重构： 去除单纯由于使测试通过的重复部分。

3A
编写测试时可以遵循以下3个步骤：
Build: 创建对象，我们希望每个测试在执行之前都执行此步；
Operation： 执行测试；
Check：验证结果。

这样的模式又带来两个问题：
1. 性能：如果众多测试中使用类似的对象，我们希望对象只被创建一次；
2. 测试隔离：每个测试的通过与否都不应该与其他测试相关。这样，如果每个对象都只被创建了一次，其中一个测试改变了对象，它必然影响其他测试。
在xUnit框架中，每个测试在执行前都会调用setup()方法创建对象，执行结束后调用teardown()方法释放对象。

要TDD我们应该怎么做：
1. 维护一张测试列表，根据需求制定并维护一张测试列表；
2. 测试优先， 在编写代码前先编写测试；
3. 显示数据，测试中避免使用magic number；