---
title: 【题解】【洛谷 P1073】 最优贸易
date: 2019-02-13 22:02:56
categories: Solution
tags:
- 题解
- 洛谷
- 图论
- SPFA
---

## 原题

题面请查看[洛谷 P1073 最优贸易](https://www.luogu.org/problemnew/show/P1073)。

## 题解

$\text{SPFA}$

<!-- more -->

### 思路

进行两次$\text{SPFA}$即可。

#### 算法的优化

1. `fread();`**读入优化**，大约可节省$60\text{ms}$的时间；
2. 存图使用**链式前向星**；
3. 手写**循环队列**；

经过优化后，算法的时间复杂度为$\text{O}(n+m+2Km+n)=\text{O}(2n+(2K+1)m)$，可以通过。

### 代码

代码如下：

```cpp
#include <cstdio>
#include <cstring>
#define min(a, b) ((a) < (b) ? (a) : (b))
#define max(a, b) ((a) > (b) ? (a) : (b))
//宏定义

#define getchar() (p1 == p2 && (p2 = (p1 = buf) + fread(buf, 1, 100000, stdin), p1 == p2) ? EOF : *p1++)
static char buf[100000], *p1 = buf, *p2 = buf;

inline int read(void)//读入优化
{
    register char ch = getchar();
    register int sum = 0;
    while (!(ch >= '0' && ch <= '9'))
        ch = getchar();
    while (ch >= '0' && ch <= '9')
        sum = (sum << 1) + (sum << 3) + ch - 48, ch = getchar();
    return sum;
}

struct Graph{
    int cnt, head[100001], to[1000001], w[1000001], Next[1000001];
    void Add_Edge(int, int, int);
};//链式前向星存图

bool vis[100001][2];
int a[100001];
int Min[100001], Max[100001];
int Q[100001], head, tail;
Graph L1, L2;

void SPFA1(int);
void SPFA2(int);

int main(void)
{
    register int n, m, i, ans = 0, x, y, z;
    n = read(), m = read();
    for (i = 1; i <= n; ++i)
        a[i] = read();
    for (i = 1; i <= m; ++i)
    {
        x = read(), y = read(), z = read();
        L1.Add_Edge(x, y, a[y]), L2.Add_Edge(y, x, a[x]);
        if (z == 2)//双向边
            L1.Add_Edge(y, x, a[x]), L2.Add_Edge(x, y, a[y]);
    }
    SPFA1(1), SPFA2(n);//两次SPFA
    for (i = 1; i <= n; ++i)
        ans = max(ans, Max[i] - Min[i]);//max()求答案
    printf("%d\n", ans);//输出并换行
    return 0;//结束程序
}

void Graph::Add_Edge(int f, int t, int val)
{
    Next[++cnt] = head[f];
    to[cnt] = t;
    w[cnt] = val;
    head[f] = cnt;
    return;
}

void SPFA1(int s)
{
    register int i, ID, To;
    head = tail = 0;
    memset(Q, 0, sizeof(Q));
    memset(Min, 0X3F, sizeof(Min));
    vis[s][1] = true;
    Q[tail++] = s;
    while (head!=tail)
    {
        ID = Q[head++];
        if (head >= 100001)
            head %= 100001;
        vis[ID][1] = false;
        for (i = L1.head[ID]; i; i = L1.Next[i])
        {
            To = L1.to[i];
            if (Min[To] > min(Min[ID], L1.w[i]))
            {
                Min[To] = min(Min[ID], L1.w[i]);
                if (!vis[To][1])
                {
                    vis[To][1] = true;
                    Q[tail++] = To;
                    if (tail >= 100001)
                        tail %= 100001;
                }
            }
        }
    }
    return;
}

void SPFA2(int s)
{
    register int i, ID, To;
    head = tail = 0;
    memset(Q, 0, sizeof(Q));
    vis[s][0] = true;
    Q[tail++] = s;
    while (head!=tail)
    {
        ID = Q[head++];
        if (head >= 100001)
            head %= 100001;
        vis[ID][0] = false;
        for (i = L2.head[ID]; i; i = L2.Next[i])
        {
            To = L2.to[i];
            if (Max[To] < max(Max[ID], L2.w[i]))
            {
                Max[To] = max(Max[ID], L2.w[i]);
                if (!vis[To][0])
                {
                    vis[To][0] = true;
                    Q[tail++] = To;
                    if (tail >= 100001)
                        tail %= 100001;
                }
            }
        }
    }
    return;
}
```

### 我的评测记录

- [洛谷 R16277015](https://www.luogu.org/recordnew/show/16277015)。
