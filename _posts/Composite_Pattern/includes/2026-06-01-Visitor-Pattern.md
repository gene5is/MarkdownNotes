---
title: "访问者模式（Visitor Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 访问者模式]
author: wjj
toc: true
---

# 访问者模式（Visitor Pattern）

## 模式定义

访问者模式表示一个作用于某对象结构中的各元素的操作。访问者模式使你可以在不改变各元素的类的前提下定义作用于这些元素的新操作。

## 原理详解

### 核心思想

访问者模式的核心在于：
1. **操作与数据结构分离**：操作和数据结构分离
2. **双分派**：通过两次分派实现操作扩展
3. **新操作**：可以添加新操作而不改变元素类
4. **封装操作**：相关操作封装在访问者中

### 结构

```
Visitor (抽象访问者)
  + visitConcreteElementA(ConcreteElementA): void
  + visitConcreteElementB(ConcreteElementB): void

ConcreteVisitorA (具体访问者A)
ConcreteVisitorB (具体访问者B)

Element (抽象元素)
  + accept(Visitor): void

ConcreteElementA (具体元素A)
  + accept(Visitor): void

ObjectStructure (对象结构)
  + add(Element): void
  + accept(Visitor): void
```

### 分派机制

```
客户端 → 对象结构.accept(visitor)
                    ↓
            element.accept(visitor)
                    ↓
            visitor.visit(element)
```

---

## Java 实现

### 基础实现

```java
interface Visitor {
    void visit(Engineer engineer);
    void visit(Manager manager);
}

interface Employee {
    void accept(Visitor visitor);
}

class Engineer implements Employee {
    private String name;
    private int code;

    public Engineer(String name, int code) {
        this.name = name;
        this.code = code;
    }

    public String getName() {
        return name;
    }

    public int getCode() {
        return code;
    }

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

class Manager implements Employee {
    private String name;
    private int subordinates;

    public Manager(String name, int subordinates) {
        this.name = name;
        this.subordinates = subordinates;
    }

    public String getName() {
        return name;
    }

    public int getSubordinates() {
        return subordinates;
    }

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

class SalaryVisitor implements Visitor {
    @Override
    public void visit(Engineer engineer) {
        System.out.println("Engineer " + engineer.getName()
            + " salary: " + (engineer.getCode() * 1000));
    }

    @Override
    public void visit(Manager manager) {
        System.out.println("Manager " + manager.getName()
            + " salary: " + (manager.getSubordinates() * 5000));
    }
}

class ReportVisitor implements Visitor {
    @Override
    public void visit(Engineer engineer) {
        System.out.println("Engineer Report: " + engineer.getName()
            + ", code: " + engineer.getCode());
    }

    @Override
    public void visit(Manager manager) {
        System.out.println("Manager Report: " + manager.getName()
            + ", subordinates: " + manager.getSubordinates());
    }
}

public class VisitorDemo {
    public static void main(String[] args) {
        List<Employee> employees = Arrays.asList(
            new Engineer("Alice", 100),
            new Engineer("Bob", 101),
            new Manager("Charlie", 5),
            new Manager("David", 3)
        );

        Visitor salaryVisitor = new SalaryVisitor();
        Visitor reportVisitor = new ReportVisitor();

        for (Employee employee : employees) {
            employee.accept(salaryVisitor);
        }

        System.out.println();

        for (Employee employee : employees) {
            employee.accept(reportVisitor);
        }
    }
}
```

---

## Python 实现

### 基础实现

