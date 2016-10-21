#TheNumberGameDivOne
作者：翁文涛

关键词：博弈，打表，数学归纳法
##题目简述
现在John和Brus在玩一个有趣的游戏。一开始他们有一个正整数$$N$$，他们会轮流对这个数进行操作。每一回合，当前操作的人可以选择一个整数$$a$$，满足$$a \in (1,N)$$，且$$a | N$$，然后把$$N$$变成$$N-a$$，不能操作的人算输。现在John先手，给定$$N$$，问最终谁会取得胜利。
##数据范围
$$N \in [1,10^{18}]$$
##题解
设$$g[n]$$表示当数为$$n$$时，先手的胜利情况。若$$g[n]=1$$，表示先手必胜，若$$g[n]=0$$，表示后手必胜。那么有转移：
$$
g[n]=\left\{
\begin{aligned}
& 1，存在一个y|n且y\in(1,n)，使得g[n-y]=0\\
& 0，\mathrm{else}
\end{aligned}
\right.
$$
直接这样做显然是会超时的，但我们可以通过这个算法打表找规律，下面是一个$$n\in [1,100]$$对应的$$g[n]$$的表。
[部分g[n]的值][1]
  [1]: http://ideone.com/EhZul2
我们可以很轻易的发现下面的规律：
$$g[n]=0$$当且仅当$$[n为奇数] \lor [n=2^k,k为奇数]$$。接下来我们可以用数学归纳法进行证明。

首先，当$$n=1$$时，$$g[n]=0$$，命题成立。
接下来，设当且的$$n > 1$$，且对于任意$$N < n$$，命题成立，对$$n$$分类讨论，有：
1. $$n$$是质数，命题显然成立。
2. $$n$$为奇数且$$n$$不是质数。否则，设$$n = a \times b$$，$$a > 1,b>1$$，易得$$a,b$$均为奇数，且$$n-a=a\times (b-1)$$。因为$$a,b$$为奇数，所以$$b-1$$为偶数，且$$a \times (b-1)$$不为$$2^k$$，根据题设，有$$g[a \times (b-1)]$$恒为$$1$$，所以$$g[n] = 0$$。
3. $$n$$为偶数且$$n \not = 2^k,k \in \mathbb{Z}$$。那么设$$n = 2^k \times a,a > 1且a为奇数$$，$$n - a$$必为奇数，根据题设，有$$g[n-a]=0$$，所以$$g[n]=1$$。
4. $$n$$为偶数且$$n=2^k,k为偶数且k>0$$。那么$$2^{k-1}|n$$，且$$k-1$$为奇数，根据题设，$$g[2^k-2^{k-1}]=g[2^{k-1}]=0$$，所以$$g[n]=1$$。
5. $$n$$为偶数且$$n=2^k,k为奇数$$且$$k > 1$$。那么$$n$$的因子为$$\{2^p|p \in (0,k)\}$$，$$2^k-2^p=2^p \times (2^{k-p}-1)$$，显然$$2^{k-p}-1$$为奇数，且$$2^k-2^p$$为偶数，根据题设，有$$g[2^k-2^p]$$恒为$$1$$，所以$$g[n]=0$$。

综上，对于任意$$N \geq 1$$，命题成立。
得证。

所以，最后的算法是，判断$$n$$是否为奇数或是$$2^{奇数}$$，是则返回Brus必胜，否则John必胜。