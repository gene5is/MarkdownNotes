---
title: "责任链模式（Chain of Responsibility Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 责任链模式]
author: wjj
toc: true
mermaid: true
---

# 责任链模式（Chain of Responsibility Pattern）

## 模式定义

责任链模式使多个对象都有机会处理请求，从而避免请求的发送者和接收者之间的耦合关系。

## 原理详解

### 核心思想

责任链模式的核心在于：
1. **链式传递**：请求在链上依次传递
2. **解耦**：发送者和接收者解耦
3. **处理选择**：每个处理者决定是否处理或传递
4. **动态组合**：可以在运行时动态组合责任链

### 结构

```
Handler (抽象处理者)
  - successor: Handler
  + setSuccessor(Handler): void
  + handleRequest(request): void

ConcreteHandlerA (具体处理者A)
  + handleRequest(request): void

ConcreteHandlerB (具体处理者B)
  + handleRequest(request): void
```

### 处理流程

```
Request → HandlerA → HandlerB → HandlerC → ...
              ↓           ↓           ↓
           处理/拒绝    处理/拒绝    处理/拒绝
```

---

## Java 实现

### 基础实现

```java
abstract class Handler {
    private Handler successor;

    public void setSuccessor(Handler successor) {
        this.successor = successor;
    }

    public Handler getSuccessor() {
        return successor;
    }

    public abstract void handleRequest(String request);
}

class HandlerA extends Handler {
    @Override
    public void handleRequest(String request) {
        if (request.equals("A")) {
            System.out.println("HandlerA handled: " + request);
        } else if (getSuccessor() != null) {
            getSuccessor().handleRequest(request);
        }
    }
}

class HandlerB extends Handler {
    @Override
    public void handleRequest(String request) {
        if (request.equals("B")) {
            System.out.println("HandlerB handled: " + request);
        } else if (getSuccessor() != null) {
            getSuccessor().handleRequest(request);
        }
    }
}

class HandlerC extends Handler {
    @Override
    public void handleRequest(String request) {
        if (request.equals("C")) {
            System.out.println("HandlerC handled: " + request);
        } else if (getSuccessor() != null) {
            getSuccessor().handleRequest(request);
        }
    }
}

public class ChainDemo {
    public static void main(String[] args) {
        Handler h1 = new HandlerA();
        Handler h2 = new HandlerB();
        Handler h3 = new HandlerC();

        h1.setSuccessor(h2);
        h2.setSuccessor(h3);

        h1.handleRequest("A");
        h1.handleRequest("B");
        h1.handleRequest("C");
        h1.handleRequest("D");
    }
}
```

### 日志系统

```java
enum LogLevel {
    DEBUG, INFO, WARNING, ERROR
}

abstract class Logger {
    protected LogLevel level;
    protected Logger nextLogger;

    public void setNextLogger(Logger nextLogger) {
        this.nextLogger = nextLogger;
    }

    public void log(LogLevel level, String message) {
        if (this.level.ordinal() <= level.ordinal()) {
            write(message);
        }
        if (nextLogger != null) {
            nextLogger.log(level, message);
        }
    }

    protected abstract void write(String message);
}

class DebugLogger extends Logger {
    public DebugLogger() {
        this.level = LogLevel.DEBUG;
    }

    @Override
    protected void write(String message) {
        System.out.println("DEBUG: " + message);
    }
}

class InfoLogger extends Logger {
    public InfoLogger() {
        this.level = LogLevel.INFO;
    }

    @Override
    protected void write(String message) {
        System.out.println("INFO: " + message);
    }
}

class ErrorLogger extends Logger {
    public ErrorLogger() {
        this.level = LogLevel.ERROR;
    }

    @Override
    protected void write(String message) {
        System.out.println("ERROR: " + message);
    }
}
```

---

## Python 实现

### 基础实现

```python
from abc import ABC, abstractmethod

class Handler(ABC):
    def __init__(self):
        self._successor = None

    def set_successor(self, successor):
        self._successor = successor
        return successor

    def get_successor(self):
        return self._successor

    @abstractmethod
    def handle(self, request):
        pass

class HandlerA(Handler):
    def handle(self, request):
        if request == "A":
            print(f"HandlerA handled: {request}")
        elif self._successor:
            self._successor.handle(request)

class HandlerB(Handler):
    def handle(self, request):
        if request == "B":
            print(f"HandlerB handled: {request}")
        elif self._successor:
            self._successor.handle(request)

if __name__ == "__main__":
    h1 = HandlerA()
    h2 = HandlerB()

    h1.set_successor(h2)

    h1.handle("A")
    h1.handle("B")
    h1.handle("C")
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>
#include <memory>

class Handler {
protected:
    std::shared_ptr<Handler> successor;

public:
    virtual ~Handler() = default;

    void setSuccessor(std::shared_ptr<Handler> successor) {
        this->successor = successor;
    }

    std::shared_ptr<Handler> getSuccessor() const {
        return successor;
    }

    virtual void handleRequest(const std::string& request) = 0;
};

class HandlerA : public Handler {
public:
    void handleRequest(const std::string& request) override {
        if (request == "A") {
            std::cout << "HandlerA handled: " << request << std::endl;
        } else if (successor) {
            successor->handleRequest(request);
        }
    }
};

class HandlerB : public Handler {
public:
    void handleRequest(const std::string& request) override {
        if (request == "B") {
            std::cout << "HandlerB handled: " << request << std::endl;
        } else if (successor) {
            successor->handleRequest(request);
        }
    }
};

int main() {
    auto h1 = std::make_shared<HandlerA>();
    auto h2 = std::make_shared<HandlerB>();

    h1->setSuccessor(h2);

    h1->handleRequest("A");
    h1->handleRequest("B");
    h1->handleRequest("C");

    return 0;
}
```

---

## 应用场景

### 1. 日志系统
不同级别的日志处理。

### 2. 过滤器链
Web 请求的过滤器链。

### 3. 审批流程
多级审批流程。

### 4. 异常处理
多层异常捕获。

### 5. 事件处理
GUI 事件冒泡。

---

## 优缺点分析

### 优点

1. **解耦**：发送者和接收者解耦
2. **灵活性**：可以动态调整责任链
3. **单一职责**：每个处理者单一职责
4. **开闭原则**：新增处理者无需修改代码

### 缺点

1. **性能问题**：请求可能不被处理
2. **调试困难**：链较长时调试困难
3. **配置复杂**：链的配置可能复杂

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 责任链模式 | 链式传递 | 请求传递 |
| 命令模式 | 请求封装 | 请求参数化 |
| 观察者模式 | 一对多通知 | 状态变化通知 |
