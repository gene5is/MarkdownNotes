---
title: "信号与系统 - 系统的状态变量"
date: 2026-05-09 00:00:00 +0800
categories: [数学, 信号]
tags: [信号, 状态变量, 状态空间]
author: wjj
toc: true
math: true
---

# 系统的状态变量

## 状态变量的基本概念

### 状态的定义

系统的状态是描述系统过去、现在和未来行为的最小一组变量。

**状态变量**：构成状态的变量，记为 $q_1(t), q_2(t), \ldots, q_n(t)$。

**状态向量**：

$$\mathbf{q}(t) = \begin{bmatrix} q_1(t) \\ q_2(t) \\ \vdots \\ q_n(t) \end{bmatrix}$$

### 状态方程的建立

**连续时间系统**：

$$\dot{\mathbf{q}}(t) = \mathbf{A} \mathbf{q}(t) + \mathbf{B} \mathbf{x}(t)$$

$$\mathbf{y}(t) = \mathbf{C} \mathbf{q}(t) + \mathbf{D} \mathbf{x}(t)$$

其中：
- $\mathbf{A}$：状态矩阵（n×n）
- $\mathbf{B}$：输入矩阵（n×p）
- $\mathbf{C}$：输出矩阵（q×n）
- $\mathbf{D}$：直接传输矩阵（q×p）

**离散时间系统**：

$$\mathbf{q}[n+1] = \mathbf{A} \mathbf{q}[n] + \mathbf{B} \mathbf{x}[n]$$

$$\mathbf{y}[n] = \mathbf{C} \mathbf{q}[n] + \mathbf{D} \mathbf{x}[n]$$

### 状态变量的选择

**选择原则**：
- 选择储能元件的输出作为状态变量
- 状态变量应线性无关
- 状态变量个数等于系统阶数

**示例**：RLC电路

$$\begin{cases}
q_1 = i_L \\
q_2 = v_C
\end{cases}$$

## 连续时间系统的状态方程

### 由微分方程建立状态方程

**步骤**：
1. 选择状态变量
2. 写出状态变量的一阶导数表达式
3. 写出输出方程

**示例**：二阶系统

$$y''(t) + a_1 y'(t) + a_0 y(t) = b_1 x'(t) + b_0 x(t)$$

**状态变量选择**：

$$q_1 = y(t)$$

$$q_2 = y'(t)$$

**状态方程**：

$$\begin{bmatrix} \dot{q}_1 \\ \dot{q}_2 \end{bmatrix} = \begin{bmatrix} 0 & 1 \\ -a_0 & -a_1 \end{bmatrix} \begin{bmatrix} q_1 \\ q_2 \end{bmatrix} + \begin{bmatrix} 0 \\ 1 \end{bmatrix} x(t)$$

**输出方程**：

$$y(t) = \begin{bmatrix} b_0 & b_1 \end{bmatrix} \begin{bmatrix} q_1 \\ q_2 \end{bmatrix}$$

### 由传递函数建立状态方程

**直接形式I**：

$$H(s) = \frac{b_m s^m + b_{m-1} s^{m-1} + \cdots + b_0}{s^n + a_{n-1} s^{n-1} + \cdots + a_0}$$

**状态方程**：

$$\mathbf{A} = \begin{bmatrix} 0 & 1 & 0 & \cdots & 0 \\ 0 & 0 & 1 & \cdots & 0 \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & 0 & \cdots & 1 \\ -a_0 & -a_1 & -a_2 & \cdots & -a_{n-1} \end{bmatrix}$$

$$\mathbf{B} = \begin{bmatrix} 0 \\ 0 \\ \vdots \\ 0 \\ 1 \end{bmatrix}$$

**直接形式II**：

$$\mathbf{A} = \begin{bmatrix} 0 & 0 & \cdots & 0 & -a_0 \\ 1 & 0 & \cdots & 0 & -a_1 \\ 0 & 1 & \cdots & 0 & -a_2 \\ \vdots & \vdots & \ddots & \vdots & \vdots \\ 0 & 0 & \cdots & 1 & -a_{n-1} \end{bmatrix}$$

### 由方框图建立状态方程

**步骤**：
1. 在积分器输出端设置状态变量
2. 写出每个状态变量的导数表达式
3. 写出输出方程

## 离散时间系统的状态方程

### 由差分方程建立状态方程

**示例**：二阶差分方程

$$y[n] + a_1 y[n-1] + a_0 y[n-2] = b_1 x[n-1] + b_0 x[n-2]$$

**状态变量选择**：

$$q_1[n] = y[n]$$

$$q_2[n] = y[n-1]$$

**状态方程**：

$$\begin{bmatrix} q_1[n+1] \\ q_2[n+1] \end{bmatrix} = \begin{bmatrix} -a_1 & -a_0 \\ 1 & 0 \end{bmatrix} \begin{bmatrix} q_1[n] \\ q_2[n] \end{bmatrix} + \begin{bmatrix} b_1 & b_0 \\ 0 & 0 \end{bmatrix} \begin{bmatrix} x[n] \\ x[n-1] \end{bmatrix}$$

