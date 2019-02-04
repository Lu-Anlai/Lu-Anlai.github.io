---
title: 【题解】【AtCoder ABC004-C】 入れ替え
date: 2019-02-04 11:59:26
categories: 题解
tags:
- 题解
- AtCoder
- 模拟
---

## 原题

题面请查看[AtCoder ABC004-C 入れ替え](https://abc004.contest.atcoder.jp/tasks/abc004_3)。

也可在洛谷上查看：[传送门](https://www.luogu.org/problemnew/show/AT817)。

## 题解

模拟

<!-- more -->

### 思路

答案$30$一循环，模拟即可。

### 代码

代码如下：

```cpp
#include <cstdio>

char str[7] = "123456";
int a;

void swap(char&, char&);

int main(void)
{
    register int i, now = 0;
    scanf("%d", &a);
    a %= 30;
    for (i = 0; i < a; ++i) {
        swap(str[now], str[now + 1]);
        if (++now == 5)
            now = 0;
    }
    puts(str);
    return 0;
}

void swap(char& a, char& b)
{
    a ^= b, b = a ^ b, a ^= b;
    return;
}
```

### 我的评测记录

- [AtCoder](https://abc004.contest.atcoder.jp/submissions/4170767)；

- [洛谷 R16059682](https://www.luogu.org/recordnew/show/16059682)。
