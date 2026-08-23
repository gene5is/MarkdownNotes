---
title: "信号与系统 - 卷积"
date: 2026-05-09 00:00:00 +0800
categories: [数学, 信号]
tags: [信号, 卷积, 卷积积分, 卷积和]
author: wjj
toc: true
math: true
---

# 卷积

卷积是线性时不变系统时域分析的核心运算，描述了信号通过系统时输入、系统特性与输出之间的关系。

## 信号的卷积分解

由[信号分解]({% post_url 2026-05-09-signals-decomp %})中的脉冲分解，任意信号 $f(t)$ 可表示为冲激信号的加权积分：

$$f(t) = \int_{-\infty}^{\infty} f(\tau) \delta(t - \tau)  d\tau$$

将 $\delta(t-\tau)$ 视为对系统的作用，由 LTI 系统的线性与时不变性，可得到系统输出的卷积表示。

## 卷积积分的定义

### 定义

设 $f(t)$ 为输入， $h(t)$ 为系统的冲激响应，则零状态响应为：

$$y(t) = f(t) * h(t) = \int_{-\infty}^{\infty} f(\tau) h(t - \tau)  d\tau$$

### 推导

1. 系统对 $\delta(t)$ 的响应为 $h(t)$
2. 由时不变性：系统对 $\delta(t-\tau)$ 的响应为 $h(t-\tau)$
3. 由齐次性：系统对 $f(\tau)\delta(t-\tau)  d\tau$ 的响应为 $f(\tau)h(t-\tau)  d\tau$
4. 由叠加性：对 $\tau$ 积分得 $y(t) = \int f(\tau)h(t-\tau)  d\tau$

## 卷积积分的图解法

**步骤**：

1. **换元**：将 $f(t)$、 $h(t)$ 中的自变量换为 $\tau$，得 $f(\tau)$、 $h(\tau)$
2. **反转**：将 $h(\tau)$ 反转得 $h(-\tau)$
3. **移位**：将 $h(-\tau)$ 平移 $t$ 得 $h(t-\tau)$
4. **相乘**：计算 $f(\tau) \cdot h(t-\tau)$
5. **积分**：对 $\tau$ 积分得 $y(t)$

**积分限的确定**：积分限由 $f(\tau)$ 与 $h(t-\tau)$ 非零区间的重叠部分决定。

## 卷积积分的性质

### 交换律

$$f(t) * h(t) = h(t) * f(t)$$

### 结合律

$$[f(t) * h_1(t)] * h_2(t) = f(t) * [h_1(t) * h_2(t)]$$

### 分配律

$$f(t) * [h_1(t) + h_2(t)] = f(t) * h_1(t) + f(t) * h_2(t)$$

### 时移性质

$$f(t - t_1) * h(t - t_2) = y(t - t_1 - t_2)$$

### 微分性质

$$\frac{d}{dt}[f(t) * h(t)] = f'(t) * h(t) = f(t) * h'(t)$$

$$\frac{d^n}{dt^n}[f(t) * h(t)] = f^{(n)}(t) * h(t) = f(t) * h^{(n)}(t)$$

### 积分性质

$$\int_{-\infty}^{t} [f(\tau) * h(\tau)]  d\tau = \left[\int_{-\infty}^{t} f(\tau)  d\tau\right] * h(t) = f(t) * \left[\int_{-\infty}^{t} h(\tau)  d\tau\right]$$

### 与冲激函数的卷积

$$f(t) * \delta(t) = f(t)$$

$$f(t) * \delta(t - t_0) = f(t - t_0)$$

$$f(t) * \delta'(t) = f'(t)$$

### 与阶跃函数的卷积

$$f(t) * u(t) = \int_{-\infty}^{t} f(\tau)  d\tau$$

### 尺度性质

$$f(at) * h(at) = \frac{1}{|a|} y(at)$$

## 卷积和

### 定义

离散时间信号的卷积和为：

$$y[n] = x[n] * h[n] = \sum_{k=-\infty}^{\infty} x[k] h[n - k]$$

> 卷积和的性质（交换律、结合律、分配律、时移）、图解计算步骤及常用卷积和表详见[离散时间系统的时域分析]({% post_url 2026-05-09-discrete-time %})，其形式与卷积积分完全对应。

### 离散与连续的对应关系

| 连续时间 | 离散时间 |
|------|------|
| 积分 $\int$ | 求和 $\sum$ |
| 冲激函数 $\delta(t)$ | 单位脉冲 $\delta[n]$ |
| 阶跃函数 $u(t)$ | 单位阶跃 $u[n]$ |
| 卷积积分 | 卷积和 |

## 卷积与系统响应

### 零状态响应

LTI 系统的零状态响应等于输入与冲激响应的卷积：

$$y_{zs}(t) = f(t) * h(t)$$

### 因果性

连续时间因果系统的冲激响应满足：

$$h(t) = 0, \quad t < 0$$

此时卷积积分限可写为：

$$y(t) = \int_{0}^{\infty} f(t - \tau) h(\tau)  d\tau = \int_{-\infty}^{t} f(\tau) h(t - \tau)  d\tau$$

### 稳定性

连续时间 LTI 系统 BIBO 稳定的充要条件是冲激响应绝对可积：

$$\int_{-\infty}^{\infty} |h(t)|  dt < \infty$$

## 常用卷积积分

| 序号 | $f_1(t)$ | $f_2(t)$ | $f_1(t) * f_2(t)$ |
|----|----|----|----|
| 1 | $\delta(t)$ | $f(t)$ | $f(t)$ |
| 2 | $u(t)$ | $u(t)$ | $t u(t)$ |
| 3 | $u(t)$ | $t u(t)$ | $\frac{1}{2} t^2 u(t)$ |
| 4 | $e^{at}u(t)$ | $u(t)$ | $\frac{1}{a}(e^{at}-1)u(t) \quad (a \neq 0)$ |
| 5 | $e^{at}u(t)$ | $e^{bt}u(t)$ | $\frac{e^{bt}-e^{at}}{b-a}u(t) \quad (a \neq b)$ |
| 6 | $e^{at}u(t)$ | $e^{at}u(t)$ | $t e^{at}u(t)$ |
| 7 | $e^{at}u(t)$ | $t u(t)$ | $\frac{e^{at} - at - 1}{a^2} u(t) \quad (a \neq 0)$ |
| 8 | $\sin(\omega t)u(t)$ | $u(t)$ | $\frac{1}{\omega}(1 - \cos(\omega t))u(t)$ |
| 9 | $\cos(\omega t)u(t)$ | $u(t)$ | $\frac{1}{\omega}\sin(\omega t)u(t)$ |

## 卷积定理

卷积运算在变换域中转化为乘积，是连接时域与频域/复频域的桥梁。

**时域卷积定理**：

$$\mathcal{F}\{f(t) * h(t)\} = F(\omega) \cdot H(\omega)$$

$$\mathcal{L}\{f(t) * h(t)\} = F(s) \cdot H(s)$$

**频域卷积定理**：

$$\mathcal{F}\{f(t) \cdot h(t)\} = \frac{1}{2\pi} F(\omega) * H(\omega)$$

**系统函数**：

$$H(\omega) = \frac{Y(\omega)}{F(\omega)}, \quad H(s) = \frac{Y(s)}{F(s)}$$

> 卷积定理的详细推导与应用分别见[傅里叶变换]({% post_url 2026-05-09-fourier-transform %})、[拉普拉斯变换]({% post_url 2026-05-09-laplace-transform %})与[z变换]({% post_url 2026-05-09-z-transform %})各章。