### 由z域传递函数建立状态方程

**直接形式**：

$$H(z) = \frac{b_m z^m + b_{m-1} z^{m-1} + \cdots + b_0}{z^n + a_{n-1} z^{n-1} + \cdots + a_0}$$

**状态方程**：

$$\mathbf{A} = \begin{bmatrix} 0 & 1 & 0 & \cdots & 0 \\ 0 & 0 & 1 & \cdots & 0 \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & 0 & \cdots & 1 \\ -a_0 & -a_1 & -a_2 & \cdots & -a_{n-1} \end{bmatrix}$$

## 状态方程的求解

### 连续时间系统的时域解

**状态转移矩阵**：

$$\Phi(t) = e^{\mathbf{A}t} = \mathcal{L}^{-1}\{(s\mathbf{I} - \mathbf{A})^{-1}\}$$

**状态方程的解**：

$$\mathbf{q}(t) = \Phi(t) \mathbf{q}(0) + \int_{0}^{t} \Phi(t-\tau) \mathbf{B} \mathbf{x}(\tau) d\tau$$

**输出方程的解**：

$$\mathbf{y}(t) = \mathbf{C} \Phi(t) \mathbf{q}(0) + \mathbf{C} \int_{0}^{t} \Phi(t-\tau) \mathbf{B} \mathbf{x}(\tau) d\tau + \mathbf{D} \mathbf{x}(t)$$

### 离散时间系统的时域解

**状态转移矩阵**：

$$\Phi[n] = \mathbf{A}^n$$

**状态方程的解**：

$$\mathbf{q}[n] = \Phi[n] \mathbf{q}[0] + \sum_{k=0}^{n-1} \Phi[n-k-1] \mathbf{B} \mathbf{x}[k]$$

**输出方程的解**：

$$\mathbf{y}[n] = \mathbf{C} \Phi[n] \mathbf{q}[0] + \mathbf{C} \sum_{k=0}^{n-1} \Phi[n-k-1] \mathbf{B} \mathbf{x}[k] + \mathbf{D} \mathbf{x}[n]$$

## 状态方程的变换域分析

### 拉普拉斯变换法

**连续时间系统**：

$$\mathbf{Q}(s) = (s\mathbf{I} - \mathbf{A})^{-1} \mathbf{q}(0) + (s\mathbf{I} - \mathbf{A})^{-1} \mathbf{B} \mathbf{X}(s)$$

$$\mathbf{Y}(s) = \mathbf{C} (s\mathbf{I} - \mathbf{A})^{-1} \mathbf{q}(0) + \left[ \mathbf{C} (s\mathbf{I} - \mathbf{A})^{-1} \mathbf{B} + \mathbf{D} \right] \mathbf{X}(s)$$

**系统函数矩阵**：

$$\mathbf{H}(s) = \mathbf{C} (s\mathbf{I} - \mathbf{A})^{-1} \mathbf{B} + \mathbf{D}$$

### z变换法

**离散时间系统**：

$$\mathbf{Q}(z) = (z\mathbf{I} - \mathbf{A})^{-1} z \mathbf{q}[0] + (z\mathbf{I} - \mathbf{A})^{-1} \mathbf{B} \mathbf{X}(z)$$

**系统函数矩阵**：

$$\mathbf{H}(z) = \mathbf{C} (z\mathbf{I} - \mathbf{A})^{-1} \mathbf{B} + \mathbf{D}$$

## 状态方程的标准形式

### 对角线标准形

**条件**：$\mathbf{A}$ 有n个不同的特征值。

**变换矩阵**：$\mathbf{P} = [\mathbf{v}_1 \mathbf{v}_2 \cdots \mathbf{v}_n]$，其中 $\mathbf{v}_i$ 为特征向量。

**对角线化**：

$$\mathbf{\Lambda} = \mathbf{P}^{-1} \mathbf{A} \mathbf{P} = \begin{bmatrix} \lambda_1 & 0 & \cdots & 0 \\ 0 & \lambda_2 & \cdots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \cdots & \lambda_n \end{bmatrix}$$

### 约当标准形

**条件**：$\mathbf{A}$ 有重特征值。

**约当块**：

$$\mathbf{J}_k = \begin{bmatrix} \lambda & 1 & 0 & \cdots & 0 \\ 0 & \lambda & 1 & \cdots & 0 \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & 0 & \cdots & \lambda \end{bmatrix}$$

## 系统的可控性与可观性

### 可控性

**定义**：对于任意初始状态 $\mathbf{q}(0)$ 和任意目标状态 $\mathbf{q}(T)$，存在控制输入 $\mathbf{x}(t)$ 使得系统在有限时间 $T$ 内从 $\mathbf{q}(0)$ 转移到 $\mathbf{q}(T)$。

**可控性矩阵**：

