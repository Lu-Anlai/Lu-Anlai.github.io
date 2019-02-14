---
title: '【题解】【洛谷 P4825】 [USACO15FEB]Cow Hopscotch (Silver) 牛跳房子(银)'
date: 2019-02-14 21:50:48
categories: 题解
tags:
- 题解
- 洛谷
- 动态规划
---

## 原题

题面请查看[洛谷 P4825 [USACO15FEB]Cow Hopscotch (Silver) 牛跳房子(银)](https://www.luogu.org/problemnew/show/P4825)。

## 题解

动态规划

<!-- more -->

### 思路

直接动态规划即可，状态转移方程为：

$$f_{ij}=\begin{cases} 1 & {i=j=1} \newline \sum^{i-1}\limits_{k=1} \sum^{j-1}\limits_{l=1} f_{kl} & {a_{ij} \neq a_{kl}} \end{cases}$$

#### 时间复杂度分析

时间复杂度为$\Omega (\frac{n^{4}-n^{2}}{2}),O (\frac{n^{4}}{2})$。

（注：$n$即为题目中的$R,C$）

需要注意的一点是：

> 如果将数据范围代入算法对应的多项式时间复杂度，所得的数字小于$5 \times 10^{7}$，则这个算法可以在$1 \text{s}$内通过。

把$n=100$带入$\frac{n^{4}}{2}$，得$T(n)=\frac{100^{4}}{2}=5 \times 10^{7}$，预计可以通过。

##### 提示

另外，程序运行时间也与计算机性能有关，主要是$\text{CPU}$主频这个参数。

在$\text{C/C++}$中，你可以运行下面这个程序来获取$\text{CPU}$型号和主频。

```cpp
#include<stdio.h>
#include<stdint.h>
#include<cpuid.h>

static void cpuid(uint32_t func,uint32_t sub,uint32_t data[4]){
    __cpuid_count(func,sub,data[0],data[1],data[2],data[3]);
}

int main(void){
    uint32_t data[4];
    char str[48];
    for(int i=0;i<3;i++){
        cpuid(0x80000002+i,0,data);
        for(int j=0;j<4;j++)
            reinterpret_cast<uint32_t*>(str)[i*4+j]=data[j];
    }
    printf("%s\n",str);
    return 0;
}
```

在洛谷$\text{IDE}$下输出：

```
Intel(R) Xeon(R) Gold 6149 CPU @ 3.10GHz

```

#### 算法的优化

假如你对算法的时间复杂度实在不放心，你可以进行常数优化。

1. `fread();`**读入优化**，大约可节省$100\text{ms}$的时间；
2. 变量定义类型改为`register int`；
3. 避免使用`long long`类型，尽量使用`int`。

### 代码

代码如下：

```cpp
#include <cstdio>
#define MOD 1000000007//宏定义MOD更快
#define getchar() (p1 == p2 && (p2 = (p1 = buf) + fread(buf, 1, 100000, stdin), p1 == p2) ? EOF : *p1++)
static char buf[100000], *p1 = buf, *p2 = buf;//fread();版读入优化

inline int read(void)//读入优化函数
{
    register char ch = getchar();
    register int sum = 0;
    while (!(ch >= '0' && ch <= '9'))
        ch = getchar();
    while (ch >= '0' && ch <= '9')
        sum = (sum << 1) + (sum << 3) + ch - 48, ch = getchar();
    return sum;
}

int n, m, a[1001][1001], f[1001][1001];//变量尽量避免使用long long

int main(void)
{
    register int i, j, k, l;//尽量使用寄存器变量
    f[1][1] = 1;//动态规划初始化
    n = read(), m = read(), read();//k没有用，不要读入
    for (i = 1; i <= n; ++i)
        for (j = 1; j <= m; ++j)
        {
            a[i][j] = read();
            for (k = 1; k < i; ++k)
                for (l = 1; l < j; ++l)
                    if (a[k][l] != a[i][j])
                        f[i][j] = (f[i][j] + f[k][l]) % MOD;//状态转移方程
        }
    printf("%d\n", f[n][m]);//输出并换行
    return 0;//结束
}
```

### 我的评测记录

- [洛谷 R16320841](https://www.luogu.org/recordnew/show/16320841)。
