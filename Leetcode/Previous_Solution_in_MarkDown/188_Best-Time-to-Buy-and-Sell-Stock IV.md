### 188. Best Time to Buy and Sell Stock IV

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete at most *two* transactions.

**Note:** You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example 1:**

```
Input: [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
             Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
```

**Example 2:**

```
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
```

**Example 3:**

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

**Submission**

- Python

```python
class Solution:
  	# beats 30% in runtime, 33% in memory
    def maxProfit(self, k: int, prices: List[int]) -> int:
        # exception handler
        n = len(prices)
        if len(prices) <= 0:
            return 0
        
        # 当k很大时相当于不限制次数
        if (k > n / 2):  
            res, hold = 0, prices[0]
            for i in range(1,n):
                res += max(0, prices[i] - prices[i-1]);
            return res
        
        dp0 = [[0] * (k+1) for i in range(n)]
        dp1 = [[0] * (k+1) for i in range(n)]
        
        for i in range(k):
            dp1[0][i] = -prices[0] 
        
        for i in range(1, n):
            # print(i)
            dp1[i][0] = max(dp1[i-1][0], -prices[i])
            
            for j in range(1,k+1):
                dp0[i][j] = max(dp0[i-1][j], dp1[i-1][j-1] + prices[i])
                dp1[i][j] = max(dp1[i-1][j], dp0[i-1][j]   - prices[i])
    
        return dp0[-1][-1]
```



- C++

```c++

```



- Java

```java

```



​	