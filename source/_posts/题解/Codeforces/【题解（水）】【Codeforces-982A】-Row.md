---
title: 【题解（水）】【Codeforces 982A】 Row
date: 2019-02-24 10:50:39
categories: 题解（水）
tags:
- 题解（水）
- Codeforces
- 模拟
- 字符串
---

## 原题

题面请查看[Codeforces 982A Row](http://codeforces.com/problemset/problem/982/A)。

也可在洛谷上查看：[传送门](https://www.luogu.org/problemnew/show/CF982A)。

## 题解

模拟+字符串

<!-- more -->

### 思路

此题太水，略去不写。

### 代码

代码如下：

```cpp
#include <cstdio>
#include <cstring>

char str[1002];
int n;

int main(void)
{
    register int i;
    scanf("%d%s", &n, str + 1);
    str[0] = str[n + 1] = '0';
    for (i = 1; i <= n; ++i)
        if (str[i] == '0' && !(str[i - 1] == '1' || str[i + 1] == '1'))
            return puts("No"), 0;
        else if (str[i] == '1' && (str[i - 1] == '1' || str[i + 1] == '1'))
            return puts("No"), 0;
        else
            continue;
    puts("Yes");
    return 0;
}
```

### 我的评测记录

- [Codeforces](http://codeforces.com/contest/982/submission/50411256)；

- [洛谷](https://www.luogu.org/recordnew/show/16617507)。
