# GooseInZooDivOne
作者：叶珈宁

关键词：DFS 计数
## 题目简述
有一张$$n\times m$$的网格图，上面的每个格子要么是空的（用字符'.'表示），要么住着一只鸟（用字符'v'表示）。

每只鸟可能是鸭子也可能是鹅，已知：

1、距离任意一只鹅曼哈顿距离不超过$$dist$$的鸟都是鹅。

2、鹅至少有一只，且总数是偶数。

问有多少种不同的合法情况。

$$1\leq n,m\leq 50,0\leq dist\leq 100$$.

## 算法

可以把一只鸟和与它曼哈顿距离不超过$$dist$$的鸟放到同一个集合里。那么认定一只鸟是鹅就相当于认定这一整个集合的鸟是鹅。

统计出大小是奇数和大小是偶数的集合个数，设为$$a,b$$。那么奇数的集合必须选偶数个，偶数的集合可以选任意个，再减掉一只鹅都没有的情况。

当$$a=0$$时，答案是$$2^b-1$$，否则答案就是$$2^{a+b-1}-1$$。

现在需要解决的问题就只有统计出大小为奇数和偶数的集合各有几个，不妨先用$$\mathcal{O}(nm)$$的复杂度预处理出每个格子上方和下方第一只鸟的位置，然后暴力DFS每只没有处理过的鸟。只需要借助预处理出的信息，继续搜索每列相对于该行上方和下方离这只鸟最近的鸟就可以了。因为一个点不会被搜两次，复杂度$$\mathcal{O}(nm^2)$$。