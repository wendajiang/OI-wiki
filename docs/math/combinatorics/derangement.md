## 错位排列

### 定义

错位排列（derangement）是没有任何元素出现在其有序位置的排列。即，对于 $1\sim n$ 的排列 $P$，如果满足 $P_i\neq i$，则称 $P$ 是 $n$ 的错位排列。

例如，三元错位排列有 $\{2,3,1\}$ 和 $\{3,1,2\}$。四元错位排列有 $\{2,1,4,3\}$、$\{2,3,4,1\}$、$\{2,4,1,3\}$、$\{3,1,4,2\}$、$\{3,4,1,2\}$、$\{3,4,2,1\}$、$\{4,1,2,3\}$、$\{4,3,1,2\}$ 和 $\{4,3,2,1\}$。错位排列是没有不动点的排列，即没有长度为 1 的循环。

### 容斥原理的计算

全集 $U$ 即为 $1\sim n$ 的排列，$|U|=n!$；属性就是 $P_i\neq i$. 套用补集的公式，问题变成求 $\left|\bigcup_{i=1}^n\overline{S_i}\right|$.

可以知道，$\overline{S_i}$ 的含义是满足 $P_i=i$ 的排列的数量。用容斥原理把问题式子展开，需要对若干个特定的集合的交集求大小，即：

$$
\left|\bigcap_{i=1}^{k}S_{a_i}\right|
$$

其中省略了 $a_i<a_{i+1}$ 的条件以方便表示。上述 $k$ 个集合的交集表示有 $k$ 个变量满足 $P_{a_i}=a_i$ 的排列数，而剩下 $n-k$ 个数的位置任意，因此排列数：

$$
\left|\bigcap_{i=1}^{k}S_{a_i}\right|=(n-k)!
$$

那么选择 $k$ 个元素的方案数为 $C_n^k$，因此有：

$$
\begin{aligned}
\left|\bigcup_{i=1}^n\overline{S_i}\right|
&=\sum_{k=1}^n(-1)^{k-1}\sum_{a_{1,\cdots,k} }\left|\bigcap_{i=1}^{k}S_{a_i}\right|\\
&=\sum_{k=1}^n(-1)^{k-1}C_n^k(n-k)!\\
&=\sum_{k=1}^n(-1)^{k-1}\frac{n!}{k!}\\
&=n!\sum_{k=1}^n\frac{(-1)^{k-1} }{k!}
\end{aligned}
$$

因此 $n$ 的错位排列数为：

$$
D_n=n!-n!\sum_{k=1}^n\frac{(-1)^{k-1} }{k!}=n!\sum_{k=0}^n\frac{(-1)^k}{k!}
$$

错位排列数列的前几项为 $0,1,2,9,44,265$（[OEIS A000166](http://oeis.org/A000166)）。

### 递推的计算

把错位排列问题具体化，考虑这样一个问题：

$n$ 封不同的信，编号分别是 $1,2,3,4,5$，现在要把这五封信放在编号 $1,2,3,4,5$ 的信封中，要求信封的编号与信的编号不一样。问有多少种不同的放置方法？

假设考虑到第 $n$ 个信封，初始时暂时把第 $n$ 封信放在第 $n$ 个信封中，然后考虑两种情况的递推：

- 前面 $n-1$ 个信封全部装错；
- 前面 $n-1$ 个信封有一个没有装错其余全部装错。

对于第一种情况，前面 $n-1$ 个信封全部装错：因为前面 $n-1$ 个已经全部装错了，所以第 $n$ 封只需要与前面任一一个位置交换即可，总共有 $D_{n-1}\times (n-1)$ 种情况。

对于第二种情况，前面 $n-1$ 个信封有一个没有装错其余全部装错：考虑这种情况的目的在于，若 $n-1$ 个信封中如果有一个没装错，那么把那个没装错的与 $n$ 交换，即可得到一个全错位排列情况。

其他情况，不可能通过一次操作来把它变成一个长度为 $n$ 的错排。

于是可得，错位排列数满足递推关系：

$$
D_n=(n-1)(D_{n-1}+D_{n-2})
$$

这里也给出另一个递推关系：

$$
D_n=nD_{n-1}+{(-1)}^n
$$

### 其他关系

错位排列数有一个向下取整的简单表达式，增长速度与阶乘仅相差常数：

$$
D_n=\left\lfloor\frac{n!}{e}\right\rfloor
$$

随着元素数量的增加，形成错位排列的概率 P 接近：

$$
P=\lim_{n\to\infty}\frac{D_n}{n!}=\frac{1}{e}
$$
