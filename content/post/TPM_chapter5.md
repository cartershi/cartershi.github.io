---
title: "TPM_chapter5"
date: 2021-04-22T16:06:32+08:00
draft: false
tags: ["local lemma"]
---

本章是著名的local lemma，处理低概率事件的神器。

# THE LEMMA

**Lemma 5.1.1** $A_1,\cdots,A_n$是任意概率空间的事件，将任意两个不独立事件连边，构成依赖图。若存在$x_1,\cdots,x_n$，使得$Pr[A_i]\le x_i\prod_{(i,j)\in E}(1-x_j)$，则$Pr[\bigwedge_{i=1}^{n}\overline{A_i}]\ge\prod_{i=1}^{n}(1-x_i)$。即所有事件可以同时**不**发生

**Proof.** 用数学归纳法证明$Pr[A_j|\bigwedge_{i=1}^{j-1}\overline{A_i}]\ge x_j$。将事件分为$A_1,\cdots,A_{j-1}$分为$S_1$：与$A_j$不独立，$S_2$：与$A_j$独立，接下来易证。$\Box$

**Remark.** $Pr[A_i]\le x_i\prod_{(i,j)\in E}(1-x_j)$可替换为$Pr[A_i|\bigwedge_{j\in S_2}\overline{A_j}]\le x_i\prod_{(i,j)\in E}(1-x_j)$。显然这是个更弱的条件

**Corollary 5.1.2** 每个事件最多与d个其他事件相关，每个事件发生概率最多为p，若$ep(d+1)\le1$，则$Pr[\bigwedge_{i=1}^{n}\overline{A_i}]>0$

**Proof.** 取$x_i=\frac{1}{d+1}$，则$Pr[A_i]<p\le\frac{1}{e(d+1)}< \frac{1}{d+1}(1-\frac{1}{d+1})^d$，得结论$\Box$

# PROPERTY B AND MULTICOLORED SETS OF REAL NUMBERS

特征B指超图中点2染色使得没有超边同色。

**Theorem 5.2.1** 直接用Corollary 5.1.2的结论，略

定义实数的k染色为每个实数染k种颜色中的一种，定义集合多色为这个集合中的实数包含所有的k中颜色。

**Theorem 5.2.2** 正整数$k,m$满足$e(m(m-1)+1)k(1-\frac{1}{k})^m\le1$，则对于m个实数的任意实数集S，存在一种染色，使得每个$x+S\quad x\in R$都是多色集合。

**Proof.** 考虑一个有限集合$X\subset R$，对$Y=\cup_{x\in X}(x+S)$进行随机k染色，定义$A_x$为$x+S$不是多色集合，则$Pr[A_x]\le k(1-\frac{1}{k})^m$，每个$s\in S$最多与m-1个集合相关，则相关事件数为$m(m-1)$，又Corollary 5.1.2得这个集合X满足条件。则由**compactness**，实数集满足条件。$\Box$

# LOWER BOUNDS FOR RAMSEY NUMBERS

$R(k,k)>(\sqrt{2}/e)(1+o(1))k2^{k/2}$

这个bound并不好看，因为每个事件相关的事件太多

$R(k,3)>c_5k^2/\log^2{k}$

$R(k,4)>k^{5/2+o(1)}$

这两个结论需要很tedious的函数计算

# A GEOMETRIC RESULT

3维空间的k折覆盖定义为每个点被至少k个开区间单位球覆盖，可分解定义为将k折覆盖划分成两个集合，每个都是1折覆盖。

**Theorem 5.4.1** 令$F=\{B_i\}_{i\in I}$是开区间单位球组成的k折覆盖，且每个点不被多于t个球覆盖，若$et^32^{18}/2^{k-1}\le 1$，则$F$可分解

**Proof.** 定义无限超图，点集为$F=\{B_i\}_{i\in I}$，超边为同时覆盖点的球，则每条超边至少k个点。接下来证明$d<t^32^{18}$（几何证明鸽了），则由定理Theorem 5.2.1，得任意有限超图有特征B。由compactness，无限超图有特征B，则按照颜色划分，每条边都被两种球覆盖，即1折覆盖。$\Box$

# THE LINEAR ARBORICITY OF GRAPHS

线性森林是每个连通分支都是一条路径，线性荫度$la(G)$为G中包含所有边的线性森林的最小数目，包含G中的所有点。

**Conjecture 5.5.1 [The Linear Arboricity Conjecture]** 每个d正则图的线性荫度都是$\lceil(d+1)/2\rceil$。

显然每个线性森林最多n-1条边，则$la(G)\ge nd/2(n-1)>d/2$，则$la\ge \lceil(d+1)/2\rceil$。所以只需要考虑$la(G)$的上界。

考虑有向图的版本

**Conjecture 5.5.2** 每个d正则有向图的线性荫度$dla(G)=d+1$

**Proposition 5.5.3**  对于最大度为d的图H，令$V=V_1\cup V_2\cup \cdots\cup V_r$为V的划分，假定每个集合大小至少为2ed，则存在一个独立集包含每个$V_i$中的一个点。

**Proof.** 只考虑每个点集大小$g=\lceil2ed\rceil$个点的情况，多余的点直接抛弃，这不影响结论。接下来每个$V_i$等概率的选一个点，证明这样的r个点有概率独立。

