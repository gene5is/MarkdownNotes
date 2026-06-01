---
title: "备忘录模式（Memento Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 备忘录模式]
author: wjj
toc: true
mermaid: true
---

# 备忘录模式（Memento Pattern）

## 模式定义

备忘录模式在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态。

## 原理详解

### 核心思想

备忘录模式的核心在于：
1. **状态保存**：保存对象的历史状态
2. **封装性**：保持对象内部状态的封装
3. **撤销恢复**：支持撤销和恢复操作
4. ** originator / caretaker / memento**：三方角色协作

### 结构

```
Originator ( originator )
  - state: State
  + createMemento(): Memento
  + restore(Memento): void

Memento (备忘录)
  - state: State
  + getState(): State
  + setState(State): void

Caretaker (负责人)
  - mementos: List<Memento>
  + addMemento(Memento): void
  + getMemento(index): Memento
```

### 角色职责

| 角色 | 职责 |
|------|------|
| Originator | 创建备忘录，恢复状态 |
| Memento | 存储 originator 的内部状态 |
| Caretaker | 保存备忘录，管理备忘录 |

---

## Java 实现

### 基础实现

```java
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }
}

class Originator {
    private String state;

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }

    public Memento createMemento() {
        return new Memento(state);
    }

    public void restore(Memento memento) {
        this.state = memento.getState();
    }
}

class Caretaker {
    private List<Memento> mementos = new ArrayList<>();

    public void addMemento(Memento memento) {
        mementos.add(memento);
    }

    public Memento getMemento(int index) {
        return mementos.get(index);
    }
}

public class MementoDemo {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        originator.setState("State 1");
        caretaker.addMemento(originator.createMemento());

        originator.setState("State 2");
        caretaker.addMemento(originator.createMemento());

        originator.setState("State 3");

        System.out.println("Current state: " + originator.getState());

        originator.restore(caretaker.getMemento(1));
        System.out.println("Restored state: " + originator.getState());

        originator.restore(caretaker.getMemento(0));
        System.out.println("Restored state: " + originator.getState());
    }
}
```

### 文本编辑器撤销

```java
class EditorMemento {
    private String content;

    public EditorMemento(String content) {
        this.content = content;
    }

    public String getContent() {
        return content;
    }
}

class Editor {
    private String content = "";

    public void type(String text) {
        content += text;
    }

    public String getContent() {
        return content;
    }

    public EditorMemento save() {
        return new EditorMemento(content);
    }

    public void restore(EditorMemento memento) {
        content = memento.getContent();
    }
}

class History {
    private List<EditorMemento> mementos = new ArrayList<>();

    public void push(EditorMemento memento) {
        mementos.add(memento);
    }

    public EditorMemento pop() {
        if (!mementos.isEmpty()) {
            return mementos.remove(mementos.size() - 1);
        }
        return null;
    }
}
```

---

## Python 实现

### 基础实现

```python
class Memento:
    def __init__(self, state):
        self._state = state

    @property
    def state(self):
        return self._state

class Originator:
    def __init__(self):
        self._state = None

    @property
    def state(self):
        return self._state

    @state.setter
    def state(self, value):
        self._state = value

    def create_memento(self):
        return Memento(self._state)

    def restore(self, memento):
        self._state = memento.state

class Caretaker:
    def __init__(self):
        self._mementos = []

    def add_memento(self, memento):
        self._mementos.append(memento)

    def get_memento(self, index):
        return self._mementos[index]

if __name__ == "__main__":
    originator = Originator()
    caretaker = Caretaker()

    originator.state = "State 1"
    caretaker.add_memento(originator.create_memento())

    originator.state = "State 2"
    caretaker.add_memento(originator.create_memento())

    originator.state = "State 3"

    print(f"Current state: {originator.state}")

    originator.restore(caretaker.get_memento(1))
    print(f"Restored state: {originator.state}")
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <memory>

class Memento {
private:
    std::string state;

public:
    Memento(const std::string& state) : state(state) {}

    std::string getState() const {
        return state;
    }
};

class Originator {
private:
    std::string state;

public:
    std::string getState() const {
        return state;
    }

    void setState(const std::string& state) {
        this->state = state;
    }

    std::unique_ptr<Memento> createMemento() {
        return std::make_unique<Memento>(state);
    }

    void restore(std::unique_ptr<Memento> memento) {
        state = memento->getState();
    }
};

class Caretaker {
private:
    std::vector<std::unique_ptr<Memento>> mementos;

public:
    void addMemento(std::unique_ptr<Memento> memento) {
        mementos.push_back(std::move(memento));
    }

    std::unique_ptr<Memento> getMemento(size_t index) {
        if (index < mementos.size()) {
            return std::move(mementos[index]);
        }
        return nullptr;
    }
};

int main() {
    Originator originator;
    Caretaker caretaker;

    originator.setState("State 1");
    caretaker.addMemento(originator.createMemento());

    originator.setState("State 2");
    caretaker.addMemento(originator.createMemento());

    originator.setState("State 3");

    std::cout << "Current state: " << originator.getState() << std::endl;

    originator.restore(caretaker.getMemento(1));
    std::cout << "Restored state: " << originator.getState() << std::endl;

    originator.restore(caretaker.getMemento(0));
    std::cout << "Restored state: " << originator.getState() << std::endl;

    return 0;
}
```

---

## 应用场景

### 1. 文本编辑器
撤销/重做功能。

### 2. 数据库事务
事务回滚。

### 3. 游戏存档
游戏进度保存与恢复。

### 4. 命令模式
支持撤销的命令实现。

---

## 优缺点分析

### 优点

1. **封装性**：保持对象内部状态的封装
2. **撤销恢复**：支持撤销和恢复操作
3. **简化 originator**：状态保存由 caretaker 管理

### 缺点

1. **内存占用**：保存大量状态可能占用内存
2. **复杂性**：需要维护备忘录的生命周期
3. **性能问题**：频繁保存状态可能影响性能

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 备忘录模式 | 状态保存恢复 | 支持撤销 |
| 命令模式 | 请求封装 | 支持撤销 |
| 迭代器模式 | 顺序访问 | 遍历聚合对象 |
