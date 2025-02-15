---
title: "Chapter13"
date: 2019-06-24T00:15:52+08:00
draft: false
tags: ["data structure","splay","working set","LCT","gele"]
---

# Splay trees

对于m个操作的序列，splay运行时间为$O(m\log n)$，所以均摊时间为$O(n)$。可以用来处理linking cutting trees，并且rebalance操作比平衡树简单很多。~~又是tarjan~~

## 复杂度分析

zig、zag是单旋（最多发生一次），zigzig、zagzag是父亲及父亲的父亲在同侧，zigzag、zagzig是父亲及父亲的父亲在异侧，直至将x转到根，这个操作称为splay(x)，这个操作均摊复杂度为$O(log n)$。

w(x)是x的权重，size(x)是以x为根的子树的点权重和，rank(x)是$\log\_2(size(x))$，Potential(T)=$\alpha\sum\_{x\in T}rand(x)$。均摊时间=实际时间+新Potential-老Potential。splay的运行时间为$\beta\times$Number of rotations。其中$w(x)\ge 0,\ \alpha\ge\beta>0$为任意给定值。

将splay的旋转按上面分的三种旋转进行逐个分析，累加得，将对根为t的树进行splay(x)的均摊时间为$3\alpha(rank(t)-rank(x))+\beta=O(\log\frac{size(t)}{size(x)})$。

令$w(x)=\frac{1}{n}$，$\alpha=\beta=1$，则单次splay的均摊时间为$3\log n+1$，Potential的总变化最多为$O(n\log n)$，则进行m次splay操作的均摊时间是$O(3m\log n + m)$，得实际时间为$O(3m\log n + m)+n\log n=O((m+n)\log n)$。

以下这几个操作的定义与12章treap中的定义完全一致。

**查找**：按照BST查找，若成功找到，则对找到的点进行一次splay，否则对发现失败的点的父亲进行splay。

**插入**：用BST的查找找到叶子节点，未找到则对叶子splay，否则插在这个叶子的子树上，然后对其splay（这里与论文中的插入不同）。

**合并**：在t1里查找正无穷，则最大的点变成了t1的根，让t2变成t1的右子树。

**分裂**：调用查找x的过程，判断根与x的大小关系分开根和它的左或右子树。

**删除**：调用查找的过程，若找到，则因为查找最后调用了splay，所以根为待删除的节点，将根的左右子树进行合并即可。

书中的分析缺少这是势能定义，还是按论文里来。对于m个操作的序列，定义Potential所有树的Potential的和操作前不在树中的数的w和，然后对每种操作都类似splay可以分析出一个均摊的时间（基本上是splay的均摊时间+不同操作导致的势能变化），Potential的总变化最多为$O(n\log n)$，将它们累加得总时间为$O((m+n)\log n)$。

## 静态最优

上面的分析只是基于$w(x)=\frac{1}{n}$得出的，若定义$q(i)$为i被查询的次数（直接或间接），定义$w(x)=\frac{q(i)}{\sum q(i)}$，得splay均摊时间$-3rank(x)+1=O(1+\log\frac{\sum q(x)}{q(x)})$，求和得$O(\sum q(x)+\sum q(x)\log\frac{\sum q(x)}{q(x)})$，Potential最大变化为$O(\sum\log\frac{\sum q(x)}{q(x)})$，由于$m=\sum q(x)$，所以总时间为$O(m+\sum q(x)\log\frac{m}{q(x)})$，这是二叉搜索树的最优结果。类似的思路可以处理finger search，可证明它比finger search tree更好。

working set property：若只有t个元素被查询，查询的时间是$O(\log t)$，若$i$的两次访问之间间隔了$t$个不同的数，则i的第二次查询时间为$O(\log(t+1))$，这里主要用到了一个权重重排的思想，首先给定一个权重，第i个首次出现元素权重设为$\frac{1}{i^2}$，当某个元素被查询时，将它的权重变为1，比他大的权重都相应的向后挪一位（相当于循环调整），这样的重拍只会Potential变小，最终时间=均摊时间+老Potential-新Potential，得类似上面的分析算出的时间只会比真实之间更大。~~这也太狠了~~

附一篇文章Alternatives to splay trees with O(log n) worst-case access times,John Iacono

splay由于w函数可以具体设定，所以它被推测可能是动态最优的，即对于任意的序列，它都可以和最好的动态二叉搜索树一样。以被证明splay树有类似finger search的性质，搜索接近的目标很快。

## LCT