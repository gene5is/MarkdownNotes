---
title: "信号与系统 - 拉普拉斯变换"
date: 2026-05-09 00:00:00 +0800
categories: [数学, 信号]
tags: [信号, 拉普拉斯变换]
author: wjj
toc: true
math: true
---

# 拉普拉斯变换

## 从傅里叶变换到拉普拉斯变换

### 傅里叶变换的局限性

傅里叶变换要求信号满足绝对可积条件：

$$\int_{-\infty}^{\infty} |f(t)| dt < \infty$$

许多实际信号（如单位阶跃信号 $u(t)$、正弦信号 $\sin(\omega t)$ 等）并不满足这一条件，因此不存在傅里叶变换。

### 拉普拉斯变换的引入

为了解决傅里叶变换的局限性，引入衰减因子 $e^{-\sigma t}$（收敛因子），将信号 $f(t)$ 乘以衰减因子后进行傅里叶变换：

$$\mathcal{L}\{f(t)\} = F(s) = \int_{-\infty}^{\infty} f(t) e^{-st} dt$$

其中 $s = \sigma + j\omega$ 为复频率变量。

### 双边拉普拉斯变换

**定义**：

$$F(s) = \mathcal{L}\{f(t)\} = \int_{-\infty}^{\infty} f(t) e^{-st} dt$$

**逆变换**：

$$f(t) = \mathcal{L}^{-1}\{F(s)\} = \frac{1}{2\pi j} \int_{\sigma - j\infty}^{\sigma + j\infty} F(s) e^{st} ds$$

### 单边拉普拉斯变换

对于因果信号（ $t < 0$ 时 $f(t) = 0$ ），常用单边拉普拉斯变换：

$$F(s) = \mathcal{L}\{f(t)\} = \int_{0^-}^{\infty} f(t) e^{-st} dt$$

**逆变换**：

$$f(t) = \mathcal{L}^{-1}\{F(s)\} = \frac{1}{2\pi j} \int_{\sigma - j\infty}^{\sigma + j\infty} F(s) e^{st} ds, \quad t \geq 0$$

## 拉普拉斯变换的收敛域

### 收敛域的定义

使积分 $\int_{-\infty}^{\infty} |f(t)e^{-\sigma t}| dt$ 收敛的 $\sigma$ 值范围称为拉普拉斯变换的收敛域（Region of Convergence, ROC）。

### 右边信号（因果信号）

对于因果信号 $f(t) = 0, t < 0$：

$$F(s) = \int_{0}^{\infty} f(t) e^{-st} dt$$

收敛域为 $\text{Re}\{s\} > \sigma_0$， 其中 $\sigma_0$ 称为收敛坐标。

**示例**：指数信号 $f(t) = e^{-at}u(t)$ 的收敛域

$$F(s) = \int_{0}^{\infty} e^{-at} e^{-st} dt = \int_{0}^{\infty} e^{-(s+a)t} dt = \frac{1}{s+a}, \quad \text{Re}\{s\} > -a$$

### 左边信号（反因果信号）

对于反因果信号 $f(t) = 0, t > 0$：

$$F(s) = \int_{-\infty}^{0} f(t) e^{-st} dt$$

收敛域为 $\text{Re}\{s\} < \sigma_0$。

**示例**： $-e^{-at}u(-t)$ 的收敛域

$$F(s) = -\int_{-\infty}^{0} e^{-at} e^{-st} dt = -\int_{-\infty}^{0} e^{-(s+a)t} dt = \frac{1}{s+a}, \quad \text{Re}\{s\} < -a$$

### 双边信号

双边信号的收敛域为两条垂直带状区域：

$$\alpha < \text{Re}\{s\} < \beta$$

**示例**： $f(t) = e^{-a|t|}$ 的收敛域

$$F(s) = \frac{1}{s+a} + \frac{1}{s-a} = \frac{2s}{s^2 - a^2}, \quad -a < \text{Re}\{s\} < a$$

## 典型信号的拉普拉斯变换

### 单位阶跃信号

$$f(t) = u(t)$$

$$\mathcal{L}\{u(t)\} = \int_{0}^{\infty} 1 \cdot e^{-st} dt = \frac{1}{s}, \quad \text{Re}\{s\} > 0$$

