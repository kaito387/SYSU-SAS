---
title: 采样
tags:
  - 信号与系统
  - 采样定理
  - 重建
lecture: 7
---

# 第7章 采样

## 一、用样本表示连续时间信号：采样定理

### 1.1 冲激串采样（理想采样）

**时域**：
$$
p(t)=\sum_{n=-\infty}^{\infty}\delta(t-nT),\quad
x_p(t)=x(t)p(t)=\sum_{n=-\infty}^{\infty}x(nT)\delta(t-nT)
$$

**频域**（$P(j\omega)=\frac{2\pi}{T}\sum_{k=-\infty}^{\infty}\delta(\omega-k\omega_s),\;\omega_s=\frac{2\pi}{T}$）：
$$
X_p(j\omega)=\frac{1}{2\pi}X(j\omega)*P(j\omega)=\frac{1}{T}\sum_{k=-\infty}^{\infty}X(j(\omega-k\omega_s))
$$

> 时域理想采样 = 频域以 $\omega_s$ 为周期延拓 $X(j\omega)$。

### 1.2 Nyquist 采样定理

要从 $X_p(j\omega)$ 不失真恢复 $X(j\omega)$，须满足：
1. $x(t)$ **带限**，最高频率 $\omega_M$
2. 采样频率 $\omega_s>2\omega_M$（Nyquist 条件）

恢复方法：理想低通滤波器，截止频率满足 $\omega_M<\omega_c<\omega_s-\omega_M$，通带增益 $T$（补偿采样引入的 $1/T$ 衰减）。

> **Nyquist 采样定理**：带限于 $\omega_M$ 的信号 $x(t)$，若以 $\omega_s>2\omega_M$ 进行理想采样，则 $x(t)$ 可由样本 $x(nT)$ 唯一确定。

### 1.3 零阶保持采样

零阶保持 = 理想采样后级联零阶保持系统 $h_0(t)$（脉宽 $T$ 的矩形脉冲）。

$$
H_0(j\omega)=\frac{2\sin(\omega T/2)}{\omega}e^{-j\omega T/2}
$$

恢复需再级联 $H_r(j\omega)=\frac{H(j\omega)}{H_0(j\omega)}$，其中 $H(j\omega)$ 为理想低通。

---

## 二、利用内插从样本重建信号

### 2.1 理想内插（带限内插）

以理想低通的 $h(t)$ 为内插函数：

$$
x(t)=x_p(t)*h(t)=\sum_{n=-\infty}^{\infty}x(nT)h(t-nT)
$$

取 $\omega_c=\omega_s/2=\pi/T$ 时：
$$
h(t)=T\cdot\frac{\sin\omega_c t}{\pi t}=\operatorname{Sa}(\omega_c t)
$$

$$
\boxed{x(t)=\sum_{n=-\infty}^{\infty}x(nT)\cdot\operatorname{Sa}[\omega_c(t-nT)]}
$$

> 每个样本 $x(nT)$ 加权一个 $\operatorname{Sa}$ 函数，所有加权 $\operatorname{Sa}$ 叠加精确重建原信号。

---

## 三、欠采样与频谱混叠

不满足 $\omega_s>2\omega_M$ 时，频谱周期延拓发生**混叠**（aliasing），无法通过理想内插恢复原信号。

但混叠后在采样点上仍有 $x_r(nT)=x(nT)$。

**例**：$x(t)=\cos\omega_0 t$，当 $\omega_0<\omega_s<2\omega_0$ 时混叠，恢复信号为 $x_r(t)=\cos[(\omega_s-\omega_0)t]$——频率变为 $\omega_s-\omega_0$，即原频率关于 $\omega_s/2$ 的"镜像"。
