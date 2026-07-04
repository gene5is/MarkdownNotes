---
title: "单例模式（Singleton Pattern）"
date: 2026-06-01 00:00:00 +0800
categories: [设计模式, 创建型模式]
tags: [设计模式, 创建型模式, 单例模式]
author: wjj
toc: true
mermaid: true
---

# 单例模式（Singleton Pattern）

## 模式定义

单例模式确保一个类只有一个实例，并提供一个全局访问点。它属于创建型设计模式，用于控制实例的创建，避免资源的重复创建和浪费。

## 原理详解

### 核心思想

单例模式的核心在于：
1. **私有化构造函数**：防止外部通过 `new` 创建实例
2. **私有化静态实例变量**：保存唯一实例
3. **公有的静态方法**：提供全局访问点获取唯一实例

### UML 类图

```mermaid
classDiagram
    class Singleton {
        -Singleton instance$
        -Singleton()
        +getInstance()$
        +businessMethod()
    }
    
    note right of Singleton "私有化构造函数\n静态变量保存实例\n全局访问点"
```

### 结构

```
Singleton
- instance: Singleton (私有静态实例)
- Singleton() (私有构造函数)
+ getInstance(): Singleton (公有静态方法)
```

### 实现方式

单例模式有多种实现方式，各有权衡：

| 实现方式 | 线程安全 | 延迟加载 | 性能 |
|----------|----------|----------|------|
| 饿汉式 | 是 | 否 | 高 |
| 懒汉式（同步方法） | 是 | 是 | 低 |
| 双重检查锁定 | 是 | 是 | 中 |
| 静态内部类 | 是 | 是 | 高 |
| 枚举 | 是 | 否 | 高 |

---

## Java 实现

### 饿汉式（推荐简单场景）

*应用场景*：适用于必用、占用内存小的全局配置类、工具类。如果一个单例对象在程序启动时就肯定会被用到，且创建时不需要从外部传入动态参数，优先选择此方式。
*代码逻辑*：利用 JVM 的类加载机制，在类挂载到内存时就直接实例化对象，天然规避了多线程并发创建对象的问题。

```java
public class Singleton {
    //类加载时立即创建，由JVM保证线程安全
    private static final Singleton instance = new Singleton();

    // 私有方法
    private Singleton() {
    }

    // 全局唯一访问点
    public static Singleton getInstance() {
        return instance;
    }
}
```

### 懒汉式（线程安全，同步方法）

```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
    }

    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

### 双重检查锁懒汉式（推荐高效场景）

*应用场景*：适用于占用资源大、可能用不到、需要动态传参的场景。例如数据库连接池、网络连接管理器或需要根据运行期配置文件初始化属性的单例对象。
*代码逻辑*：采用“延迟加载”。通过两次 if (instance == null) 检查，第一次提升性能，第二次保证线程安全。配合 volatile 关键字禁止指令重排，确保多线程下获取到完全初始化好的对象。

```java
public class DclSingleton {
    
    // 1. volatile 关键字至关重要！防止指令重排，确保多线程下拿到完全初始化好的对象
    private static volatile DclSingleton instance;

    // 2. 私有化构造方法，阻止外部通过 new 显式创建实例
    private DclSingleton() {
        // 可选：在此处加入防止反射破坏的代码
        if (instance != null) {
            throw new RuntimeException("单例构造器禁止反射调用！");
        }
    }

    // 3. 全局唯一访问点
    public static DclSingleton getInstance() {
        // 第一次检查：如果实例已经创建，直接返回，避免不必要的 synchronized 加锁开销（提升性能）
        if (instance == null) {
            
            // 局部加锁：只有在实例未创建时，才对类对象加锁（<<synchronized>>）
            synchronized (DclSingleton.class) {
                
                // 第二次检查：防止线程 A 和线程 B 同时通过了第一次检查
                // 此时 A 拿到锁创建了对象，释放锁后 B 进去，若不检查就会再次创建对象
                if (instance == null) {
                    // 隐患点：new 操作在底层包含3步指令（分配内存、初始化对象、引用指向内存）
                    // volatile 阻止了这3步指令重排，保证其他线程不会拿到“未初始化完的半成品”
                    instance = new DclSingleton();
                }
            }
        }
        return instance;
    }

    // 4. 业务方法
    public void businessMethod() {
        System.out.println("懒汉式单例业务方法执行中...");
    }
}

