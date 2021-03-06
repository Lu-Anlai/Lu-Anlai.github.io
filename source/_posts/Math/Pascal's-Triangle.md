---
title: 杨辉三角
date: 2019-02-23 12:48:31
categories: Math
tags:
- 数学
- 杨辉三角
- 组合数
---

杨辉三角是一个形如下面这样的一个三角形。

$$
1 \\
1 \quad 1 \\
1 \quad 2 \quad 1 \\
1 \quad 3 \quad 3 \quad 1 \\
1 \quad 4 \quad 6 \quad 4 \quad 1 \\
...
$$

<!-- more -->

**注：本文中用$\dbinom{n}{k}$代替$C^{k}_{n}$。**

# 杨辉三角的定义

杨辉三角有多种定义，这里简单介绍两种：

记$P_{i,j}$表示杨辉三角从上往下第$i$行，从左往右第$j$列的数字。

那么第一种定义方法可以表示成：

$$
P_{i,j}=
\begin{cases}
1 & {i=1 \quad \text{or} \quad j=i} \\
P_{i-1,j-1}+P_{i-1,j} & {0 < j < i}
\end{cases}
$$

第二种定义方法可以表示为：

$$
P_{i,j}=\dbinom{i-1}{j-1} \quad 0 < j < i
$$

两种定义方法是等价的，证明极其容易，主要原理是$\dbinom{a}{0}=1$以及$\dbinom{n}{k}=\dbinom{n-1}{k-1}+\dbinom{n-1}{k}$。

# 杨辉三角的奇妙之处

## $11$的幂

如果我们将杨辉三角的每一位连起来，我们就会发现第$n$行的数，正好对应$11$的$n-1$次幂。

**注：在十进制下第六层以后要考虑进位。**

$$
1=11^{0} \\
11=11^{1} \\
121=11^{2} \\
1331=11^{3} \\
14641=11^{4} \\
1 \quad 5 \quad 10 \quad 10 \quad 5 \quad 1 \to 161051=11^{5} \\
...
$$

用公式表达为：

$$
\sum^{n}_{i=1} 10^{n-i} P_{n,i} =11^{n-1} \quad n > 0
$$

使用第二种定义可表示为：

$$
\sum^{n}_{i=0} 10^{n-i} \dbinom{n}{i} =11^{n}
$$

### 规律的证明

我们选择使用**二项式定理**证明。

**二项式定理**

$$
(a+b)^{n}=\sum^{n}_{i=0} \dbinom{n}{i} a^{n-i} b^{i}
$$

令$a=10,b=1$，则得

$$
\begin{aligned}
	11^{n} & = (10+1)^{n} \\
	& = \sum^{n}_{i=0} 10^{n-i} \dbinom{n}{i}
\end{aligned}
$$

得证。

## 斐波那契数列

斐波那契数列是一个形如这样的数列：

$$1,1,2,3,5,8,13,21,34,...$$

它的定义是：

$$
f_{i}=
\begin{cases}
1 & i=1 \quad \text{or} \quad i=2 \\
f_{i-1}+f_{i-2} & i \geq 3
\end{cases}
$$

如果我们把杨辉三角排列成一个直角三角形，我们就会发现：

$$
\begin{aligned}
&\swarrow \\
& 1 \swarrow \ \ \swarrow \\
& 1 \quad 1 \swarrow \ \ \swarrow \\
& 1 \quad 2 \quad 1 \swarrow \ \ \swarrow \\
& 1 \quad 3 \quad 3 \quad 1 \swarrow \\
& 1 \quad 4 \quad 6 \quad 4 \quad 1 \\
...
\end{aligned}
$$

如果沿着箭头方向的数字相加，我们就能得到一个斐波那契数列。

## 规律的证明

（未完待续）
