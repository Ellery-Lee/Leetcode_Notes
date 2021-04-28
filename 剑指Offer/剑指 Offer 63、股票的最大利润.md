# [剑指offer63、股票的最大利润](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)

- 题目要求：假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？




## 方法一：动态规划 97.99%

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0){
            return 0;
        }
        //维护最小买入价格
        int min = prices[0];
        //状态含义：前i日最大利润
        int[] dp = new int[prices.length];
        dp[0] = 0;
        for(int i = 1; i < prices.length; i++){
            if(prices[i] < min){
                min = prices[i];
                dp[i] = dp[i-1];
                continue;
            }
            dp[i] = Math.max(dp[i-1], prices[i] - min);
        }
        return dp[prices.length - 1];
    }
}
```

- 时间复杂度：O(n)
- 空间复杂度：O(n) 



## 方法一：动态规划(空间优化) 97.99%

```java
class Solution {
    public int maxProfit(int[] prices) {
        if(prices == null || prices.length == 0){
            return 0;
        }
        //维护最小买入价格
        int min = prices[0];
        //状态含义：前i日最大利润
        int dp = 0;
        for(int i = 1; i < prices.length; i++){
            if(prices[i] < min){
                min = prices[i];
                dp = dp;
                continue;
            }
            dp = Math.max(dp, prices[i] - min);
        }
        return dp;
    }
}
```

- 时间复杂度：O(n)
- 空间复杂度：O(1) 