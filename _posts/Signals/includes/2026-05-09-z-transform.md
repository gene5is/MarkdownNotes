---
title: "信号与系统 - z变换、离散时间系统的z域分析"
date: 2026-05-09 00:00:00 +0800
categories: [数学, 信号]
tags: [信号, z变换, z域分析]
author: wjj
toc: true
math: true
---

# z变换、离散时间系统的z域分析

## z变换的定义

### 双边z变换

**定义**：

$$X(z) = \mathcal{Z}\{x[n]\} = \sum_{n=-\infty}^{\infty} x[n] z^{-n}$$

其中 $z$ 是复变量，$z = re^{j\omega}$。

### 单边z变换

**定义**：

$$X(z) = \mathcal{Z}\{x[n]u[n]\} = \sum_{n=0}^{\infty} x[n] z^{-n}$$

### 收敛域

使级数 $\sum_{n=-\infty}^{\infty} |x[n] z^{-n}|$ 收敛的 $z$ 值范围称为收敛域（ROC）。

## 典型序列的z变换

### 单位脉冲序列

$$\mathcal{Z}\{\delta[n]\} = 1, \quad \text{整个z平面}$$

### 单位阶跃序列

$$\mathcal{Z}\{u[n]\} = \frac{1}{1-z^{-1}} = \frac{z}{z-1}, \quad |z| > 1$$

### 指数序列

$$\mathcal{Z}\{a^n u[n]\} = \frac{1}{1-a z^{-1}} = \frac{z}{z-a}, \quad |z| > |a|$$

### 正弦序列

$$\mathcal{Z}\{\sin(\omega_0 n)u[n]\} = \frac{z \sin(\omega_0)}{z^2 - 2z \cos(\omega_0) + 1}, \quad |z| > 1$$

### 余弦序列

$$\mathcal{Z}\{\cos(\omega_0 n)u[n]\} = \frac{z(z - \cos(\omega_0))}{z^2 - 2z \cos(\omega_0) + 1}, \quad |z| > 1$$

### 衰减指数序列

$$\mathcal{Z}\{a^n \sin(\omega_0 n)u[n]\} = \frac{a z \sin(\omega_0)}{z^2 - 2a z \cos(\omega_0) + a^2}, \quad |z| > |a|$$

### 幂序列

$$\mathcal{Z}\{n u[n]\} = \frac{z}{(z-1)^2}, \quad |z| > 1$$

$$\mathcal{Z}\{n^2 u[n]\} = \frac{z(z+1)}{(z-1)^3}, \quad |z| > 1$$

## z变换的性质

### 线性性质

$$\mathcal{Z}\{a x_1[n] + b x_2[n]\} = a X_1(z) + b X_2(z)$$

### 时移性质

**右移**：

$$\mathcal{Z}\{x[n-m]u[n-m]\} = z^{-m} X(z)$$

**左移**：

$$\mathcal{Z}\{x[n+m]u[n]\} = z^m \left(X(z) - \sum_{k=0}^{m-1} x[k] z^{-k}\right)$$

### z域尺度变换

$$\mathcal{Z}\{a^n x[n]\} = X\left(\frac{z}{a}\right)$$

### 时域反转

$$\mathcal{Z}\{x[-n]\} = X\left(\frac{1}{z}\right)$$

### 卷积定理

**时域卷积**：

$$\mathcal{Z}\{x_1[n] * x_2[n]\} = X_1(z) \cdot X_2(z)$$

**z域卷积**：

$$\mathcal{Z}\{x_1[n] \cdot x_2[n]\} = \frac{1}{2\pi j} \oint_{C} X_1(v) X_2\left(\frac{z}{v}\right) \frac{dv}{v}$$

### 差分性质

**一阶差分**：

$$\mathcal{Z}\{x[n] - x[n-1]\} = (1 - z^{-1}) X(z)$$

**二阶差分**：

$$\mathcal{Z}\{x[n] - 2x[n-1] + x[n-2]\} = (1 - z^{-1})^2 X(z)$$

### z域微分

$$\mathcal{Z}\{n x[n]\} = -z \frac{dX(z)}{dz}$$

$$\mathcal{Z}\{n^k x[n]\} = \left(-z \frac{d}{dz}\right)^k X(z)$$

### 初值定理

$$x[0] = \lim_{z \to \infty} X(z)$$

### 终值定理

$$x[\infty] = \lim_{z \to 1} (z-1) X(z)$$

**条件**：$(z-1)X(z)$ 的极点都在单位圆内。

## z逆变换

### 幂级数展开法

**长除法**：

$$X(z) = \frac{b_0 + b_1 z^{-1} + \cdots + b_M z^{-M}}{a_0 + a_1 z^{-1} + \cdots + a_N z^{-N}}$$

### 部分分式展开法

**单极点**：

