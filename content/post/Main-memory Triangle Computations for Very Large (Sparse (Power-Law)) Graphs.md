---
title: "Main-memory Triangle Computations for Very Large (Sparse (Power-Law)) Graphs"
date: 2020-11-08T22:43:00+08:00
draft: false
tags: ["power law"]
---

本文处理稀疏图上的三角形查找、计数、按点计数问题。

## 最快计数算法

ayz-node-counting算法思路就是先计算有度小节点参与的所有三角形，把这些点剔除后剩下的部分进行矩阵乘法。

Theorem 2的证明比较简单，不过要基于同时有邻接表和邻接矩阵。结论时复杂度为$O(m^{1.41})$，比著名的那个定向算法好一点。它的好处是即使最坏有$O(m^{1.5})$个三角形，算法也不需要$O(m^{1.5})$的时间。坏处在于最坏情况下需要处理n*n的矩阵。

## 时间最优列举算法

这里由于需要列举，所以最好也只能$O(m^{1.5})$解决。

2. vertex-listing算法，对于某个点，判断它的邻居是否相邻。

3. edge-listing算法，对于某条边，查找他们的公共邻居。

4. tree-listing算法，对于每个联通分支，判断剩余边是否能与覆盖树构成三角形。

**复杂度分析**：考虑覆盖树最多多少个即可。

5. ayz-listing算法先vertex-listing计算有度小节点参与的所有三角形，把这些点剔除后进行edge-listing。

6. forward算法，acm里那个三角形计数算法。

**评注**：本算法的主要优势在于只需要邻接表，空间复杂度低。

7. compact-forward算法，这个算法与forward算法的不同在于不再记录定向后的边，而是直接对已有的邻接表排序。

### 新算法

注意到vertex-listing算法需要复杂度为$O(d^2(v))$，所以对于度大的节点效果不佳。

8. new-vertex-listing算法，直接穷举每条边，$O(1)$判断它的端点是否都是v的邻居。复杂度为$O(m)$
9. new-listing算法，大度点用new-vertex-listing，剩下的三角形用edge-listing。

## power law下的复杂度分析

这里是本文的出发点。
定义$p_k=k^{-\alpha+1}-(k+1)^{-\alpha+1}$为度数的分布

### 定理16

度数大于等于K的概率为$K^{-\alpha+1}$，则new-listing算法的复杂度为$O(nK^{-\alpha+1}m+mK)$，最小时$K=n^{\frac{1}{\alpha}}$。

compact-forward算法的核心在于穷举的节点数，注意到这个值同时被当前节点的度以及比当前度更大的节点数限制住。这两个值恰好趋势相反，所以最大值在两个相等时达到，即$K=nK^{-\alpha+1}$，得$K=n^{\frac{1}{\alpha}}$。