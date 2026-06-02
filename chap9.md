---
title: 拉普拉斯变换
tags:
  - 信号与系统
  - 复频域分析
  - 拉普拉斯变换
lecture: "09"
---

# 第9章 拉普拉斯变换

## 9.0 引言

傅里叶变换以 $e^{j\omega t}$ 为基底分解信号；拉普拉斯变换以更一般的 $e^{st}\ (s=\sigma+j\omega)$ 为基底。$s=j\omega$ 时退化为傅里叶变换。拉普拉斯变换（及 z 变换）覆盖傅里叶分析的全部能力，且能处理傅里叶方法不适用的情形。

---

## 9.1 双边拉普拉斯变换

**定义**：

$$X(s) = \int_{-\infty}^{\infty} x(t)e^{-st}dt, \quad s = \sigma + j\omega$$

- $\sigma=0$ 时即为傅里叶变换：$X(s)|_{s=j\omega} = X(j\omega)$
- 本质：$X(s) = \mathcal{F}[x(t)e^{-\sigma t}]$，即 $x(t)e^{-\sigma t}$ 的傅里叶变换

**例**：
- $x(t)=e^{-at}u(t) \xrightarrow{\mathcal{L}} X(s)=\frac{1}{s+a},\ \mathrm{Re}[s]>-a$
- $x(t)=-e^{-at}u(-t) \xrightarrow{\mathcal{L}} X(s)=\frac{1}{s+a},\ \mathrm{Re}[s]<-a$

> 不同信号可有相同 $X(s)$ 表达式，靠 **ROC**（收敛域）区分。$X(s)$ 表达式 + ROC 才与信号一一对应。

### 零极点图

若 $X(s)$ 为有理函数：

$$X(s) = \frac{N(s)}{D(s)} = M\frac{\prod_i(s-\beta_i)}{\prod_i(s-\alpha_i)}$$

- **零点**：分子根 $\beta_i$；**极点**：分母根 $\alpha_i$
- 零极点图 + ROC 可唯一确定 $X(s)$（最多差常数因子 $M$）
- ROC 总是各分量 ROC 的交集，边界平行于 $j\omega$ 轴，与分母根对应

---

## 9.2 收敛域（ROC）的性质

| # | 性质 | 说明 |
|---|------|------|
| 1 | 带状区域 | ROC 是 $s$ 平面内平行于 $j\omega$ 轴的带形区域 |
| 2 | 无极点 | 有理 $X(s)$ 的 ROC 内无极点 |
| 3 | 时限信号 | 绝对可积的时限信号，ROC = 整个 $s$ 平面 |
| 4 | 右边信号 | ROC 位于最右边极点的右边 |
| 5 | 左边信号 | ROC 位于最左边极点的左边 |
| 6 | 双边信号 | ROC 为相邻两极点的带形区域 |
| 7 | 极点分割 | 有理 $X(s)$ 的 ROC 总是由极点分割 |

> 性质 4/5 推导核心：若 $\sigma_0$ 在 ROC 内，则对 $\sigma_1 > \sigma_0$（右边信号），$\int |x(t)|e^{-\sigma_1 t}dt \leq e^{-(\sigma_1-\sigma_0)T}\int |x(t)|e^{-\sigma_0 t}dt < \infty$。

---

## 9.3 拉普拉斯反变换

**定义**：

$$x(t) = \frac{1}{2\pi j}\int_{\sigma-j\infty}^{\sigma+j\infty} X(s)e^{st}ds$$

> $x(t)$ 被分解为复振幅 $\frac{1}{2\pi j}X(s)ds$ 的复指数信号 $e^{st}$ 的线性组合。

### 部分分式展开法

1. 将 $X(s)$ 展开为部分分式
2. 根据 ROC 确定每一项的 ROC
3. 利用常用变换对 + 性质逐项反变换

