---
title: "策略模式（Strategy Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 策略模式]
author: wjj
toc: true
mermaid: true
---

# 策略模式（Strategy Pattern）

## 模式定义

策略模式定义一系列算法，把它们一个个封装起来，并且使它们可相互替换。

## 原理详解

### 核心思想

策略模式的核心在于：
1. **算法封装**：将每个算法封装为独立的策略类
2. **可替换**：策略可以动态切换
3. **解耦**：将使用算法的代码与算法实现解耦
4. **扩展性**：新增算法无需修改已有代码

### 结构

```
Context (上下文)
  - strategy: Strategy
  + setStrategy(Strategy): void
  + execute(): void

Strategy (抽象策略)
  + algorithm(): void

ConcreteStrategyA
  + algorithm(): void

ConcreteStrategyB
  + algorithm(): void
```

### 与状态模式对比

| 对比项 | 策略模式 | 状态模式 |
|--------|----------|----------|
| 客户端 | 主动选择策略 | 被动状态转换 |
| 切换方式 | 显式设置 | 自动转换 |
| 上下文依赖 | 不依赖 | 依赖 |
| 复杂度 | 较简单 | 较复杂 |

---

## Java 实现

### 基础实现

```java
interface Strategy {
    int execute(int a, int b);
}

class AddStrategy implements Strategy {
    @Override
    public int execute(int a, int b) {
        return a + b;
    }
}

class MultiplyStrategy implements Strategy {
    @Override
    public int execute(int a, int b) {
        return a * b;
    }
}

class SubtractStrategy implements Strategy {
    @Override
    public int execute(int a, int b) {
        return a - b;
    }
}

class Context {
    private Strategy strategy;

    public Context(Strategy strategy) {
        this.strategy = strategy;
    }

    public void setStrategy(Strategy strategy) {
        this.strategy = strategy;
    }

    public int executeStrategy(int a, int b) {
        return strategy.execute(a, b);
    }
}

public class StrategyDemo {
    public static void main(String[] args) {
        Context context = new Context(new AddStrategy());
        System.out.println("10 + 5 = " + context.executeStrategy(10, 5));

        context.setStrategy(new MultiplyStrategy());
        System.out.println("10 * 5 = " + context.executeStrategy(10, 5));

        context.setStrategy(new SubtractStrategy());
        System.out.println("10 - 5 = " + context.executeStrategy(10, 5));
    }
}
```

### 支付系统

```java
interface PaymentStrategy {
    boolean pay(double amount);
}

class CreditCardPayment implements PaymentStrategy {
    private String cardNumber;

    public CreditCardPayment(String cardNumber) {
        this.cardNumber = cardNumber;
    }

    @Override
    public boolean pay(double amount) {
        System.out.println("Paid " + amount + " with Credit Card: " + cardNumber);
        return true;
    }
}

class PayPalPayment implements PaymentStrategy {
    private String email;

    public PayPalPayment(String email) {
        this.email = email;
    }

    @Override
    public boolean pay(double amount) {
        System.out.println("Paid " + amount + " with PayPal: " + email);
        return true;
    }
}

class BitcoinPayment implements PaymentStrategy {
    private String walletAddress;

    public BitcoinPayment(String walletAddress) {
        this.walletAddress = walletAddress;
    }

    @Override
    public boolean pay(double amount) {
        System.out.println("Paid " + amount + " with Bitcoin: " + walletAddress);
        return true;
    }
}

class ShoppingCart {
    private List<Item> items = new ArrayList<>();

    public void addItem(Item item) {
        items.add(item);
    }

    public double getTotal() {
        return items.stream().mapToDouble(Item::getPrice).sum();
    }

    public boolean pay(PaymentStrategy strategy) {
        return strategy.pay(getTotal());
    }
}
```

---

## Python 实现

### 基础实现

```python
from abc import ABC, abstractmethod

class Strategy(ABC):
    @abstractmethod
    def execute(self, a, b):
        pass

class AddStrategy(Strategy):
    def execute(self, a, b):
        return a + b

class MultiplyStrategy(Strategy):
    def execute(self, a, b):
        return a * b

class SubtractStrategy(Strategy):
    def execute(self, a, b):
        return a - b

class Context:
    def __init__(self, strategy):
        self._strategy = strategy

    @property
    def strategy(self):
        return self._strategy

    @strategy.setter
    def strategy(self, strategy):
        self._strategy = strategy

    def execute_strategy(self, a, b):
        return self._strategy.execute(a, b)

if __name__ == "__main__":
    context = Context(AddStrategy())
    print(f"10 + 5 = {context.execute_strategy(10, 5)}")

    context.strategy = MultiplyStrategy()
    print(f"10 * 5 = {context.execute_strategy(10, 5)}")
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>

class Strategy {
public:
    virtual ~Strategy() = default;
    virtual int execute(int a, int b) = 0;
};

class AddStrategy : public Strategy {
public:
    int execute(int a, int b) override {
        return a + b;
    }
};

class MultiplyStrategy : public Strategy {
public:
    int execute(int a, int b) override {
        return a * b;
    }
};

class SubtractStrategy : public Strategy {
public:
    int execute(int a, int b) override {
        return a - b;
    }
};

class Context {
private:
    Strategy* strategy;

public:
    Context(Strategy* strategy) : strategy(strategy) {}

    void setStrategy(Strategy* strategy) {
        this->strategy = strategy;
    }

    int executeStrategy(int a, int b) {
        return strategy->execute(a, b);
    }
};

int main() {
    Context context(new AddStrategy());
    std::cout << "10 + 5 = " << context.executeStrategy(10, 5) << std::endl;

    context.setStrategy(new MultiplyStrategy());
    std::cout << "10 * 5 = " << context.executeStrategy(10, 5) << std::endl;

    context.setStrategy(new SubtractStrategy());
    std::cout << "10 - 5 = " << context.executeStrategy(10, 5) << std::endl;

    return 0;
}
```

---

## 应用场景

### 1. 排序算法
不同排序策略的选择。

### 2. 支付方式
支付宝、微信、信用卡等。

### 3. 压缩算法
ZIP、RAR、7z 等压缩方式。

### 4. 路由算法
最短路径、最小费用等。

### 5. 验证策略
不同输入的不同验证规则。

---

## 优缺点分析

### 优点

1. **算法切换**：可以动态切换算法
2. **解耦**：算法与使用代码解耦
3. **扩展性**：新增算法无需修改已有代码
4. **复用**：相同算法可以在不同地方复用

### 缺点

1. **类数量增加**：每个算法都需要一个类
2. **客户端知情**：客户端需要了解所有策略
3. **性能开销**：策略模式可能增加系统开销

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 策略模式 | 算法可替换 | 算法灵活切换 |
| 状态模式 | 状态决定行为 | 状态自动转换 |
| 模板方法 | 算法骨架复用 | 步骤复用 |
| 命令模式 | 请求封装 | 请求参数化 |
