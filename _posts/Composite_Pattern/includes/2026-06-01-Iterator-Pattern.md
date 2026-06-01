---
title: "迭代器模式（Iterator Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 迭代器模式]
author: wjj
toc: true
mermaid: true
---

# 迭代器模式（Iterator Pattern）

## 模式定义

迭代器模式提供一种方法顺序访问一个聚合对象中各个元素，而又无需暴露该对象的内部表示。

## 原理详解

### 核心思想

迭代器模式的核心在于：
1. **顺序访问**：提供统一的遍历接口
2. **封装遍历**：将遍历逻辑从聚合对象中分离
3. **多种遍历**：可以定义多种遍历方式
4. **解耦**：客户端与聚合对象解耦

### 结构

```
Iterator (抽象迭代器)
  + hasNext(): boolean
  + next(): Object

ConcreteIterator (具体迭代器)
  - aggregate: Aggregate
  - current: int
  + hasNext(): boolean
  + next(): Object

Aggregate (抽象聚合)
  + createIterator(): Iterator

ConcreteAggregate (具体聚合)
  + createIterator(): Iterator
```

### 内迭代器 vs 外迭代器

| 类型 | 特点 | 说明 |
|------|------|------|
| 外迭代器 | 客户端控制遍历 | 遍历由客户端控制 |
| 内迭代器 | 聚合对象控制遍历 | 遍历由聚合对象控制 |

---

## Java 实现

### 基础实现

```java
interface Iterator<T> {
    boolean hasNext();
    T next();
}

interface Aggregate<T> {
    Iterator<T> createIterator();
}

class ConcreteAggregate<T> implements Aggregate<T> {
    private List<T> items = new ArrayList<>();

    public void add(T item) {
        items.add(item);
    }

    public T get(int index) {
        return items.get(index);
    }

    public int size() {
        return items.size();
    }

    @Override
    public Iterator<T> createIterator() {
        return new ConcreteIterator<>(this);
    }
}

class ConcreteIterator<T> implements Iterator<T> {
    private ConcreteAggregate<T> aggregate;
    private int current = 0;

    public ConcreteIterator(ConcreteAggregate<T> aggregate) {
        this.aggregate = aggregate;
    }

    @Override
    public boolean hasNext() {
        return current < aggregate.size();
    }

    @Override
    public T next() {
        return aggregate.get(current++);
    }
}

public class IteratorDemo {
    public static void main(String[] args) {
        ConcreteAggregate<String> aggregate = new ConcreteAggregate<>();
        aggregate.add("Item 1");
        aggregate.add("Item 2");
        aggregate.add("Item 3");

        Iterator<String> iterator = aggregate.createIterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

### 使用 Java 内置迭代器

```java
List<String> list = Arrays.asList("A", "B", "C");
Iterator<String> iterator = list.iterator();

while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

### 反向迭代器

```java
class ReverseIterator<T> implements Iterator<T> {
    private List<T> items;
    private int current;

    public ReverseIterator(List<T> items) {
        this.items = items;
        this.current = items.size() - 1;
    }

    @Override
    public boolean hasNext() {
        return current >= 0;
    }

    @Override
    public T next() {
        return items.get(current--);
    }
}
```

---

## Python 实现

### 基础实现

```python
from abc import ABC, abstractmethod

class Iterator(ABC):
    @abstractmethod
    def has_next(self):
        pass

    @abstractmethod
    def next(self):
        pass

class Aggregate(ABC):
    @abstractmethod
    def create_iterator(self):
        pass

class ConcreteAggregate(Aggregate):
    def __init__(self):
        self._items = []

    def add(self, item):
        self._items.append(item)

    def get(self, index):
        return self._items[index]

    def size(self):
        return len(self._items)

    def create_iterator(self):
        return ConcreteIterator(self)

class ConcreteIterator(Iterator):
    def __init__(self, aggregate):
        self._aggregate = aggregate
        self._current = 0

    def has_next(self):
        return self._current < self._aggregate.size()

    def next(self):
        item = self._aggregate.get(self._current)
        self._current += 1
        return item

if __name__ == "__main__":
    aggregate = ConcreteAggregate()
    aggregate.add("Item 1")
    aggregate.add("Item 2")
    aggregate.add("Item 3")

    iterator = aggregate.create_iterator()
    while iterator.has_next():
        print(iterator.next())
```

### Python 风格实现

```python
class ConcreteAggregate:
    def __init__(self):
        self._items = []

    def add(self, item):
        self._items.append(item)

    def __iter__(self):
        return iter(self._items)

if __name__ == "__main__":
    aggregate = ConcreteAggregate()
    aggregate.add("Item 1")
    aggregate.add("Item 2")
    aggregate.add("Item 3")

    for item in aggregate:
        print(item)
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>
#include <vector>
#include <memory>

template<typename T>
class Iterator {
public:
    virtual ~Iterator() = default;
    virtual bool hasNext() = 0;
    virtual T next() = 0;
};

template<typename T>
class Aggregate {
public:
    virtual ~Aggregate() = default;
    virtual std::unique_ptr<Iterator<T>> createIterator() = 0;
    virtual T get(size_t index) = 0;
    virtual size_t size() = 0;
};

template<typename T>
class ConcreteAggregate : public Aggregate<T> {
private:
    std::vector<T> items;

public:
    void add(const T& item) {
        items.push_back(item);
    }

    T get(size_t index) override {
        return items.at(index);
    }

    size_t size() override {
        return items.size();
    }

    std::unique_ptr<Iterator<T>> createIterator() override;
};

template<typename T>
class ConcreteIterator : public Iterator<T> {
private:
    ConcreteAggregate<T>* aggregate;
    size_t current = 0;

public:
    ConcreteIterator(ConcreteAggregate<T>* aggregate)
        : aggregate(aggregate) {}

    bool hasNext() override {
        return current < aggregate->size();
    }

    T next() override {
        return aggregate->get(current++);
    }
};

template<typename T>
std::unique_ptr<Iterator<T>> ConcreteAggregate<T>::createIterator() {
    return std::make_unique<ConcreteIterator<T>>(this);
}

int main() {
    ConcreteAggregate<std::string> aggregate;
    aggregate.add("Item 1");
    aggregate.add("Item 2");
    aggregate.add("Item 3");

    auto iterator = aggregate.createIterator();
    while (iterator->hasNext()) {
        std::cout << iterator->next() << std::endl;
    }

    return 0;
}
```

---

## 应用场景

### 1. 集合遍历
Java Collection Framework、STL 容器。

### 2. 数据库游标
结果集遍历。

### 3. 文件遍历
目录文件列表。

### 4. DOM 遍历
XML/HTML DOM 树遍历。

---

## 优缺点分析

### 优点

1. **单一职责**：将遍历逻辑分离出来
2. **开闭原则**：可以新增聚合和迭代器
3. **灵活遍历**：可以定义多种遍历方式
4. **解耦**：客户端与聚合对象解耦

### 缺点

1. **类数量增加**：需要为每个聚合创建迭代器
2. **过度设计**：简单场景可能不需要

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 迭代器模式 | 顺序访问 | 遍历聚合对象 |
| 组合模式 | 树形结构 | 构建对象树 |
| 访问者模式 | 操作封装 | 操作与数据分离 |
