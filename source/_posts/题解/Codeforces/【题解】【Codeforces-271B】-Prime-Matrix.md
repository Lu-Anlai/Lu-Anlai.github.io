---
title: 【题解】【Codeforces 271B】 Prime Matrix
date: 2019-02-03 21:47:01
categories: 题解
tags:
- 题解
- Codeforces
- 埃氏筛
---

## 原题

题面请查看[Codeforces 271B Prime Matrix](http://codeforces.com/problemset/problem/271/B)。

也可在洛谷上查看：[传送门](https://www.luogu.org/problemnew/show/CF271B)。

## 题解

埃氏筛

<!-- more -->

### 思路

1. 用埃氏筛求出$1$~$10^{5}+3$以内的所有素数；

2. 求出矩阵内每个元素变为素数的操作次数；

3. 为最后统计方便，记`a[i][0]`为第$i$行的操作总数，`a[0][j]`为第$j$列的操作总数；

4. 统计答案。

#### 细节

$10^5$经过操作后的素数是$100003$，所以埃氏筛要筛到$100003$。

### 代码

```cpp
#include <cstdio>
#define INF 0X3F3F3F3F3F3F3F3F
#define min(a, b) ((a) < (b) ? (a) : (b))
//头文件，正无穷，函数min()

bool isNotPrime[100004];//埃氏筛的标记数组
int n, m, a[501][501];

int main(void)
{
    register int i, j;
    register long long now, temp, ans = INF;
    scanf("%d%d", &n, &m);//读入n,m

    /*----埃氏筛----*/
    isNotPrime[1] = true;
    for (i = 2; i <= 100003; ++i) {
        if (!isNotPrime[i])
            for (j = (i << 1); j <= 100003; j += i)
                isNotPrime[j] = true;
    }

    for (i = 1; i <= n; ++i)
        for (j = 1; j <= m; ++j) {
            scanf("%d", &a[i][j]);//先读入
            now = temp = a[i][j];
            while (isNotPrime[now])
                ++now;
            //寻找最近的素数now
            a[i][j] = now - temp;//求操作次数
            a[i][0] += a[i][j];
            a[0][j] += a[i][j];
            //为方便统计，记a[i][0]为第i行的操作总数，a[0][j]为第j列的操作总数
        }
    for (i = 1; i <= n; ++i)
        ans = min(ans, a[i][0]);
    for (j = 1; j <= m; ++j)
        ans = min(ans, a[0][j]);//统计
    printf("%lld\n", ans);//输出并换行
    return 0;
}
```

### 我的评测记录

- [Codeforces](http://codeforces.com/contest/271/submission/49398471)；

- [洛谷](https://www.luogu.org/recordnew/show/16053322)。
