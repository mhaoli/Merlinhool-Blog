title: Codeforces 434D Nanami's Power Plant
comment: true
date: 2014-12-27 10:23:58
categories: Competitive Programming
tags: [Flow,Minimum Cut,Editorial,Codeforces]
mathjax: true
---
###Brief description:
___
有n个点，每个点有一个值x_i，取值范围$l_i \leq x_i \leq r_i$，并且给m个限制关系，每个限制关系给定u, v, d，意为$x_u \leq x_v + d$。每个点的权值$f_i = a_i \times x_i^2 + b_i \times  x_i + c_i$。求$\sum f(i)$最大。              
$n \leq 50,\ m \leq 100,\ -100 \leq l_i,\ r_i \leq 100$         
<!--more-->

###Analysis:
___
考虑最小割。          
因为问题要权值和最大， 所以令$F(i, t) = bigInteger - f(i, t)$。其中f(i, t)表示x_i = t的时候f(i)的值。只需要最小化$\sum F(i)$。          

先不考虑限制关系。              
对每个点的每种取值拆点。用node(i, j)表示第i个点，且权值为j + l_i。              
建三种边：              
$<source,\ node(i, 0),\ F(i, l_i)>$，             
$<node(i, j),\ node(i, j+1),\ F(i, l_i + j + 1)>$，               
$<node(i, r_i - l_i),\ target,\ inf>$。           
这样，求$n \times bigInteger - flow_{mincut}$即是答案。         
<br>
下面添加限制条件。              
对$x_v \geq x_u - d$，也即是说，当u点相关的割出现在值为i的时候，v点的割不能出现在i - d之前。            
那么，连边:$<node(u, i),\ node(v, i-d),\ inf>$。              

###External Links:
___
two related problems:[SRM 590 Hard](http://community.topcoder.com/stat?c=problem_statement&pm=12727&rd=15702&rm=318618&cr=22744264), [Codechef Course Selection](../../26/4/index.html)。                
[code](http://codeforces.com/contest/434/submission/9225919)
<br>
