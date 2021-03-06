---
title: '【题解】【洛谷 P1198】 [JSOI2008]最大数'
date: 2019-02-07 09:21:56
categories: Solution
tags:
- 题解
- 洛谷
- JSOI2008
- 线段树
---

## 原题

题面请查看[洛谷 P1198 [JSOI2008]最大数](https://www.luogu.org/problemnew/show/P1198)。

## 题解

线段树

<!-- more -->

### 思路

为节省写代码的时间，我们采用阉割版线段树（只具有单点修改和区间查询两个功能）。

#### 具体实现过程

1. 定义空树`Tree`，记`len`为当前数列的长度；

2. 模拟操作：

    - 查询操作：

        记`T=Tree.Query(1,1,m,len-L+1,len)`，输出`T`并换行即可；

    - 插入操作：
    
        单点修改：`Tree.Update(1,1,m,++len,(num+T)%D)`；

3. 结束。

### 代码

代码如下：

```cpp
#include <cstdio>
#define INF 0X3F3F3F3F3F3F3F3F//定义正无穷
#define max(a, b) ((a) > (b) ? (a) : (b))//定义max()函数
typedef long long ll

struct Segment_Tree //线段树模板
{
    ll unit[(200000 << 2) + 1];          //线段树空间要开到4倍
    void Update(int, int, int, int, ll); //更新函数
    ll Query(int, int, int, int, int);   //查询函数
};

char ch[2];//操作符
int m, len;//len表示数列长度
ll D, T, num;
Segment_Tree Tree; //线段树

int main(void)
{
    register int i;
    scanf("%d%lld", &m, &D);//读入
    for (i = 1; i <= m; ++i)//模拟
    {
        scanf("%s%lld", ch, &num);
        if (ch[0] == 'Q')
        {
            if (!num)
                T = 0;
            else
                T = Tree.Query(1, 1, m, len - num + 1, len) % D;//查询
            printf("%lld\n", T);//输出并换行
        }
        if (ch[0] == 'A')
        {
            ++len;//数列边长
            Tree.Update(1, 1, m, len, (num + T) % D);//更新
        }
    }
    return 0;
}

void Segment_Tree::Update(int ID, int l, int r, int index, ll val)
{
    if (l == r)
        unit[ID] = val;
    else
    {
        register int mid = (l + r) >> 1;
        if (index <= mid)
            Update(ID << 1, l, mid, index, val); //更新左子树
        if (index > mid)
            Update(ID << 1 | 1, mid + 1, r, index, val); //更新右子树
        unit[ID] = max(unit[ID << 1], unit[ID << 1 | 1]) % D;
    }
    return;
}

ll Segment_Tree::Query(int ID, int l, int r, int x, int y)
{
    if (x <= l && r <= y)
        return unit[ID];
    register int mid = (l + r) >> 1;
    register ll a = -INF, b = -INF;
    if (x <= mid)
        a = Query(ID << 1, l, mid, x, y); //查询左子树
    if (y > mid)
        b = Query(ID << 1 | 1, mid + 1, r, x, y); //查询右子树
    return max(a, b);                             //返回查询结果
}

```

### 我的评测记录

- [洛谷 R16096515](https://www.luogu.org/recordnew/show/16096515)。
