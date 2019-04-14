---
title: '【题解】【洛谷 P3879】 [TJOI2010]阅读理解'
date: 2019-03-16 19:42:19
categories: Solution
tags:
- 题解
- 洛谷
- 字符串
- STL
---

## 原题

题面请查看[洛谷 P3879 \[TJOI2010\]阅读理解](https://www.luogu.org/problemnew/show/P3879)。

### 题解

$\text{STL}$

<!-- more -->

### 思路

用$\text{STL}$模拟即可。

### 代码

代码如下：

```cpp
#include <cstdio>
#include <cstring>
#include <iostream>
#include <map>
#include <string>
#include <vector>
using std::cin;
using std::map;
using std::string;
using std::vector;

bool T[1001];
int n, m, l;
string temp;
map<string, vector<int> /* */> M;

int main(void)
{
    register int i;
    scanf("%d", &n);
    for (i = 1; i <= n; ++i)
    {
        scanf("%d", &l);
        while (l--)
        {
            cin >> temp;
            M[temp].push_back((int)i);
        }
    }
    scanf("%d", &m);
    while (m--)
    {
        memset(T, false, sizeof(T));
        cin >> temp;
        for (i = 0; i < (int)M[temp].size(); ++i)
        {
            if (!T[M[temp][i]])
            {
                T[M[temp][i]] = true;
                printf("%d ", M[temp][i]);
            }
        }
        putchar('\n');
    }
    return 0;
}
```

### 我的评测记录

- [洛谷 R17052569](https://www.luogu.org/recordnew/show/17052569)。
