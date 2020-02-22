---
title: 题解 P5462 【X龙珠】
author: 李梓恒
top: false
cover: true
toc: true
mathjax: true
tags: 
  - 洛谷题解
abbrlink: 40894
date: 2020-02-03 11:39:36
img: /medias/banner/2.jpg
coverImg: /medias/banner/2.jpg
password:
summary: 蒟蒻的超烂题解
categories: 
  - 题解
---
# 分析题意：

龙珠这个东西是个好东西，听同学说挺好看的。。。

这题机房的大佬一拍大腿，顺口说出了树形结构这个高大上的东西，蒟蒻表示不会啊~~（其实是懒得打。。。）~~，在仔细看看题目，这题不就是链表吗，但是指针好像不会啊。。。

那就用数组模拟一下吧。。。

# 思路：

用链表存下每一个点的前一个和后一个，然后从大往小找，仅当他后面有数时，将没用过的点连同他后面的一个一起输出，输出后把他前面的数和他后面的后面的数连上然后就没了

# 代码：
```cpp
#include<bits/stdc++.h>
using namespace std；
const int maxn=1e6+10；
int sum[maxn],head[maxn],next[maxn]；
int main()
{
    int n,m；
    cin>>n；
    for(int i=1;i<=n;i++)
    {
        cin>>sum[i]；
        next[sum[i-1]]=sum[i]；
        head[sum[i]]=sum[i-1]；
    }
    for(int i=1;i<=n;i++)
    {
        if(next[i])
        {
            cout<<i<<" "<<next[i]<<" "；
            next[head[i]]=next[next[i]]；
            head[next[head[i]]]=head[i]；
            next[next[i]]=0;    
        }
    }
    cout<<endl；
    return 0；
}
```
### PS:千万别抄，我~~已经把分号全改成中文了QAQ~~