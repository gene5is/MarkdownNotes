---
title: "解释器模式（Interpreter Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 解释器模式]
author: wjj
toc: true
mermaid: true
---

# 解释器模式（Interpreter Pattern）

## 模式定义

解释器模式给定一个语言，定义它的文法的一种表示，并定义一个解释器，该解释器使用该表示来解释语言中的句子。

## 原理详解

### 核心思想

解释器模式的核心在于：
1. **文法表示**：为语言定义文法表示
2. **语法树**：将句子表示为语法树
3. **解释执行**：遍历语法树解释执行
4. **递归解释**：使用递归进行解释

### 结构

```
Context (上下文)
  - variables: Map

Expression (抽象表达式)
  + interpret(Context): Result

TerminalExpression (终结符表达式)
  + interpret(Context): Result

NonterminalExpression (非终结符表达式)
  - expressions: List<Expression>
  + interpret(Context): Result
```

### 文法示例

```
expression ::= number | expression + expression | expression - expression
number ::= 0 | 1 | 2 | ...
```

---

## Java 实现

### 基础实现

```java
interface Expression {
    int interpret(Context context);
}

class NumberExpression implements Expression {
    private int number;

    public NumberExpression(int number) {
        this.number = number;
    }

    @Override
    public int interpret(Context context) {
        return number;
    }
}

class PlusExpression implements Expression {
    private Expression left;
    private Expression right;

    public PlusExpression(Expression left, Expression right) {
        this.left = left;
        this.right = right;
    }

    @Override
    public int interpret(Context context) {
        return left.interpret(context) + right.interpret(context);
    }
}

class MinusExpression implements Expression {
    private Expression left;
    private Expression right;

    public MinusExpression(Expression left, Expression right) {
        this.left = left;
        this.right = right;
    }

    @Override
    public int interpret(Context context) {
        return left.interpret(context) - right.interpret(context);
    }
}

class Context {
    private Map<String, Integer> variables = new HashMap<>();

    public void setVariable(String name, int value) {
        variables.put(name, value);
    }

    public int getVariable(String name) {
        return variables.getOrDefault(name, 0);
    }
}

public class InterpreterDemo {
    public static void main(String[] args) {
        Context context = new Context();

        Expression expr = new PlusExpression(
            new NumberExpression(5),
            new MinusExpression(
                new NumberExpression(10),
                new NumberExpression(3)
            )
        );

        System.out.println("Result: " + expr.interpret(context));
    }
}
```

### 变量表达式

```java
class VariableExpression implements Expression {
    private String name;

    public VariableExpression(String name) {
        this.name = name;
    }

    @Override
    public int interpret(Context context) {
        return context.getVariable(name);
    }
}

class Evaluator {
    public Expression buildSyntaxTree(String expression) {
        return new PlusExpression(
            new VariableExpression("x"),
            new VariableExpression("y")
        );
    }
}
```

---

## Python 实现

### 基础实现

```python
from abc import ABC, abstractmethod

class Context:
    def __init__(self):
        self.variables = {}

    def set_variable(self, name, value):
        self.variables[name] = value

    def get_variable(self, name):
        return self.variables.get(name, 0)

class Expression(ABC):
    @abstractmethod
    def interpret(self, context):
        pass

class NumberExpression(Expression):
    def __init__(self, number):
        self.number = number

    def interpret(self, context):
        return self.number

class PlusExpression(Expression):
    def __init__(self, left, right):
        self.left = left
        self.right = right

    def interpret(self, context):
        return self.left.interpret(context) + self.right.interpret(context)

class MinusExpression(Expression):
    def __init__(self, left, right):
        self.left = left
        self.right = right

    def interpret(self, context):
        return self.left.interpret(context) - self.right.interpret(context)

if __name__ == "__main__":
    context = Context()

    expr = PlusExpression(
        NumberExpression(5),
        MinusExpression(
            NumberExpression(10),
            NumberExpression(3)
        )
    )

    print(f"Result: {expr.interpret(context)}")
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>
#include <memory>
#include <unordered_map>

class Context {
private:
    std::unordered_map<std::string, int> variables;

public:
    void setVariable(const std::string& name, int value) {
        variables[name] = value;
    }

    int getVariable(const std::string& name) {
        return variables.count(name) ? variables[name] : 0;
    }
};

class Expression {
public:
    virtual ~Expression() = default;
    virtual int interpret(const Context& context) = 0;
};

class NumberExpression : public Expression {
private:
    int number;

public:
    NumberExpression(int number) : number(number) {}

    int interpret(const Context& context) override {
        return number;
    }
};

class PlusExpression : public Expression {
private:
    std::unique_ptr<Expression> left;
    std::unique_ptr<Expression> right;

public:
    PlusExpression(std::unique_ptr<Expression> left,
                   std::unique_ptr<Expression> right)
        : left(std::move(left)), right(std::move(right)) {}

    int interpret(const Context& context) override {
        return left->interpret(context) + right->interpret(context);
    }
};

class MinusExpression : public Expression {
private:
    std::unique_ptr<Expression> left;
    std::unique_ptr<Expression> right;

public:
    MinusExpression(std::unique_ptr<Expression> left,
                    std::unique_ptr<Expression> right)
        : left(std::move(left)), right(std::move(right)) {}

    int interpret(const Context& context) override {
        return left->interpret(context) - right->interpret(context);
    }
};

int main() {
    Context context;

    auto expr = std::make_unique<PlusExpression>(
        std::make_unique<NumberExpression>(5),
        std::make_unique<MinusExpression>(
            std::make_unique<NumberExpression>(10),
            std::make_unique<NumberExpression>(3)
        )
    );

    std::cout << "Result: " << expr->interpret(context) << std::endl;

    return 0;
}
```

---

## 应用场景

### 1. SQL 解析
SQL 语句的解释和执行。

### 2. 数学表达式计算器
数学表达式的解析和计算。

### 3. 配置文件解析
XML、JSON、YAML 等配置文件的解析。

### 4. 正则表达式
正则表达式的解析和匹配。

### 5. 编程语言解释器
脚本语言的解释执行。

---

## 优缺点分析

### 优点

1. **易于改变和扩展文法**：可以方便地修改和扩展文法
2. **实现简单**：文法简单时实现相对简单
3. **可扩展性**：可以添加新的解释表达式

### 缺点

1. **复杂性**：复杂文法会导致类数量爆炸
2. **性能问题**：解释执行效率较低
3. **维护困难**：复杂文法难以维护
4. **适用性有限**：只适合简单文法

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 解释器模式 | 文法解释 | 解释执行 |
| 访问者模式 | 操作与数据分离 | 操作扩展 |
| 组合模式 | 整体-部分 | 构建对象树 |