$$X(z) = \sum_{k=1}^{N} \frac{A_k z}{z - p_k}$$

其中 $A_k = \lim_{z \to p_k} (z - p_k) \frac{X(z)}{z}$

**共轭复数极点**：

$$\frac{A z}{z - re^{j\theta}} + \frac{A^* z}{z - re^{-j\theta}} \Longleftrightarrow 2|A| r^n \cos(n\theta + \arg A) u[n]$$

**多重极点**：

$$\frac{A_1 z}{z - p} + \frac{A_2 z}{(z - p)^2} + \cdots + \frac{A_m z}{(z - p)^m}$$

### 留数法

$$x[n] = \frac{1}{2\pi j} \oint_{C} X(z) z^{n-1} dz = \sum_{k=1}^{N} \text{Res}[X(z) z^{n-1}, p_k]$$

## 离散时间系统的z域分析

### 系统函数

**定义**：

$$H(z) = \frac{Y(z)}{X(z)} = \mathcal{Z}\{h[n]\}$$

**差分方程**：

$$\sum_{k=0}^{N} a_k y[n-k] = \sum_{m=0}^{M} b_m x[n-m]$$

**z域表示**：

$$H(z) = \frac{\sum_{m=0}^{M} b_m z^{-m}}{\sum_{k=0}^{N} a_k z^{-k}}$$

### 系统的稳定性

**因果系统稳定条件**：所有极点都在单位圆内。

$$|p_k| < 1, \quad \forall k$$

### 系统的频率响应

**定义**：

$$H(e^{j\omega}) = H(z)\Big|_{z=e^{j\omega}} = |H(e^{j\omega})| e^{j\varphi(\omega)}$$

**幅度响应**：

$$|H(e^{j\omega})| = \left| \frac{\sum_{m=0}^{M} b_m e^{-j\omega m}}{\sum_{k=0}^{N} a_k e^{-j\omega k}} \right|$$

**相位响应**：

$$\varphi(\omega) = \arg\left( \frac{\sum_{m=0}^{M} b_m e^{-j\omega m}}{\sum_{k=0}^{N} a_k e^{-j\omega k}} \right)$$

### 系统的因果性

**因果系统**：单位脉冲响应 $h[n] = 0, n < 0$

**充分必要条件**：系统函数 $H(z)$ 的收敛域为 $|z| > R$（$R$ 为最大极点模）。

## z变换与拉普拉斯变换的关系

### 映射关系

$$z = e^{sT}$$

其中 $T$ 为采样周期。

### s平面到z平面的映射

| s平面 | z平面 |
|--------|--------|
| 虚轴（$s = j\omega$） | 单位圆（$|z| = 1$） |
| 左半平面（$\text{Re}\{s\} < 0$） | 单位圆内（$|z| < 1$） |
| 右半平面（$\text{Re}\{s\} > 0$） | 单位圆外（$|z| > 1$） |

### 频率映射

$$\omega_d = \Omega T$$

其中 $\omega_d$ 为数字频率，$\Omega$ 为模拟频率。

## 常用z变换表

| 序号 | $x[n]$（$n \geq 0$） | $X(z)$ | 收敛域 |
|------|----------------------|--------|--------|
| 1 | $\delta[n]$ | $1$ | 全部 |
| 2 | $u[n]$ | $\frac{z}{z-1}$ | $\|z\| > 1$ |
| 3 | $a^n$ | $\frac{z}{z-a}$ | $\|z\| > \|a\|$ |
| 4 | $n$ | $\frac{z}{(z-1)^2}$ | $\|z\| > 1$ |
| 5 | $n^2$ | $\frac{z(z+1)}{(z-1)^3}$ | $\|z\| > 1$ |
| 6 | $\sin(\omega_0 n)$ | $\frac{z \sin(\omega_0)}{z^2 - 2z \cos(\omega_0) + 1}$ | $\|z\| > 1$ |
| 7 | $\cos(\omega_0 n)$ | $\frac{z(z - \cos(\omega_0))}{z^2 - 2z \cos(\omega_0) + 1}$ | $\|z\| > 1$ |
| 8 | $a^n \sin(\omega_0 n)$ | $\frac{a z \sin(\omega_0)}{z^2 - 2a z \cos(\omega_0) + a^2}$ | $\|z\| > \|a\|$ |
| 9 | $a^n \cos(\omega_0 n)$ | $\frac{z(z - a \cos(\omega_0))}{z^2 - 2a z \cos(\omega_0) + a^2}$ | $\|z\| > \|a\|$ |
| 10 | $x[n-1]u[n-1]$ | $z^{-1} X(z)$ | — |
| 11 | $x[n+1]u[n]$ | $z X(z) - z x[0]$ | — |
| 12 | $n x[n]$ | $-z \frac{dX(z)}{dz}$ | — |
