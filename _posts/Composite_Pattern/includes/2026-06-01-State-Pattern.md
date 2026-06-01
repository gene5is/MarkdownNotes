---
title: "状态模式（State Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 状态模式]
author: wjj
toc: true
---

# 状态模式（State Pattern）

## 模式定义

状态模式允许对象在其内部状态改变时改变它的行为。对象看起来似乎修改了它的类。

## 原理详解

### 核心思想

状态模式的核心在于：
1. **状态决定行为**：对象行为由内部状态决定
2. **状态转换**：状态之间可以相互转换
3. **消除条件**：消除大量 if-else/switch 语句
4. **封装状态**：每个状态封装为独立类

### 结构

```
Context (上下文)
  - state: State
  + request(): void
  + setState(State): void

State (抽象状态)
  + handle(): void

ConcreteStateA (具体状态A)
  + handle(): void
  + handle(context): void (可转换状态)

ConcreteStateB (具体状态B)
  + handle(): void
  + handle(context): void (可转换状态)
```

### 与策略模式对比

| 对比项 | 状态模式 | 策略模式 |
|--------|----------|----------|
| 客户端 | 无需知道状态 | 需要选择策略 |
| 状态转换 | 自动进行 | 外部控制 |
| 上下文依赖 | 状态依赖上下文 | 策略不依赖 |
| 数量 | 通常有限 | 可以很多 |

---

## Java 实现

### 基础实现

```java
interface State {
    void handle(Context context);
}

class Context {
    private State state;

    public Context(State state) {
        this.state = state;
    }

    public void setState(State state) {
        this.state = state;
    }

    public State getState() {
        return state;
    }

    public void request() {
        state.handle(this);
    }
}

class ConcreteStateA implements State {
    @Override
    public void handle(Context context) {
        System.out.println("State A handling, transitioning to State B");
        context.setState(new ConcreteStateB());
    }
}

class ConcreteStateB implements State {
    @Override
    public void handle(Context context) {
        System.out.println("State B handling, transitioning to State A");
        context.setState(new ConcreteStateA());
    }
}

public class StateDemo {
    public static void main(String[] args) {
        Context context = new Context(new ConcreteStateA());

        context.request();
        context.request();
        context.request();
    }
}
```

### 订单状态管理

```java
interface OrderState {
    void pay(Order order);
    void ship(Order order);
    void deliver(Order order);
    void cancel(Order order);
}

class Order {
    private OrderState state;
    private String orderId;

    public Order(String orderId) {
        this.orderId = orderId;
        this.state = new PendingState();
    }

    public void setState(OrderState state) {
        this.state = state;
    }

    public void pay() {
        state.pay(this);
    }

    public void ship() {
        state.ship(this);
    }

    public void deliver() {
        state.deliver(this);
    }

    public void cancel() {
        state.cancel(this);
    }

    public String getOrderId() {
        return orderId;
    }
}

class PendingState implements OrderState {
    @Override
    public void pay(Order order) {
        System.out.println("Payment received for order: " + order.getOrderId());
        order.setState(new PaidState());
    }

    @Override
    public void ship(Order order) {
        System.out.println("Cannot ship unpaid order");
    }

    @Override
    public void deliver(Order order) {
        System.out.println("Cannot deliver unpaid order");
    }

    @Override
    public void cancel(Order order) {
        System.out.println("Order cancelled: " + order.getOrderId());
        order.setState(new CancelledState());
    }
}

class PaidState implements OrderState {
    @Override
    public void pay(Order order) {
        System.out.println("Order already paid");
    }

    @Override
    public void ship(Order order) {
        System.out.println("Order shipped: " + order.getOrderId());
        order.setState(new ShippedState());
    }

    @Override
    public void deliver(Order order) {
        System.out.println("Cannot deliver unshipped order");
    }

    @Override
    public void cancel(Order order) {
        System.out.println("Cannot cancel paid order (refund required)");
        order.setState(new RefundState());
    }
}
```

---

## Python 实现

### 基础实现

```python
from abc import ABC, abstractmethod

class State(ABC):
    @abstractmethod
    def handle(self, context):
        pass

class Context:
    def __init__(self, state):
        self._state = state

    def set_state(self, state):
        self._state = state

    def get_state(self):
        return self._state

    def request(self):
        self._state.handle(self)

class ConcreteStateA(State):
    def handle(self, context):
        print("State A handling, transitioning to State B")
        context.set_state(ConcreteStateB())

class ConcreteStateB(State):
    def handle(self, context):
        print("State B handling, transitioning to State A")
        context.set_state(ConcreteStateA())

if __name__ == "__main__":
    context = Context(ConcreteStateA())

    context.request()
    context.request()
    context.request()
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>
#include <memory>

class Context;

class State {
public:
    virtual ~State() = default;
    virtual void handle(std::shared_ptr<Context> context) = 0;
};

class Context {
private:
    std::shared_ptr<State> state;

public:
    Context(std::shared_ptr<State> state) : state(state) {}

    void setState(std::shared_ptr<State> state) {
        this->state = state;
    }

    std::shared_ptr<State> getState() const {
        return state;
    }

    void request() {
        state->handle(std::shared_ptr<Context>(this));
    }
};

class ConcreteStateA : public State {
public:
    void handle(std::shared_ptr<Context> context) override {
        std::cout << "State A handling, transitioning to State B" << std::endl;
        context->setState(std::make_shared<ConcreteStateB>());
    }
};

class ConcreteStateB : public State {
public:
    void handle(std::shared_ptr<Context> context) override {
        std::cout << "State B handling, transitioning to State A" << std::endl;
        context->setState(std::make_shared<ConcreteStateA>());
    }
};

int main() {
    auto context = std::make_shared<Context>(std::make_shared<ConcreteStateA>());

    context->request();
    context->request();
    context->request();

    return 0;
}
```

---

## 应用场景

### 1. 订单管理
订单的待支付、已支付、已发货、已完成等状态。

### 2. 文档状态
草稿、审核、发布、归档等。

### 3. 游戏状态
开始、运行、暂停、结束等。

### 4. 线程状态
新建、就绪、运行、阻塞、死亡。

### 5. 网络连接
连接、断开、重连等状态。

---

## 优缺点分析

### 优点

1. **消除条件**：消除大量 if-else 语句
2. **状态转换封装**：状态转换逻辑封装在状态类中
3. **扩展性**：新增状态只需添加新类
4. **符合开闭原则**：扩展而非修改

### 缺点

1. **类数量增加**：每个状态需要一个类
2. **复杂性**：状态过多时系统复杂
3. **状态耦合**：状态之间可能耦合

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 状态模式 | 状态决定行为 | 行为随状态变化 |
| 策略模式 | 算法可替换 | 算法灵活切换 |
| 装饰器模式 | 动态增加职责 | 功能扩展 |
