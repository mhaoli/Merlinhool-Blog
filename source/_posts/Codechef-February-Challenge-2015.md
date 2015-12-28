title: Codechef February Challenge 2015
comment: true
mathjax: true
date: 2015-02-16 17:36:01
categories: Competitive Programming
tags: [Programming Contests,Editorial,Codechef,Dynamic Programming,FFT,Math,Precalculation,Greedy]
---

rank 71 		
<!--more-->

##[Chef and Strings(STRQ)](http://www.codechef.com/FEB15/problems/STRQ)

####**Brief Description:**
由'c','h','e','f'组成的长为n的字符串，Q次询问，每次询问为区间[l,r]中有多少个以字符a开头，字符b结尾的字符串。  		
n, Q <= 10^6 		
		
####**Analysis:**
显然首先将询问分成16种...对每种(a,b)的询问，预处理出cnt[i]表示第i个a后面有多少个b，posA[i]表示第i个a在原串中的位置，posB[i]表示第i个b在原串中的位置。 		
	 		
那么有$ans = S - cnt_a * tb$ 		
$where \ S = \sum_{posA_i \in [l,r]}cnt_i, \ cnt_a = \sum_{posA_i \in [l,r]} 1, \ tb = \sum_{posB_i > r} 1$

S, cnt_a, tb都比较好求了...不过要记得用O(n)方法。

##[Time to Study Graphs with Chef(CHEFGRPH)](http://www.codechef.com/FEB15/problems/CHEFGRPH)

####**Brief Description:**
一个n+2层有向图，从左到右每层标号为0-n+1，0层和n+1层各有一个节点，其它层每层m个节点，任意的i < n+1，第i层任意一个点，都有到第i+1层所有点的有向边各一条。现在向图中加边k条边，对加边(a,b)保证a节点所在层编号比b节点小。问加边以后，从第0层走到第n+1层有多少种方法。mod (7 + 1e9)。 		
n <= 10^12，m <= 10^5, k <= 5*10^4 			

####**Analysis:**
将新加入的边记为特殊边，连有特殊边的节点记为特殊点，含有特殊点的层记为特殊层。虽然n很大，但是特殊边、点、层的数量都是10^5。 		

对第i个特殊点，指向它的特殊点集为B[i]，它所在的列标号为idx[i]。 		 	

对第i个特殊列，pos[i]表示其对应的列标号，A[i]表示它含有的所有特殊点。

设对某个编号为j，在第i层的节点，从起点到它的方案中，最后一条边不是特殊边的方案有F[i]种，是特殊边的方案有G[j]种。也即是说，到第i层的普通节点每个点有F[i]种方案，到该层的特殊节点j每层有F[i] + G[j]种方案。于是有： 		

$$F_i = F_{i-1} * m^{pos_i\ -\ pos_{i-1}} + \sum_{j \in A_{i-1}} G_j * m^{pos_i\ -\ pos_{i-1}\ -\ 1}$$

$$G_i = \sum_{j \in B_i} G_j + F_{idx_j}$$


##[Xor Matrix(XRMTRX)](http://www.codechef.com/FEB15/problems/XRMTRX)
这个题是真没什么好说的....虽然过得人很少，但其实就是找规律，写暴力验证规律对不对，在哪不对然后修正规律...花时间就能做出来的题。  		

##[Jigsaw Puzzle Solving(CHPUZZLE)](http://www.codechef.com/FEB15/problems/CHPUZZLE)
challenge题，感觉没什么好说的...也没补这题....

Happy New Year!