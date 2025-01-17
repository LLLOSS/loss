---
title: 波函数、Dirac表示与矩阵表示的对比
# 隐藏的模块
hide:
  #  - navigation # 隐藏左边导航
  #  - toc #隐藏右边导航
  #  - footer #隐藏翻页
  #  - feedback  #隐藏反馈
tags:
  - 量子力学
---

# **波函数、Dirac 表示与矩阵表示的对比**

## **微观粒子的运动状态**

### 表示形式

#### **波函数表示：**

微观粒子状态通过波函数 $\psi(x)$ 描述，模平方 $|\psi(x)|^2$ 表示粒子在位置 $x$ 的概率密度。

波函数满足薛定谔方程：

$$
i\hbar \frac{\partial \psi(x,t)}{\partial t} = \hat{H} \psi(x,t)
$$

#### **Dirac 表示**

在 Dirac 表示中，量子态通过**态矢量** $|\psi\rangle$ 表示，称为右矢，是波函数的一种抽象形式。

对于任意算符 $\hat{A}$，其作用在态矢量上表现为：

$$
\hat{A} |\psi\rangle
$$

相应地，左矢是右矢的共轭转置，用 $\langle \psi|$ 表示。

如果右矢 $|\psi\rangle$ 是列向量~~（当然这有点像矩阵表示）~~：

$$
|\psi\rangle = \begin{pmatrix}
a_1 \\
a_2 \\
\vdots \\
a_n
\end{pmatrix}
$$

则左矢 $\langle \psi|$ 是其共轭转置，即：

$$
\langle \psi| = \begin{pmatrix}
a_1^* & a_2^* & \cdots & a_n^*
\end{pmatrix}
$$

#### **矩阵表示**

在矩阵表示中，态矢量表示为列向量：

$$
|\psi\rangle = \begin{pmatrix} a_1 \\ a_2 \\ \vdots \\ a_n \end{pmatrix}
$$

相应的力学量（算符）用**矩阵**表示，态的演化可通过**矩阵运算**进行。

### 归一化、束缚态、游离态

#### **波函数表示**

**归一化条件**：

$$
\int |\psi(x)|^2 dx = 1
$$

**束缚态**：

波函数在无穷远趋于零：

$$
\lim_{|x| \to \infty} \psi(x) = 0
$$

能量对应哈密顿算符的离散本征值。

**游离态**：

波函数在无穷远处不归零，通常为平面波形式：

$$
\psi(x) \sim e^{ikx}
$$

能量对应哈密顿算符的连续本征值。

#### **Dirac 表示**

**归一化条件**：

$$
\langle \psi | \psi \rangle = 1
$$

**束缚态**：

能量离散，对应哈密顿算符的离散本征值 $\{E_n\}$：

$$
\hat{H} |\psi_n\rangle = E_n |\psi_n\rangle
$$

态矢量在**完备基**中展开为有限和：

$$
|\psi\rangle = \sum_n c_n |\psi_n\rangle
$$

**游离态**：

能量连续，对应哈密顿算符的连续本征值 ：

$$
\hat{H} |\psi_E\rangle = E |\psi_E\rangle
$$

游离态的正交性用狄拉克归一化表示（真正交，假归一）：

$$
\langle \psi_E | \psi_{E'} \rangle = \delta(E - E')
$$

#### **矩阵表示**

**归一化条件**：

$$
\psi^\dagger \psi = 1
$$

**束缚态**：

本征值为离散的矩阵特征值。

对应的态分量在有限维空间中用列向量表示。

**游离态**：

本征值为连续的矩阵特征值。

对应态分量在无穷维空间中表示。

### 正交

#### **波函数表示**

在波函数表示中，不同状态的正交性表明波函数的内积为零，即：

$$
\int \psi_m^*(x) \psi_n(x) dx = 0, \quad m \neq n
$$

对于连续谱中的游离态，其正交性满足狄拉克归一化条件：

$$
\int \psi_E^*(x) \psi_{E'}(x) dx = \delta(E - E')
$$

#### **Dirac 表示中**

