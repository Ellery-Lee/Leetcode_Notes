#### [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

- 题目要求：一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

  答案需要取模**1e9+7（1000000007**，如计算初始结果为：1000000008，请返回 1。




## 方法一：动态规划 100%

```java
class Solution {
    public int numWays(int n) {
        if(n <= 0){
            return 1;
        }
        if(n == 1){
            return 1;
        }
        if(n == 2){
            return 2;
        }
        int prev = 1;
        int curr = 2;
        for(int i = 3; i <= n; i++){
            int sum = (curr + prev) % 1000000007;
            prev = curr;
            curr = sum;
        }
        return curr;
    }
}
```

- 时间复杂度：*O*(n) 递归
- 空间复杂度：O(n) 递归
- 思路：动态规划，从下向上



9.21