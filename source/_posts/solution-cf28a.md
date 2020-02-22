
---
title: 题解 CF28A 【Bender Problem】
author: 李梓恒
top: false
cover: true
toc: true
mathjax: true
tags:
  - 洛谷题解
categories:
  - 题解
abbrlink: 53050
date: 2020-02-06 16:39:00
img: /medias/banner/4.jpg
coverImg: /medias/banner/4.jpg
password:
summary: 蒟蒻的超烂题解
---
## 分析题意：
给定一个$n$个点的多边形，相邻两个点之间要么$x$坐标相同，要么$y$坐标相同。你有$m$个可弯曲一次的棍子，你可以在棍子的任意一个点将其弯曲，然后将弯曲点固定在一个点上，两端固定在相邻的点上。不允许出现棍子的重叠，请问能否有一种固定若干个棍子的方案，使得构成这样一个$n$个点的封闭多边形。
存在则输出方案。

## 思路：
我们先预处理出所有弯曲点固定点所需要的棍子的长度，然后我们发现如果要使得这个多边形封闭，那么必然有一个固定点是第1个点或第2个点，那么直接暴力枚举可以放置的棍子放置即可。

## 代码：
```cpp
#include<bits/stdc++.h>
#define ll long long
using namespace std;
int n,m;
struct point{
    int x,y;
    void read(){scanf("%d%d",&x,&y);}
}p[504];
int dis_t(point A,point B){
    return abs(A.x-B.x)+abs(A.y-B.y);
}
int lc[504],olc[504];
int len[504],ans[504];

int in_(int x){
    return (x+n)%n;
}
bool work(int bg){
    memset(ans,-1,sizeof(ans));
    for(int i=0;i<m;i++)olc[i]=len[i];
    for(int i=bg;i<n;i+=2){
        bool flag=1;
        for(int j=0;j<m;j++){
            if(lc[i]==olc[j]){
                olc[j]=-1;
                ans[i]=j+1;
                flag=0;
                break;
            }
        }
        if(flag)return 0;
    }
    puts("YES");
    for(int i=0;i<n;i++)printf("%d ",ans[i]);
    puts("");
    return 1;
}
int main(){
    scanf("%d%d",&n,&m);
    for(int i=0;i<n;i++)p[i].read();
    for(int i=0;i<m;i++)scanf("%d",&len[i]);
    for(int i=0;i<n;i++){
        lc[i]=dis_t(p[in_(i-1)],p[i])+dis_t(p[in_(i+1)],p[i]);
    }
    if(work(0))return 0;
    if(work(1))return 0;
    puts("NO");
    return 0;
}
```
## 后记：
这道题目并不是很难，关键要**读懂题目的意思**，便能**迎刃而解**$qwq$

最后，祝大家**新年快乐**！