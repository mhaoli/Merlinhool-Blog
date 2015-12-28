title: Codechef January Challenge 2015
comment: true
date: 2015-01-12 15:14:31
categories: Competitive Programming
tags: [Programming Contests,Editorial,Codechef,Dynamic Programming,Math,Constructive Algorithms,Data Structure,Persistent Data Structure,Persistent Segment Tree,Persistent Trie,平衡树,块状链表]
mathjax: true
---

rank 132	
<!--more-->			

##[Queries on the String](http://www.codechef.com/JAN15/problems/QSET)
首先，求每个点的前缀和，在模3的情况下。		

每次询问相当于，在区间中任选两个前缀和相同的点，有多少种选法。需要数据结构支持快速查找key值大于V的有多少个。		

每次修改相当于，对一个区间中每个点的前缀和都加1，加2，或不修改。需要数据结构支持快速合并和分离。		

平衡树随便搞。				

##[Xor Queries](http://www.codechef.com/JAN15/problems/XRQRS)
这是本场AC数最少的题，难度分类却仅仅medium。		

大概的原因是，操作3,4显然可以用不带修改的主席树做，操作1是经典问题，用trie树搞（见[Codechef PPTREE](http://www.codechef.com/problems/PPTREE))。		

然后，对于操作0，2这样的修改，对trie可持久化即可。		

<br>
<br>
**下面是三道相对较有意思的题**

##[Chef and A Large Permutation](http://www.codechef.com/JAN15/problems/CLPERM)

####**Brief Description:**
多组case。在1-N中，有K个数被丢弃了，其余数可用。找到最小的，不能用可用数拼凑出来的数（每次拼凑每个数最多用一次）。		
T <= 10^5，N <= 10^9，K <= 10^5，sum of K <= 5 * 10^5

####**Analysis:**
脑洞题。看了题毫无思路，但是过得人很多。于是敲了个暴力，然后脑补。		

首先，设剩下可用的数的集合为A，那么答案最大为$\sum_{i \subseteq A}i + 1$。			

答案还有一种可能，对于一个丢弃的数i，设比它小的可用的数集合为$A_i$，那么如果$i > \sum_{t \subseteq A_i}t$，i也可能为答案。		

除此之外，不可能存在答案。

##[Sereja and LCM](http://www.codechef.com/JAN15/problems/SEALCM)
####**Brief Description:**
对于范围1-M的数组A[N]，f(x)表示x | LCM(A[i])的数组个数，给定l, r求$\sum_{i = l}^{r}f(i)$。		
$N \leqslant 6 \times 10^5,\ M, l, r \leqslant 1000$

####**Analysis:**
枚举f(x)的x，设$x = \prod p_i^{k_i}$，那么每个$p_i^{k_i}$都相当于一个条件，对每个条件数组A[M]中都要有至少一个数满足。		

因为条件数最多4个，所以就存在最多16种状态，这就像是在一张16个节点的图上做dp，用矩阵优化就能AC了。			

##[Ranka](http://www.codechef.com/JAN15/problems/RANKA)		
####**Brief Description:**
两个人下围棋，怎样下一盘棋能超过10000次落子。要满足无同形再现。

####**Analysis:**
虽然过得少，其实还是很简单的。先用黑子将棋盘盖满，每下一颗黑子前都用白子将其余所有点填满（放下黑子就能把所有白子删掉那种），这样，大概能下6400次。			

反过来再用白子覆盖棋盘一次即可。		

##[Sereja and Number Division 2](http://www.codechef.com/JAN15/problems/SEAND2)		
马拉松题，我的解法赛后rejudge 70+pts。

大概思路是，每次交换两个数位的时候计算一下交换这两个数位会不会使答案更优，计算的时间代价是100。然后各种优化。

**2015.01.21UPD: 今天出了官网题解，我发现大部分人都是基于随机交换两个数位,优化尝试次数的思想。在[这篇blog](http://gauravsen.blog.com/2015/01/14/hello-world/)里面提到了一个思想：在全部随机化的情况下，估计出最大的70个除数可能会贡献出答案的90%，所以忽略比较小的30个除数。**