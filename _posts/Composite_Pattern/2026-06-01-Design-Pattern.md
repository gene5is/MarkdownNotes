---
title: "设计模式"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式]
tags: [设计模式]
author: wjj
toc: true
mermaid: true
---

# 设计模式

本笔记详细介绍了 GoF（Gang of Four）提出的 23 种经典设计模式，涵盖创建型、结构型和行为型三大类别。每个模式都包含原理详解、Java/Python/C++ 多语言实现、应用场景以及优缺点分析。

## 目录

### 一、创建型模式（Creational Patterns）

创建型模式关注对象的创建机制，封装对象实例化的细节，使系统独立于其组件的创建方式。

1. [单例模式（Singleton Pattern）]({% post_url 2026-06-01-Singleton-Pattern %})
   - Ensure a class only has one instance, and provide a global point of access to it.
   - 确保某个类只有一个实例，并提供一个全局访问点。

2. [工厂方法模式（Factory Method Pattern）]({% post_url 2026-06-01-Factory-Method-Pattern %})
   - Define an interface for creating an object, but let subclasses decide which class to instantiate.
   - 定义一个创建对象的接口，让子类决定实例化哪个类。

3. [抽象工厂模式（Abstract Factory Pattern）]({% post_url 2026-06-01-Abstract-Factory-Pattern %})
   - Provide an interface for creating families of related or dependent objects without specifying their concrete classes.
   - 提供一个创建一系列相关或相互依赖对象的接口，而无需指定它们具体的类。

4. [建造者模式（Builder Pattern）]({% post_url 2026-06-01-Builder-Pattern %})
   - Separate the construction of a complex object from its representation.
   - 将一个复杂对象的构建与它的表示分离。

5. [原型模式（Prototype Pattern）]({% post_url 2026-06-01-Prototype-Pattern %})
   - Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.
   - 用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。

### 二、结构型模式（Structural Patterns）

结构型模式关注对象和类的组合，通过继承和组合来创建更大结构。

6. [组合模式（Composite Pattern）]({% post_url 2026-06-01-Composite-Pattern %})
   - Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.
   - 将对象组合成树形结构以表示"部分-整体"的层次结构。组合模式使得用户对单个对象和组合对象的使用具有一致性。

7. [适配器模式（Adapter Pattern）]({% post_url 2026-06-01-Adapter-Pattern %})
   - Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.
   - 将一个类的接口转换成客户希望的另外一个接口。适配器模式使得原本由于接口不兼容而不能一起工作的那些类可以一起工作。

8. [装饰器模式（Decorator Pattern）]({% post_url 2026-06-01-Decorator-Pattern %})
   - Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to subclassing for extending functionality.
   - 动态地给一个对象添加一些额外的职责。就增加功能来说，装饰器模式相比生成子类更为灵活。

9. [代理模式（Proxy Pattern）]({% post_url 2026-06-01-Proxy-Pattern %})
   - Provide a surrogate or placeholder for another object to control access to it.
   - 为其他对象提供一种代理以控制对这个对象的访问。

10. [桥接模式（Bridge Pattern）]({% post_url 2026-06-01-Bridge-Pattern %})
    - Decouple an abstraction from its implementation so that the two can vary independently.
    - 将抽象部分与它的实现部分分离，使它们都可以独立地变化。

11. [外观模式（Facade Pattern）]({% post_url 2026-06-01-Facade-Pattern %})
    - Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.
    - 为子系统中的一组接口提供一个一致的界面，外观模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。

12. [享元模式（Flyweight Pattern）]({% post_url 2026-06-01-Flyweight-Pattern %})
    - Use sharing to support large numbers of fine-grained objects efficiently.
    - 运用共享技术有效地支持大量细粒度的对象。

### 三、行为型模式（Behavioral Patterns）

行为型模式关注对象之间的通信和职责分配。

13. [观察者模式（Observer Pattern）]({% post_url 2026-06-01-Observer-Pattern %})
    - Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
    - 定义对象间的一种一对多的依赖关系，当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并被自动更新。

14. [策略模式（Strategy Pattern）]({% post_url 2026-06-01-Strategy-Pattern %})
    - Define a family of algorithms, encapsulate each one, and make them interchangeable.
    - 定义一系列的算法,把它们一个个封装起来, 并且使它们可相互替换。

