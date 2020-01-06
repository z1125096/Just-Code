<span id = "00"></span>
## 一维		
 - [70. Climbing Stairs](#70-climbing-stairs)
 - [53. Maximum Subarray](#53-maximum-subarray)
 - [62. Unique Paths](#62-unique-paths)
 - [63. Unique Paths II](#63-unique-paths-ii)
 - [120. Triangle	很少考](#120-triangle)
 - [279. Perfect Squares](#279-perfect-squares)
 - [139. Word Break](#139-word-break)
 - [375. Guess Number Higher or Lower II](#375-guess-number-higher-or-lower-ii)
 - [312. Burst Balloons](#312-burst-balloons)
 - [322. Coin Change](#322-coin-change)
## 股票最大利润问题
 - [121. Best Time to Buy and Sell Stock](#121-best-time-to-buy-and-sell-stock)
 - [122. Best Time to Buy and Sell Stock II](#122-best-time-to-buy-and-sell-stock-ii)
 - [123. Best Time to Buy and Sell Stock III](#123-best-time-to-buy-and-sell-stock-iii)
 - [188	Best Time to Buy and Sell Stock IV]
 - [309	Best Time to Buy and Sell Stock with Cooldown]
## 二维		
 - [256	Paint House] **?**
 - [265	Paint House II] **?**
 - [64. Minimum Path Sum](#64-minimum-path-sum)
 - [72. Edit Distance](#72-edit-distance)
 - [300. Longest Increasing Subsequence](#300-longest-increasing-subsequence)
 - [1143. Longest Common Subsequence](#1143-longest-common-subsequence)
 - [97. Interleaving String](#97-interleaving-string)
 - [174	Dungeon Game]
 - [221. Maximal Square](#221-maximal-square)
 - [85	Maximal Rectangle]
 - [363	Max Sum of Rectangle No Larger Than K]
## 化简		
 - [198. House Robber](#198-house-robber)
 - [213. House Robber II](#213-house-robber-ii)
 - [276	Paint Fence]
 - [91. Decode Ways](#91-decode-ways)
 - [10. Regular Expression Matching](#10-regular-expression-matching)
 - [44. Wildcard Matching](#44-wildcard-matching)

## 70. Climbing Stairs

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

你正在爬楼梯。它需要n步才能达到顶峰。

每次你可以爬1或2步。您可以通过多少不同的方式登顶？

注意：给定n将是一个正整数。

**Example**

```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

---

### Python Solution
**分析：** 从简单到难理解动态规划，即利用前面的子问题的解求得后面问题的解。不递归调用，而只是存储子问题解并且通过状态转移来解决。

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n
        dp = [0] * n
        dp[0], dp[1] = 1, 2
        for i in range(2,n):
            dp[i] = dp[i - 1] + dp[i- 2]
        return dp[-1]
```

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        a, b = 1, 0
        for _ in range(n + 1):
            a, b = a + b, a
        return b
```

[返回目录](#00)

## 53. Maximum Subarray

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

给定一个整数数组nums，找到具有最大总和的连续子数组（至少包含一个数字）并返回其总和。

**Example**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

---

### Python Solution
**分析：** 动态规划做法及其优化。实际上用 best 存储当前 dp 的最大值， curr 存储 dp[i]。

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = [0 for _ in range(len(nums))]
        dp[0] = nums[0]
        for i in range(1, len(nums)):
            dp[i] = max(dp[i-1]+nums[i], nums[i])
        return max(dp)
```

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        best = curr = nums[0]
        for i in range(1, len(nums)):
            curr = max(nums[i], curr + nums[i])
            best = max(best, curr)
        return best
```

[返回目录](#00)

## 62. Unique Paths

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

机器人位于 m x n 矩阵的左上角（在下图中标记为“开始”）。 机器人只能在任何时间点上下移动。 机器人试图到达网格的右下角（在下图中标记为“完成”）。 有多少种可能的独特路径？

**Example**

```
Example 1:
Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right

Example 2:

Input: m = 7, n = 3
Output: 28
```

---

### Python Solution
**分析：**

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1 for _ in range(n)] for _ in range(m)]
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]

        return dp[-1][-1]
```

**可简化为一维**

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [1 for _ in range(n)]
        for i in range(1, m):
            for j in range(1, n):
                dp[j] = dp[j] + dp[j-1]
        return dp[-1]
```

**数学方法**

```python
from math import factorial

class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        return int(factorial(n+m-2) / (factorial(n-1) * factorial(m-1)))
```

[返回目录](#00)

## 63. Unique Paths II

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

机器人位于m x n网格的左上角（在下图中标记为“开始”）。 机器人只能在任何时间点上下移动。 机器人试图到达网格的右下角（在下图中标记为“完成”）。 现在考虑是否在网格中添加了一些障碍。 会有多少条独特的路径？ 障碍物和空白区域在网格中分别标记为1和0。

**Example**

```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

---

### Python Solution
**分析：**

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if not obstacleGrid or not obstacleGrid[0]:
            return 0
        if obstacleGrid[0][0] == 1 or obstacleGrid[-1][-1] == 1:
            return 0
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        dp = [[0 for x in range(n)] for y in range(m)]
        #dp = [[0] * n] * m    和上一行的区别为这一行实际上是浅拷贝。非常不安全。
        i = j = 0
        while i < m and obstacleGrid[i][0] == 0:
                dp[i][0] = 1
                i += 1
        while j < n and obstacleGrid[0][j] == 0:
                dp[0][j] = 1
                j += 1
        for i in range(1, m):
            for j in range(1, n):
                if obstacleGrid[i][j] == 1:
                    dp[i][j] = 0
                else:
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        return dp[-1][-1]
```

**可简化为一维**

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if not obstacleGrid or not obstacleGrid[0]:
            return 0
        if obstacleGrid[0][0] == 1 or obstacleGrid[-1][-1] == 1:
            return 0
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        dp = [0 for _ in range(n)]
        dp[0] = 1
        for i in range(m):
            if obstacleGrid[i][0] == 1:
                dp[0] = 0
            for j in range(1, n):
                if obstacleGrid[i][j] == 0:
                    dp[j] = dp[j] + dp[j - 1]
                else:
                    dp[j] = 0
        return dp[-1]
```

[返回目录](#00)

## 120. Triangle

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

给定一个三角形，找到从上到下的最小路径总和。您可以将每一步移至下面一行中的相邻数字。

**Example**

```
For example, given the following triangle

[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).
```

---

### Python Solution
**分析：** 从低向上找到更小的值合并到最开始的一个元素。

```python
class Solution(object):
    def minimumTotal(self, triangle):
        dp = triangle[-1][:]
        for i in range(len(triangle)-2, -1, -1):
            for j in range(i+1):
                dp[j] = min(dp[j], dp[j+1]) + triangle[i][j]
        return dp[0]
```

**写成一行的形式：**

```python
class Solution(object):
    def minimumTotal(self, triangle):
        return reduce(lambda a, b:[min(a[i], a[i+1])+n for i, n in enumerate(b)], triangle[::-1])[0]
```

[返回目录](#00)

## 279. Perfect Squares

Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

给定一个正整数n，求和为n的最小平方数（例如1、4、9、16，...）。

**Example**

```
Example 1:

Input: n = 12
Output: 3
Explanation: 12 = 4 + 4 + 4.
Example 2:

Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

---

### Python Solution
**分析：**  DP 解法。

```python
class Solution(object):
    _dp = [0]
    def numSquares(self, n):
        dp = self._dp
        while len(dp) <= n:   # 下面这句话的意思是求出所以能加一个平方数（即一个操作）到目前位置的dp[?]。
            dp += min(dp[-i*i] for i in range(1, int(len(dp)**0.5+1))) + 1,
        return dp[n]
```

[返回目录](#00)

## 139. Word Break

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

Note:

The same word in the dictionary may be reused multiple times in the segmentation.
You may assume the dictionary does not contain duplicate words.

给定一个非空字符串s和包含非空单词列表的字典wordDict，请确定s是否可以分段为一个或多个字典单词的以空格分隔的序列。

注意：

字典中的同一单词在细分中可能会重复使用多次。 您可能会认为词典中没有重复的单词。

**Example**

```
Example 1:

Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
Example 2:

Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
Example 3:

Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```

---

### Python Solution
**分析：** 两种解法，一种是逐个遍历，True表示可以到达这个地方，一直推导到最后一个,之所以是 len(s)+1 是因为最后一位必须要取到。另一种是递归的做法。

```python
class Solution:
    def wordBreak(self, s, words):
        ok = [True]
        max_len = max(map(len,words+['']))
        words = set(words)
        for i in range(1, len(s)+1):
            ok += any(ok[j] and s[j:i] in words for j in range(max(0, i-max_len),i)),
        return ok[-1]
```

```python
class Solution:    # 效率很高!
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dic = dict()
        def helper(s):
            if not s: return True
            elif s in dic:
              return dic[s]
            else:
              dic[s]=any(helper(s[len(w):]) for w in wordDict if s.startswith(w))
              return dic[s]
        return helper(s)
```

[返回目录](#00)

## 375. Guess Number Higher or Lower II

We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number I picked is higher or lower.

However, when you guess a particular number x, and you guess wrong, you pay $x. You win the game when you guess the number I picked.

我们正在玩猜猜游戏。 游戏如下：我选择一个从1到n的数字。 您必须猜测我选了哪个号码。 每次您猜错了，我都会告诉您我选的数字是高还是低。 但是，当您猜一个特定的数字x时，如果您猜错了，您需要支付$ x。 当您猜到我选的号码时，您就赢得了比赛。

**Example**

```
n = 10, I pick 8.

First round:  You guess 5, I tell you that it's higher. You pay $5.
Second round: You guess 7, I tell you that it's higher. You pay $7.
Third round:  You guess 9, I tell you that it's lower. You pay $9.

Game over. 8 is the number I picked.

You end up paying $5 + $7 + $9 = $21.
```

---

### Python Solution
**分析：** 一种是自下向上的带备忘录的动态规划，一种是递归的做法。

```python
class Solution(object):
    def getMoneyAmount(self, n):
        need = [[0] * (n+1) for _ in range(n+1)]
        for lo in range(n, 0, -1):
            for hi in range(lo+1, n+1):
                need[lo][hi] = min(x + max(need[lo][x-1], need[x+1][hi])
                                   for x in range(lo, hi))
        return need[1][n]
```

```python
class Solution(object):
    def getMoneyAmount(self, n):
        def play(l = 1, h = n, dp = {}):
            if l >= h: return 0
            if (l, h) not in dp:
                dp[(l, h)] = min(g + max(play(l, g - 1, dp), play(g + 1, h, dp)) for g in range((l + h) / 2, h))
            return dp[(l, h)]

        return play()
```

[返回目录](#00)

## 312. Burst Balloons

Given n balloons, indexed from 0 to n-1. Each balloon is painted with a number on it represented by array nums. You are asked to burst all the balloons. If the you burst balloon i you will get nums[left] * nums[i] * nums[right] coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

给定n个气球，索引从0到n-1。 每个气球上都涂有一个数字，该数字由数组num表示。 要求您爆破所有气球。 如果您爆破气球i，您将获得nums [left] * nums [i] * nums [right]个硬币。 这里的左和右是i的相邻索引。 爆破后，左右会相邻。 明智地爆破气球，找到可以收集的最大硬币数。

**Example**

```
Input: [3,1,5,8]
Output: 167
Explanation: nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
             coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
```

---

### Python Solution
**分析：** 这道题没搞懂，感觉和暴力一样，头大。

```python
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        nums = [1] + [x for x in nums if x > 0] + [1]
        n = len(nums)
        dp = [[0] * n for _ in range(n)]
        for j in range(1, n):
            for i in range(j - 2, -1, -1):
                ans = 0
                for mid in range(i + 1, j):
                    tmp = nums[i] * nums[mid] * nums[j] + dp[i][mid] + dp[mid][j]       
                    if tmp > ans: ans = tmp
                dp[i][j] = ans
        return dp[0][n - 1]
```

[返回目录](#00)

## 322. Coin Change

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

系统会为您提供不同面额的硬币和总金额。 编写一个函数来计算组成该数量所需的最少数量的硬币。 如果这笔钱不能用硬币的任何组合来弥补，请返回-1。

**Example**

```
Example 1:

Input: coins = [1, 2, 5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

Example 2:

Input: coins = [2], amount = 3
Output: -1
```

---

### Python Solution
**分析：** 经典的换零钱问题，需要着重掌握。

```python
class Solution:
    def coinChange(self, coins, amt):
        def do(count, have, i, res):
            coin = coins[i]
            if count - (have - amt) // coin >= res:
                return res
            need = amt-have
            if need % coin is 0:
                x = count + need//coin
                return x if x < res else res
            if i is 0:
                return res
            for j in range(need // coin, -1, -1):
                sub = do(count+j, have+coin*j, i-1, res)
                if sub < res:
                    res = sub
            return res

        coins.sort()
        ret = do(0, 0, len(coins)-1, amt+1)
        return -1 if ret == amt+1 else ret
```

```python
class Solution:
    def coinChange(self, coins, amount):
        MAX = float('inf')
        dp = [0] + [MAX] * amount

        for i in range(1, amount + 1):
            dp[i] = min([dp[i - c] if i - c >= 0 else MAX for c in coins]) + 1

        return [dp[amount], -1][dp[amount] == MAX]
```

[返回目录](#00)

## 121. Best Time to Buy and Sell Stock

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

假设您有一个数组，第i个元素是第i天给定股票的价格。

如果只允许您最多完成一笔交易（即买入和卖出一股股票），请设计一种算法以找到最大的利润。

**Example**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

---

### Python Solution
**分析：**

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        low = 1 << 33
        for price in prices:
            if price < low:
                low = price
            elif price - low > profit:
                profit = price - low
        return profit
```

```python
class Solution:
    def maxProfit(self, prices):
        min_p, max_v = 1 << 33, 0
        for i in range(len(prices)):
            min_p = min(min_p, prices[i])
            max_v = max(max_v, prices[i] - min_p)
        return max_v
```

[返回目录](#00)

## 122. Best Time to Buy and Sell Stock II

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

假设您有一个数组，第i个元素是第i天给定股票的价格。 设计算法以找到最大的利润。 您可以根据需要完成尽可能多的交易（即，买入一份并多次出售一股股票）。 注意：您可能无法同时进行多项交易（即必须先出售股票才能再次购买）。

**Example**

```
Example 1:

Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.

Example 2:

Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

---

### Python Solution
**分析：** 两种解法：1. 动态规划的解法。 2. 贪心的解法，因为不限制买卖次数，所以我们只要后一天比前一天价格高，我们就在答案里加上差值，可以看作我们前一天买了今天买了，如果明天的比今天还高也没有关系，今天再买入、明天卖掉的方案和昨天买明天卖的方案是等价的。

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        n = len(prices)
        dp, j = [0] * n, n-1
        for i in range(n-2, -1, -1):
            if prices[i] > prices[i+1]:
                j = i
            dp[i] = dp[i+1] if i == j else prices[j] - prices[i] + dp[j]
        return dp[0] if dp else 0
```

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        res = 0
        for i in range(1, len(prices)):
            if prices[i] > prices[i-1]:
                res += prices[i] - prices[i-1]
        return res

# 可以简化为：
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        return sum(max(b-a,0)for a,b in zip(prices,prices[1:]))
```

[返回目录](#00)

## 123. Best Time to Buy and Sell Stock III

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

假设您有一个数组，第i个元素是第i天给定股票的价格。 设计算法以找到最大的利润。 您最多可以完成两次交易。 注意：您可能无法同时进行多项交易（即必须先出售股票才能再次购买）。

**Example**

```
Example 1:

Input: [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
             Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.

Example 2:

Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

---

### Python Solution
**分析：**

**一维的解法**

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        hold1 = hold2 = float('-inf')
        sold1 = sold2 = 0
        for v in prices:
            sold2 = max(sold2, hold2 + v)
            hold2 = max(hold2, sold1 - v)
            sold1 = max(sold1, hold1 + v)
            hold1 = max(hold1, -v)
        return  sold2
```

[返回目录](#00)

## 64. Minimum Path Sum

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

给定一个m×n的网格，其中填充有非负数，请找到一条从左上到右下的路径，该路径将沿其路径的所有数字的总和最小化。

注意：您只能在任何时间点向下或向右移动。

**Example**

```
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```

---

### Python Solution
**分析：** 二维的动态规划，是比较简单的题目，有点类似于[剑指 offer #47 礼物最大价值](https://github.com/YaxeZhang/Just-Interview/blob/master/%E5%89%91%E6%8C%87offer%EF%BC%88%E7%AC%AC%E4%BA%8C%E7%89%88%EF%BC%89/%E5%89%91%E6%8C%87offer%EF%BC%88%E7%AC%AC%E4%BA%8C%E7%89%88%EF%BC%89.md#47%E7%A4%BC%E7%89%A9%E7%9A%84%E6%9C%80%E5%A4%A7%E4%BB%B7%E5%80%BC)，但是区别在于最大价值对于第一行的初始化不用特意初始化，而求最小的值的话第一行是必须向后逐个累加的，所以第一行初始化要用前缀和。当然二维的可以写成一维的，这里就只给出一维 dp 的写法。

**一维的解法**

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        dp = grid[0][:]
        for i in range(1, n):
            dp[i] += dp[i-1]
        for i in range(1, m):
            for j in range(n):
                if j > 0:
                    dp[j] = grid[i][j] + min(dp[j], dp[j-1])
                else:
                    dp[j] = grid[i][j] + dp[j]
        return dp[-1]
```

[返回目录](#00)

## 72. Edit Distance

Given two words word1 and word2, find the minimum number of operations required to convert word1 to word2.
You have the following 3 operations permitted on a word:
1. Insert a character
2. Delete a character
3. Replace a character

给定两个单词word1和word2，找到将word1转换为word2所需的最少操作数。
您可以对一个单词进行以下3个操作：
1. 插入一个字符
2. 删除一个字符
3. 替换一个字符

**Example**

```
Example 1:

Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation:
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')

Example 2:

Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation:
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```

---

### Python Solution
**分析：** 十分经典的动态规划题目，如何理解要依靠表格来解决。可以发现 二维dp 转移是从左上角向右下角迭代的，之后不再是需求更之前的状态，所以可以简化为 一维dp 来表示。

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        m, n = len(word1), len(word2)
        dp = [[0] * (n+1) for _ in range(m+1)]
        for i in range(n+1):
            dp[0][i] = i
        for i in range(m+1):
            dp[i][0] = i
        for i in range(1, m+1):
            for j in range(1, n+1):
                if word1[i-1] == word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = min(dp[i-1][j], dp[i-1][j-1], dp[i][j-1]) + 1
        return dp[-1][-1]
```

**一维的解法**

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        m, n = len(word1), len(word2)
        dp = list(range(n + 1))
        for i in range(m):
            new = [i + 1]
            for j in range(n):
                if word1[i] == word2[j]:
                    new.append(dp[j])
                else:
                    new.append(1 + min(dp[j+1], dp[j],new[-1]))
            dp = new
        return dp[-1]
```

[返回目录](#00)

## 300. Longest Increasing Subsequence

Given an unsorted array of integers, find the length of longest increasing subsequence.

给定一个未排序的整数数组，请找到最长递增子序列的长度。

**Example**

```
Input: [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```

---

### Python Solution
**分析：** 非常精彩的题目，常规动态规划解法是 O(n^2) 的时间复杂度，但是用二分搜索可以减少到 O(nlgn)，尤其是迭代更新的部分需要好好品味下。

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1] * len(nums)
        for i in range(1, len(nums)):
            for j in range(1, i+1):
                if nums[i] > nums[i-j]:
                    dp[i] = max(dp[i], dp[i-j]+1)
        return max(dp) if dp else 0
```

**O(nlgn)的解法**

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if len(nums) < 2:
            return len(nums)
        dp = [nums[0]]
        for n in nums[1:]:
            if n > dp[-1]:
                dp.append(n)
            else:
                left,right = 0, len(dp)
                while left < right:
                    mid = left + (right-left)//2
                    if dp[mid] < n:
                        left = mid + 1
                    else:
                        right = mid
                dp[left] = n
        return len(dp)
```

[返回目录](#00)

## 1143. Longest Common Subsequence

Given two strings text1 and text2, return the length of their longest common subsequence.

A subsequence of a string is a new string generated from the original string with some characters(can be none) deleted without changing the relative order of the remaining characters. (eg, "ace" is a subsequence of "abcde" while "aec" is not). A common subsequence of two strings is a subsequence that is common to both strings.

给定两个字符串text1和text2，返回它们最长的公共子序列的长度。 字符串的子序列是从原始字符串生成的新字符串，其中删除了一些字符（可以是一个字符），而不会更改其余字符的相对顺序。 （例如，“ ace”是“ abcde”的子序列，而“ aec”则不是）。 两个字符串的共同子序列是两个字符串共同的子序列。

**Example**

```
Example 1:
Input: text1 = "abcde", text2 = "ace"
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.

Example 2:
Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.

Example 3:
Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
```

---

### Python Solution
**分析：** 和上一题差不多，字符串的动态规划解题思路都差不多，无非就是相等递进，替换，删除，插入这样。本题里只涉及相等递进，取两种情况最大值。

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1), len(text2)
        dp = [0] * (n+1)
        for i in range(m):
            cur = [0] * (n+1)
            for j in range(n):
                if text1[i] == text2[j]:
                    cur[j+1] = dp[j] + 1
                else:
                    cur[j+1] = max(cur[j], dp[j+1])
            dp = cur
        return dp[-1]
```

[返回目录](#00)

## 97. Interleaving String

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

给定s1，s2，s3，找出s3是否由s1和s2的交错形成。

**Example**

```
Example 1:
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true

Example 2:
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
Output: false
```

---

### Python Solution
**分析：** 动态规划？第一种解法是带备忘录的递归，第二章一维动态规划。

```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        memo = {}
        def check(p1, p2, p3):
            if (p1, p2) in memo:
                return memo[(p1, p2)]
            if p3 == len(s3):
                return p1 == len(s1) and p2 == len(s2)
            memo[(p1, p2)] = False
            if p1 < len(s1) and s1[p1]==s3[p3]:
                memo[(p1, p2)] |= check(p1+1, p2, p3+1)
            if p2 < len(s2) and s2[p2]==s3[p3]:
                memo[(p1, p2)] |= check(p1, p2+1, p3+1)
            return memo[(p1, p2)]
        return check(0, 0, 0)
```

```python
class Solution: # 动态规划解法
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        r, c, l= len(s1), len(s2), len(s3)
        if r+c != l:
            return False
        dp = [True for _ in range(c+1)]
        for j in range(1, c+1):
            dp[j] = dp[j-1] and s2[j-1] == s3[j-1]
        for i in range(1, r+1):
            dp[0] = (dp[0] and s1[i-1] == s3[i-1])
            for j in range(1, c+1):
                dp[j] = (dp[j] and s1[i-1] == s3[i-1+j]) or (dp[j-1] and s2[j-1] == s3[i-1+j])
        return dp[-1]
```

[返回目录](#00)

## 221. Maximal Square

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

给定一个填充有0和1的2D二进制矩阵，找到仅包含1的最大正方形并返回其面积。

**Example**

```
Input:

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```

---

### Python Solution
**分析：** 二维的动态规划，将 dp[i][j] 作为矩形的右下角则只用考虑 dp[i-1][j], dp[i][j-1], A[i-1][j-1] 的最小值即可，当然也可以简化成一维的动态规划。而是否需要额外的空间来建立 dp 矩阵就看具体想法和要求了。

```python
class Solution:
    def maximalSquare(self, A):
        for i in range(len(A)):
            for j in range(len(A[i])):
                A[i][j] = int(A[i][j])
                if A[i][j] and i and j:
                    A[i][j] = min(A[i-1][j], A[i-1][j-1], A[i][j-1]) + 1
        return len(A) and max(map(max, A)) ** 2
```

**一维的解法**

```python
class Solution:
    def maximalSquare(self, A):
        area = 0
        if A:
            p = [0] * len(A[0])
            for row in A:
                s = list(map(int, row))
                for j, c in enumerate(s[1:], 1):
                    if s[j]:
                        s[j] = min(p[j-1], p[j], s[j-1]) + 1
                area = max(area, max(s) ** 2)
                p = s
        return area
```

[返回目录](#00)

## 198. House Robber

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

您是计划在街道上抢房屋的专业强盗。 每栋房屋都藏有一定数量的钱，阻止您抢劫每座房屋的唯一限制是相邻房屋都已连接了安全系统，如果在同一晚闯入两栋相邻房屋，它将自动与警方联系。 给定一个表示每个房屋的金额的非负整数列表，请确定您今晚可以盗用的最大金额，而无需通知警察。

**Example**

```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```

---

### Python Solution
**分析：** 当前房间偷不偷取决于上上间加当前房间的价值和上一间的值哪个大。状态方程在下面。当然 如果看穿了以后就可以简化成第二种写法。处理 base case 更干净简单。

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums: return 0
        if len(nums) == 1: return nums[0]
        dp = nums[:]
        dp[1] = max(dp[0], dp[1])
        for i in range(2, len(nums)):
            dp[i] = max(nums[i] + dp[i-2], dp[i-1])
        return dp[-1]
```

**看破实质后的解脱**

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        prev1, prev2 = 0, 0
        for num in nums:
            prev1, prev2 = max(prev2 + num, prev1), prev1
        return prev1
```

[返回目录](#00)

## 213. House Robber II

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

您是计划在街道上抢房屋的专业强盗。 每个房子都藏有一定数量的钱。 这个地方的所有房屋都排成一圈。 这意味着第一所房子是最后一个的邻居。 同时，相邻房屋已连接了安全系统，如果在同一晚闯入两个相邻房屋，它将自动与警方联系。 给定一个表示每个房屋的金额的非负整数列表，请确定您今晚可以盗用的最大金额，而无需通知警察。

**Example**

```
Example 1:
Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.

Example 2:
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

---

### Python Solution
**分析：** 和上一题的区别就是首尾相连的需要考虑，所以需要考虑这个条件即可。

```python
class Solution:
    def rob(self, nums):
        def rob(nums):
            now = prev = 0
            for n in nums:
                now, prev = max(now, prev + n), now
            return now
        return max(rob(nums[len(nums) != 1:]), rob(nums[:-1]))
```

[返回目录](#00)

## 91. Decode Ways

A message containing letters from A-Z is being encoded to numbers using the following mapping:
'A' -> 1
'B' -> 2
...
'Z' -> 26
Given a non-empty string containing only digits, determine the total number of ways to decode it.

使用以下映射，将包含AZ字母的消息编码为数字：'A'-> 1'B'-> 2 ...'Z'-> 26给定一个仅包含数字的非空字符串，请确定解码方式的总数。

**Example**

```
Example 1:

Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).

Example 2:

Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

---

### Python Solution
**分析：** 先智商判断一下，把 0 的情况排掉，规避很多不好做的条件。

```python
class Solution:
    def numDecodings(self, s: str) -> int:
        s = s.replace('20', '')
        s = s.replace('10', '')
        if '0' in s: return 0
        l = r = 1
        for i in range(len(s)-1):
            if s[i] == '1' or s[i] == '2' and s[i+1] < '7':
                l, r = r, l+r
            else:
                l = r
        return r
```

[返回目录](#00)

## 10. Regular Expression Matching

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

'.' Matches any single character.
'*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).

给定一个输入字符串（s）和一个模式（p），实现支持'。'的正则表达式匹配。 和“ *”。 '。' 匹配任何单个字符。 '*'匹配零个或多个前一个元素。 匹配项应覆盖整个输入字符串（而非部分）。

**Example**

```
Example 1:

Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".

Example 2:

Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".

Example 3:

Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".
```

---

### Python Solution
**分析：** 一道困难程度的题，判断条件必须要分析好，最好纸上记下推一下，不然很容易乱。

```python
class Solution(object):
    def isMatch(self, s, p):
        dp = [[False] * (len(p) + 1) for _ in range(len(s) + 1)]
        dp[0][0] = True
        for j in range(1, len(p) + 1):
            if p[j - 1] == "*":
                dp[0][j] = dp[0][j - 2]

        for i in range(1, len(s) + 1):
            for j in range(1, len(p) + 1):
                if p[j - 1] != "*":  # 上一位可以到达并且 可以匹配。
                    dp[i][j] = dp[i - 1][j - 1] and (s[i - 1] == p[j - 1] or p[j - 1] == ".")
                else:                # 忽略掉 A× 或者 重复 A
                    dp[i][j] = dp[i][j - 2] or dp[i - 1][j] and (p[j - 2] == s[i - 1] or p[j - 2] == ".")
        return dp[-1][-1]
```

[返回目录](#00)

## 44. Wildcard Matching

Given an input string (s) and a pattern (p), implement wildcard pattern matching with support for '?' and '*'.

'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).
The matching should cover the entire input string (not partial).

给定一个输入字符串（s）和一个模式（p），实现通配符模式匹配并支持'？' 和“ *”。 '？' 匹配任何单个字符。 '*'匹配任何字符序列（包括空序列）。 匹配项应覆盖整个输入字符串（而非部分）。

**Example**

```
Example 1:
Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".

Example 2:
Input:
s = "aa"
p = "*"
Output: true
Explanation: '*' matches any sequence.

Example 3:
Input:
s = "cb"
p = "?a"
Output: false
Explanation: '?' matches 'c', but the second letter is 'a', which does not match 'b'.

Example 4:
Input:
s = "adceb"
p = "*a*b"
Output: true
Explanation: The first '*' matches the empty sequence, while the second '*' matches the substring "dce".

Example 5:
Input:
s = "acdcb"
p = "a*c?b"
Output: false
```

---

### Python Solution
**分析：** 普通做法 二维到一维，然后优化。

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        dp = [[False] * (len(p)+1) for _ in range(len(s)+1)]
        dp[0][0] = True
        for j in range(1, len(p)+1):
            if p[j-1] != '*':
                break
            dp[0][j] = True
        for i in range(1, len(s)+1):
            for j in range(1, len(p)+1):
                if p[j-1] != '*':
                    dp[i][j] = dp[i-1][j-1] and p[j-1] in (s[i-1], '?')
                else:
                    dp[i][j] = dp[i-1][j] or dp[i][j-1]
        return dp[-1][-1]
```

**一维**

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        dp = [False] * (len(p)+1)
        dp[0] = True
        for j in range(1, len(p)+1):
            if p[j-1] != '*':
                break
            dp[j] = True
        for i in range(1, len(s)+1):
            tmp = [False] * (len(p)+1)
            for j in range(1, len(p)+1):
                if p[j-1] != '*':
                    tmp[j] = dp[j-1] and p[j-1] in (s[i-1], '?')
                else:
                    tmp[j] = dp[j] or tmp[j-1]
            dp = tmp
        return dp[-1]
```

[返回目录](#00)
