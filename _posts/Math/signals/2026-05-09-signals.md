
---

title: "信号"

categories: [信号]

tags: [信号]

---

# 数学基础

## 三角函数

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



# 信号分类
### 指数信号

$$
f(t) = Ke^{at}
$$


### 正弦信号

$$
f(t) = K\sin(\omega t +\theta)
$$

周期 
$T$ 
与角频率
$\omega$ 
和频率 
$f$ 
满足：

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


#### 冲击函数的性质

####



### 冲击偶信号

# 信号分解

# 系统

# 连续时间系统

## 连续时间系统的时域分析

## 傅里叶变换

## 拉普拉斯变换

# 离散时间系统
## 离散时间系统的时域分析

## z变换-离散时间系统的z域分析

## 离散傅里叶变换以及其他离散正交变换