**例**：$X(s)=\frac{1}{(s+1)(s+2)}$，极点 $s=-1,-2$，三种 ROC → 三种信号：
- $\mathrm{Re}[s]>-1$：右边信号
- $\mathrm{Re}[s]<-2$：左边信号
- $-2<\mathrm{Re}[s]<-1$：双边信号，$x(t)=-e^{-2t}u(t)-e^{-t}u(-t)$

---

## 9.4 由零极点图对傅里叶变换几何求值

若 $X(s)$ 的 ROC 包含 $j\omega$ 轴，则 $X(j\omega)$ 可由零极点图几何求值：

$$|X(j\omega)| = M\frac{\prod_i |\vec{v}_{zi}|}{\prod_j |\vec{v}_{pj}|},\quad \angle X(j\omega) = \sum_i \angle\vec{v}_{zi} - \sum_j \angle\vec{v}_{pj}$$

其中 $\vec{v}_{zi}$ 是从零点 $\beta_i$ 到 $j\omega$ 的矢量，$\vec{v}_{pj}$ 是从极点 $\alpha_j$ 到 $j\omega$ 的矢量。

**应用**：
- **一阶系统** $H(s)=\frac{1/\tau}{s+1/\tau}$：$|H(j\omega)|$ 在 $\omega=0$ 最大，$|\omega|=1/\tau$ 时降为 $1/\sqrt{2}$
- **全通系统** $H(s)=\frac{s-a}{s+a}$：零点与极点关于 $j\omega$ 轴对称，$|H(j\omega)|=1$，用于相位均衡

---

## 9.5 拉普拉斯变换的性质

| # | 性质 | 公式 | ROC |
|---|------|------|-----|
| 1 | 线性 | $ax_1+bx_2 \leftrightarrow aX_1+bX_2$ | $\supseteq R_1\cap R_2$ |
| 2 | 时移 | $x(t-t_0) \leftrightarrow X(s)e^{-st_0}$ | $R$（不变） |
| 3 | $s$ 域平移 | $x(t)e^{s_0t} \leftrightarrow X(s-s_0)$ | $R+\mathrm{Re}[s_0]$ |
| 4 | 尺度变换 | $x(at) \leftrightarrow \frac{1}{|a|}X(\frac{s}{a})$ | $aR$ |
| 5 | 共轭 | $x^*(t) \leftrightarrow X^*(s^*)$ | $R$ |
| 6 | 卷积 | $x_1*x_2 \leftrightarrow X_1X_2$ | $\supseteq R_1\cap R_2$ |
| 7 | 时域微分 | $\frac{dx}{dt} \leftrightarrow sX(s)$ | 包含 $R$，可能扩大 |
| 8 | $s$ 域微分 | $-tx(t) \leftrightarrow \frac{dX(s)}{ds}$ | $R$ |
| 9 | 时域积分 | $\int_{-\infty}^t x(\tau)d\tau \leftrightarrow \frac{1}{s}X(s)$ | $R\cap(\mathrm{Re}[s]>0)$ |
| 10 | 初值/终值 | $x(0^+)=\lim_{s\to\infty}sX(s)$; $\lim_{t\to\infty}x(t)=\lim_{s\to 0}sX(s)$ | 因果信号，终值要求极点全在左半平面（$s=0$ 最多单极点） |

> 卷积/线性性质中 ROC 可能因零极点相消而扩大。

---

## 9.7 用拉普拉斯变换分析与表征 LTI 系统

### 系统函数

$$Y(s) = X(s) \cdot H(s)$$

$H(s) = \mathcal{L}[h(t)]$ 称为**系统函数/传递函数**。$H(s)$ + ROC 完全描述 LTI 系统。

### 因果性与稳定性

| 属性 | 条件 |
|------|------|
| 因果系统 | $h(t)$ 右边信号，$H(s)$ 的 ROC 是最右边极点的右边 |
| 反因果系统 | $h(t)$ 左边信号，ROC 是最左边极点的左边 |
| 稳定系统 | ROC 包含 $j\omega$ 轴（充要条件） |
| 因果稳定 | ROC 为包含 $j\omega$ 轴的右半平面 |

### 由微分方程求系统函数

