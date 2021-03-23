# 计划

## 前期

前期 (NOIp之前) 计划分为四个阶段

* 第一阶段对 NOIp 的知识点进行扫尾, 定于三月份.

* 第二阶段将 `进阶指南` 的内容学完, 并加以拓展, 定于四五月份.

* 第三阶段, 学习省选内容, 但是由于很难找到系统的教程. 借助大佬博客, 对每个研究方向进行专项学习, 定于六到九月.

* 第四阶段, 刷题训练, 以历届真题为主, 配以 CF 的思维训练, 定于十月到十二月.

### 第一阶段

* 第一周
将偏弱的数学部分集中学习, 达到 NOIp 的标准.

| 出处                                                     | 题目             | 知识点                  |
| -------------------------------------------------------- | ---------------- | ----------------------- |
| [P1403-AHOI2005](https://www.luogu.com.cn/problem/P1403) | 约数研究         | 基础数论                |
| [P3811](https://www.luogu.com.cn/problem/P3811)          | 乘法逆元         | 乘法逆元                |
| [P4549](https://www.luogu.com.cn/problem/P4549)          | 裴蜀定理         | 欧几里得算法(gcd)       |
| [P5656](https://www.luogu.com.cn/problem/P5656)          | 二元一次不定方程 | 扩展欧几里得算法(exgcd) |
| [P1082](https://www.luogu.com.cn/problem/P1082)          | 同余方程         | 扩展欧几里得算法(exgcd) |
| [P5091](https://www.luogu.com.cn/problem/P5091)          | 扩展欧拉定理     | 扩展欧拉定理, 快速幂    |
| [P3807](https://www.luogu.com.cn/problem/P3807)          | 卢卡斯定理       | 卢卡斯定理, 组合数学    |
___

* 第二周
动态规划 (DP) 的巩固和加深, 内容是: 期望 DP, 基环树 DP, 树上 DP, 斜率优化, 四边形不等式优化.

| 出处                                                                                                     | 题目     | 知识点                         |
| -------------------------------------------------------------------------------------------------------- | -------- | ------------------------------ |
| [P3195-HNOI2008](https://www.luogu.com.cn/problem/P3195)                                                 | 玩具装箱 | 斜率优化                       |
| [P2365](https://www.luogu.com.cn/problem/P2365)&[P5785-SDOI2012](https://www.luogu.com.cn/problem/P5785) | 任务安排 | 斜率优化, 二分查找             |
| [P2120-ZJOI2007](https://www.luogu.com.cn/problem/P2120)                                                 | 仓库建设 | 斜率优化                       |
| [P1912-NOI2009](https://www.luogu.com.cn/problem/P1912)                                                  | 诗人小G  | 四边形不等式, 字符串, 二分查找 |
| [P4767-IOI2000](https://www.luogu.com.cn/problem/P4767)                                                  | 邮局     | 四边形不等式                   |

___

* 第三周
图论, 字符串的巩固和加深, 内容是: 双连通分量,  求 LCA 的 Tarjan, KMP


| 出处                                            | 题目          | 知识点  |
| ----------------------------------------------- | ------------- | ------- |
| [P3375](https://www.luogu.com.cn/problem/P3375) | KMP字符串匹配 | KMP算法 |


___

### 第二阶段

* 第 $1-2$ 周
数据结构进阶, 包括数据结构持久化, 边带权/扩展域并查集, CDQ 分治, 莫队算法.

* 第 $3-4$ 周
图论和搜索, $k$ 短路, 二分图, 启发式搜索 ($A^*, IDA^*$), 差分约束, 负环(SPFA).

* 第 $5-6$ 周
DP, 计数 DP, 图论相关 DP (换根树形 DP, DAG 上的 DP), 后效性处理 (高斯消元).

* 第 $7-8$ 周
数学, 基础数论, 组合数, 简单容斥, 莫比乌斯函数, $0/1$ 分数规划, 博弈论.

### 第三阶段

* 六月
由于期末考试, 所以时间相对较短. 所以对非常规题型进行适应性学习, 如: 提交答案题, 交互题, 通信题, 构造题, 大模拟.
附加 `C++` 语法相关

* 七月
不考虑学考的问题, 进行数据结构 + 字符串 + 搜索的学习. 内容包括: 左偏树(可并堆), 树链剖分, LCT, KD-Tree, 树套树, 莫队进阶, 红黑树, SBT, 珂朵莉树, zkw线段树, 笛卡尔树, 李超线段树, 树上启发式合并, 点分治, 析合树; AC 自动机, 后缀自动机, 序列自动机, 后缀树和后缀数组, 回文树, Manacher, 最小表示, Lyndon 分解, EXKMP, Boyer-Moore 算法; Dancing Links.

* 八月
DP + 图论, 上下界最大流, 费用流, ISAP/当前弧优化的Dinic, 斯坦纳树, 虚树, 矩阵树定理, 最小树形图, 生成树相关(次小生成树, 最短路径生成树, 最小直径生成树, 最优比率生成树), 最短路相关(乘积最短路, 加和最短路, 同余最短路), 圆方树, Prufer 序列, LGV 引理, 弦图; 插头 DP, WQS 优化, CDQ 分治优化 (DP重在练习).

* 九月
数学, 多项式相关 (快速傅里叶变换(FFT), 快速数论变换(NTT), 快速沃尔什变换(FWT), 拉格朗日插值, 多项式除法, 多项式求逆, 多项式开根, 多项式求对数, 多项式快速幂, 多项式指数函数), 牛顿迭代, 生成函数(数学), 线性代数, 线性规划, 组合数学进阶, 容斥原理, 博弈论, 群论, 数列, 高等数学, 计算几何(半平面交, 凸包, 旋转卡壳), 数论(原根, 筛法(杜教筛, Min_25筛, 洲阁筛), 反演相关(多项式反演, 莫比乌斯反演等), 素数, 整除与同余).

## 中期(如果有的话)

中期 (NOIp-省选), 大概从一月到四月, 包括NOIp, WC, 省选三个时间节点, 对前面所学内容进行集中刷题巩固.

## 后期(如果有的话)

后期 (省选-NOI), 大致从五月到七月, 这段时间, 会有一些国际性比赛, 如: APIO, THU-PC, IOI, USACO 等, 加以各大网站的网赛练习, 充分练习比赛技巧.
