---
title: 【题解】【Codeforces 574A】 Bear and Elections
date: 2019-02-09 21:41:32
categories: Solution
tags:
- 题解
- Codeforces
- 模拟
- 排序
---

## 原题

题面请查看[Codeforces 574A Bear and Elections](http://codeforces.com/problemset/problem/574/A)。

也可在洛谷上查看：[传送门](https://www.luogu.org/problemnew/show/CF574A)。

洛谷题面翻译来自[@卢安来](https://www.luogu.org/space/show?uid=38502)，~~其实就是我~~。

## 题解

模拟+排序

<!-- more -->

### 思路

根据正常人的想法和思维，选票最多的人是`Limak`最大的敌人，我们应该多贿赂他的支持者。

因为每次贿赂后，选票最多的人都会改变，所以我们每次操作（实行贿赂）后进行排序即可。

#### 具体实现

设`vote`为`Limak`当前选票，那么每次的操作就可以写成这样：

```cpp
while (a[n - 1] >= vote) //如果Limak无法获胜
{                        //开始贿赂
    --a[n - 1];          //贿赂选票最多的人的一名支持者
    sort(a + 1, a + n);  //重新排序
    ++vote;              //Limak的选票增加
    ++ans;               //计数器自增
}
```


### 代码

代码如下：

```cpp
#include <algorithm>
#include <cstdio>
using std::sort; //排序

int n, vote, a[101]; //变量如上文所述

int main(void)
{
    register int i, ans = 0;
    scanf("%d%d", &n, &vote); //读入
    for (i = 1; i < n; ++i)   //除去Limak还有n-1个人
        scanf("%d", &a[i]);
    sort(a + 1, a + n);      //要先排序
    while (a[n - 1] >= vote) //如果Limak无法获胜
    {                        //开始贿赂
        --a[n - 1];          //贿赂选票最多的人的一名支持者
        sort(a + 1, a + n);  //重新排序
        ++vote;              //Limak的选票增加
        ++ans;               //计数器自增
    }
    printf("%d\n", ans); //输出并换行
    return 0;
}
```

### 我的评测记录

- [Codeforces](http://codeforces.com/contest/574/submission/49663968)；

- [洛谷](https://www.luogu.org/recordnew/show/16146974)。