在 Dirac 表示中，量子态的正交性体现在内积为零：

$$
\langle \psi_m | \psi_n \rangle = 0, \quad m \neq n
$$

对于离散谱的束缚态，正交性条件为：

$$
\langle \psi_n | \psi_m \rangle = \delta_{nm}
$$

对于连续谱的游离态，正交性条件满足狄拉克归一化：

$$
\langle \psi_E | \psi_{E'} \rangle = \delta(E - E')
$$

#### **矩阵表示**

在矩阵表示中，态矢量的正交性用向量内积表示：

$$
\psi_m^\dagger \psi_n = 0, \quad m \neq n
$$

其中 $\psi_m^\dagger$ 是态矢量 $\psi_m$ 的共轭转置。

对于离散态的正交性：

$$
\psi_n^\dagger \psi_m = \delta_{nm}
$$

对于连续态的正交性，满足狄拉克归一化条件：

$$
\psi_E^\dagger \psi_{E'} = \delta(E - E')
$$

## **力学量**

### **矩阵元**

**波函数表示**：

矩阵元通过波函数积分定义：

$$
A_{ij} = \int \psi_i^*(x) \hat{A} \psi_j(x) dx
$$

**Dirac 表示**：

矩阵元表示为：

$$
A_{ij} = \langle \phi_i | \hat{A} | \phi_j \rangle
$$

**矩阵表示**：

力学量 $\hat{A}$ 的矩阵表示为：

$$
A_{ij} = \psi_i^\dagger \hat{A} \psi_j
$$

### **共轭算符**

**波函数表示：**

在波函数表示中，共轭算符 $\hat{A}^\dagger$ 满足：

$$
\int \psi^*(x) \left(\hat{A}^\dagger \phi(x)\right) dx = \int \left(\hat{A} \psi(x)\right)^* \phi(x) dx
$$

**Dirac 表示：**

在 Dirac 表示中，共轭算符 $\hat{A}^\dagger$ 满足：

$$
\langle \psi | \hat{A}^\dagger \phi \rangle = \langle \phi | \hat{A} \psi \rangle^*
$$

**矩阵表示：**

在矩阵表示中，共轭算符 $\hat{A}^\dagger$ 表现为矩阵的共轭转置：

$$
A^\dagger = (A^*)^T
$$

### **厄米算符**

**波函数表示**：
波函数表示下，厄米算符的性质可以通过积分形式表示出来：

$$
\int \phi^*(x) \hat{A} \psi(x) \, dx = \int \psi^*(x) \hat{A} \phi(x) \, dx
$$

**Dirac 表示**：

$$
\langle \phi | \hat{A} | \psi \rangle = \langle \psi | \hat{A} | \phi \rangle^*
$$

**矩阵表示**：

$$
A_{ij} = A^*_{ji}
$$

## 力学量的本征方程

**波函数表示**

$$
\hat{A} \psi = a \psi
$$

**Dirac 表示**：

$$
\hat{A} |\psi\rangle = a |\psi\rangle
$$

**矩阵表示**：

$$
A \psi = a \psi
$$

~~不知道写点啥~~

## **态的线性叠加**

**波函数表示**

量子态波函数的线性叠加为：

$$
\psi = c_1 \psi_1 + c_2 \psi_2 + ···
$$

**Dirac 表示**

态矢量的线性叠加为：

$$
|\psi\rangle = c_1 |\psi_1\rangle + c_2 |\psi_2\rangle + ···
$$

**矩阵表示**

向量叠加为：

$$
\psi = c_1 \psi_1 + c_2 \psi_2 + ···
$$

## **力学量的平均值**

**波函数表示**：

平均值通过积分定义为：

$$
\langle A \rangle = \int \psi^*(x) \hat{A} \psi(x) dx
$$

**Dirac 表示**：

平均值表示为：

$$
\langle A \rangle = \langle \psi | \hat{A} | \psi \rangle
$$

**矩阵表示**：

平均值为：

$$
\langle A \rangle = \psi^\dagger A \psi
$$

最后这一部分不知道该写些什么，可能是我学艺不精吧。整理至此。
