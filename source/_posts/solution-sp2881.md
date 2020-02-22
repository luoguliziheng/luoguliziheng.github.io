---
title: 题解 SP2881 【CLONE - Find the Clones】
author: 李梓恒
top: false
cover: true
toc: true
mathjax: true
summary: 蒟蒻的超烂题解
tags:
  - 洛谷题解
categories:
  - 题解
abbrlink: 29747
img: /medias/banner/1.jpg
date: 2020-02-08 20:51:20
coverImg:
password:
---
## 解题思路
最近在学习字典树，刚开始看到这题也想用字典树来做。思考后发现其实可以用更简单的$map$来实现。定义类型为$map<char*, int>$的变量，记录字符串出现的次数。然后开辟数组$num[20000]$，记录出现$i(1<=i<=n)$次的字符串的个数。再遍历map，以当前字符串出现的字数减$1$记为$k$作为索引，更新$num[k]$，使得$num[k]++$。

实现时需要注意的地方：

1、因为在定义$map$时的$key$类型是$char *$，因此需要自定义比较函数。

2、为避免每次都$new$新的字符串，定义字符数组，需要$new$的地方，直接从数组中取。

## 代码：
```cpp
#include<bits/stdc++.h>
using namespace std;
struct cmp
{
	bool operator()(const char *s1, const char *s2) const
	{
		return strcmp(s1, s2) < 0;
	}
};
int main()
{
	char *dna;
	char dnas[20000][21];
	int num[20000];
	map<char*, int, cmp> mp;
	int i, j, m, n;
	
	while(scanf("%d%d", &n, &m))
	{
		if(n == 0 && m == 0)
			break;
 
		j = 0;
		mp.clear();
		for(i = 0; i < n; i++)
		{
			dna = dnas[j++];
			scanf("%s", dna);
			mp[dna]++;
		}
 
		memset(num, 0, sizeof(num));
		map<char*, int, cmp>::iterator iter = mp.begin();
		while(iter != mp.end())
		{
			num[iter->second - 1]++;
			iter++;
		}
		for(i = 0; i < n; i++)
		{
			printf("%d\n", num[i]);
		}
	}
	return 0;
}
```
## 后记：
利用$map$实现，程序的执行效率比较低。有时间再用$Trie$方法实现，比较两者的效率（猜测$Trie$肯定比$map$实现高效）。