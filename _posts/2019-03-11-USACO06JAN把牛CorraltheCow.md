---
layout: article
title: 动态规划 | [USACO06JAN]把牛Corral the Cows
categories: 题目
mode: immersive
header:
  theme: dark
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: 'http://pic.netbian.com/uploads/allimg/190224/204454-15510122943266.jpg'
---

<!--more-->

## Desciption

Farmer John wishes to build a corral for his cows. Being finicky beasts, they demand that the corral be square and that the corral contain at least C (1 <= C <= 500) clover fields for afternoon treats. The corral's edges must be parallel to the X,Y axes.

FJ's land contains a total of N (C <= N <= 500) clover fields, each a block of size 1 x 1 and located at with its lower left corner at integer X and Y coordinates each in the range 1..10,000. Sometimes more than one clover field grows at the same location; such a field would have its location appear twice (or more) in the input. A corral surrounds a clover field if the field is entirely located inside the corral's borders.

Help FJ by telling him the side length of the smallest square containing C clover fields.

约翰打算建一个围栏来圈养他的奶牛.作为最挑剔的兽类，奶牛们要求这个围栏必须是正方 形的，而且围栏里至少要有C< 500)个草场，来供应她们的午餐.

约翰的土地上共有C<=N<=500)个草场，每个草场在一块1x1的方格内，而且这个方格的 坐标不会超过10000.有时候，会有多个草场在同一个方格内，那他们的坐标就会相同.

告诉约翰，最小的围栏的边长是多少？

## Input

Line 1: Two space-separated integers: C and N

Lines 2..N+1: Each line contains two space-separated integers that are the X,Y coordinates of a clover field.

## Output

Line 1: A single line with a single integer that is length of one edge of the minimum size square that contains at least C clover fields.

## Sample Input

```txt
3 4
1 2
2 1
4 1
5 2
```

## Sample Output

```txt
4
```

## Hint

Explanation of the sample:

|* *

| * *

+------Below is one 4x4 solution (C's show most of the corral's area); many others exist.

|CCCC

|CCCC

|*CCC*

|C*C*

+------

## 分析

**二分搜索栅栏的边长**，每次将边长带入到图中，计算出最多能覆盖到的草场的数量即可
{:.success}

要计算覆盖草场的数量，选定一块草场 $i$ ，将 $x[i]$ 设为覆盖的上边界，得出下边界，在上边界和下边界中二分查找（使用 $ lower\_\;bound $）找到左右边界的草场编号范围（当然这需要提前对草场位置排序）

## Codes

```cpp
#include <cstdio>
#include <iostream>
#include <algorithm>
#define maxn 10001
#define fr(na,st,ed) for(int na=st;na<=ed;na++)
using namespace std;
int x[maxn],y[maxn];
int id1[maxn],id2[maxn];
int n,c; int l=1,r,mid;
inline bool cmp1(int q,int w){
	return x[q]<x[w];
}
inline bool cmp2(int q,int w){
	return y[q]<y[w];
}

inline bool check(int size){
	int st,ed,k,sum;
	fr(i,1,n){
		k=1; sum=0;
		st=x[id1[i]]; ed=st+size-1;
		fr(j,1,n){
			while(y[id2[k]]-y[id2[j]]+1<=size && k<=n){
				if(st<=x[id2[k]] && x[id2[k]]<=ed) sum++;
				k++;
			}
			if(sum>=c) return true;
			if(st<=x[id2[j]] && x[id2[j]]<=ed) sum--;
		}
	}
	return false;
}
int main(){
	#ifndef ONLINE_JUDGE
	freopen("t3.in","r",stdin);
	freopen("t3.out","w",stdout);
	#endif
	cin>>c>>n;
	fr(i,1,n){
		cin>>x[i]>>y[i];
		r=max(r,max(x[i],y[i]));
		id1[i]=id2[i]=i;
	}
	sort(id1+1,id1+n+1,cmp1);
	sort(id2+1,id2+n+1,cmp2);
	while(l<=r){
		mid=(l+r)>>1;
		if(check(mid)) r=mid-1;
		else l=mid+1;
	}
	cout<<l;
	return 0;
}
```

