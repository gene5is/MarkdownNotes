---
title: "信号与系统 - 离散时间系统的时域分析"
date: 2026-05-09 00:00:00 +0800
categories: [数学, 信号]
tags: [信号, 离散时间系统, 时域分析]
author: wjj
toc: true
math: true
---

# 离散时间系统的时域分析

## 离散时间信号

### 离散时间信号的表示

离散时间信号是定义在离散时刻 $n$（ $n$ 为整数）的信号，记为 $x[n]$。

**示例**：
- 单位脉冲序列： $\delta[n] = \begin{cases} 1, & n=0 \\ 0, & n \neq 0 \end{cases}$
- 单位阶跃序列： $u[n] = \begin{cases} 1, & n \geq 0 \\ 0, & n < 0 \end{cases}$
- 矩形序列： $R_N[n] = \begin{cases} 1, & 0 \leq n \leq N-1 \\ 0, & \text{其他} \end{cases}$

### 常用离散信号

**指数序列**：

$$x[n] = a^n u[n]$$

**正弦序列**：

$$x[n] = \sin(\omega n)u[n]$$

**复指数序列**：

$$x[n] = e^{j\omega n} = \cos(\omega n) + j\sin(\omega n)$$

**抽样信号**：

$$Sa[n] = \frac{\sin(\omega n)}{\omega n}$$

### 信号的基本运算

**移位**： $y[n] = x[n - n_0]$

**反转**： $y[n] = x[-n]$

**尺度变换**： $y[n] = x[kn]$（ $k$ 为整数）

**加法**： $y[n] = x_1[n] + x_2[n]$

**乘法**： $y[n] = x_1[n] \cdot x_2[n]$

### 离散时间信号的分解

**单位脉冲分解**：

$$x[n] = \sum_{k=-\infty}^{\infty} x[k] \delta[n-k]$$

## 离散时间系统

### 线性时不变系统

**线性性质**：

$$T\{a x_1[n] + b x_2[n]\} = a T\{x_1[n]\} + b T\{x_2[n]\}$$

**时不变性质**：

$$\text{若 } T\{x[n]\} = y[n], \text{ 则 } T\{x[n-n_0]\} = y[n-n_0]$$

### 差分方程

**一阶差分**：

$$\Delta x[n] = x[n] - x[n-1]$$

**二阶差分**：

$$\Delta^2 x[n] = \Delta(\Delta x[n]) = x[n] - 2x[n-1] + x[n-2]$$

**线性常系数差分方程**：

$$\sum_{k=0}^{N} a_k y[n-k] = \sum_{m=0}^{M} b_m x[n-m]$$

### 单位脉冲响应

线性时不变系统对单位脉冲 $\delta[n]$ 的响应称为单位脉冲响应，记为 $h[n]$。

**系统输出**：

$$y[n] = x[n] * h[n] = \sum_{k=-\infty}^{\infty} x[k] h[n-k]$$

## 卷积和

### 卷积和的定义

$$y[n] = x[n] * h[n] = \sum_{k=-\infty}^{\infty} x[k] h[n-k]$$

### 卷积和的性质

**交换律**：

$$x[n] * h[n] = h[n] * x[n]$$

**结合律**：

$$(x[n] * h_1[n]) * h_2[n] = x[n] * (h_1[n] * h_2[n])$$

**分配律**：

$$x[n] * (h_1[n] + h_2[n]) = x[n] * h_1[n] + x[n] * h_2[n]$$

**时移性质**：

$$x[n-n_1] * h[n-n_2] = y[n-n_1-n_2]$$

### 卷积和的计算

**图解法步骤**：
1. 反转：将 $h[k]$ 反转得到 $h[-k]$
2. 移位：将 $h[-k]$ 移位 $n$ 位得到 $h[n-k]$
3. 相乘： $x[k] \cdot h[n-k]$
4. 求和： $\sum_{k=-\infty}^{\infty} x[k] h[n-k]$

## 差分方程的时域解法

### 递推法

**示例**：求解 $y[n] - 0.5y[n-1] = x[n], \quad y[-1] = 1$

