---
title: 【题解】【洛谷 P2574】 XOR的艺术
date: 2019-02-05 20:39:58
categories: Solution
tags:
- 题解
- 洛谷
- 数据结构
- 线段树
---

## 原题

题面请查看[洛谷 P2574 XOR的艺术](https://www.luogu.org/problemnew/show/P2574)。

## 题解

线段树

<!-- more -->

### 思路

把线段树的`LazyTag[]`的更新方式修改一下即可，其他可照抄线段树模板。

#### 更新`LazyTag[]`的方式

1. 左右子树的`LazyTag[]`都要对一按位异或；

    代码表示为：
    ```cpp
    tag[ID << 1] ^= 1;
    tag[ID << 1 | 1] ^= 1;
    ```

2. 左右子树的值全部变成区间长度减去当前值；

    代码表示为：
    ```cpp
    register int len = r - l + 1;//len为当前节点区间长度
    unit[ID << 1] = (len - (len >> 1)) - unit[ID << 1];//左子树根节点区间长度为(len - (len >> 1))
    unit[ID << 1 | 1] = (len >> 1) - unit[ID << 1 | 1];//右子树根节点区间长度为(len >> 1)
    ```

### 代码

代码如下：

```cpp
#include <cstdio>//头文件

struct Segment_Tree//线段树模板
{
    int unit[(200000 << 2) + 1], tag[(200000 << 2) + 1];//线段树空间要开到4倍
    void Build(int, int, int, bool[]);//建树函数
    void Update(int, int, int, int, int);//更新函数
    int Query(int, int, int, int, int);//查询函数
    void Pushdown(int, int, int);//更新LazyTag[]的函数
};

bool a[200001];
int n, m;
Segment_Tree Tree;//线段树

int main(void)
{
    register int i;
    scanf("%d%d", &n, &m);
    for (i = 1; i <= n; ++i)
    {
        static int temp;
        scanf("%1d", &temp);
        a[i] = temp;
    }
    Tree.Build(1, 1, n, a);//建树
    while (m--)
    {
        static int opt, l, r;
        scanf("%d%d%d", &opt, &l, &r);
        if (opt == 0)//更新
            Tree.Update(1, 1, n, l, r);
        if (opt == 1)//查询
            printf("%d\n", Tree.Query(1, 1, n, l, r));//输出查询结果并换行
    }
    return 0;//结束时加上return 0;是一个好习惯
}

void Segment_Tree::Build(int ID, int l, int r, bool a[])
{
    if (l == r)
        unit[ID] = a[l];//递归停止
    else
    {
        register int mid = (l + r) >> 1;
        Build(ID << 1, l, mid, a);//构建左子树
        Build(ID << 1 | 1, mid + 1, r, a);//构建左子树
        unit[ID] = unit[ID << 1] + unit[ID << 1 | 1];
    }
    return;
}

void Segment_Tree::Update(int ID, int l, int r, int x, int y)
{
    if (x <= l && r <= y)
    {
        unit[ID] = (r - l + 1) - unit[ID];
        tag[ID] ^= 1;
    }
    else
    {
        Pushdown(ID, l, r);
        int mid = (l + r) >> 1;
        if (x <= mid)
            Update(ID << 1, l, mid, x, y);//更新左子树
        if (y > mid)
            Update(ID << 1 | 1, mid + 1, r, x, y);//更新右子树
        unit[ID] = unit[ID << 1] + unit[ID << 1 | 1];
    }
    return;
}

int Segment_Tree::Query(int ID, int l, int r, int x, int y)
{
    if (x <= l && r <= y)
        return unit[ID];
    Pushdown(ID, l, r);//更新LazyTag[]
    int mid = (l + r) >> 1, sum = 0;
    if (x <= mid)
        sum += Query(ID << 1, l, mid, x, y);//查询左子树
    if (y > mid)
        sum += Query(ID << 1 | 1, mid + 1, r, x, y);//查询右子树
    return sum;//返回查询结果
}

void Segment_Tree::Pushdown(int ID, int l, int r)
{
    register int len = r - l + 1;
    if (tag[ID])
    {
        tag[ID << 1] ^= 1;
        tag[ID << 1 | 1] ^= 1;
        //左右子树的LazyTag[]都要对一按位异或

        unit[ID << 1] = (len - (len >> 1)) - unit[ID << 1];
        unit[ID << 1 | 1] = (len >> 1) - unit[ID << 1 | 1];
        //左右子树的值全部变成区间长度减去当前值

        tag[ID] = 0;//记得清空当前节点的标记
    }
    return;
}
```

### 我的评测记录

- [洛谷 R16079272](https://www.luogu.org/recordnew/show/16079272)。

### 其他

线段树模板的代码算中等长度，下面我们来压行。

源代码共$102$行，压行后$7$行。

压行的评测记录：[洛谷 R16080174](https://www.luogu.org/recordnew/show/16080174)。

```cpp
#include <cstdio>
int n, m, opt, l, r,unit[(200000 << 2) + 1], tag[(200000 << 2) + 1];
void Build(int ID, int l, int r){(l == r)?(scanf("%1d", &unit[ID])):(Build(ID << 1, l, ((l + r) >> 1)),Build(ID << 1 | 1, ((l + r) >> 1) + 1, r),unit[ID] = unit[ID << 1] + unit[ID << 1 | 1]);}
void Pushdown(int ID, int l, int r){tag[ID]?(tag[ID << 1] ^= 1,tag[ID << 1 | 1] ^= 1,unit[ID << 1] = ((r - l + 1) - ((r - l + 1) >> 1)) - unit[ID << 1],unit[ID << 1 | 1] = ((r - l + 1) >> 1) - unit[ID << 1 | 1],tag[ID] = 0):0;}
void Update(int ID, int l, int r, int x, int y){(x <= l && r <= y)?(unit[ID] = (r - l + 1) - unit[ID],tag[ID] ^= 1,0):(Pushdown(ID, l, r),((x <= ((l + r) >> 1))?(Update(ID << 1, l, ((l + r) >> 1), x, y),0):0),((y > ((l + r) >> 1))?(Update(ID << 1 | 1, ((l + r) >> 1) + 1, r, x, y),0):0),unit[ID] = unit[ID << 1] + unit[ID << 1 | 1],0);}
int Query(int ID, int l, int r, int x, int y){return ((x <= l && r <= y)?(unit[ID]):(Pushdown(ID, l, r),((x <= ((l + r) >> 1))?(Query(ID << 1, l, ((l + r) >> 1), x, y)):0)+((y > ((l + r) >> 1))?(Query(ID << 1 | 1, ((l + r) >> 1) + 1, r, x, y)):0)));}
int main(void){scanf("%d%d", &n, &m),Build(1, 1, n);while (m--)(scanf("%d%d%d", &opt, &l, &r),opt==0)?(Update(1, 1, n, l, r),0):(printf("%d\n",Query(1, 1, n, l, r)));}
```

也许这就是**压行的艺术**。
