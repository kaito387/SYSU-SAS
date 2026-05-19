---
title: 通信系统
tags:
  - 信号与系统
  - 调制解调
  - 复用
lecture: 8
---

# 第8章 通信系统

## 一、正弦幅度调制（DSB）

### 1.1 调制原理

基带信号 $x(t)$ 乘以载波 $c(t)=\cos\omega_c t$：

$$
y(t)=x(t)\cos\omega_c t
$$

频域：$C(j\omega)=\pi[\delta(\omega-\omega_c)+\delta(\omega+\omega_c)]$

$$
Y(j\omega)=\frac{1}{2}[X(j(\omega-\omega_c))+X(j(\omega+\omega_c))]
$$

> 基带频谱被对称搬移到 $\pm\omega_c$ 两侧，同时保留上、下两个边带 → **双边带调制（DSB）**。

---

## 二、正弦幅度调制的解调

### 2.1 同步解调

已调信号再次与同频载波相乘：

$$
\begin{aligned}
w(t)&=y(t)\cos\omega_c t=x(t)\cos^2\omega_c t \\
&=\frac{1}{2}x(t)+\frac{1}{2}x(t)\cos 2\omega_c t
\end{aligned}
$$

低通滤波（截止频率 $W$：$\omega_M<W<2\omega_c-\omega_M$）滤除 $2\omega_c$ 分量，恢复 $x(t)$。

### 2.2 载波相位的影响

调制载波 $\cos(\omega_c t+\theta_c)$，解调载波 $\cos(\omega_c t+\phi_c)$：

$$
w(t)=\frac{1}{2}x(t)\cos(\theta_c-\phi_c)+\frac{1}{2}x(t)\cos(2\omega_c t+\theta_c+\phi_c)
$$

| 条件 | 结果 |
|------|------|
| $\theta_c-\phi_c$ 恒定且 $\neq\pm\pi/2$ | 可解调，输出乘以常数 $\cos(\theta_c-\phi_c)$ |
| $\theta_c-\phi_c=\pm\pi/2$ | $\cos=0$，完全无法解调 |

> 要求调制与解调载波**严格同频同相** → 故名"同步解调"。

---

## 三、频分多路复用（FDM）

每路信号调制到不同载频 $\omega_{c1},\omega_{c2},\dots$，各路频谱在频域不重叠，共用同一信道传输。

解调时先用带通滤波器选出一路信号，再对该路进行同步解调。

---

## 四、单边带正弦幅度调制（SSB）

DSB 信号的上、下边带对称冗余。用边带滤波器滤除一个边带，即可得到**单边带（SSB）**信号，带宽减半。

---

## 五、脉冲串作载波的幅度调制

### 5.1 频域分析

载波为周期脉冲串（周期 $T$，脉宽 $\Delta$）：

$$
C(j\omega)=2\pi\sum_{k=-\infty}^{\infty}a_k\delta\!\left(\omega-\frac{2\pi}{T}k\right),\quad
a_k=\frac{\Delta}{T}\operatorname{sinc}\!\left(\frac{\Delta}{T}k\right)
$$

$$
Y(j\omega)=\sum_{k=-\infty}^{\infty}a_k X\!\left[j\!\left(\omega-\frac{2\pi}{T}k\right)\right]
$$

> $X(j\omega)$ 以 $\omega_s=2\pi/T$ 为周期加权延拓。恢复条件：$2\omega_M<2\pi/T$，低通截止频率 $\omega_M<W<\omega_c-\omega_M$。

### 5.2 时分多路复用（TDM）

能否解调与脉宽 $\Delta$ 无关 → 在一个周期内为每路信号分配一个时隙，只要时隙不重叠即可同时传送多路信号。

| 复用方式 | 域 | 分隔方式 |
|----------|-----|---------|
| FDM | 频域 | 不同载频 |
| TDM | 时域 | 不同时隙 |

---

## 六、脉冲幅度调制（PAM）

### 6.1 基本概念

用 $x(t)$ 在各时隙的样本值 $x(nT)$ 去调制载波脉冲的幅度 → 实质是零阶保持采样。

### 6.2 数字 PAM 与 PCM

| 类型 | 特点 |
|------|------|
| 数字 PAM | 样本 $x(nT)$ 量化，脉冲幅度只有有限个可能值 |
| PCM（脉冲编码调制） | 数字 PAM 再经编码变换为二进制序列，提高传输可靠性 |

> 量化 + 编码 = 数字通信的基础框架。