$$y[n] = 0.5y[n-1] + x[n]$$

### 经典解法

**齐次解 + 特解**：

1. **齐次方程**： $\sum_{k=0}^{N} a_k y_h[n-k] = 0$
2. **特征方程**： $\sum_{k=0}^{N} a_k r^k = 0$
3. **齐次解**： $y_h[n] = \sum_{i=1}^{N} A_i r_i^n$（单根情况）
4. **特解**：根据激励形式假设特解形式
5. **完全解**： $y[n] = y_h[n] + y_p[n]$
6. **确定系数**：利用初始条件确定 $A_i$

### 零输入响应和零状态响应

**零输入响应**（仅由初始条件引起）：

$$y_{zi}[n] = \sum_{i=1}^{N} A_i r_i^n$$

**零状态响应**（仅由输入引起）：

$$y_{zs}[n] = x[n] * h[n]$$

**完全响应**：

$$y[n] = y_{zi}[n] + y_{zs}[n]$$

## 系统的因果性和稳定性

### 因果性

系统是因果的当且仅当：

$$h[n] = 0, \quad n < 0$$

### 稳定性

系统是稳定的当且仅当单位脉冲响应绝对可和：

$$\sum_{n=-\infty}^{\infty} |h[n]| < \infty$$

### 因果稳定系统

$$h[n] = 0, \quad n < 0 \quad \text{且} \quad \sum_{n=0}^{\infty} |h[n]| < \infty$$

## 离散时间系统的时域特性

### 记忆系统与无记忆系统

**无记忆系统**：输出仅取决于当前输入

$$y[n] = F(x[n])$$

**记忆系统**：输出与过去或未来输入有关

### 线性系统的判断

**叠加性**： $T\{x_1[n] + x_2[n]\} = T\{x_1[n]\} + T\{x_2[n]\}$

**齐次性**： $T\{a x[n]\} = a T\{x[n]\}$

### 时不变系统的判断

$$T\{x[n-n_0]\} = y[n-n_0]$$

## 状态方程

### 状态变量的选择

**选择原则**：选择系统的储能元件的输出作为状态变量

### 状态方程的建立

**一阶系统**：

$$
\begin{cases}
q[n+1] = a q[n] + b x[n] \\
y[n] = c q[n] + d x[n]
\end{cases}
$$

**矩阵形式**：

$$
\begin{bmatrix} q_1[n+1] \\
q_2[n+1] \\
\vdots \\ q_N[n+1] 
\end{bmatrix} = 
\begin{bmatrix} 
a_{11} & a_{12} & \cdots & a_{1N} \\
a_{21} & a_{22} & \cdots & a_{2N} \\
\vdots & \vdots & \ddots & \vdots \\
a_{N1} & a_{N2} & \cdots & a_{NN} 
\end{bmatrix}
\begin{bmatrix} 
q_1[n] \\ q_2[n] \\ \vdots \\ q_N[n] 
\end{bmatrix} +
\begin{bmatrix} 
b_1 \\ b_2 \\ \vdots \\ b_N 
\end{bmatrix} x[n]
$$

$$
y[n] = 
\begin{bmatrix} 
c_1 & c_2 & \cdots & c_N 
\end{bmatrix} 
\begin{bmatrix} 
q_1[n] \\ q_2[n] \\ \vdots \\ q_N[n] 
\end{bmatrix} + d x[n]
$$

## 离散时间系统的时域分析总结

| 概念 | 描述 |
|------|------|
| 单位脉冲响应 | $h[n] = T\{\delta[n]\}$ |
| 卷积和 | $y[n] = x[n] * h[n]$ |
| 差分方程 | $\sum_{k=0}^{N} a_k y[n-k] = \sum_{m=0}^{M} b_m x[n-m]$ |
| 零输入响应 | 仅由初始条件引起 |
| 零状态响应 | 仅由输入引起 |
| 因果性 | $h[n] = 0, n < 0$ |
| 稳定性 | $\sum_{n=-\infty}^{\infty} \|h[n]\| < \infty$ |
