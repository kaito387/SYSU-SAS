---
title: 信号与系统的时域和频域特性
tags:
  - 信号与系统
  - 频域分析
  - 滤波器
lecture: 6
---

# 第6章 信号与系统的时域和频域特性

## 一、傅里叶变换的模和相位表示

### 1.1 模-相位表示

$$
X(j\omega)=|X(j\omega)|e^{j\angle X(j\omega)}\qquad
X(e^{j\omega})=|X(e^{j\omega})|e^{j\angle X(e^{j\omega})}
$$

两种失真来源：
- **幅度失真**：$|X(j\omega)|$ 改变
- **相位失真**：$\angle X(j\omega)$ 改变

> 在图像中，相位携带了大部分结构信息（轮廓、边缘），幅度决定各频率分量的强度权重。

### 1.2 图像傅里叶变换示例

| 情形 | 效果 |
|------|------|
| 仅保留幅度、相位置零 | 图像完全无法辨认 |
| 仅保留相位、幅度置1 | 仍可辨认图像轮廓 |
| 用图A的相位 + 图B的幅度 | 最终图像更接近图A |

> 结论：相位在信号重建中比幅度更关键。

---

## 二、LTI系统频率响应的模和相位

LTI系统的作用：
$$
Y(j\omega)=X(j\omega)H(j\omega),\quad
|Y(j\omega)|=|X(j\omega)||H(j\omega)|,\quad
\angle Y(j\omega)=\angle H(j\omega)+\angle X(j\omega)
$$

### 2.1 线性与非线性相位

- **线性相位** $H(j\omega)=e^{-j\omega t_0}$ → $y(t)=x(t-t_0)$，仅时延，波形不变
- **非线性相位** → 各频率分量的时移不同，叠加后波形畸变

### 2.2 无失真传输条件

$$
y(t)=kx(t-t_0),\quad y[n]=kx[n-n_0]
$$

| 域 | 连续时间 | 离散时间 |
|----|---------|---------|
| 频域 | $H(j\omega)=ke^{-j\omega t_0}$ | $H(e^{j\omega})=ke^{-j\omega n_0}$ |
| 时域 | $h(t)=k\delta(t-t_0)$ | $h[n]=k\delta[n-n_0]$ |

即：$|H(j\omega)|=k$（常数），$\angle H(j\omega)=-\omega t_0$（线性）。

> 系统若在信号带宽内满足上述条件，则对该信号为不失真系统。$|H(j\omega)|$ 恒为常数的系统称为**全通系统**。

---

## 三、理想频率选择性滤波器

### 3.1 频率特性

| 类型 | 通带 |
|------|------|
| 低通 | $0\sim\omega_c$ |
| 高通 | $\omega> \omega_c$ |
| 带通 | $\omega_1\sim\omega_2$ |
| 带阻 | $0\sim\omega_1$ 和 $\omega>\omega_2$ |

### 3.2 理想低通滤波器的时域特性

$$
H(j\omega)=\begin{cases}1,&|\omega|<\omega_c\\0,&|\omega|>\omega_c\end{cases}
\quad\overset{\mathcal{F}^{-1}}{\longrightarrow}\quad
h(t)=\frac{\sin\omega_c t}{\pi t}=\frac{\omega_c}{\pi}\operatorname{Sa}(\omega_c t)
$$

**问题**：
- $h(t)$ 在 $t<0$ 时非零 → 非因果，物理不可实现
- $h(t)$ 存在振荡（Gibbs 现象）

> 工程中需在时域与频域特性之间折中。后续 6.4~6.7 节不要求。
