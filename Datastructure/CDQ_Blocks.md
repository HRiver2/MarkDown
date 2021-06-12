# CDQ 分治

## 二元关系

有两个集合 $A$, $B$, 他们的笛卡尔积 $A \times B$ 是 $|A|\times|B|$ 个点对构成的集合, 即 $A$ 中的每个元素和 $B$ 中每个元素组成的有序点对.

定义 $A \times B$ 的一个子集 $R$, 则 $R$ 是 $A$ 和 $B$ 的一个二元关系.

## 偏序

偏序也是一种二元关系, 设一个定义在同一个集合 $A$ 中的二元关系 $R \in A \times A$, 满足以下性质:

- 自反性

  对于每个元素 $a \in A$ 有 $(a, a) \in R$.

- 反对称性

  如果存在 $(a, b) \in R$ 且 $(b, a) \in R$, 则 $a = b$.

- 传递性

  如果存在 $(a, b) \in R$ 且 $(b, c) \in R$, 则 $(a, c) \in R$.

则 $R$ 是一个偏序.

如果 $R$ 还满足:

- 完全性

  对于每一个 $a \in A$, $b \in A$, 一定有 $(a, b) \in R$ 或 $(b, a) \in R$.

则 $R$ 是一个全序.

一般我们说的偏序都是非严格偏序 (自反偏序), 但是与之相对, 有一种严格偏序 (反自反偏序), 严格偏序在满足传递性的基础上, 满足:

- 反自反性

  对于每个元素 $a \in A$ 不存在 $(a, a) \in R$.

- 禁对称性

  如果存在 $(a, b) \in R$ 则不存在 $(b, a) \in R$.

其实对于每个严格偏序中的点对, 在对应的非严格偏序中一定存在, 如果每个点对表示一条有向边, 则严格偏序一定对应一个 DAG, 而非严格偏序中会增加一些自环和重边.

算法竞赛中的题目, 一般偏序的要求是满足反自反性, 对称性和传递性.

## 二维偏序

如果有有序二元组 $(a, b)$ 构成的集合 $A$, 则一个有序二元组的有序点对 $R \in A \times A$ 就是一个二维偏序.

如果规定 $((a_i, b_i), (a_j, b_j)) \in R$, 当且仅当 $a_i \leq a_j$ 且 $b_i \leq b_j$, 求 $|R|$, 这就是一道很简单的二维偏序题.

很幸运, 二维偏序一般不需要 CDQ 分治, 只要对所有二元组按 $a$ 排序, 然后建立树状数组, 从第一个开始, 依次查询 $[1, b_i]$ 的 $b$ 的数量, 然后插入 $b_i$ 即可.

高端的食材, 往往只需要采用最朴素的烹饪方式.

但是, 我们使用同样高端的烹饪方式又有何不可?

尝试用 CDQ 分治解决二维偏序.

已经按 $a$ 排好序了, 将所有二元组分成左右两部分, $[1, Mid]$, $(Mid, n]$. 这时, 满足 $((a_i, b_i), (a_j, b_j)) \in R$ 的 $i$, $j$ 有三种情况:

- $i \in [1, Mid]$, $j \in (Mid, n]$

- $i \in [1, Mid]$, $j \in [1, Mid]$

- $i \in (Mid, n]$, $j \in (Mid, n]$

对于第一种情况, 可以用双指针 $O(n)$ 求出, 对于后两种, 可以递归解决, 总复杂度还是 $O(nlogn)$.

这种双指针 + 递归的分治思想是不是非常眼熟? 没错, 这就是归并排序的加强版.

## 三维偏序

同理, 如果有有序三元组 $(a, b, c)$ 构成的集合 $A$, 定义 $R \in A * A$, 当前仅当 $a_i \leq a_j$, $b_i \leq b_j$, $c_i \leq c_j$ 同时成立时, $((a_i, b_i, c_i), (a_j, b_j, c_j)) \in R$. 求 $|R|$.

很显然, 这是一道三维偏序题, 仍然是先按 $a$ 排序. 然后分成两部分, 还是存在那三种情况.

- $i \in [1, Mid]$, $j \in (Mid, n]$

- $i \in [1, Mid]$, $j \in [1, Mid]$

- $i \in (Mid, n]$, $j \in (Mid, n]$

仍然思考如何求出第一种情况数量. 因为已知 $a_i \leq a_j$, 所以相当于在 $A$ 的子集 $B$, $C$ (即左右两段的点代表的集合), 求二维偏序 $R \in B \times C$ 的 $|R|$.

参考二维偏序的做法, 对于左右两段分别按 $b$ 排序, 双指针 $i$, $j$ 扫描, 使得 $b_i = b_j$. 然后不断将左段的 $c_i$ 加入树状数组, 然后查询 $[1, c_j]$ 的数量, 统计答案, 然后递归求子问题.

参考前面 CDQ 分治求二维偏序, 发现三维偏序用 CDQ 转化来的二维偏序问题也可以用 CDQ 分治再来一层.