---
title: 【题解】【洛谷 P1340】 兽径管理
date: 2019-02-06 16:24:05
categories: Solution
tags:
- 题解
- 洛谷
- Kruskal
- 并查集
---

## 原题

题面请查看[洛谷 P1340 兽径管理](https://www.luogu.org/problemnew/show/P1340)。

## 题解

$\text{Kruskal}$算法

<!-- more -->

### 思路

1. 先读入所有边，每条边以时间为编号`ID`；
2. 对边以**边权**为关键字进行排序；
3. 以$1$~$w$为参数进行$\text{Kruskal}$算法：
    - 如果这条边的编号大于所给参数，这条边不参与算法；
    - 否则寻找最小生成树。
4. 输出答案。

### 代码

代码如下：

```cpp
#include <algorithm>
#include <cstdio>
//头文件
using std::sort;//快速排序

struct Edge//定义 边 的结构体
{
    int ID, f, t, val;
    bool operator<(const Edge &a) const
    {
        return val < a.val;
    }
};

struct Union_Find//定义 并查集 的结构体
{
    int ID[201];
    Union_Find(int);//析构函数，用于并查集的初始化，参数为n
    void connect(int, int);//并
    bool search(int, int);//查
    int find(int);//查
};

int n, w;
Edge E[6001];

int Kruskal(int);

int main(void)
{
    register int i;
    scanf("%d%d", &n, &w);
    for (i = 1; i <= w; ++i)
    {
        E[i].ID = i;//每条边以时间为编号
        scanf("%d%d%d", &E[i].f, &E[i].t, &E[i].val);//读入
    }
    sort(E + 1, E + w + 1);//快速排序
    for (i = 1; i <= w; ++i)
        printf("%d\n", Kruskal(i));//调用函数并输出结果
    return 0;//在主函数末尾加上return 0;是一个好习惯
}

Union_Find::Union_Find(int n)//析构函数，用于并查集的初始化，参数为n
{
    register int i;
    for (i = 1; i <= n; ++i)
        ID[i] = i;
    return;
}

void Union_Find::connect(int a, int b)
{
    register int ra = find(a), rb = find(b);
    if (ra != rb)
        ID[rb] = ra;
    return;
}

bool Union_Find::search(int a, int b)
{
    return find(a) == find(b);
}

int Union_Find::find(int x)
{
    if (x == ID[x])
        return x;
    else
        return ID[x] = find(ID[x]);//路径压缩
}

int Kruskal(int time)
{
    register int i, cnt = 0, sum = 0;
    //cnt为连接边的数量
    Union_Find UF(n);//先定义一个并查集UF，析构函数的参数为n
    for (i = 1; i <= w && cnt < n - 1; ++i)
        if (E[i].ID > time)//如果这条边的编号大于所给参数，这条边不参与算法
            continue;
        else if (!UF.search(E[i].f, E[i].t))//如果这条边连接的两个点不在同一个集合内
        {
            ++cnt;
            sum += E[i].val;
            UF.connect(E[i].f, E[i].t);
        }//统计答案
    if (cnt != n - 1)//如果无法构成树
        return -1;//题目要求输出-1
    else
        return sum;//返回答案
}
```

### 我的评测记录

- [洛谷 R16089070](https://www.luogu.org/recordnew/show/16089070)。
