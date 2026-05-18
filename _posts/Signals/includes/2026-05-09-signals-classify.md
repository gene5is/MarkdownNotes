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