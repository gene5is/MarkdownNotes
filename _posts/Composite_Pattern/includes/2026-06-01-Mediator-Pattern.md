---
title: "中介者模式（Mediator Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 行为型模式]
tags: [设计模式, 行为型模式, 中介者模式]
author: wjj
toc: true
---

# 中介者模式（Mediator Pattern）

## 模式定义

中介者模式用一个中介对象来封装一系列的对象交互。中介者使各对象不需要显式地相互引用，从而使其耦合松散。

## 原理详解

### 核心思想

中介者模式的核心在于：
1. **集中控制**：通过中介者集中管理对象间交互
2. **解耦**：对象间不直接引用，降低耦合
3. **简化通信**：对象通过中介者通信
4. **协调工作**：中介者协调各对象的工作

### 结构

```
Mediator (抽象中介者)
  + notify(sender, event): void

ConcreteMediator (具体中介者)
  - colleague1: Colleague1
  - colleague2: Colleague2
  + notify(sender, event): void

Colleague (抽象同事类)
  - mediator: Mediator
  + notify(mediator, event): void

ConcreteColleague1 (具体同事类1)
ConcreteColleague2 (具体同事类2)
```

### 对象关系

```
Colleague1 ──┐
             ├──► Mediator ◄──┤
Colleague2 ──┘                │
                               │
Colleague3 ───────────────────┘
```

---

## Java 实现

### 基础实现

```java
interface Mediator {
    void notify(Component sender, String event);
}

class Button {
    private Mediator mediator;

    public void setMediator(Mediator mediator) {
        this.mediator = mediator;
    }

    public void click() {
        System.out.println("Button clicked");
        mediator.notify(this, "click");
    }
}

class TextBox {
    private Mediator mediator;

    public void setMediator(Mediator mediator) {
        this.mediator = mediator;
    }

    public void input(String text) {
        System.out.println("TextBox input: " + text);
        mediator.notify(this, "input");
    }
}

class Label {
    private Mediator mediator;

    public void setMediator(Mediator mediator) {
        this.mediator = mediator;
    }

    public void update(String text) {
        System.out.println("Label updated: " + text);
    }
}

class DialogMediator implements Mediator {
    private Button button;
    private TextBox textBox;
    private Label label;

    public void setButton(Button button) {
        this.button = button;
        this.button.setMediator(this);
    }

    public void setTextBox(TextBox textBox) {
        this.textBox = textBox;
        this.textBox.setMediator(this);
    }

    public void setLabel(Label label) {
        this.label = label;
        this.label.setMediator(this);
    }

    @Override
    public void notify(Component sender, String event) {
        if (sender == button && "click".equals(event)) {
            label.update("Button was clicked!");
        } else if (sender == textBox && "input".equals(event)) {
            label.update("Text was entered!");
        }
    }
}

public class MediatorDemo {
    public static void main(String[] args) {
        DialogMediator mediator = new DialogMediator();

        Button button = new Button();
        TextBox textBox = new TextBox();
        Label label = new Label();

        mediator.setButton(button);
        mediator.setTextBox(textBox);
        mediator.setLabel(label);

        button.click();
        textBox.input("Hello");
    }
}
```

### 聊天室示例

```java
interface ChatMediator {
    void sendMessage(String message, User sender);
    void addUser(User user);
}

class ChatRoom implements ChatMediator {
    private List<User> users = new ArrayList<>();

    @Override
    public void sendMessage(String message, User sender) {
        for (User user : users) {
            if (user != sender) {
                user.receive(message, sender.getName());
            }
        }
    }

    @Override
    public void addUser(User user) {
        users.add(user);
    }
}

class User {
    private String name;
    private ChatMediator mediator;

    public User(String name, ChatMediator mediator) {
        this.name = name;
        this.mediator = mediator;
    }

    public String getName() {
        return name;
    }

    public void send(String message) {
        System.out.println(name + " sends: " + message);
        mediator.sendMessage(message, this);
    }

    public void receive(String message, String from) {
        System.out.println(name + " received from " + from + ": " + message);
    }
}
```

