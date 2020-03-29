# 题目：硬币面值为1、2、4、5，问n可以被兑换成硬币的最小数目？

我先用这道题解释下动态规划dp的两种方式，然后大家可以试试做下这类题目

# 朴素的递归
```
base_cases = [0, 1, 1, 2, 1, 1]

def count_coins(n):
    global base_cases
    if n <= 5:
        return base_cases[n]
    else:
        return min(count_coins(n-1), count_coins(n-2), count_coins(n-4), count_coins(n-5)) + 1
```
公式找对了，但是时间复杂度是指数级的，需要用dp降一下


# 自下而上的dp

```
def count_coins(n):
    coins = [0] * (max(n + 1), 6)
    coins[:6] = [0, 1, 1, 2, 1, 1]
	
    # coins数组每次算第i项时，i之前的项都记录好了，直接可以用
    for i in range(6, n + 1):
        coins[i] = min(coins[i-1], coins[i-2], coins[i-4], coins[i-5]) + 1
    return coins[n]
```
计算跟n的时候，对小于n的情况都算完了。所以事先把算过的结果都记录下，省得再次计算


# 自上而下的dp
```
mydict = {
	0: 0,
	1: 1,
	2: 1,
	3: 2,
	4: 1,
	5: 1,
}

def count_coins(n):
    global mydict
    # 首先看mydict里面有没有，有的话直接返回
    if n in mydict:
        return mydict[n]

    # 算完n相关的后，立马存入mydict中
    mydict[n] = min(count_coins(n-1), count_coins(n-2), count_coins(n-4), count_coins(n-5)) + 1

	return mydict[n]
```
这种方式也叫做记忆化搜索。每次算好的结果要存起来；每次调用前查看一下之前是否算过，如果计算过了，就直接返回之前记忆过的结果


# O(1)的算法
```
def count_coins(n):
    return base_cases[n % 20] + 4 * (n // 20)
```
O(1)的算法，是这样的。1、2、4、5的最小公倍数是20，所以每个20都用4个5来表示。小于20的都当base cases，预先算好
