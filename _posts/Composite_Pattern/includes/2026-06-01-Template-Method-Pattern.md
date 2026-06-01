---
title: "模板方法模式（Template Method Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 模板方法模式]
author: wjj
toc: true
---

# 模板方法模式（Template Method Pattern）

## 模式定义

模板方法模式定义一个操作中的算法的骨架，而将一些步骤延迟到子类中。

## 原理详解

### 核心思想

模板方法模式的核心在于：
1. **算法骨架**：定义算法的结构
2. **可变步骤**：将可变步骤延迟到子类
3. **钩子方法**：提供可被子类覆盖的钩子
4. **复用**：复用不变的算法骨架

### 结构

```
AbstractClass (抽象类)
  + templateMethod(): void (模板方法)
  # step1(): void (抽象步骤)
  # step2(): void (抽象步骤)
  # hook(): void (钩子方法)

ConcreteClass (具体类)
  + step1(): void
  + step2(): void
  + hook(): void
```

### 模板方法调用流程

```
templateMethod()
  ├── step1()
  ├── step2()
  └── hook() // optional
```

---

## Java 实现

### 基础实现

```java
abstract class Game {
    public final void play() {
        initialize();
        startPlay();
        endPlay();
    }

    protected abstract void initialize();
    protected abstract void startPlay();
    protected abstract void endPlay();

    protected void hook() {
    }
}

class Cricket extends Game {
    @Override
    protected void initialize() {
        System.out.println("Cricket Game Initialized!");
    }

    @Override
    protected void startPlay() {
        System.out.println("Cricket Game Started!");
    }

    @Override
    protected void endPlay() {
        System.out.println("Cricket Game Finished!");
    }
}

class Football extends Game {
    @Override
    protected void initialize() {
        System.out.println("Football Game Initialized!");
    }

    @Override
    protected void startPlay() {
        System.out.println("Football Game Started!");
    }

    @Override
    protected void endPlay() {
        System.out.println("Football Game Finished!");
    }
}

public class TemplateMethodDemo {
    public static void main(String[] args) {
        Game cricket = new Cricket();
        cricket.play();

        System.out.println();

        Game football = new Football();
        football.play();
    }
}
```

### 带钩子方法的模板方法

```java
abstract class CaffeineBeverage {
    public final void prepareRecipe() {
        boilWater();
        brew();
        pourInCup();
        if (customerWantsCondiments()) {
            addCondiments();
        }
    }

    protected void boilWater() {
        System.out.println("Boiling water");
    }

    protected void pourInCup() {
        System.out.println("Pouring into cup");
    }

    protected abstract void brew();
    protected abstract void addCondiments();

    protected boolean customerWantsCondiments() {
        return true;
    }
}

class Coffee extends CaffeineBeverage {
    @Override
    protected void brew() {
        System.out.println("Dripping coffee through filter");
    }

    @Override
    protected void addCondiments() {
        System.out.println("Adding sugar and milk");
    }

    @Override
    protected boolean customerWantsCondiments() {
        return false;
    }
}

class Tea extends CaffeineBeverage {
    @Override
    protected void brew() {
        System.out.println("Steeping the tea");
    }

    @Override
    protected void addCondiments() {
        System.out.println("Adding lemon");
    }
}
```

---

## Python 实现

### 基础实现

```python
from abc import ABC, abstractmethod

class Game(ABC):
    def play(self):
        self.initialize()
        self.start_play()
        self.end_play()

    @abstractmethod
    def initialize(self):
        pass

    @abstractmethod
    def start_play(self):
        pass

    @abstractmethod
    def end_play(self):
        pass

class Cricket(Game):
    def initialize(self):
        print("Cricket Game Initialized!")

    def start_play(self):
        print("Cricket Game Started!")

    def end_play(self):
        print("Cricket Game Finished!")

class Football(Game):
    def initialize(self):
        print("Football Game Initialized!")

    def start_play(self):
        print("Football Game Started!")

    def end_play(self):
        print("Football Game Finished!")

if __name__ == "__main__":
    cricket = Cricket()
    cricket.play()

    print()

    football = Football()
    football.play()
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>
#include <memory>

class Game {
public:
    void play() {
        initialize();
        startPlay();
        endPlay();
    }

protected:
    virtual void initialize() = 0;
    virtual void startPlay() = 0;
    virtual void endPlay() = 0;
};

class Cricket : public Game {
protected:
    void initialize() override {
        std::cout << "Cricket Game Initialized!" << std::endl;
    }

    void startPlay() override {
        std::cout << "Cricket Game Started!" << std::endl;
    }

    void endPlay() override {
        std::cout << "Cricket Game Finished!" << std::endl;
    }
};

class Football : public Game {
protected:
    void initialize() override {
        std::cout << "Football Game Initialized!" << std::endl;
    }

    void startPlay() override {
        std::cout << "Football Game Started!" << std::endl;
    }

    void endPlay() override {
        std::cout << "Football Game Finished!" << std::endl;
    }
};

int main() {
    std::unique_ptr<Game> cricket = std::make_unique<Cricket>();
    cricket->play();

    std::cout << std::endl;

    std::unique_ptr<Game> football = std::make_unique<Football>();
    football->play();

    return 0;
}
```

---

## 应用场景

### 1. 框架
Spring、Hibernate 等框架的模板方法。

### 2. 数据处理
数据读取 → 处理 → 保存的流程。

### 3. 排序
定义排序流程，具体比较由子类实现。

### 4. 测试框架
JUnit 的测试方法执行流程。

---

## 优缺点分析

### 优点

1. **复用**：复用不变的算法骨架
2. **扩展性**：可变步骤由子类实现
3. **符合开闭原则**：扩展而不是修改
4. **简洁**：将复杂逻辑封装在父类

### 缺点

1. **类数量增加**：每个变体需要子类
2. **继承限制**：受限于继承结构
3. **维护困难**：层级过多时维护困难

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 模板方法 | 算法骨架复用 | 步骤复用 |
| 策略模式 | 算法可替换 | 算法灵活切换 |
| 工厂方法 | 子类决定创建 | 对象创建延迟 |