### 单位冲激信号

$$f(t) = \delta(t)$$

$$\mathcal{L}\{\delta(t)\} = \int_{0}^{\infty} \delta(t) e^{-st} dt = 1, \quad \text{整个s平面}$$

如果冲激出现在 $t= t_0 (t_0>0)$ 时刻,

$$
\mathcal{L}[\delta(t-t_0)] = \int_0^\infty \delta(t-t_0)e^{-st_0}dt = e^{-st_0}
$$

### 指数信号

$$f(t) = e^{-at}u(t)$$

$$\mathcal{L}\{e^{-at}u(t)\} = \int_{0}^{\infty} e^{-at} e^{-st} dt = \frac{1}{s+a}, \quad \text{Re}\{s\} > -a$$

### 正弦信号

$$f(t) = \sin(\omega t)u(t)$$

$$\mathcal{L}\{\sin(\omega t)u(t)\} = \frac{\omega}{s^2 + \omega^2}, \quad \text{Re}\{s\} > 0$$


$$
f(t) = \sin(\omega t) = \frac{1}{2j}(e^{j\omega t}- e^{-j\omega t}) \\
\mathcal{L}[e^{j\omega t}] = \frac{1}{s-j\omega} \\
\mathcal{L}[e^{-j\omega t}] = \frac{1}{s+j\omega} \\
\mathcal{L}[\sin(\omega t)] = \frac{1}{2j}(\frac{1}{s-j\omega}-\frac{1}{s+j\omega}) = \frac{\omega}{s^2+\omega^2}
$$


### 余弦信号

$$f(t) = \cos(\omega t)u(t)$$

$$\mathcal{L}\{\cos(\omega t)u(t)\} = \frac{s}{s^2 + \omega^2}, \quad \text{Re}\{s\} > 0$$


$$
f(t) = \cos(\omega t) = \frac{1}{2j}(e^{j\omega t} + e^{-j\omega t}) \\
\mathcal{L}[e^{j\omega t}] = \frac{1}{s-j\omega} \\
\mathcal{L}[e^{-j\omega t}] = \frac{1}{s+j\omega} \\
\mathcal{L}[\cos(\omega t)] = \frac{1}{2j}(\frac{1}{s-j\omega}+\frac{1}{s+j\omega}) = \frac{s}{s^2+\omega^2}
$$

### 衰减正弦信号

$$f(t) = e^{-at}\sin(\omega t)u(t)$$

$$\mathcal{L}\{e^{-at}\sin(\omega t)u(t)\} = \frac{\omega}{(s+a)^2 + \omega^2}, \quad \text{Re}\{s\} > -a$$

### 衰减余弦信号

$$f(t) = e^{-at}\cos(\omega t)u(t)$$

$$\mathcal{L}\{e^{-at}\cos(\omega t)u(t)\} = \frac{s+a}{(s+a)^2 + \omega^2}, \quad \text{Re}\{s\} > -a$$

### 幂函数

$$f(t) = t^n u(t)$$

$$\mathcal{L}\{t^n u(t)\}= \frac{n!}{s^{n+1}}, \quad \text{Re}\{s\} > 0$$

$$\mathcal{L}\{t^n u(t)\} = \int_0^\infty t^n e^{-st}dt = -\frac{t^n e^{-st}}{s}|_0^\infty + \frac{n}{s}\int_0^\infty t^{n-1}e^{-st}dt = \frac{n}{s}\int_0^\infty t^{n-1}e^{-st}dt $$

$$
\mathcal{L}[t^n] = \frac{n}{s}\mathcal{L}[t^{n-1}]
$$


特别地， $\mathcal{L}\{t\} = \frac{1}{s^2}$， $\mathcal{L}\{t^2\} = \frac{2}{s^3}$

$$\mathcal{L}\{t^n u(t)\}= \frac{n!}{s^{n+1}}, \quad \text{Re}\{s\} > 0$$

### 斜变信号

$$f(t) = t u(t)$$

$$\mathcal{L}\{t u(t)\} = \frac{1}{s^2}, \quad \text{Re}\{s\} > 0$$

### 冲激偶信号

$$f(t) = \delta'(t)$$

