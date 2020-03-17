我先用这道题解释下动态规划dp的两种方式，然后大家可以试试做下这类题目

<img src="https://github.com/Chris0325/leetcode/blob/master/static/naive_recursion.png" width = "50%" />


这个是朴素的递归，递归的公式找对了，但是时间复杂度太高，指数级的。需要用dp降一下

<img src="https://github.com/Chris0325/leetcode/blob/master/static/dp_from_bottom.png" width = "50%" />

dp的第一种方式是自下而上。算跟n相关的时候，对小于n的情况都算完了，事先把结果都记录好，省得再次计算

第二种dp是自上而下，也叫做记忆化搜索。一般都用自下而上的就够了
<img src="https://github.com/Chris0325/leetcode/blob/master/static/dp_from_top.png" width = "50%" />


自上而下这种递归，每次算好的结果要存起来；每次调用前查看一下之前是否算过，如果计算过了，就直接返回之前记忆过的结果

这类题目容易上手哈，而且就这两种思路，基本不需要数据结构的知识[Smirk]

O(1)的算法，是这样的。1、2、4、5的最小公倍数是20，所以每个20都用4个5来表示。小于20的都当base cases，预先算好

<img src="https://github.com/Chris0325/leetcode/blob/master/static/greedy.png" width = "50%" />
