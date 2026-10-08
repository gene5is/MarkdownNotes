---
title: "信号与系统 - 信号分类"
date: 2026-05-09 00:00:00 +0800
categories: [数学, 信号]
tags: [信号, 信号分类]
author: wjj
toc: true               
math: true                
---

# 信号分类

- 确定性信号与随机信号
    - 确定性信号（规则信号）：若信号被表示为一确定的时间函数，对于指定的某一时刻，可确定一相应的函数值
    - 随机信号：实际传输的信号具有不可预知的不确定性
- 周期信号与非周期信号
    - 周期信号：依一定的时间间隔周而复始且无始无终的信号
    - 非周期信号：当周期信号的周期T趋于无穷大时，成为非周期信号
- 连续时间信号与离散时间信号
    - 连续信号：在所讨论的时间间隔内，除若干不连续点之外，对于任意时间值都可给出确定的函数值，称此信号为连续信号
        - 模拟信号：连续信号的时间和幅值都连续的信号
        - 量化信号：时间连续但幅值是有限个不连续的点
    - 离散信号：时间上不连续的信号
        - 抽样信号：时间不连续但幅值连续
        - 数字信号：时间和幅值都不连续

**按时间与幅值的连续性分类**：

| 信号类型 | 时间 | 幅值 |
|---------|------|------|
| 模拟信号 | 连续 | 连续 |
| 量化信号 | 连续 | 离散 |
| 抽样信号 | 离散 | 连续 |
| 数字信号 | 离散 | 离散 |

### 指数信号

$$
f(t) = Ke^{at}
$$


### 正弦信号

$$
f(t) = K\sin(\omega t +\theta)
$$

周期 $T$ 与角频率 $\omega$ 和频率 $f$ 满足：

$$
T = \frac{2\pi}{\omega} = \frac{1}{f}
$$

### 复指数信号

$$
f(t) = Ke^{st}= Ke^{\sigma+j\omega} = Ke^{\sigma t}\cos(\omega t) + jKe^{\sigma t}\sin(\omega t)
$$

### 抽样信号

$$
Sa(t) = \frac{\sin t}{t}
$$

$$
sinc(t) = \frac{\sin(\pi t)}{\pi t}
$$

$$
\int_{0}^\infty Sa(t) dt = \frac{\pi}{2}
$$

$$
\int_{-\infty}^\infty Sa(t) dt = \pi
$$

### 钟形信号

$$
f(t) = Ee^{-(\frac{t}{\tau})^2}
$$


### 单位斜变信号

$$
f(t) = \begin{cases} 
0 \quad (t<0) \\ 
t \quad (t\geq 0)
 \end{cases}
$$

$$
f(t - t_0) =
\begin{cases}
0 & \text{if } t < t_0 \\ 
t - t_0 & \text{if } t \geq t_0
\end{cases}
$$

### 单位阶跃信号

$$
u(t) = 
\begin{cases} 
0 \quad (t<0) \\
1 \quad (t\geq 0)
 \end{cases}
$$

#### 矩形脉冲

$$
R_T(t) = u(t) - u(t-T)
$$

$$
G_T(t) = u(t+\frac{T}{2}) - u(t-\frac{T}{2})
$$




#### 符号函数

$$
sgn(t) = 2u(t) - 1
$$

### 冲激信号

$$
\delta(t) = \lim_{t\to 0} \frac{1}{\tau}[u(t+\frac{\tau}{2})-u(t-\frac{\tau}{2})]
$$

狄拉克的定义：

$$
\begin{cases}
\int_{-\infty}^{\infty}\delta(t)dt =1\\
\delta(t) = 0 \quad (t\neq 0)
\end{cases}
$$

#### 用三角形脉冲表示冲激函数

$$
\delta(t) =  \lim_{\tau  \to 0}\{\frac{1}{\tau}(1-\frac{\vert t \vert}{\tau})[u(t+\tau) - u(t-\tau)] \}
$$


#### 用双边指数脉冲表示冲激函数

$$
\delta(t) = \lim_{\tau  \to 0}(\frac{1}{2\tau}e^{-\frac{\vert t\vert}{\tau}})
$$


#### 用钟形脉冲表示冲激函数

$$
\delta(t) = \lim_{\tau \to 0}(\frac{1}{\tau}e^{-\pi (\frac{t}{\tau})^2})
$$

#### 用抽样信号表示冲激函数

$$
\delta(t) = \lim_{k \to \infty} [ \frac{k}{\pi}Sa(kt)]
$$


#### 冲激函数的性质

$$
u(t) = \int_{-\infty}^{t}\delta(\tau)d\tau = 
\begin{cases}
 1 \quad(t>0)\\
 0 \quad(t\leq 0)
\end{cases}
$$

$$
\frac{d}{dt}u(t) = \delta(t)
$$

$$
\delta(t) = \delta(-t)
$$

$$
\int_{-\infty}^{\infty}\delta(t)f(t)dt = \int_{-\infty}^{\infty}\delta(t)f(0)dt = f(0)\int_{-\infty}^{\infty}\delta(t)dt = f(0)
$$

$$
\int_{-\infty}^{\infty}\delta(t-t_0)f(t)dt = \int_{-\infty}^{\infty}\delta(t-t_0)f(0)dt = f(0)\int_{-\infty}^{\infty}\delta(t-t_0)dt = f(t_0)
$$


### 冲激偶信号

#### 冲激偶信号的性质

$$
\int_{-\infty}^{\infty} \delta'(t) f(t)dt = f(t)\delta(t)  \vert _{-\infty}^{\infty} - \int_{-\infty}^{\infty}f'(t)\delta(t)dt =-f'(0)
$$

$$
\int_{-\infty}^{\infty}\delta'(t)dt = 0
$$
