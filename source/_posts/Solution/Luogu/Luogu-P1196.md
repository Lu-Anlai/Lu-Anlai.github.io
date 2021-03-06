---
title: '【题解】【洛谷 P1196】 [NOI2002]银河英雄传说'
date: 2019-02-03 17:54:47
categories: Solution
tags:
- 题解
- 洛谷
- NOIp提高组
- 图论
- 并查集
---

## 原题

题面请查看[洛谷 P1196 \[NOI2002\]银河英雄传说](https://www.luogu.org/problemnew/show/P1196)。

## 题解

并查集

<!-- more -->

### 思路

- 观察合并指令：$M_{i,j}$，说到合并，就能想到一个优秀的**【数据结构】并查集**。

~~这就好比说到六六大顺，就能想到六小龄童，说到六小龄童，就想到他在西游记中的角色孙悟空。今年年初，中美合拍的西游记即将正式开机，六小龄童继续扮演美猴王孙悟空，六小龄童会用美猴王艺术形象努力创造一个正能量的形象，文体两开花，弘扬中华文化，希望大家多多关注。~~

- 观察询问指令：$C_{i,j}$，运用**前缀和**的思想，我们设$\text{front[x]}$为$x$前面有多少架战舰，那么查询的答案就是$| front[i]-front[j] | - 1$。

记$\text{num[i]}$为第$i$列飞船的数量，那么我们只需要对并查集的$\text{int find(int);}$函数进行魔改即可维护$\text{front[]}$数组。

### 代码

代码如下：

```cpp
#include <cstdio>
#include <iostream>
using std::cin;
#define abs(a) ((a) > 0 ? (a) : (-(a)))

int T, ID[30001], front[30001], num[30001];

int find(int);

int main(void)
{
    register int i;
    scanf("%d", &T);
    for (i = 1; i <= 30000; ++i)
    {
        ID[i] = i;
        num[i] = 1;
    }
    while (T--)
    {
        static char ch;
        static int x, y, fx, fy;
        cin >> ch;
        scanf("%d%d", &x, &y);
        fx = find(x), fy = find(y);
        if (ch == 'M')
        {
            front[fx] += num[fy];
            ID[fx] = fy;
            num[fy] += num[fx];
            num[fx] = 0;
        }
        else if (fx != fy)
            puts("-1");
        else
            printf("%d\n", abs(front[x] - front[y]) - 1);
    }
    return 0;
}

int find(int x)
{
    if (ID[x] == x)
        return ID[x];
    else
    {
        register int root = find(ID[x]);
        front[x] += front[ID[x]];
        return ID[x] = root;
    }
}
```