```python
from abc import ABC, abstractmethod

class Visitor(ABC):
    @abstractmethod
    def visit_engineer(self, engineer):
        pass

    @abstractmethod
    def visit_manager(self, manager):
        pass

class Employee(ABC):
    @abstractmethod
    def accept(self, visitor):
        pass

class Engineer(Employee):
    def __init__(self, name, code):
        self.name = name
        self.code = code

    def accept(self, visitor):
        visitor.visit_engineer(self)

class Manager(Employee):
    def __init__(self, name, subordinates):
        self.name = name
        self.subordinates = subordinates

    def accept(self, visitor):
        visitor.visit_manager(self)

class SalaryVisitor(Visitor):
    def visit_engineer(self, engineer):
        print(f"Engineer {engineer.name} salary: {engineer.code * 1000}")

    def visit_manager(self, manager):
        print(f"Manager {manager.name} salary: {manager.subordinates * 5000}")

class ReportVisitor(Visitor):
    def visit_engineer(self, engineer):
        print(f"Engineer Report: {engineer.name}, code: {engineer.code}")

    def visit_manager(self, manager):
        print(f"Manager Report: {manager.name}, subordinates: {manager.subordinates}")

if __name__ == "__main__":
    employees = [
        Engineer("Alice", 100),
        Engineer("Bob", 101),
        Manager("Charlie", 5),
        Manager("David", 3)
    ]

    salary_visitor = SalaryVisitor()
    report_visitor = ReportVisitor()

    for employee in employees:
        employee.accept(salary_visitor)

    print()

    for employee in employees:
        employee.accept(report_visitor)
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>
#include <vector>
#include <memory>
#include <string>

class Engineer;
class Manager;

class Visitor {
public:
    virtual ~Visitor() = default;
    virtual void visit(const Engineer& engineer) = 0;
    virtual void visit(const Manager& manager) = 0;
};

class Employee {
public:
    virtual ~Employee() = default;
    virtual void accept(const Visitor& visitor) = 0;
};

class Engineer : public Employee {
private:
    std::string name;
    int code;

public:
    Engineer(const std::string& name, int code) : name(name), code(code) {}

    std::string getName() const { return name; }
    int getCode() const { return code; }

    void accept(const Visitor& visitor) override {
        visitor.visit(*this);
    }
};

class Manager : public Employee {
private:
    std::string name;
    int subordinates;

public:
    Manager(const std::string& name, int subordinates)
        : name(name), subordinates(subordinates) {}

    std::string getName() const { return name; }
    int getSubordinates() const { return subordinates; }

    void accept(const Visitor& visitor) override {
        visitor.visit(*this);
    }
};

class SalaryVisitor : public Visitor {
public:
    void visit(const Engineer& engineer) override {
        std::cout << "Engineer " << engineer.getName()
                  << " salary: " << engineer.getCode() * 1000 << std::endl;
    }

    void visit(const Manager& manager) override {
        std::cout << "Manager " << manager.getName()
                  << " salary: " << manager.getSubordinates() * 5000 << std::endl;
    }
};

class ReportVisitor : public Visitor {
public:
    void visit(const Engineer& engineer) override {
        std::cout << "Engineer Report: " << engineer.getName()
                  << ", code: " << engineer.getCode() << std::endl;
    }

    void visit(const Manager& manager) override {
        std::cout << "Manager Report: " << manager.getName()
                  << ", subordinates: " << manager.getSubordinates() << std::endl;
    }
};

int main() {
    std::vector<std::unique_ptr<Employee>> employees;
    employees.push_back(std::make_unique<Engineer>("Alice", 100));
    employees.push_back(std::make_unique<Engineer>("Bob", 101));
    employees.push_back(std::make_unique<Manager>("Charlie", 5));
    employees.push_back(std::make_unique<Manager>("David", 3));

    SalaryVisitor salaryVisitor;
    ReportVisitor reportVisitor;

    std::cout << "=== Salary Report ===" << std::endl;
    for (const auto& employee : employees) {
        employee->accept(salaryVisitor);
    }

    std::cout << "\n=== Employee Report ===" << std::endl;
    for (const auto& employee : employees) {
        employee->accept(reportVisitor);
    }

    return 0;
}
```

---

## 应用场景

### 1. 编译器
AST 节点的遍历和操作。

### 2. 文件系统
文件和目录的统计、导出操作。

### 3. 报表生成
不同类型数据的报表生成。

### 4. 收藏品估价
不同类型收藏品的估价。

---

## 优缺点分析

### 优点

1. **扩展操作**：可以添加新操作而不改变元素类
2. **相关操作集中**：相关操作封装在访问者中
3. **双分派**：通过两次分派实现灵活扩展

### 缺点

1. **元素类约束**：元素类需要暴露接口给访问者
2. **类数量增加**：新增元素需要修改所有访问者
3. **违反开闭原则**：新增元素需要修改访问者
4. **类型安全**：访问者类型安全难以保证

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 访问者模式 | 操作与数据分离 | 操作扩展 |
| 迭代器模式 | 顺序访问 | 遍历聚合对象 |
| 组合模式 | 整体-部分 | 构建对象树 |
