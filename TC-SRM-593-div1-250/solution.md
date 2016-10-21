HexagonalBoard
==============

作者：袁宇韬

关键词：二分图

题目简述
--------

有一个$$n \times n$$的棋盘，每个格子与上、下、左、右、右上、左下六个格子
相邻。给定其中的一些格子，问最少用多少种颜色可以对这些格子染色且相邻的格
子颜色不同。

算法一
------

将坐标为$$(x, y)$$的格子染成颜色$$(x + y) \mod 3$$可以用最多三种颜色完成
染色。因此只要考虑能否用一种或两种颜色染色。

将需要染色的格子视为点，相邻的格子之间连边，则能用一种颜色染色的条件为图
的每个连通分量大小为1，能用最多两种颜色完成染色的条件为图是二分图。

时间复杂度$$O(n^2)$$。