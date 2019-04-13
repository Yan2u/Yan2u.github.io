---
layout: article
title: 分治 | Best Cow Fences
tags: 
- 分治
- 二分
mode: immersive
header:
  theme: dark
article_header:
  type: overlay
  theme: dark
  background_color: '#203028'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: 'https://s2.ax1x.com/2019/04/06/AWRHC4.jpg'

---

<!--more-->

## Description

Farmer John's farm consists of a long row of N (1 <= N <= 100,000)fields. Each field contains a certain number of cows, 1 <= ncows <= 2000.

FJ wants to build a fence around a contiguous group of these fields in order to maximize the average number of cows per field within that block. The block must contain at least F(1 <= F <= N) fields, where F given as input.

Calculate the fence placement that maximizes the average, given the constraint. 

## Input

- Line 1: Two space-separated integers, N and F.

- Lines 2..N+1: Each line contains a single integer, the number of cows in a field. Line 2 gives the number of cows in field 1,line 3 gives the number in field 2, and so on.

## Output

- Line 1: A single integer that is 1000 times the maximal average.Do not perform rounding, just print the integer that is 1000*ncows/nfields.

## Sample Input

```txt
10 6
6
4
2
10
3
8
5
9
4
1
```
## Sample Output

```txt
6500
```
## Hint

USACO 2003 March Green

## 分析

**二分题目所求的连续序列平均数**，需要用到前缀和，递推式：
$$
f[i]=max(\sum_{k=1}^iv[i]-\sum_{i=1}^jv[j]，j\in [1,i-f])
$$
发现 $\sum_{k=1}^iv[i]​$ 是定值，可以用前缀和处理出来，于是：
$$
f[i]=sum(i)-min(sum(j)，j\in [1,i-f])
$$
而 $i$ 变到 $i+1$ 时，$j$ 的选择范围扩大了 $1​$ ，于是：
$$
min(sum(j+1))=min(min(sum(j)，sum(j+1))
$$
**预处理 + 二分猜答案来做**


## Codes

```cpp
#include <cstdio>
#include <iostream>
#include <cstring>
#include <algorithm>
#include <cmath>
#define maxn 100001
#define INF 1e-6
using namespace std;
double v[maxn]; int n,f;
double prefix[maxn];
double minu[maxn];
double maxar,minar;
bool check(double avar){
	for(int i=1;i<=n;i++){
		prefix[i]=prefix[i-1]+v[i]-avar;
		minu[i]=min(minu[i-1],prefix[i]);
	}
	double ans=-99999.0;
	for(int i=f;i<=n;i++)
		ans=max(ans,prefix[i]-minu[i-f]);
	return ans>=0;
	return false;
}
int main(){
	#ifndef ONLINE_JUDGE
	freopen("t1.in","r",stdin);
	freopen("t1.out","w",stdout);
	#endif
	cin>>n>>f;
	for(int i=1;i<=n;i++){
		scanf("%lf",&v[i]);
		v[i]*1.0; minar+=v[i];
		maxar+=v[i];
	}
	minar=minar/(double)(n);
	double mid;
	while(abs(minar-maxar)>=INF){
		mid=(minar+maxar)/2.0;
		if(check(mid)) minar=mid;
		else maxar=mid;
	}
	printf("%d",(int)(maxar*1000));
	return 0;
}
```

