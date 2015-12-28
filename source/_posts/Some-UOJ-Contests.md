title: Some UOJ Contests
comment: true
date: 2015-04-23 17:34:03
categories: Competitive Programming
tags: [Editorial,UOJ,Dynamic Programming,树的直径]
mathjax: true
---

[Code](https://github.com/Merlinhool/ACM-Source-Code/tree/master/Problems/UOJ)
<!--more--> 		

##UOJ Test Round #1
###B
如果所有优先级都知道，放到优先队列里面随便求。。			
<br>
假设第$x$题不知道优先级，那么求出在$t_x$时刻有哪些已经得到但没做完的题。注意到这样一个性质，在时间段$[t_x,T]$做过的题都在$[t_x,T]$做完了，那么就能知道时间段$[t_x,T]$做了哪些题，$x$题一定是其中优先级最低的。。。 			
<br>
然后随便求。。。 		

###C
找到所有黑点点对中距离最远的一对$(x,y)$，这个就类似于，以黑点为节点的树的直径。。。 		
<br>
注意到直径的性质，对任意节点$i$，可以得到如下两个性质（记$MaxDis_i$为最远点和它的距离）： 			

1. 那么对于任意$i$，$MaxDis_i = max(dis(i,x), dis(i,y))$
2. 如果存在点$j$，如果$MaxDis_i = dis(i,j)$，且$i$和$j$都不在路径$(x,y)$上，那么路径$(i,j)$和$(x,y)$必定相交 		

利用这两个性质，把白色节点分成两种——在链$(x,y)$上的和不在链$(x,y)$上的。$O(n)$随便求。。。

##UOJ Round #1
###B
注意到两个性质：（称真正改变了$x$值的$a_i$为真正起了作用） 		 		

1. 若$a_i$和$a_j$真正起了作用且$a_i > a_j$，则$a_i$一定排在$a_j$前面
2. 令$y = x\ mod\ t$，若$x \neq y$，那么$(y * 2) < x$。所以，真正起了作用的$a_i$不超过$\lg_2 5000 = 12$个

考虑动规。$dp[i,j,k]$表示前$j$个中有$i$个真正起作用，作用后$x$的值为$k$的情况有多少种。写得优美点，90ms就跑出来了。。。 		 			
<br>
Ps：我是利用了性质2在暴力dp。UOJ题解给的利用组合数学+dp更加优美...