$$\mathcal{L}\{\delta'(t)\} = s, \quad \text{整个s平面}$$

## 拉普拉斯变换的性质

### 线性性质

若 $\mathcal{L}\{f_1(t)\} = F_1(s)$ ， $\mathcal{L}\{f_2(t)\} = F_2(s)$ ，则：

$$\mathcal{L}\{a f_1(t) + b f_2(t)\} = a F_1(s) + b F_2(s)$$

**收敛域**： $F_1(s)$ 和 $F_2(s)$ 收敛域的交集（可能扩大）

### 时移性质

$$\mathcal{L}\{f(t - t_0)u(t - t_0)\} = e^{-st_0} F(s), \quad t_0 > 0$$

**收敛域**：与 $F(s)$ 相同

### 复频移性质（调制定理）

$$\mathcal{L}\{e^{s_0 t} f(t)\} = F(s - s_0)$$

**收敛域**：平移 $\text{Re}\{s_0\}$

### 尺度变换性质

$$\mathcal{L}\{f(at)\} = \frac{1}{|a|} F(\frac{s}{a}), \quad a > 0$$

**收敛域**：按比例变化

### 时域微分性质

若 $\mathcal{L}\{f(t)\} = F(s)$，则：

$$\mathcal{L}\{\frac{df(t)}{dt}\} = sF(s) - f(0^-)$$

**一般形式**：

$$\mathcal{L}\{\frac{d^n f(t)}{dt^n}\} = s^n F(s) - s^{n-1}f(0^-) - s^{n-2}f'(0^-) - \cdots - f^{(n-1)}(0^-)$$

**收敛域**：与 $F(s)$ 相同（可能添加无穷远点）

### 复频域微分性质

$$\mathcal{L}\{t f(t)\} = -\frac{dF(s)}{ds}$$

**一般形式**：

$$\mathcal{L}\{t^n f(t)\} = (-1)^n \frac{d^n F(s)}{ds^n}$$

### 时域积分性质

$$\mathcal{L}\{\int_{-\infty}^{t} f(\tau) d\tau\} = \frac{F(s)}{s} + \frac{f^{-1}(0^-)}{s}$$

其中 $f^{-1}(0^-) = \int_{-\infty}^{0^-} f(\tau) d\tau$

**特例**（因果信号）：

$$\mathcal{L}\{\int_{0}^{t} f(\tau) d\tau\} = \frac{F(s)}{s}$$

### 复频域积分性质

$$\mathcal{L}\{\frac{f(t)}{t}\} = \int_{s}^{\infty} F(\eta) d\eta$$

### 卷积定理

#### 时域卷积定理

$$\mathcal{L}\{f_1(t) * f_2(t)\} = F_1(s) \cdot F_2(s)$$

#### 复频域卷积定理

$$\mathcal{L}\{f_1(t) \cdot f_2(t)\} = \frac{1}{2\pi j} F_1(s) * F_2(s)$$

### 初值定理

**命题**

若 $f(t)$ 在 $t = 0^+$ 不包含冲激函数，则：

$$\lim_{t\to 0_+}f(t) = f(0_+) = \lim_{s \to \infty} sF(s)$$

若 $f(t)$ 包含冲激函数 $k\delta(t)$ ，则： $\mathcal{L}[f(t)] = F(s)=k+F_1(s)$ , 其中 $F_1(s)$ 为真分式， 初值定理表示为

$$
f(0_+) = \lim_{s\to\infty}[sF(s) - ks] \\
\text{或者} \\
f(0_+) = \lim_{s \to \infty} sF(s)
$$ 

**证明**
由原函数时域微分定理知

$$
\begin{aligned}
sF(s) - f(0_-) &= \mathcal{L}[\frac{df(t)}{dt}] \\
&= \int_{0_-}^{\infty} \frac{df(t)}{dt}e^{-st}dt  \\
&=\int_{0_-}^{0_+} \frac{df(t)}{dt}e^{-st}dt + \int_{0_+}^{\infty} \frac{df(t)}{dt}e^{-st}dt \\
&= f(0_+) - f(0_-) + \int_{0_+}^{\infty} \frac{df(t)}{dt}e^{-st}dt \\ 
\end{aligned}
$$

有

$$
sF(s)= f(0_+)+ \int_{0_+}^{\infty} \frac{df(t)}{dt}e^{-st}dt
$$

当 $s\to \infty$ , 有 
$$
\lim_{s\to \infty}[\int_{0_+}^{\infty} \frac{df(t)}{dt}e^{-st}dt] = \int_{0_+}^{\infty} \frac{df(t)}{dt}[\lim_{s\to \infty}e^{-st}]dt = 0
$$

故 $s\to \infty$ ，有

$$
\lim_{s \to \infty} sF(s) = f(0_+)
$$

### 终值定理

**命题**

若 $\lim_{t \to \infty} f(t)$ 存在，则：

$$f(\infty) = \lim_{s \to 0} sF(s)$$

**使用条件**： $sF(s)$ 的收敛域包含 $s = 0$（即 $s = 0$ 在收敛域内或在边界上）

**证明**
由原函数时域微分定理知

$$
\begin{aligned}
sF(s) - f(0_-) &= \mathcal{L}[\frac{df(t)}{dt}] \\
&= \int_{0_-}^{\infty} \frac{df(t)}{dt}e^{-st}dt  \\
&=\int_{0_-}^{0_+} \frac{df(t)}{dt}e^{-st}dt + \int_{0_+}^{\infty} \frac{df(t)}{dt}e^{-st}dt \\
&= f(0_+) - f(0_-) + \int_{0_+}^{\infty} \frac{df(t)}{dt}e^{-st}dt \\ 
\end{aligned}
$$

有

$$
sF(s)= f(0_+)+ \int_{0_+}^{\infty} \frac{df(t)}{dt}e^{-st}dt
$$
 
当 $s\to 0$

$$
\lim_{s\to 0}sF(s) = f(0_+) + \lim_{s\to 0} \int_0^{\infty}\frac{df(t)}{dt}e^{-st}dt = f(0_+) + \lim_{t\to\infty}f(t) - f(0_+) = \lim_{t\to\infty}f(t) 
$$

## 拉普拉斯逆变换

### 部分分式展开法

当 $F(s)$ 为有理函数时，可将其展开为部分分式之和。

#### 单重实数极点

若 $F(s) = \frac{N(s)}{D(s)}$， $s = p_i$ 为单重极点，则：

$$F(s) = \sum_{i=1}^{n} \frac{A_i}{s - p_i}$$

其中系数：

$$A_i = \lim_{s \to p_i} (s - p_i) F(s) = (s - p_i) F(s) \Big|_{s = p_i}$$

#### 共轭复数极点

若 $F(s)$ 包含共轭复数极点 $s = -\alpha \pm j\beta$，可配方法：

$$\frac{s + \alpha}{(s + \alpha)^2 + \beta^2} \Longleftrightarrow e^{-\alpha t}\cos(\beta t)u(t)$$

$$\frac{\beta}{(s + \alpha)^2 + \beta^2} \Longleftrightarrow e^{-\alpha t}\sin(\beta t)u(t)$$

#### 多重极点

若 $s = p_1$ 为 $m$ 阶极点，则：

$$F(s) = \sum_{i=1}^{m} \frac{A_i}{(s - p_1)^i} + \text{其他项}$$

其中：

$$A_i = \frac{1}{(m-i)!} \lim_{s \to p_1} \frac{d^{m-i}}{ds^{m-i}}[(s - p_1)^m F(s)]$$

**时间函数形式**：

$$\frac{1}{(s - p_1)^i} \Longleftrightarrow \frac{t^{i-1}}{(i-1)!} e^{p_1 t} u(t)$$

### 留数法

$$f(t) = \sum_{i} \text{Res}[F(s)e^{st}, p_i]$$

**一阶极点**：

$$\text{Res}[F(s)e^{st}, p_i] = \lim_{s \to p_i} (s - p_i) F(s) e^{st}$$

**$m$ 阶极点**：

$$\text{Res}[F(s)e^{st}, p_i] = \frac{1}{(m-1)!} \lim_{s \to p_i} \frac{d^{m-1}}{ds^{m-1}}[(s - p_i)^m F(s) e^{st}]$$

## 拉普拉斯变换与傅里叶变换的关系

### 关系式

令 $s = \sigma + j\omega$，则：

$$F(\omega) = F(s)\Big|_{s = j\omega} = F(j\omega)$$

即将拉普拉斯变换的收敛轴 $s = j\omega$ 代入即可得到傅里叶变换。

### 收敛域的影响

| 信号类型 | 拉普拉斯变换 | 收敛域 | 傅里叶变换 |
|----------|--------------|--------|------------|
| 右边信号 | $F(s)$ | $\text{Re}\{s\} > \sigma_0$ | $F(j\omega)$（ $\sigma_0 < 0$ ） |
| 左边信号 | $F(s)$ | $\text{Re}\{s\} < \sigma_0$ | $F(j\omega)$（ $\sigma_0 > 0$ ） |
| 双边信号 | $F(s)$ | $\alpha < \text{Re}\{s\} < \beta$ | 部分存在 |

### 常用关系

| 拉普拉斯变换 | 傅里叶变换 |
|-------------|------------|
| $\frac{1}{s+a}$ | $\frac{1}{j\omega + a}$（ $a > 0$ ） |
| $\frac{1}{s}$ | $\pi\delta(\omega) + \frac{1}{j\omega}$ |
| $\frac{1}{s^2}$ | $\pi\delta'(\omega) - \frac{1}{\omega^2}$ |

## 拉普拉斯变换的应用

### 微分方程求解

拉普拉斯变换将微分方程转换为代数方程：

**步骤**：
1. 对微分方程两边进行拉普拉斯变换
2. 利用初始条件，得到 $Y(s)$ 的代数表达式
3. 求 $Y(s)$ 的逆变换得到 $y(t)$

**示例**：求解 $y'(t) + 2y(t) = e^{-t}, \quad y(0) = 1$

1. 两边拉普拉斯变换：
$$sY(s) - y(0) + 2Y(s) = \frac{1}{s+1}$$

2. 代入初始条件：
$$(s + 2)Y(s) - 1 = \frac{1}{s+1}$$

$$Y(s) = \frac{1}{s+1} + \frac{1}{(s+1)(s+2)}$$

3. 部分分式展开：
$$Y(s) = \frac{2}{s+1} - \frac{1}{s+2}$$

4. 逆变换：
$$y(t) = (2e^{-t} - e^{-2t})u(t)$$

### 系统分析

#### 系统函数

线性时不变系统的系统函数（传递函数）定义为：

$$H(s) = \frac{Y(s)}{X(s)} = \mathcal{L}\{h(t)\}$$

其中 $h(t)$ 为系统的单位冲激响应。

#### 系统稳定性

- **因果系统稳定**：所有极点都在左半平面（ $\text{Re}\{p_i\} < 0$ ）
- **BIBO 稳定**：收敛域包含 $j\omega$ 轴

#### 系统因果性

- **线性时不变系统因果** $\Longleftrightarrow$ 收敛域为右边平面（ $\text{Re}\{s\} > \sigma_0$ ）

### 电路分析

拉普拉斯变换可用于分析包含动态元件的电路：

| 元件 | 时域关系 | 复频域阻抗 |
|------|----------|------------|
| 电阻 $R$ | $v(t) = Ri(t)$ | $Z(s) = R$ |
| 电感 $L$ | $v(t) = L\frac{di(t)}{dt}$ | $Z(s) = sL$ |
| 电容 $C$ | $i(t) = C\frac{dv(t)}{dt}$ | $Z(s) = \frac{1}{sC}$ |

**分析步骤**：
1. 将电路元件替换为复频域阻抗
2. 应用直流电路分析方法（欧姆定律、基尔霍夫定律）
3. 求得响应的拉普拉斯变换
4. 逆变换得到时域响应

## 常用拉普拉斯变换表

| 序号 | $f(t)$（$t \geq 0$） | $F(s)$ | 收敛域 |
|------|----------------------|--------|--------|
| 1 | $\delta(t)$ | $1$ | 全部 |
| 2 | $u(t)$ | $\frac{1}{s}$ | $\text{Re}\{s\} > 0$ |
| 3 | $e^{-at}$ | $\frac{1}{s+a}$ | $\text{Re}\{s\} > -a$ |
| 4 | $\sin(\omega t)$ | $\frac{\omega}{s^2+\omega^2}$ | $\text{Re}\{s\} > 0$ |
| 5 | $\cos(\omega t)$ | $\frac{s}{s^2+\omega^2}$ | $\text{Re}\{s\} > 0$ |
| 6 | $t\sin(\omega t)$ | $\frac{2\omega s}{(s^2+\omega^2)^2}$ | $\text{Re}\{s\} > 0$ |
| 7 | $t\cos(\omega t)$ | $\frac{s^2-\omega^2}{(s^2+\omega^2)^2}$ | $\text{Re}\{s\} > 0$ |
| 8 | $e^{-at}\sin(\omega t)$ | $\frac{\omega}{(s+a)^2+\omega^2}$ | $\text{Re}\{s\} > -a$ |
| 9 | $e^{-at}\cos(\omega t)$ | $\frac{s+a}{(s+a)^2+\omega^2}$ | $\text{Re}\{s\} > -a$ |
| 10 | $t$ | $\frac{1}{s^2}$ | $\text{Re}\{s\} > 0$ |
| 11 | $t^n$ | $\frac{n!}{s^{n+1}}$ | $\text{Re}\{s\} > 0$ |
| 12 | $t e^{-at}$ | $\frac{1}{(s+a)^2}$ | $\text{Re}\{s\} > -a$ |
| 13 | $t^n e^{-at}$ (n为正整数) | $\frac{n!}{(s+a)^{n+1}}$ | $\text{Re}\{s\} > -a$ |
| 14 | $\sinh(\omega t)$ | $\frac{\omega}{s^2-\omega^2}$ | $\text{Re}\{s\} > 0$ |
| 15 | $\cosh(\omega t)$ | $\frac{s}{s^2-\omega^2}$ | $\text{Re}\{s\} > 0$ |
| 16 | $f'(t)$ | $sF(s) - f(0^-)$ | — |
| 17 | $\int_{-\infty}^{t} f(\tau)d\tau$ | $\frac{F(s)}{s} + \frac{f^{-1}(0^-)}{s}$ | — |

## 拉式变换性质

$$
\mathcal{L}[f(t)] = F(s) ,\ \mathcal{L}[f_1(t)] = F_1(s),\ \mathcal{L}[f_2(t)] = F_2(s)
$$

|序号 |名称 |结论 |
|------|---------|-------------------|
| 1 | 线性（叠加） | $$\mathcal{L}[K_1f_1(t)+K_2f_2(t)] = K_1F_1(s)+K_2F_2(s)$$ |
| 2 | 对t微分 | $$\begin{aligned}&\mathcal{L}[\frac{df(t)}{dt}] = sF(s)-f(0) \\ &\mathcal{L}[\frac{d^nf(t)}{dt}] = s^nF(s) - \sum_{r=0}^{n-1} s^{n-r-1}f^{(r)}(0) \end{aligned}$$ |
| 3 | 对t积分| $$\mathcal{L}[\int_{-\infty}^t f(\tau)d\tau] = \frac{F(s)}{s} + \frac{f^{-1}(0)}{s}$$|
| 4 | 时域平移| $$\mathcal{L}[f(t-t_0)u(t-t_0)] = e^{-st_0}F(s)$$|
| 5 | s域平移| $$\mathcal{L}[f(t)e^{-at}] = F(s+a)$$|
| 6 | 尺度变换| $$\mathcal{L}[f(at)] = \frac{1}{a}F(\frac{s}{a})$$|
| 7 | 初值| $$\lim_{t\to 0}f(t) = \lim_{s\to\infty}sF(s)$$|
| 8 | 终止| $$\lim_{t\to\infty} = \lim_{s\to0}sF(s)$$|
| 9 | 卷积| $$\mathcal{L}[\int_0^tf_1(\tau)f_2(t-\tau)dt]=F_1(s)F_2(s)$$|
| 10 | 相乘| $$\frac{1}{2\pi j}\int_{\sigma-j\infty}^{\sigma+j\infty}F_1(p)F_2(s-p)dp = \mathcal{L}[f_1(t)f_2(t)]$$|
| 11 | 对s微分 | $$\mathcal{L}[-tf(t)] = \frac{dF(s)}{ds}$$|
| 12 | 对s积分| $$\mathcal{L}[\frac{f(t)}{t}]= \int_s^\infty F(s)ds$$| 