15. [命令模式（Command Pattern）]({% post_url 2026-06-01-Command-Pattern %})
    - Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.
    - 将一个请求封装为一个对象，从而使你可用不同的请求对客户进行参数化；对请求排队或记录请求日志，以及支持可撤销的操作。

16. [迭代器模式（Iterator Pattern）]({% post_url 2026-06-01-Iterator-Pattern %})
    - Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
    - 提供一种方法顺序访问一个聚合对象中各个元素，而又无需暴露该对象的内部表示。

17. [模板方法模式（Template Method Pattern）]({% post_url 2026-06-01-Template-Method-Pattern %})
    - Define the skeleton of an algorithm in an operation, deferring some steps to subclasses.
    - 定义一个操作中的算法的骨架，而将一些步骤延迟到子类中。

18. [状态模式（State Pattern）]({% post_url 2026-06-01-State-Pattern %})
    - Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.
    - 允许对象在其内部状态改变时改变它的行为。对象看起来似乎修改了它的类。

19. [责任链模式（Chain of Responsibility Pattern）]({% post_url 2026-06-01-Chain-of-Responsibility-Pattern %})
    - Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request.
    - 使多个对象都有机会处理请求，从而避免请求的发送者和接收者之间的耦合关系。

20. [中介者模式（Mediator Pattern）]({% post_url 2026-06-01-Mediator-Pattern %})
    - Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly.
    - 用一个中介对象来封装一系列的对象交互。中介者使各对象不需要显式地相互引用，从而使其耦合松散。

21. [访问者模式（Visitor Pattern）]({% post_url 2026-06-01-Visitor-Pattern %})
    - Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.
    - 表示一个作用于某对象结构中的各元素的操作。访问者模式使你可以在不改变各元素的类的前提下定义作用于这些元素的新操作。

22. [备忘录模式（Memento Pattern）]({% post_url 2026-06-01-Memento-Pattern %})
    - Without violating encapsulation, capture and externalize an object's internal state so that the object can be restored to this state later.
    - 在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。

23. [解释器模式（Interpreter Pattern）]({% post_url 2026-06-01-Interpreter-Pattern %})
    - Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.
    - 给定一个语言，定义它的文法的一种表示，并定义一个解释器，该解释器使用该表示来解释语言中的句子。

---

## 设计模式分类总览

| 类别 | 模式名称 | 核心意图 |
|------|----------|----------|
| **创建型** | 单例模式 | 保证唯一实例 |
| **创建型** | 工厂方法 | 子类决定创建 |
| **创建型** | 抽象工厂 | 创建产品族 |
| **创建型** | 建造者模式 | 分离构建表示 |
| **创建型** | 原型模式 | 克隆获取实例 |
| **结构型** | 组合模式 | 树形整体部分 |
| **结构型** | 适配器模式 | 接口转换 |
| **结构型** | 装饰器模式 | 动态添加职责 |
| **结构型** | 代理模式 | 间接访问控制 |
| **结构型** | 桥接模式 | 抽象实现分离 |
| **结构型** | 外观模式 | 统一接口简化 |
| **结构型** | 享元模式 | 共享高效细粒 |
| **行为型** | 观察者模式 | 一对多通知 |
| **行为型** | 策略模式 | 算法可替换 |
| **行为型** | 命令模式 | 请求封装为对象 |
| **行为型** | 迭代器模式 | 顺序访问聚合 |
| **行为型** | 模板方法 | 算法骨架复用 |
| **行为型** | 状态模式 | 状态决定行为 |
| **行为型** | 责任链模式 | 链式处理请求 |
| **行为型** | 中介者模式 | 对象间接交互 |
| **行为型** | 访问者模式 | 操作与数据分离 |
| **行为型** | 备忘录模式 | 状态保存恢复 |
| **行为型** | 解释器模式 | 语法解释执行 |

---

## 参考资料

- Erich Gamma, Richard Helm, Ralph Johnson, John Vlissides. *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley, 1994.
- Robert C. Martin. *Agile Software Development, Principles, Patterns, and Practices*. Prentice Hall, 2002.
