---
title: "命令模式（Command Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 命令模式]
author: wjj
toc: true
---

# 命令模式（Command Pattern）

## 模式定义

命令模式将一个请求封装为一个对象，从而使你可用不同的请求对客户进行参数化；对请求排队或记录请求日志，以及支持可撤销的操作。

## 原理详解

### 核心思想

命令模式的核心在于：
1. **请求封装**：将请求封装为命令对象
2. **参数化**：可以用不同命令参数化客户
3. **队列化**：命令可以排队执行
4. **可撤销**：可以记录命令实现撤销操作

### 结构

```
Invoker (调用者)
  - command: Command
  + executeCommand(): void

Command (抽象命令)
  + execute(): void
  + undo(): void

Receiver (接收者)
  + action(): void

ConcreteCommand (具体命令)
  - receiver: Receiver
  + execute(): void
  + undo(): void
```

### 与其他模式对比

| 对比项 | 命令模式 | 策略模式 |
|--------|----------|----------|
| 目的 | 请求封装 | 算法切换 |
| 执行者 | receiver | context |
| 可撤销 | 支持 | 不支持 |

---

## Java 实现

### 基础实现

```java
interface Command {
    void execute();
    void undo();
}

class Light {
    public void on() {
        System.out.println("Light is ON");
    }

    public void off() {
        System.out.println("Light is OFF");
    }
}

class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.on();
    }

    @Override
    public void undo() {
        light.off();
    }
}

class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.off();
    }

    @Override
    public void undo() {
        light.on();
    }
}

class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }

    public void pressUndo() {
        command.undo();
    }
}

public class CommandDemo {
    public static void main(String[] args) {
        Light light = new Light();

        Command lightOn = new LightOnCommand(light);
        Command lightOff = new LightOffCommand(light);

        RemoteControl remote = new RemoteControl();

        remote.setCommand(lightOn);
        remote.pressButton();

        remote.setCommand(lightOff);
        remote.pressButton();

        remote.pressUndo();
    }
}
```

### 宏命令和命令队列

```java
class MacroCommand implements Command {
    private List<Command> commands;

    public MacroCommand() {
        this.commands = new ArrayList<>();
    }

    public void addCommand(Command command) {
        commands.add(command);
    }

    public void removeCommand(Command command) {
        commands.remove(command);
    }

    @Override
    public void execute() {
        for (Command command : commands) {
            command.execute();
        }
    }

    @Override
    public void undo() {
        for (int i = commands.size() - 1; i >= 0; i--) {
            commands.get(i).undo();
        }
    }
}
```

---

## Python 实现

### 基础实现

```python
from abc import ABC, abstractmethod

class Command(ABC):
    @abstractmethod
    def execute(self):
        pass

    @abstractmethod
    def undo(self):
        pass

class Light:
    def on(self):
        print("Light is ON")

    def off(self):
        print("Light is OFF")

class LightOnCommand(Command):
    def __init__(self, light):
        self.light = light

    def execute(self):
        self.light.on()

    def undo(self):
        self.light.off()

class LightOffCommand(Command):
    def __init__(self, light):
        self.light = light

    def execute(self):
        self.light.off()

    def undo(self):
        self.light.on()

class RemoteControl:
    def __init__(self):
        self.command = None

    def set_command(self, command):
        self.command = command

    def press_button(self):
        self.command.execute()

    def press_undo(self):
        self.command.undo()

if __name__ == "__main__":
    light = Light()

    light_on = LightOnCommand(light)
    light_off = LightOffCommand(light)

    remote = RemoteControl()

    remote.set_command(light_on)
    remote.press_button()

    remote.set_command(light_off)
    remote.press_button()
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>
#include <memory>
#include <stack>

class Command {
public:
    virtual ~Command() = default;
    virtual void execute() = 0;
    virtual void undo() = 0;
};

class Light {
public:
    void on() {
        std::cout << "Light is ON" << std::endl;
    }

    void off() {
        std::cout << "Light is OFF" << std::endl;
    }
};

class LightOnCommand : public Command {
private:
    Light* light;

public:
    LightOnCommand(Light* light) : light(light) {}

    void execute() override {
        light->on();
    }

    void undo() override {
        light->off();
    }
};

class LightOffCommand : public Command {
private:
    Light* light;

public:
    LightOffCommand(Light* light) : light(light) {}

    void execute() override {
        light->off();
    }

    void undo() override {
        light->on();
    }
};

class RemoteControl {
private:
    std::unique_ptr<Command> command;

public:
    void setCommand(std::unique_ptr<Command> cmd) {
        command = std::move(cmd);
    }

    void pressButton() {
        if (command) {
            command->execute();
        }
    }

    void pressUndo() {
        if (command) {
            command->undo();
        }
    }
};

int main() {
    Light light;

    RemoteControl remote;
    remote.setCommand(std::make_unique<LightOnCommand>(&light));
    remote.pressButton();

    remote.setCommand(std::make_unique<LightOffCommand>(&light));
    remote.pressButton();

    remote.pressUndo();

    return 0;
}
```

---

## 应用场景

### 1. 遥控器
家电遥控器控制。

### 2. 撤销/重做
文本编辑器、图形编辑器的撤销重做。

### 3. 宏命令
批量执行多个命令。

### 4. 队列请求
任务队列、日程安排。

### 5. 事务管理
数据库事务操作。

---

## 优缺点分析

### 优点

1. **解耦**：请求者和执行者解耦
2. **可撤销**：支持撤销和重做操作
3. **队列化**：可以排队执行命令
4. **宏命令**：可以组合多个命令

### 缺点

1. **复杂性增加**：需要为每个命令创建类
2. **内存占用**：大量命令对象可能占用内存

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 命令模式 | 请求封装 | 请求参数化、可撤销 |
| 策略模式 | 算法切换 | 算法可替换 |
| 观察者模式 | 一对多通知 | 状态变化通知 |