边的端点被同时选中的概率$Pr[A_f]\le1/g^2$，与$A_f$相关的事件必然是端点与f在同一个集合里的，所以相关事件少于2gd，则有Corollary 5.1.2得结论。 $\Box$

**Theorem 5.5.4** 令$G=(U,F)$为d正则有向图，它的girth $g\ge 8ed$，则$dla(G)=d+1$

**Proof.** 构造二部图$(U,U,F)$，则其有d个完美匹配，每个匹配$F_i$是$r_i$个圈的集合，显然每个圈至少$8ed$条边，所有的圈构成$F$的一个划分。定义线图H，点集为$F$，边为G中相邻的边，由于G中每个点有d条入边d条出边，则每条边的邻居边为$2(d+d-1)=4d-2$，即H为4d-2正则图。由Proposition 5.5.3，存在一个H的独立集包含每个圈中至少一条边，互不相邻，即一个匹配M。显然匹配也是一个线性森林，每个$F_i/M$也是一个线性森林，即$dla(G)\le d+1$。

在考虑下界，每个线性森林最多|U|-1条边，共|U|d条边，则$dla(G)\ge |U|d/(|U|-1)> d$。$\Box$

**Remark** 这个定理说明若有向图没有小的环时，Conjecture 5.5.2成立。通过染色将图做拆分，每个子图用Theorem 5.5.4。

**Lemma 5.5.5** 令$G=(V,E)$是d正则有向图，d足够大，p为整数$10\sqrt{d}\le p\le 20\sqrt{d}$。则存在一个p染色使得对于每个点和每种颜色i，$N^+(v,i)=|\{u\in V:(v,u)\in E且u染色为i\}|$，$N^-(v,i)=|\{u\in V:(u,v)\in E且u染色为i\}|$满足$|N^-(v,i)-d/p|,|N^+(v,i)-d/p|\le3\sqrt{d/p}\sqrt{\log{d}}$

**Proof.** 每个点随机染色，定义$A^+_{v,i}$为事件$|N^+(v,i)-d/p|\le3\sqrt{d/p}\sqrt{\log{d}}$不成立。显然$N^+(v,i)$是二项独立事件，期望$d/p$，标准差$\sqrt{(d/p)(1-1/p)}<\sqrt{d/p}$，则$Pr[A^+_{v,i}]<1/d^4$。同理$Pr[A^-_{v,i}]<1/d^4$。事件依赖关系最多为$(2d)^2p$，由Corollary 5.1.2得结论。

令p为一个质数，对G进行p染色，定义$G_i$为色差mod p为i的子图，则度$\le d/p+3\sqrt{d/p}\sqrt{\log{d}}$。由群论基本知识得，每个$G_i$girth至少是p，通过加点加边变成正则图，由Theorem 5.5.4，$dla(G_i)\le d/p+3\sqrt{d/p}\sqrt{\log{d}}+1$。$G_0$直接强行破圈$dla(G_0)\le 2(d/p+3\sqrt{d/p}\sqrt{\log{d}})$，求和得

**Theorem 5.5.6** $dla(G)\le d+cd^{3/4}(\log d)^{1/2}$

应用到无向图上（无向图定向）

**Theorem 5.5.7** $la(G)\le d/2+cd^{3/4}(\log d)^{1/2}$

# LATÍN TRANSVERSALS

定义n*n的整数矩阵A的一个Latin transversal为一个1..n的排列$\pi$，使得所有的$a_{i\pi(i)}$都不同。

**Theorem 5.6.1** 假定$k\le (n-1)/(4e)$且无整数在A中出现超过k次，则A有Latin transversal。

**Proof.** 随机选取一个排列$\pi$，定义四元组$(i,j,i',j')$为$i<i'\& a_{ij}=a_{i'j'}$。对于每个四元组，定义$A_{iji'j'}$为事件$\pi(i)=j\& \pi(i')=j'$，则这些事件均不成立即Latin transversal。$A_{iji'j'}$相关事件在第i、i'行或第j、j'列中，<4n个，每个最多在k个四元组中，所以相关事件<4nk。接下来$Pr[A_{iji'j'}|\bigwedge_{j\in S}\overline{A_{pqp'q'}}]\le \frac{1}{n(n-1)}$，不失一般性，令$i=j=1,i'=j'=2$，定义$S_{ij}$为满足$\pi(1)=i,\pi(2)=j$且$\bigwedge_{j\in S}\overline{A_{pqp'q'}}$的排列集合，对于$\pi\in S_{12}$，将$\pi$中ij对应的位置与12互换，则也是$S_{ij}$中的一个排列，得$|S_{12}|\le S_{ij}$，counting得结论。$\Box$

# THE ALGORITHMIC ASPECT

本节内容太老，被moser算法吊打，gele

# Directed Cycles

令$D(V,E)$为简单有向图，最小出度为$\delta$，最大入度为$\Delta$。

**Theorem 1** 若$e(\Delta\delta+1)(1-1/k)^{\delta}<1$，则D包含一个简单有向圈，长度=0(mod k)

**Proof.** 考虑出度都是$\delta$的子图，对每个点随机k染色，定义$A_v$为事件v的邻居均不为$f(v)+1 (mod\ k)$，则$Pr[A_v]=(1-1/k)^\delta$。$A_v$相关的事件是与v和v的邻居相关的节点为$(\Delta+\delta+\Delta\delta)$?，不断走+1色的地方知道遇到重复，必然是k倍长度的圈。