```

### 静态内部类实现

*应用场景*：适用于追求高并发性能、且需要延迟加载，但不需要动态传参的框架级核心组件。这是开源项目（如 Spring、MyBatis）中最常见的单例写法。
*代码逻辑*：当外部类 StaticInnerSingleton 被加载时，其静态内部类 Holder 并不会被加载。只有当第一次调用 getInstance() 方法时，JVM 才会加载 Holder 并初始化它的静态变量 INSTANCE。

```java
public class Singleton {
    private Singleton() {
    }

    // 静态内部类：只有在被调用时才会被JVM加载并初始化
    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

---

## Python 实现

### 懒汉式（线程安全）

```python
import threading

class Singleton:
    _instance = None
    _lock = threading.Lock()

    def __new__(cls):
        if cls._instance is None:
            with cls._lock:
                if cls._instance is None:
                    cls._instance = super().__new__(cls)
        return cls._instance
```

### 模块单例（最Pythonic方式）

```python
# singleton.py
class Singleton:
    pass

instance = Singleton()
```

```python
# 使用
from singleton import instance
```

### 装饰器实现

```python
import threading

def singleton(cls):
    instances = {}
    lock = threading.Lock()

    def get_instance(*args, **kwargs):
        if cls not in instances:
            with lock:
                if cls not in instances:
                    instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance

@singleton
class MySingleton:
    pass
```

---

## C++ 实现

### 饿汉式

```cpp
class Singleton {
private:
    static Singleton instance;
    Singleton() {}

public:
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

    static Singleton& getInstance() {
        return instance;
    }
};

Singleton Singleton::instance;
```

### 懒汉式（线程安全，C++11）

```cpp
#include <mutex>

class Singleton {
private:
    static Singleton* instance;
    static std::mutex mtx;

    Singleton() {}

public:
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

    static Singleton* getInstance() {
        std::lock_guard<std::mutex> lock(mtx);
        if (instance == nullptr) {
            instance = new Singleton();
        }
        return instance;
    }
};

Singleton* Singleton::instance = nullptr;
std::mutex Singleton::mtx;
```

### 局部静态变量（C++11，推荐）

```cpp
class Singleton {
private:
    Singleton() {}

public:
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

    static Singleton& getInstance() {
        static Singleton instance;
        return instance;
    }
};
```

### 双重检查锁定

```cpp
#include <atomic>

class Singleton {
private:
    static std::atomic<Singleton*> instance;
    static std::mutex mtx;

    Singleton() {}

public:
    Singleton(const Singleton&) = delete;
    Singleton& operator=(const Singleton&) = delete;

    static Singleton* getInstance() {
        Singleton* tmp = instance.load(std::memory_order_relaxed);
        std::atomic_thread_fence(std::memory_order_acquire);
        if (tmp == nullptr) {
            std::lock_guard<std::mutex> lock(mtx);
            tmp = instance.load(std::memory_order_relaxed);
            if (tmp == nullptr) {
                tmp = new Singleton();
                std::atomic_thread_fence(std::memory_order_release);
                instance.store(tmp, std::memory_order_relaxed);
            }
        }
        return tmp;
    }
};
```

---

## 应用场景

### 1. 日志系统
日志系统通常只需要一个实例来避免文件冲突和资源竞争。

### 2. 配置管理器
应用配置应该全局唯一，避免配置不一致。

### 3. 数据库连接池
数据库连接池管理整个应用的数据库连接，复用连接提高性能。

### 4. 缓存系统
全局缓存管理器，避免重复缓存。

### 5. 线程池
线程池管理器管理所有工作线程。

### 6. 设备驱动对象
硬件设备驱动通常只需要一个实例。

### 7. 对话框、窗口管理器
UI 应用中的对话框、窗口管理器等。

---

## AI/机器学习/深度学习领域应用

### 1. 模型管理器（Model Manager）
在深度学习训练和推理过程中，单例模式用于管理预训练模型的加载：

```python
class ModelManager:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance.models = {}
        return cls._instance
    
    def load_model(self, model_name, model_path):
        if model_name not in self.models:
            self.models[model_name] = self._load_from_disk(model_path)
        return self.models[model_name]
    
    def get_model(self, model_name):
        return self.models.get(model_name)
```

### 2. GPU资源管理器（GPU Resource Manager）
管理GPU设备分配和显存使用：

```python
class GPUManager:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance.gpu_devices = self._detect_gpus()
            cls._instance.allocated_memory = {}
        return cls._instance
    
    def allocate_gpu(self, gpu_id, memory_requirement):
        # 检查GPU可用性并分配资源
        pass
```

### 3. 训练状态追踪器（Training State Tracker）
全局追踪训练进度、损失值、准确率等指标：

```python
class TrainingTracker:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance.epoch = 0
            cls._instance.loss_history = []
            cls._instance.metrics = {}
        return cls._instance
    
    def update(self, epoch, loss, metrics):
        self.epoch = epoch
        self.loss_history.append(loss)
        for key, value in metrics.items():
            self.metrics[key] = value
```

### 4. 超参数配置中心（Hyperparameter Config Center）
统一管理机器学习实验的超参数：

```python
class HyperparameterConfig:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance.config = self._load_config()
        return cls._instance
    
    def get(self, key, default=None):
        return self.config.get(key, default)
```

### 5. 数据预处理管道（Data Preprocessing Pipeline）
全局数据预处理管道，确保数据处理的一致性：

```python
class DataPreprocessor:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance.transformers = {}
        return cls._instance
    
    def register_transformer(self, name, transformer):
        self.transformers[name] = transformer
    
    def transform(self, data, transformers):
        for name in transformers:
            data = self.transformers[name](data)
        return data
```

### 6. TensorBoard日志记录器（TensorBoard Logger）
全局TensorBoard日志记录器，确保所有训练指标写入同一日志目录：

```python
class TensorBoardLogger:
    _instance = None
    
    def __new__(cls, log_dir=None):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
            cls._instance.writer = SummaryWriter(log_dir)
        return cls._instance
    
    def log_scalar(self, tag, value, step):
        self.writer.add_scalar(tag, value, step)
    
    def close(self):
        self.writer.close()
```

### 应用场景总结

| 应用场景 | AI/ML领域具体应用 | 技术要点 |
|----------|-------------------|----------|
| 模型管理 | 预训练模型加载与缓存 | 避免重复加载，节省内存 |
| GPU资源管理 | 多卡训练资源分配 | 显存管理，设备调度 |
| 训练状态追踪 | 损失、准确率等指标记录 | 全局状态同步 |
| 超参数管理 | 实验配置统一管理 | 配置一致性保障 |
| 数据预处理 | 全局数据变换管道 | 数据处理一致性 |
| 日志记录 | TensorBoard等日志工具 | 统一日志入口 |

---

## 优缺点分析

### 优点

1. **全局访问点**：提供受控的全局访问方式
2. **减少内存开支**：只存在一个实例，减少内存开销
3. **避免资源竞争**：减少同时访问资源时的冲突
4. **实例控制**：单例可以扩展为实例池
5. **懒加载**：可以延迟加载实例

### 缺点

1. **违反单一职责原则**：单例模式职责过重
2. **全局状态污染**：单例会引入全局状态
3. **难以测试**：单例使单元测试困难
4. **隐藏依赖**：单例可能隐藏类之间的依赖
5. **线程安全问题**：需要考虑线程安全
6. **违背开闭原则**：扩展单例类困难

---

## 注意事项

### 1. 线程安全

在多线程环境下，必须确保单例的唯一性。推荐使用：
- C++11 局部静态变量（自动线程安全）
- Java 双重检查锁定 + volatile
- Python threading.Lock

### 2. 序列化问题

如果单例需要序列化：
- Java: 实现 `Serializable` 并提供 `readResolve` 方法
- Python: 自定义 `__reduce__` 方法
- C++: 避免序列化或自定义实现

### 3. 反射攻击防御

防止通过反射调用私有构造函数：
```java
// Java 防御反射攻击
private Singleton() {
    if (instance != null) {
        throw new IllegalStateException("Already instantiated");
    }
}
```

---

## 模式对比

| 模式 | 特点 | 适用场景 |
|------|------|----------|
| 单例模式 | 全局唯一实例 | 只需一个对象的场景 |
| 工厂模式 | 生产对象 | 需要灵活创建对象的场景 |
| 原型模式 | 克隆复制 | 需要复制对象的场景 |
| 建造者模式 | 分步构建 | 构建复杂对象的场景 |