---

## Python 实现

### 基础实现

```python
from abc import ABC, abstractmethod

class Mediator(ABC):
    @abstractmethod
    def notify(self, sender, event):
        pass

class Button:
    def __init__(self):
        self._mediator = None

    def set_mediator(self, mediator):
        self._mediator = mediator

    def click(self):
        print("Button clicked")
        self._mediator.notify(self, "click")

class TextBox:
    def __init__(self):
        self._mediator = None

    def set_mediator(self, mediator):
        self._mediator = mediator

    def input(self, text):
        print(f"TextBox input: {text}")
        self._mediator.notify(self, "input")

class Label:
    def __init__(self):
        self._mediator = None

    def set_mediator(self, mediator):
        self._mediator = mediator

    def update(self, text):
        print(f"Label updated: {text}")

class DialogMediator(Mediator):
    def __init__(self):
        self.button = None
        self.textbox = None
        self.label = None

    def set_components(self, button, textbox, label):
        self.button = button
        self.textbox = textbox
        self.label = label

    def notify(self, sender, event):
        if sender == self.button and event == "click":
            self.label.update("Button was clicked!")
        elif sender == self.textbox and event == "input":
            self.label.update("Text was entered!")

if __name__ == "__main__":
    mediator = DialogMediator()

    button = Button()
    textbox = TextBox()
    label = Label()

    mediator.set_components(button, textbox, label)

    button.click()
    textbox.input("Hello")
```

---

## C++ 实现

### 基础实现

```cpp
#include <iostream>
#include <memory>
#include <string>

class Mediator {
public:
    virtual ~Mediator() = default;
    virtual void notify(void* sender, const std::string& event) = 0;
};

class Component {
protected:
    Mediator* mediator;

public:
    virtual ~Component() = default;
    void setMediator(Mediator* mediator) {
        this->mediator = mediator;
    }
};

class Button : public Component {
public:
    void click() {
        std::cout << "Button clicked" << std::endl;
        mediator->notify(this, "click");
    }
};

class TextBox : public Component {
public:
    void input(const std::string& text) {
        std::cout << "TextBox input: " << text << std::endl;
        mediator->notify(this, "input");
    }
};

class Label : public Component {
public:
    void update(const std::string& text) {
        std::cout << "Label updated: " << text << std::endl;
    }
};

class DialogMediator : public Mediator {
private:
    Button* button;
    TextBox* textBox;
    Label* label;

public:
    void setComponents(Button* button, TextBox* textBox, Label* label) {
        this->button = button;
        this->textBox = textBox;
        this->label = label;
    }

    void notify(void* sender, const std::string& event) override {
        if (sender == button && event == "click") {
            label->update("Button was clicked!");
        } else if (sender == textBox && event == "input") {
            label->update("Text was entered!");
        }
    }
};

int main() {
    DialogMediator mediator;

    Button button;
    TextBox textBox;
    Label label;

    button.setMediator(&mediator);
    textBox.setMediator(&mediator);
    label.setMediator(&mediator);

    mediator.setComponents(&button, &textBox, &label);

    button.click();
    textBox.input("Hello");

    return 0;
}
```

---

## 应用场景

### 1. GUI 对话框
对话框中各组件的交互。

### 2. 聊天室
聊天室中用户间的消息传递。

### 3. 航空管制
飞机间的通信协调。

### 4. 中介软件
房产中介、婚姻介绍所。

---

## 优缺点分析

### 优点

1. **解耦**：对象间解耦
2. **简化通信**：通过中介者统一管理
3. **集中控制**：交互逻辑集中
4. **复用**：对象可以复用

### 缺点

1. **中介者复杂**：中介者可能变得复杂
2. **性能问题**：所有消息都经过中介者
3. **违反单一职责**：中介者职责过重

---

## 模式对比

| 模式 | 特点 | 目的 |
|------|------|------|
| 中介者模式 | 间接通信 | 集中控制交互 |
| 观察者模式 | 一对多通知 | 状态变化通知 |
| 责任链模式 | 链式传递 | 请求传递 |
