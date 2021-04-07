# 倍增求后缀数组 (Suffix Array)

定义一个字符串第 $i$ 个字符为起点的后缀为 $Suff_i$. 将一个字符串的所有后缀按字典序升序排序, 后缀数组 $SA_i$ 表示排第 $i$ 个的后缀的起点位置.

## 朴素

将所有后缀枚举出来, 字符不足的用空字符补全, 重载字符串比较运算符, 快速排序. 一次比较时间复杂度是字符串长度, 也就是 $O(n)$, 对 $n$ 个字符串进行快排需要 $O(nlogn)$ 次比较, 所以复杂度是 $O(n^2logn)$. 对字符串和首字符位置的二元组排序, 排序完可以直接得到 $SA$.

## 桶排序 (Bucket Sort)

假设 $n$ 个整数, 值域是 $[0, N]$, 这时开一个 $O(N)$ 的数组 $b$ 记录每个数出现的次数, 记录前缀和 $sumb$, 可以 $O(1)$ 求出任意数字排好序后的位置.

这时 $sumb_i$ 的右边界应当是开区间, 也就是说 $sumb_i = \displaystyle{\sum_{i = 0}^{n - 1} b_i}$, 表示比 $i$ 小的元素的个数. 那么 $i$ 在排好序的数组中下标应当是 $sumb_i + 1$

建一个临时数组 $Tmp$, 枚举待排序数组 $a$, 将 $a_i$ 放到 $Tmp_{sumb_{a_i} + 1}$, 并且把 $sumb_{a_i}$ 加上 $1$, 因为下一个和 $a_i$ 相等的数字应该放到 $a_i$ 新位置的后面而不是放到 $a_i$ 的新位置.

相当于在 $Tmp$ 中维护了 $N$ 个栈 (有的是空栈), 每个栈的栈底就是 $sumb_i + 1$, 每次将 $a_i$ 压入第 $a_i$ 个栈里, 排完序后相邻的栈首尾相接, 便得到了排好序的数组.

最后将排好序的数组从 $Tmp$ 中倒回 $a$ 里.

时空复杂度 $O(n + N)$

## 基数排序 (Radix Sort)

在 $N$ 很大的时候, 桶排序的时空效率都会降到很差的水平. 对于 $n$ 个整数, 有一种排序方式可以将时间复杂度优化到 $O(nlog_wN)$, $log_wN$ 是 $w$ 进制下, $n$ 个数中最长的数. 这就是基数排序, 它的空间复杂度为 $O(n + w)$, 时间复杂度时 $O(nlog_wN)$, 可以在 $w$ 选取合适的情况下将 $log_wN$ 视为常数, 实现线性复杂度排序, 做到基于比较的排序方式达不到的效率.

它的做法是将先将整数表示成 $w$ 进制, 然后从低到高, 对每一位进行排序.

按最低位为关键字进行桶排序后, 按第二位为关键字桶排序时, 这时待排序数组已经按第一位排好序了, 所以在往 $w$ 个栈里压的时候, 同一个栈里, 第一位小的数一定在第一位大的数之前入栈. 也就是说, 第二次桶排序后, 每个栈里的数字, 第二位相同, 第一位递增.

假设现在排序的是第 $i$ 位, 这时原数组已经以最低的 $i - 1$ 位为关键字排好序了. 将待排序的数按第 $i$ 位为关键字桶排序, 按原数组的顺序压入对应的栈, 每个栈中第 $i$ 位相同, $[1, i)$ 位递增, $w$ 个栈在数组中按共同的第 $i$ 位递增, 所以排序完后数组中的数 $[1, i]$ 位递增.

因为对 $n$ 个数的第 $i$ 位的一次桶排序是 $O(n)$, 一共有 $O(log_wN)$ 位, 所以总时间是 $O(nlog_wN)$, 近似地看成 $O(n)$.

上面说的是 LSD (Least significant digital) 基数排序的原理, 即从低位到高位的排序. 还有 MSD (Most significant digital) 的版本, 即从高位到低位, 二者有常数差距, 但原理相同.

## 倍增