$$H(s) = \frac{Y(s)}{X(s)} = \frac{\sum_{k=0}^M b_k s^k}{\sum_{k=0}^N a_k s^k}$$

若系统满足初始松弛条件（因果 LTI），ROC 为最右边极点的右边。

### 巴特沃斯低通滤波器

模平方函数：$|B(j\omega)|^2 = \frac{1}{1+(j\omega/j\omega_c)^{2N}}$

- $\omega=0$ 处前 $2N-1$ 阶导数为零（最大平坦性）；通带/阻带内单调下降；$\omega=\omega_c$ 时幅度为 $1/\sqrt{2}$
- 拓展到 $s$ 平面：$B(s)B(-s) = \frac{1}{1+(s/j\omega_c)^{2N}}$，共 $2N$ 个极点等间隔分布于半径 $\omega_c$ 的圆上
- 因果稳定系统取左半平面 $N$ 个极点：

$$B(s) = \frac{\omega_c^N}{\prod_{k=0}^{N-1}(s-s_k)},\quad s_k = \omega_c \exp\!\left[j\!\left(\frac{\pi(2k+1)}{2N}+\frac{\pi}{2}\right)\right]$$

---

## 9.8 系统函数的代数属性与方框图

### 互联方式

| 方式 | $H(s)$ | ROC |
|------|--------|-----|
| 级联 | $H_1(s)H_2(s)$ | $\supseteq R_1\cap R_2$ |
| 并联 | $H_1(s)+H_2(s)$ | $\supseteq R_1\cap R_2$ |
| 反馈 | $\frac{H_1(s)}{1+G(s)H_1(s)}$ | $\supseteq R_1\cap R_2$ |

### 方框图实现

- **直接型**：从 $s^nY(s) = X(s) - \sum a_k s^k Y(s)$ 出发，级联积分器实现
- **级联型**：$H(s)$ 分解为一阶/二阶子系统之积
- **并联型**：$H(s)$ 部分分式展开，各分式并联

> 零极点相消在方框图中可能导致不可控/不可观的问题。

---

## 9.9 单边拉普拉斯变换

**定义**：

$$\mathcal{X}(s) = \int_{0^-}^{\infty} x(t)e^{-st}dt$$

仅考虑 $t \geq 0^-$ 部分。因果信号的单边与双边 LT 相同。ROC 必为最右边极点的右边，无多义性。

### 时域微分（关键区别）

$$\frac{dx(t)}{dt} \xleftrightarrow{\mathcal{L}_u} s\mathcal{X}(s) - x(0^-)$$

$$\frac{d^2x(t)}{dt^2} \xleftrightarrow{\mathcal{L}_u} s^2\mathcal{X}(s) - sx(0^-) - x'(0^-)$$

### 求解含初始条件的微分方程

对微分方程两边做单边 LT → 代入初始条件 → 分解为零输入响应 + 零状态响应：

$$\mathcal{Y}(s) = \underbrace{\frac{y(0^-)(s+3)+y'(0^-)}{s^2+3s+2}}_{\text{零输入响应}} + \underbrace{\frac{\mathcal{X}(s)}{s^2+3s+2}}_{\text{零状态响应}}$$

> 单边 LT 是分析增量线性系统（非零初始条件的 LTI 系统）的核心工具。

---

## 本章知识图谱

```mermaid
graph TD
    A[拉普拉斯变换] --> B[双边 LT]
    A --> C[单边 LT]
    B --> D[定义: X(s)=∫x(t)e^{-st}dt]
    B --> E[ROC 性质]
    B --> F[反变换: 部分分式]
    B --> G[几何求值: 零极点图→H(jω)]
    B --> H[性质: 线性/时移/卷积/微分…]
    B --> I[系统分析: H(s), 因果性, 稳定性]
    I --> J[巴特沃斯滤波器]
    I --> K[方框图: 级联/并联/反馈]
    C --> L[定义: 积分从 0⁻ 起]
    C --> M[时域微分: s𝒳(s)-x(0⁻)]
    C --> N[增量线性系统求解]
```
