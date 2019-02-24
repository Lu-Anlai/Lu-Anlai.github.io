---
title: 【题解（水）】【Codeforces 579A】 Raising Bacteria
date: 2019-02-12 19:17:10
categories: 题解（水）
tags:
- 题解（水）
- Codeforces
- 模拟
- 二进制
---

## 原题

题面请查看[Codeforces 579A Raising Bacteria](http://codeforces.com/problemset/problem/579/A)。

也可在洛谷上查看：[传送门](https://www.luogu.org/problemnew/show/CF579A)。

## 题解

模拟+二进制

<!-- more -->

### 思路

此题太水，略去不写。

### 代码

代码如下：

```cpp
#include <cstdio>

int x;

int main(void)
{
    register int cnt = 0;
    scanf("%d", &x);
    while (x)
    {
        if (x & 1)
            ++cnt;
        x >>= 1;
    }
    printf("%d\n", cnt);
    return 0;
}
```

### 我的评测记录

- [Codeforces](http://codeforces.com/contest/579/submission/49825335)；

- [洛谷](https://www.luogu.org/recordnew/show/16227402)。

