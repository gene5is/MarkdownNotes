---
title: "信号与系统 - 数学基础"
date: 2026-05-09 00:00:00 +0800
categories: [数学, 信号]
tags: [信号, 数学基础]
author: wjj
toc: true               
math: true                
---

# 数学基础

## 三角函数基本公式

$$
\sin(\alpha+\beta) = \sin\alpha\cos\beta+\cos\alpha\sin\beta
$$

$$
\sin(\alpha-\beta) = \sin\alpha\cos\beta-\cos\alpha\sin\beta
$$

$$
\cos(\alpha+\beta) = \cos\alpha\cos\beta-\sin\alpha\sin\beta
$$

$$
\cos(\alpha-\beta) = \cos\alpha\cos\beta+\sin\alpha\sin\beta
$$


## 三角函数积化和差

$$
\sin\alpha\cos\beta = \frac{1}{2}[\sin(\alpha+\beta)+\sin(\alpha-\beta)]
$$

$$
\cos\alpha\sin\beta = \frac{1}{2}[\sin(\alpha+\beta)-\sin(\alpha-\beta)]
$$

$$
\cos\alpha\cos\beta = \frac{1}{2}[\cos(\alpha+\beta)+\cos(\alpha-\beta)]
$$

$$
\sin\alpha\sin\beta = \frac{1}{2}[\cos(\alpha-\beta)-\cos(\alpha+\beta)]
$$




## 三角函数和差化积

$$
\sin\alpha+ \sin \beta = 2\sin\frac{\alpha+\beta}{2}\cos\frac{\alpha-\beta}{2}
$$


$$
\sin\alpha - \sin \beta = 2\cos\frac{\alpha+\beta}{2}\sin\frac{\alpha-\beta}{2}
$$


$$
\cos\alpha + \cos \beta = 2\cos\frac{\alpha+\beta}{2}\cos\frac{\alpha-\beta}{2}
$$

$$
\cos\alpha - \cos \beta = 2\sin\frac{\alpha+\beta}{2}\sin\frac{\alpha-\beta}{2}
$$




## 欧拉公式

$$
e^{j\omega t} = \cos(\omega t) + j\sin(\omega t)
$$

$$
e^{-j\omega t} = \cos(\omega t) - j\sin(\omega t)
$$

$$
\cos(\omega t) = \frac{1}{2}(e^{j\omega t} + e^{-j\omega t})
$$

$$
\sin(\omega t) = \frac{1}{2j} (e^{j\omega t} - e^{-j\omega t})
$$

## 正交函数集

*定义*: 在区间 $(t_1,t_2)$ 上的函数集 $\{g_1(t), g_2(t), \ldots, g_n(t)\}$ ，当所有函数在区间 $(t_1, t_2)$ 上满足下列条件时

$$
\int_{t_1}^{t_2}g_i(t)g_j(t)dt = 
\begin{cases}  
0 & (i\neq j) \\
k_i \neq 0 & (i=j)
\end{cases}
$$

则称此函数集为区间 $(t_1,t_2)$ 上的正交函数集

$\cos t$ , $\cos 2t$ $\ldots$ $\cos nt$ (n为正整数) 在 $(0,2\pi)$ 上是正交函数集

$$
\int_0^{2\pi}cos(nt)cos(mt)dt = \frac{1}{2}\int_0^{2\pi}cos[(n+m)t]dt - \frac{1}{2}\int_0^{2\pi}cos[(n-m)t]dt
$$

$n \neq m$ 时
$n = m$ 时

## 完备正交函数集
### 三角函数集

$\{ 1, \sin n \omega t, \cos n \omega t \}$ 其中 $T = \frac{2\pi}{\omega}$