对于字符串的排序, 相当于一些大整数排序, 这时如果直接用基数排序, 取构成字符串的字符集为底数 $w$, 时间复杂度为 $O(n^2)$, 貌似没有快多少. 这时就要利用这些字符串都是同一个母串的后缀的性质了.

我们在以第一个字符为关键字桶排序后, 每个后缀的首字符的大小关系就已经确定了, 而第 $Suff_i$ 的第二个字符就是 $Suff_{i + 1}$ 的首字符, 也就是说, 每个字符的相对大小就确定了.

接下来考虑倍增, 首先考虑在已经对所有后缀以它们的前 $d$ 位组成的前缀为关键字排序后, 如何 $O(1)$ 地确定每个后缀按 $[d + 1, 2d]$ 的区间为关键字排序后的相对顺序. 假设每个后缀的前 $d$ 位次序是 $RK_i$, 则很容易得到这个后缀 $[d + 1, 2d]$ 相对次序是 $RK_{i + d}$.

接下来, 要想将得到按前 $2d$ 位排序的 $n$ 个后缀, 只要按 $RK_i$ 为第一关键字, $RK_{i + d}$ 为第二关键字排序即可 ($i + d > n$ 的视为 $0$). 相当于关键字是 $n$ 进制的两位数的基数排序 (进制为 $n$ 是因为到最后一共会出现 $O(n)$ 种不同的键值), 时间复杂度 $O(n)$.

要排序的次数是 $O(log_2n)$ 次, 因为每轮排序 $d$ 倍增一次, 因次总复杂度 $O(nlog_2n)$ 

## 实现

