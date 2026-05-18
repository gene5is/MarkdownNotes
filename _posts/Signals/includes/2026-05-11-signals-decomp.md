---
title: "信号与系统 - 信号分解"
date: 2026-05-11 00:00:00 +0800
categories: [数学, 信号]
tags: [信号, 信号分解]
author: wjj
toc: true               
math: true                
---

# 信号分解

## 直流分量和交流分量
原信号 $f(t)$ 可分解为直流分量 $f_D$ 和交流分量 $f_A(t)$


$$
\begin{aligned}
\text{信号平均功率}\ P &= \frac{1}{T} \int_{-\frac{T}{2}}^{\frac{T}{2}} f^2(t)  dt \\
&= \frac{1}{T} \int_{-\frac{T}{2}}^{\frac{T}{2}} [f_D + f_A(t)]^2  dt \\
&= \frac{1}{T} \int_{-\frac{T}{2}}^{\frac{T}{2}} [ f_D^2 + f_A^2(t) + 2f_D f_A(t) ]  dt \\
&= f_D^2 + \frac{1}{T} \int_{-\frac{T}{2}}^{\frac{T}{2}} f_A^2(t)  dt
\end{aligned}
$$


## 偶分量和奇分量

$$
f_e(t) = f_e(-t)
$$

$$
f_o(t) = -f_o(-t)
$$

$$
f_e(t) = \frac{1}{2}[f(t)+f(-t)]
$$

$$
f_o(t) =\frac{1}{2}[f(t)-f(-t)]
$$

## 脉冲分量

$$
f(t_0) = \int_{-\infty}^{\infty}f(t)\delta(t-t_0)dt = \int_{-\infty}^{\infty}f(t)\delta(t_0-t)dt
$$


## 实部分量和虚部分量


$$
f(t) = f_r(t) + jf_i(t)
$$

$$
f^*(t) = f_r(t) - jf_i(t)
$$

$$
f_r(t) = \frac{1}{2}[f(t)+f^*(t)]
$$

$$
jf_i(t) = \frac{1}{2}[f(t)-f^*(t)]
$$

$$
\vert f(t) \vert^2 = f(t)f^*(t) = f_r^2(t)+f_i^2(t)
$$

## 正交函数分量
后续的傅里叶变换