title: Codechef December Challenge 2014
comment: true
date: 2014-12-26 11:54:01
categories: Competitive Programming
tags: [Programming Contests,Editorial,Codechef,Dynamic Programming,Math,Mobius,Minimum Cut,Flow,启发式合并]
mathjax: true
---
rank 97
<!--more-->

##[Chef and Bracket-Pairs](http://www.codechef.com/DEC14/problems/CHEFBR)
比较简单的区间计数dp....

设sing[i][j]表示i和j是配对的括号的情况下，A[i...j]中有多少子序列合法。f[i][j]表示A[i]和A[j]被选入子序列的条件下，A[i...j]有多少个合法子序列。g[i][j]表示A[i..j]有多少合法子序列。答案即为g[0][n-1]。

##[Chef Under Pressure](http://www.codechef.com/DEC14/problems/CHEFPRES)
点分治也许是可以做的，不过我已经快忘了这个东西了.....于是写了个链表的启发式合并。

##[Sereja and GCD](http://www.codechef.com/DEC14/problems/SEAGCD)

####**Brief Description:**
每个询问给定N,M,L,R，求从[1, M]可重复地选出N个数，并且L <= gcd <= R的方案数。
询问数 <= 10，N,M,L,R <= 10^7，time limit <= 15s

####**Analysis:**
暴力枚举gcd然后用mobius求，TLE....		
不过我看见xllend3大爷大力常数优化11sAC....		具体做法大概就是枚举i的时候，如果m/i == m/(i+1)结果是相同的不用计算。		
然后我推导了一种比较猎奇的公式7sAC（欲知正解请移步看官方题解）。		

以下$\mu (n)$表示mobius函数。		

* **Preliminary: 如果$n = 1$, 则$\sum_{d\mid n}\mu(d) = 1$, 否则$\sum_{d\mid n}\mu(d) = 0$**

设$ans = F(R) - F(L-1)$。

设$f(n)$为$n = gcd(A[0]...A[n-1])$的方案数，$g(n)$为$n \mid (gcd(A[0]...A[n-1])$的方案数。显然$g(n) = (\frac{M}{n})^{N}$。

由定义知：	
$$
g(d) = \sum_{d \mid n}f(n)\ \ \Rightarrow f(d) = \sum_{d \mid n}g(n) \times \mu (\frac{n}{d})$$

故：
$$\begin{equation}\begin{split}
\Rightarrow F(n) &= \sum_{i = 1}^{n}f(i) = \sum_{i=1}^{n} \sum_{k=1}^{\left \lfloor \frac{M}{i} \right \rfloor}g(k\times i) \times \mu (k)\\
&= \sum_{a=1}^{M}g(a) \times \sum_{b\leq n,\,b \mid a}\mu(\frac{a}{b})\\
&= g(1) + \sum_{a=2}^{M}g(a) \sum_{b\leq n,\,b \mid a}\mu(\frac{a}{b})\\
&= g(1) - \sum_{a=2}^{M}g(a) \sum_{b < \left \lceil \frac{a}{n} \right \rceil,\,b \mid a}\mu(b)\\
&= g(1) - \sum_{a=2}^{M} \sum_{a\leq M,\,b < \left \lceil \frac{a}{n} \right \rceil,\,b \mid a}g(a) \times \mu(b)\\
&= g(1) - \sum_{b=1}^{M} \sum_{k=n+1}^{\left \lfloor \frac{M}{b} \right \rfloor}\mu(b) \times g(b\times k)
\end{split}\end{equation}$$

注意一个很有效的优化：给定了$N,M$后，预处理出所有$g(i)$，预处理的方法是，如果i为质数则暴力求，否则$g(i) = g(t) \times g(i/t)$。

这样写一写就过了...

##[Kali and Devtas](http://www.codechef.com/DEC14/problems/KALKI)

####**Brief Description:**
马拉松题。给定平面上n个点，求一棵生成树，使得Ci的最大值最小。Ci的定义：对树上每个节点i，设生成树中与其相连且距离最短的点与其距离为R，以i为圆心R为半径作圆，圆内每个点Ci值加1。

####**Analysis:**
想了几个方法都打不过MST....70pts左右		
题解给了篇英文论文，还有中文blog的方法也不是太懂....		
弃坑。

##[Divide or die](http://www.codechef.com/DEC14/problems/DIVIDEN)

####**Brief Description:**
给一个$n^\circ$的角，问能不能用尺规作图将其分成n个$1^\circ$度的角。

####**Analysis:**
首先，根据事实：用尺规作图不可能将任何角三等分。易推，当 $3 \mid n$时无解。

首先用尺规作图作出 $36^\circ$和 $30^\circ$，然后得到 $6^\circ$，然后得到 $3^\circ$。

用 $3^\circ$和 $n^\circ$搞出 $1^\circ$。

然后就是写写写....（不打算码了

##[Course Selection](http://www.codechef.com/DEC14/problems/RIN)
不错的最小割题....但是和Codeforces #248 D && SRM 590 Hard一模一样....[My Editorial](../../27/Codeforces-434D/index.html)
<br>
<br>
<br>  