模板: [luogu3809](https://www.luogu.com.cn/problem/P3809)

首先是字符串处理, 因为字符集是大小写字母和数字, 所以一共是 $62$ 个字符, 将输入的字符串离散化成整数数列, 并且将本来下标从 $0$ 开始的字符串转化成题目中下标从 $1$ 开始的字符串.

输入 $\&$ 预处理

```cpp
cin.getline(Inch, 1000001);
n = strlen(Inch);
for (register unsigned i(0); i < n; ++i) {
  if(Inch[i] <= '9' && Inch[i] >= '0') {
    Inch[i] -= 47;
    continue;
  }
  if(Inch[i] <= 'Z' && Inch[i] >= 'A') {
    Inch[i] -= 53;
    continue;
  }
  if(Inch[i] <= 'z' && Inch[i] >= 'a') {
    Inch[i] -= 59;
    continue;
  }
}
for (register unsigned i(0); i < n; ++i) {
  Bucket[Inch[i]] = 1;
}
for (register unsigned i(0); i < 64; ++i) {
  if(Bucket[i]) {
    Tmpch[i] = ++Cnt;                               // 让桶从 1 开始, 空出 0 的位置
    Bucket[i] = 0;
  }
}
for (register unsigned i(0); i < n; ++i) {          // 将字符串离散化成整数序列
    S[i + 1].RK = Tmpch[Inch[i]];                   // 字符串读入是 [0, n) 的, 题意中字符串是 (0, n] 的 
}
```

接下来就是倍增了, 外层循环枚举当前倍增的阶段, 即最后一次排序的关键字长度. 每次预处理好本次基数排序的第二关键字, 然后基数排序.

```cpp
for (register unsigned i(1); i <= n; i <<= 1) {     // 当前按前 i 个字符排完了, 每次 i 倍增
  for (register unsigned j(1); j + i <= n; ++j) {   // 针对第二关键字不为 0 的 
    S[j].SubRK = S[j + i].RK;
  }
  for (register unsigned j(n - i + 1); j <= n; ++j) {  
    S[j].SubRK = 0;                                 // 第二关键字为 0 
  }
  RadixSort();
}
```

最后统计答案, 利用 $RK$ 数组, $O(n)$ 地求出 $SA$, 输出.

```cpp
for (register unsigned i(1); i <= n; ++i) {
  b[S[i].RK] = i;
}
for (register unsigned i(1); i <= n; ++i) {
  printf("%u ", b[i]);
}
```

下面来看看 `RadixSort` 的实现

这里用的是 LSD 基数排序, 即先按第二关键字 $SubRK$ 桶排序, 再按第一关键字 $RK$ 排一遍. 由于字符串的位置交换复杂度不是 $O(1)$ 而是 $O(n)$, 所以我们针对下标排序. 将一个后缀分成两部分, 键和卫星数据. 按下标数组访问到键, 用键做关键字排序下标, 用排好序的下标更新键, 不管卫星数据.

更多细节参见代码注释.

```cpp
void RadixSort () {
  unsigned MX(0);                                     // 记录最大键值 
  for (register unsigned i(1); i <= n; ++i) {
    ++Bucket[S[i].SubRK];                             // 第二关键字入桶
    MX = max(S[i].SubRK, MX);
  }
  sumBucket[0] = 0;
  for (register unsigned i(1); i <= MX; ++i) {        // 求前缀和以确定在排序后的序列中的位置
    sumBucket[i] = sumBucket[i - 1] + Bucket[i - 1];  // 求桶前缀和, 前缀和右边界是开区间, 所以计算的是比这个键值小的所有元素个数 
    Bucket[i - 1] = 0;                                // 清空桶 
  }
  Bucket[MX] = 0;
  for (register unsigned i(1); i <= n; ++i) {         // 排好的下标存到 b 中, 即 b[i] 为第 i 小的后缀编号 
    b[++sumBucket[S[i].SubRK]] = i;                   // 前缀和自增是因为 
  }
  b[0] = 0;                                           // 边界 (第 0 小的不存在) 
  for (register unsigned i(1); i <= n; ++i) {
    a[i] = b[i];
  }
  MX = 0; 
  for (register unsigned i(1); i <= n; ++i) {
    ++Bucket[S[i].RK];                                // 第一关键字入桶
    MX = max(S[i].RK, MX);
  }
  sumBucket[0] = 0;
  for (register unsigned i(1); i <= MX; ++i) {
    sumBucket[i] = sumBucket[i - 1] + Bucket[i - 1];
    Bucket[i - 1] = 0;
  }
  Bucket[MX] = 0;
  for (register unsigned i(1); i <= n; ++i) {
    b[++sumBucket[S[a[i]].RK]] = a[i];                // 由于 a[i] 是 b[i] 的拷贝, 表示第 i 小的后缀编号, 所以枚举 i 一定是从最小的后缀开始填入新意义下的 b 
  }
  b[0] = 0;
  Cnt = 0;                                            // 使 RK 不那么分散 
  for (register unsigned i(1); i <= n; ++i) {
    if(S[b[i]].SubRK != S[b[i - 1]].SubRK || S[b[i]].RK != S[b[i - 1]].RK) {
      a[b[i]] = ++Cnt;                                // 第 i 小的后缀和第 i - 1 小的后缀不等排名不等 
    }
    else {
      a[b[i]] = Cnt;                                  // 第 i 小的后缀和第 i - 1 小的后缀相等排名也相等 
    }
  }
  for (register unsigned i(1); i <= n; ++i) {
    S[i].RK = a[i];                                   // 将 a 中暂存的新次序拷贝回来 
  }
  return;
}
```

## 反向优化

一开始没考虑下标从 $0$ 开始还是从 $1$ 开始, 所以直接按 $0$ 开始做, 输出时下标加 $1$.

由于看这个细节不爽, 所以就将原字符串预处理成 $1$ 开始的了, 没想到总运行时间从 $2.91s$ 优化到了 $3.48s$.

思考跑得慢的原因, 发现当排序后的 $RK$ 重复程度大的时候, 大小为 $n$ 的桶里面大部分都是 $0$, 所以会导致大量无效枚举. 将关键字值域压到最小, 即更新 $RK$ 的时候用一个计数器, 仅区分每个 $RK$ 的大小关系用于做排序的关键字.

然后将程序从 $3.48s$ 优化到 $3.63s$

$$
\bold{工程奇迹}
$$

所以以后只要 AC 了就别瞎优化, 否则你也能创造奇迹......
