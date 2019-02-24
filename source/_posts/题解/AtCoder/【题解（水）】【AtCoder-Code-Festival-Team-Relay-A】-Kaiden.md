---
title: 【题解（水）】【AtCoder Code Festival Team Relay A】 Kaiden
date: 2019-02-09 15:52:06
categories: 题解（水）
tags:
- 题解（水）
- AtCoder
- 模拟
---

## 原题

题面请查看[AtCoder ABC004-C 入れ替え](https://cf17-relay-open.contest.atcoder.jp/tasks/relay2_a)。

也可在洛谷上查看：[传送门](https://www.luogu.org/problemnew/show/AT3626)。

## 题解

模拟

<!-- more -->

### 思路

此题太水，略去不写。

### 代码

代码如下：

```cpp
#include <cstdio>

long long a, b, k;

int main(void)
{
    scanf("%lld%lld%lld", &k, &a, &b);
    if (k <= a)
        puts("1");
    else if (a <= b)
        puts("-1");
    else
        printf("%lld\n", ((k - a) / (a - b) + bool((k - a) % (a - b))) << 1 | 1);
    return 0;
}
```

### 我的评测记录

- [AtCoder](https://cf17-relay-open.contest.atcoder.jp/submissions/4201707)；

- [洛谷 R16137986](https://www.luogu.org/recordnew/show/16137986)。
