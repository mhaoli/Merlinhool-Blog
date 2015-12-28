title: Some String Problems
comment: true
date: 2015-01-28 19:43:52
categories: Competitive Programming
tags: [String,Editorial,Hash,Manacher,Aho-Corasick Automaton,Suffix Array,Suffix Automaton]
mathjax: true
---
在原来wordpress的blog发现了一点有意义的东西。		
于是搬过来。		
<!--more-->

##1. 求每类回文子串的个数
[2012 ACM-ICPC Asia Changchun Regional G](http://acm.zju.edu.cn/onlinejudge/showProblem.do?problemCode=3661) 			
[6th BUPT Programming Contest Final A](http://www.acm.uestc.edu.cn/#/problem/show/606)			

[Editorial](http://www.fcjy.org/g/) 		
[My Code](http://acm.hust.edu.cn/vjudge/contest/viewSource.action?id=2824512)(目前HUST上rank 1st^ ^)			
<br>
2014UPD：今天看14年集训队论文，发现这个问题还有别的解法，[My Code](http://acm.hust.edu.cn/vjudge/contest/viewSource.action?id=2868017)。(用set代替了Hash表，导致略慢一点)			
<br>

##2. AC自动机及fail tree

###**BZOJ 2434 [NOI 2011]阿狸的打字机**		
题意：将输入转化成一个最多$10^5$个点的Trie树，然后最多$10^5$个询问，每次询问包含Trie树的两个节点x和y，求x节点代表的字符串在y点的字符串中出现的次数。		
<br>
我是第一次做AC自动机的fail tree的题，感觉很好。。。		
<br>
[Editorial](http://seter.is-programmer.com/posts/31838.html)
代码可以看CLJ的。。。		

###**BZOJ 2754 [SCOI2012]喵星球上的点名**
我写的解题报告[My Editorial](http://plumrain.org/bzoj-2754/)。。。（请叫窝题解搬运工。。。		

###**BZOJ 2780 [Spoj]8093 Sevenk Love Oimaster**
就是BZOJ 2754的第一问。。。		

###**BZOJ 2746 [HEOI2012]旅行问题**
每次询问，对某两个字符串求，以某两点为终点的最长公共子串。。。fail tree上求LCA即可。。。当然，这题后缀数组和Hash也可做。。
<br>

##3. BZOJ 1014 [JSOI2008]火星人prefix
对字符串进行三个操作，某位置插入一个字符，某位置字符修改，询问某两个后缀的LCP。		
<br>
求LCP可以Hash+二分，有修改的话，Splay维护即可。			
<br>

##4. ZOJ 3199
将字符串表示成*xx*的形式(*为通用匹配符)，求x的最大长度。		
<br>
~~显然二分+后缀数组是可做的。。。~~不过cwj神犇的blog上给出了 两个非常优美的解法。		
<br>
[CWJ's Editorial 1](http://edward-mj.com/archives/1907)：分治+扩展kmp		
[CWJ's Editorial 2](http://edward-mj.com/archives/450)：枚举答案+lcp+lcs 		

###**BZOJ 2119**
上题的加强版。。。 		
[My Code](http://acm.hust.edu.cn/vjudge/problem/viewSource.action?id=2877510)(枚举答案)				
分治....待坑....		
<br>

##5. BZOJ 2565
求最长的可以分成两个回文串的子串		
<br>
感觉可以用数据结构O(nlogn)解决此题，貌似很多人都是O(nlogn)。不过有更优美更简单的O(n)解法。具体可以看2014年的集训队论文，徐毅的《浅谈回文子串问题》，代码可以看cmg神犇的，非常简洁。		
<br>

##6. BZOJ 2342
给定字符串，求最长双倍回文子串的长度。			
<br>
会做上面那题就会这题吧。。不过还是贴两个题解		
<br>
[Editorial 1](http://www.java123.net/v/583932.html)，[Editorial 2](http://lazycal.logdown.com/posts/195268-bzoj2342)		
<br>

##7. SAM

###**HDU 4436**
给N个数字串，把他们所有子串放进set去重后，和模2012是多少		
<br>
之前做过的题，重做一遍，复习下后缀自动机。[CWJ's Editorial](http://edward-mj.com/archives/835)。 		
<br>
（CLJ那个ppt虽然入门时觉得难懂，现在看却觉得讲得很好）		

###**Codeforces MemSQL Start[c]UP 2.0 – Round 1 E Three Strings**
懒得写题意，给题目链接吧。。[Problem Link](http://codeforces.com/contest/452/problem/E)。 		
<br>
貌似没后缀自动机的题解，看我的代码吧。。[My Code](http://codeforces.com/contest/452/submission/8247561)。 		

###**Uva 12361**
题意：有n个字符串s[n](n <= 60)，你可以随便写下一个字符串t，在s[n]中选出所有含有t为其子串的字符串形成一个集合A，问可能形成多少种非空集合。		
<br>
后缀数组可做，不过后缀自动机更简单。。可以看看这篇题解，[WUYIQI's Editorial](http://wuyiqi.net/house/suffix_datastructures_problems)。 			
<br>

##8. 回文性质的相等关系和不等关系
就在14年徐毅的论文上看见了一题。。。。BZOJ 3103 POI Palindromic Equivalence。。。。由于BZOJ没有VIP号，且没有理清证明过程，且弦图的相关知识空白，所以这题就留个坑待填吧。。。		
<br>

##一些无意义的水题/代码题
BZOJ 1559：AC自动机+状压dp，恶心的是，要输出符合答案的串。。更恶心的是，卡内存。。。		
<br>
BZOJ 2258：带修改的求LCP的题，类似于上面的BZOJ 1014，不过修改最多200次，所以可以不用Splay维护，每次修改完后暴力处理即可。不过后缀数组T了，改了二分+Hash才过。。	 			
<br>
BZOJ 3172: 后缀数组/AC自动机模板题。。。Ps：最近做了不少字符串的题目，感觉对AC自动机的理解提升了很多啊。。 			