$$\mathbf{C}_c = \begin{bmatrix} \mathbf{B} & \mathbf{A}\mathbf{B} & \mathbf{A}^2\mathbf{B} & \cdots & \mathbf{A}^{n-1}\mathbf{B} \end{bmatrix}$$

**可控性判据**：系统完全可控当且仅当 $\text{rank}(\mathbf{C}_c) = n$。

### 可观性

**定义**：通过测量有限时间内的输出 $\mathbf{y}(t)$，可以唯一确定系统的初始状态 $\mathbf{q}(0)$。

**可观性矩阵**：

$$\mathbf{C}_o = \begin{bmatrix} \mathbf{C} \\ \mathbf{C}\mathbf{A} \\ \mathbf{C}\mathbf{A}^2 \\ \vdots \\ \mathbf{C}\mathbf{A}^{n-1} \end{bmatrix}$$

**可观性判据**：系统完全可观当且仅当 $\text{rank}(\mathbf{C}_o) = n$。

### 对偶原理

**可控性与可观性的对偶关系**：

- 系统 $(\mathbf{A}, \mathbf{B}, \mathbf{C})$ 可控 $\Longleftrightarrow$ 系统 $(\mathbf{A}^T, \mathbf{C}^T, \mathbf{B}^T)$ 可观
- 系统 $(\mathbf{A}, \mathbf{B}, \mathbf{C})$ 可观 $\Longleftrightarrow$ 系统 $(\mathbf{A}^T, \mathbf{C}^T, \mathbf{B}^T)$ 可控

## 状态反馈与状态观测器

### 状态反馈

**状态反馈控制律**：

$$\mathbf{u}(t) = -\mathbf{K} \mathbf{q}(t) + \mathbf{r}(t)$$

其中 $\mathbf{K}$ 为反馈增益矩阵，$\mathbf{r}(t)$ 为参考输入。

**闭环系统**：

$$\dot{\mathbf{q}}(t) = (\mathbf{A} - \mathbf{B}\mathbf{K}) \mathbf{q}(t) + \mathbf{B} \mathbf{r}(t)$$

**极点配置**：通过选择 $\mathbf{K}$ 可以任意配置闭环系统的极点。

### 状态观测器

**全阶观测器**：

$$\dot{\hat{\mathbf{q}}}(t) = \mathbf{A} \hat{\mathbf{q}}(t) + \mathbf{B} \mathbf{u}(t) + \mathbf{L} (\mathbf{y}(t) - \hat{\mathbf{y}}(t))$$

其中 $\mathbf{L}$ 为观测器增益矩阵。

**观测误差**：

$$\mathbf{e}(t) = \mathbf{q}(t) - \hat{\mathbf{q}}(t)$$

$$\dot{\mathbf{e}}(t) = (\mathbf{A} - \mathbf{L}\mathbf{C}) \mathbf{e}(t)$$

## 状态变量法的应用

### 控制系统设计

- 极点配置
- 最优控制
- 自适应控制

### 信号处理

- 滤波器设计
- 自适应滤波
- 状态空间建模

### 系统仿真

- 数字仿真
- 实时仿真
- 硬件在环仿真

## 状态变量法的优缺点

### 优点
- 适用于多输入多输出系统
- 提供系统内部状态信息
- 便于计算机实现
- 统一的数学框架

### 缺点
- 状态变量选择不唯一
- 计算复杂度较高
- 需要更多的计算资源

## 状态变量与系统函数的关系

**系统函数**：

$$H(s) = \frac{\mathbf{C} \text{adj}(s\mathbf{I} - \mathbf{A}) \mathbf{B} + \mathbf{D} \det(s\mathbf{I} - \mathbf{A})}{\det(s\mathbf{I} - \mathbf{A})}$$

**特征方程**：

$$\det(s\mathbf{I} - \mathbf{A}) = 0$$

**极点**：特征方程的根，即 $\mathbf{A}$ 的特征值。

## 总结

状态变量法是分析和设计复杂系统的强大工具，它提供了系统内部状态的完整描述，便于进行现代控制理论的各种设计方法。

| 概念 | 描述 |
|------|------|
| 状态向量 | $\mathbf{q}(t) = [q_1, q_2, \ldots, q_n]^T$ |
| 状态方程 | $\dot{\mathbf{q}} = \mathbf{A}\mathbf{q} + \mathbf{B}\mathbf{x}$ |
| 输出方程 | $\mathbf{y} = \mathbf{C}\mathbf{q} + \mathbf{D}\mathbf{x}$ |
| 状态转移矩阵 | $\Phi(t) = e^{\mathbf{A}t}$ |
| 可控性 | $\text{rank}([\mathbf{B}, \mathbf{A}\mathbf{B}, \ldots, \mathbf{A}^{n-1}\mathbf{B}]) = n$ |
| 可观性 | $\text{rank}([\mathbf{C}, \mathbf{C}\mathbf{A}, \ldots, \mathbf{C}\mathbf{A}^{n-1}]^T) = n$ |
