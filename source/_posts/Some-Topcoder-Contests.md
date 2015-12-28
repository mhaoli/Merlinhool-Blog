title: Some Topcoder Contests
comment: true
date: 2015-04-24 22:30:17
categories: Competitive Programming
tags: [Topcoder,SRM,TCO,Inclusion-Exclusion,Dynamic Programming,Math,Graph Theory]
mathjax: true
---
SRM 653-658  				
TCO 2015 			
连载中...  					
还有很多SRM的题解写在以前的blog里 			
[Code](https://github.com/Merlinhool/ACM-Source-Code/tree/master/Problems/Topcoder/) 				 		
<!--more-->  		

##SRM 658

####**Easy**
按到0点的距离奇偶性分成两个集合，奇集合所有点都置成0点的子节点，偶集合除了0点都置为奇集合任一点的子节点。。。。如果该树不满足题意，那么一定不存在满足题意的树。。。 					

####**Medium** 
注意到，假设第i个SCV被$-9$的次数是$a_i$，被$-3$的次数是$b_i$，被$-1$的次数是$c_i$。 					
<br>
有一个很重要的性质：一共攻击T次，要求每次攻击$-9$，$-3$，$-1$不能作用于同一个SCV，等价于$a_i + b_i + c_i \leq T\ for\ all\ i$。 				
<br>
那二分答案，然后dp判定。$dp[i][j][k]$表示前i个SCV，用掉j次$-9$，用掉$k$次$-3$的情况下，最少用多少次$-1$。 						

####**Hard**
记男孩为A集合，女孩为B集合，集合X的邻点集为$nei(X)$。 						

如果有这样一个结论，将设当前图的最大匹配为$(T_A,\ T_B)$，那么一定存在一组满足题意所求的匹配$a-b$满足$b \subseteq T_B$。 					
<br>
那么，我们只需将当前图求最大匹配$(T_A,\ T_B)$，如果最大匹配不满足题意所求，那么将$nei(B - T_B)$中所有点均设为不可用，再在可用点中求最大匹配，做重复工作直到最大匹配满足题意为止。详见[wenhanhuang's Code](http://community.topcoder.com/stat?c=problem_solution&rm=326176&rd=16461&pm=13760&cr=40037065) 							
<br>
下面证明这个结论： 					

- 构造网络流($(S, A_i, 1),\ (B_i, T, 1),\ (A_i, B_j, INF)$)求最大流，然后一定存在一个割集，其中必有至少一条边是和汇点T相连的。  		
- 割集中每条边对应一个A或B中的点，设对应A中点集为a，B中为b，此时最大流为n - MAX，那么$nei(A - a) \subseteq b$，且$|A - a| = |b| + MAX$。
- 由Hall定理，在A - a和b构成的图上，必存在一个包含了所有b中点的匹配。得证。


##SRM 657

####**Easy**
可以直接算....像我这么弱肯定是二分判定了... 					

####**Medium**
<font color="red">Nice Problem</font>  			
<br>
因为现在官方题解还没出，推荐[jiry_2的代码](http://community.topcoder.com/stat?c=problem_solution&rm=326126&rd=16417&pm=13461&cr=23309233)。大概思想就是首先按质数分开算，然后按幂的大小分层算最优。。。。   			
<br>
感觉这种问题做少了，碰到几次都不太会。。。。 		

##SRM 656

####**Easy**
很简单辣。。。dp或者组合数学都可以。。。

####**Medium**
首先，考虑容斥，可以$O(2^{pos.size()})$。。。列出求答案的式子就能看出如何dp。。 			

##SRM 655

####**Easy**
倒着做，从结束态变换初始态。每次找到同色$k \times k$正方形，将他们标记为任意色，然后继续找同色正方形，若能让所有格点都变为任意色则Possible，否则Impossible。  				

####**Medium**
首先，$O(5000\ \times 9^n \times 9 \times 5)$的dp是很简单的。。 		
<br>
注意到一个性质，虽然d[]有5000个变量，但只有$2^5$种。若$d_i = d_j$，那么他们对于方程组的影响是一样的，可以当做一个变量来dp。 		
<br>
预处理合成变量值为0～8各有多少种可能，可以做到$O(2^5 \times 9^5 \times 9 \times 5)$。   				

##SRM 654

####**Easy**
最直接的想法是$n^2$枚举每一个substring然后判断。。。 					
<br>
感觉自己写麻烦了，推荐[cgy4ever的代码](http://community.topcoder.com/stat?c=problem_solution&rm=325620&rd=16318&pm=13694&cr=22769059)。 				

####**Medium**
首先，很容易发现一个性质：两个括号要么嵌套，要么没有交集。然后发现前者对应的等式结果包含于后者，即只需要考虑后者。。。 		 			
<br>
然后想了好久数据结构维护，结果发现是个暴力dp。。。。 			
<br>
$dp[i][j][0]$表示，前i个数字，已经用了j个括号，且第j个括号已经完整出现的最大答案。					
$dp[i][j][1]$表示，前i个数字，已经用了j个括号，且第j个括号只用了左括弧的最大答案。 					
<br>
后来看别人代码发现，因为最多只有两个括号，所以不需要发现那个性质，直接$dp[i][4]$记录状态就好了。。。  				

####**Hard**
<font color="red">Nice Problem</font> 					
<br>
首先，如果只有一个Entrance，那是很简单的。令$sz[x]$表示x的子树节点数，$dp[x]$表示x的子树的合法排列数，$C[][]$表示组合数，$E[x]$表示x的子节点集合。$dp[x]$求法如下：
```
int tot = sz[x] - 1;
for(int i : E[x]) {
                dp[x] = dp[x] * (1ll * dp[i] * C[tot][sz[i]] % mod) % mod;
                tot -= sz[i];
}
```
<br>
现在来看两个Entrance的情况。 				
<br>
树的形状变成了，一条s1到s2的链$pat_0, pat_1, \ldots pat_{m-1}$，然后每个$pat_i$都挂了一颗子树。  			
<br>
考虑那条链，注意到，当$t1 > t2 > t3$时，$pat_{t1}$和$pat_{t3}$不可能都比$pat_{t2}$先选取。换句话说，对于链的一个substring，$i \ldots j$，最先选择的要么是i要么是j，所以可以dp了。 				
<br>
$f[t1][t2]$表示链上第t1到第t2个点及其子树全部被选取的情况下合法排列数，它要么由$f[t1+1][t2]$转移得到，要么由$f[t1][t2-1]$转移得到。转移的方法与上面那种dp同。$f[0][m-1]$即为答案。 				

##SRM 653

####**Easy**
奇怪的题。。。计数dp。。。 					

####**Medium**
最小割。。。裸裸的。。。

####**Hard**
shenmegui。。。quite easy。。。quite boring。。。 					

将题目条件转化为等式，然后消消元推一推就出来了。。。 			

##TCO 2015 Round 1A 			

####**Easy** 
虽然有$10^5$个数，但是只有$2^{10}$种，统计每种有多少个，更新答案。。。 			

####**Medium**
关键性质：如果点i和点j矛盾，点j和点k矛盾，那么i,k也矛盾。 				
<br>
那么，处理有多少个连通块，可行方案为每个联通块贡献1个或0个点。  			

####**Hard**
关键性质：不存在perfect matching的充要条件是，存在点集A，其前驱集合为点集B，满足$|A| > |B|$。 			
<br>
我们称每条边都是从左边的点集指向右边的点集。记边权为$w[]$，没有边边权为0。 			
<br>
因为每个左边的点对右边点集的影响是独立的，所以枚举每个右边的点集A，对每个点i求$f[A][i] = \sum_{j\in A} w[i][j]$，然后取最小的$n - |A| + 1$个$f[A][i]$之和更新答案。。。

##TCO 2015 Round 1B 			

####**Easy**
$10^8$的暴力。。。  				

####**Medium**
记集合$A_i$为能到达$i$点的所有点。记题目给的概率为$p_i$ 				
<br>
$i$点最终会被找到的概率为$pp_i = 1 - \prod_{j \in A_i} (1 - p_i)$ 				
<br>
$ans = \sum pp_i$

####**Hard**
Man sequence类似于一个高为4的树，只需要确定高度为4那一层，就能确定这棵树主干上的4个节点，其他节点选择方案数通过组合数学求。。  									
<br>
$dp[i][j]$表示以第$i$个节点为Man sequence中第$j$个节点的方案数，然后递推计数就好了。。。 					

##TCO 2015 Round 1C
水。。。。。30min大家都AK了。。。 				

####**Easy**
随便dp一下....贪心貌似也可过

####**Medium**
求一下叶子节点个数就好了。。。 					

####**Hard**
n^4随便dp。。。。方法太多了。。。 				
