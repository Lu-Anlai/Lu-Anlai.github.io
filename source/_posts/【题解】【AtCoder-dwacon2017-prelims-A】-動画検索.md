---
title: 【题解】【AtCoder dwacon2017-prelims-A】 動画検索
date: 2019-02-04 12:06:17
categories: 题解
tags:
- 题解
- AtCoder
- 模拟
---

## 原题

题面请查看[AtCoder dwacon2017-prelims-A 動画検索](https://dwacon2017-prelims.contest.atcoder.jp/tasks/dwango2017qual_a)。

也可在洛谷上查看：[传送门](https://www.luogu.org/problemnew/show/AT2238)。

## 题解

模拟

<!-- more -->

### 思路

模拟即可，注意答案的合法性。

### 代码

代码如下：

```cpp
#include <cstdio>

int n, a, b;

int main(void){
    scanf("%d%d%d", &n, &a, &b);
    if(a+b>n)
        printf("%d\n", a + b - n);
    else
        puts("0");
    return 0;
}
```

### 我的评测记录

- [AtCoder](https://dwacon2017-prelims.contest.atcoder.jp/submissions/4170787)；

- [洛谷 R16059768](https://www.luogu.org/recordnew/show/16059768)。
