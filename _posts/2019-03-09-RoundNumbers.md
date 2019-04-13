---
layout: article
title: 动态规划 | 数位 | Round Numbers
tags: 
- 动态规划
- 数论
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

The cows, as you know, have no  fingers or thumbs and thus are unable to play Scissors, Paper, Stone'  (also known as 'Rock, Paper, Scissors', 'Ro, Sham, Bo',and a host of  other names) in order to make arbitrary decisions such as who gets to be  milked first. They can't even flip a coin because it's so hard to  tossusing hooves.

Theyhave thus resorted to "round number"  matching. The first cow picks aninteger less than two billion. The  second cow does the same. If the numbers areboth "round numbers", the  first cow wins, otherwise the second cowwins.

A positive integer  N is said to be a "round number" if the binary representation of N has as  many or more zero es than it has ones. For example,the integer 9, when  written in binary form, is 1001. 1001 has two zero es and two ones; thus, 9  is a round number. The integer 26 is 11010 in binary; since it has two  zero es and three ones, it is not a round number.

Obviously,it  takes cows a while to convert numbers to binary, so the winner takes a  while to determine. Bessie wants to cheat and thinks she can do that if  she knows how many "round numbers" are in a given range.

Helpher by  writing a program that tells how many round numbers appear in  theinclusive range given by the input (1 < Start < Finish  <2,000,000,000).

## Input

Line 1: Two space-separated integers, respectively Start and Finish.

## Output

Line 1: A single integer that is the count of round numbers in the inclusive range Start..Finish

## Sample Input

```txt
2 12
```

## Sample Output

```txt
6
```

## Hint

No Hint

## 分析

一道数位 $DP$ 题，根据题目要求，要在 $[L，R]$ 区间内求出转化为二进制之后 $0$ 的个数不少于 $1 $ 的个数的数字个数，用**试填法 + $DFS$ 的记忆化实现**

注意前导0的问题，代码中用 $lead$ l来指示前导0

## Codes

```cpp
#include <cstdio>
#include <iostream>
#include <cstring>
#define maxn 41
using namespace std;
typedef long long LL;
LL dp[maxn][maxn][maxn];
int spr[maxn];
LL dfs(int x,int c1,int c0,bool lead,bool lim){
	if(x==0) return c0>=c1;
	if(!lim && dp[x][c1][c0]!=-1) return dp[x][c1][c0];
	LL ans=0; int imax=lim?spr[x]:1;
	for(int i=0;i<=imax;i++){
		if(i==1)
			ans+=dfs(x-1,c1+1,c0,lead && i==0,lim && i==imax);
		if(i==0 && lead)
			ans+=dfs(x-1,c1,c0,lead && i==0,lim && i==imax);
		else if(i==0)
			ans+=dfs(x-1,c1,c0+1,lead && i==0,lim && i==imax);
	}
	if(dp[x][c1][c0]==-1) dp[x][c1][c0]=ans;
	return ans;
}
inline LL res(int x)
{
	memset(spr,0,sizeof(spr));
	int cnt=0;
	while(x>0){
		spr[++cnt]=x&1;
		x>>=1;
	}
	return dfs(cnt,0,0,1,1);
}
int main(){
	#ifndef ONLINE_JUDGE
	freopen("t2.in","r",stdin);
	freopen("t2.out","w",stdout);
	#endif
	memset(dp,-1,sizeof(dp));
	LL a,b;
	cin>>a>>b;
	cout<<res(b)-res(a-1);
	return 0;
}
```

