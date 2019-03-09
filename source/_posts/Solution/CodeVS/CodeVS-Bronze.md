---
title: 【题解】【CodeVS 天梯】 青铜 Bronze
date: 2019-03-03 10:31:08
categories: Solution
tags:
- 题解
- CodeVS
---

## 原题

题目请查看[CodeVS 天梯 青铜 Bronze](http://codevs.cn/ladder/?id=1)。

<!-- more -->

## 题解

### [1201 最小数和最大数](http://codevs.cn/problem/1201/)

```cpp
#include <cstdio>
#define INF 0X7FFFFFFF
#define min(a, b) ((a) < (b) ? (a) : (b))
#define max(a, b) ((a) > (b) ? (a) : (b))

int n, temp;

int main(void)
{
    register int Min = INF, Max = -INF;
    scanf("%d", &n);
    while (n--)
    {
        scanf("%d", &temp);
        Min = min(Min, temp);
        Max = max(Max, temp);
    }
    printf("%d %d\n", Min, Max);
    return 0;
}
```

### [1202 求和](http://codevs.cn/problem/1202/)

```cpp
#include <cstdio>

int n, temp;

int main(void)
{
    register int sum = 0;
    scanf("%d", &n);
    while (n--)
    {
        scanf("%d", &temp);
        sum += temp;
    }
    printf("%d\n", sum);
    return 0;
}
```

### [1203 判断浮点数是否相等](http://codevs.cn/problem/1203/)

```cpp
#include <cmath>
#include <cstdio>
#define eps 1e-8

double a, b;

int main(void)
{
    scanf("%lf%lf", &a, &b);
    if (fabs(a - b) < eps)
        puts("yes");
    else
        puts("no");
    return 0;
}
```

### [1206 保留两位小数](http://codevs.cn/problem/1206/)

```cpp
#include <cstdio>

double a;

int main(void)
{
    scanf("%lf", &a);
    printf("%.2f\n", a);
    return 0;
}
```

### [2235 机票打折](http://codevs.cn/problem/2235/)

```cpp
#include <cstdio>

int a;
double b;

int main(void)
{
    scanf("%d%lf", &a, &b);
    a *= b / 10;
    if (a % 10 > 4)
        printf("%d\n", a / 10 * 10 + 10);
    else
        printf("%d\n", a / 10 * 10);
    return 0;
}
```

### [1204 寻找子串位置](http://codevs.cn/problem/1204/)

```cpp
#include <cstdio>
#include <iostream>
using std::cin;
#include <string>
using std::string;

string a, b;

int main(void)
{
    cin >> a >> b;
    printf("%llu\n", a.find(b) + 1);
    return 0;
}
```

### [1205 单词翻转](http://codevs.cn/problem/1205/)

```cpp
#include <cstdio>
#include <iostream>
using std::cin;
using std::cout;
#include <string>
using std::string;
#include <stack>
using std::stack;

string temp;
stack<string> S;

int main(void)
{
    while (cin >> temp)
        S.push(temp);
    cout << S.top();
    S.pop();
    while (!S.empty())
    {
        cout << ' ' << S.top();
        S.pop();
    }
    putchar('\n');
    return 0;
}
```
