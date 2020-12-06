#### [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

- 题目要求：写一个函数，输入 `n` ，求斐波那契（Fibonacci）数列的第 `n` 项。答案需要取模 **1e9+7（1000000007）**，如计算初始结果为：1000000008，请返回 1。



## 方法一：动态规划 100%

```java
class Solution {
    public int fib(int n) {
        if(n == 0){
            return 0;
        }
        if(n == 1){
            return 1;
        }
        int prev = 0;
        int curr = 1;
        int i = 2;
        while(i <= n){
            int sum = (curr + prev) % 1000000007;
            prev = curr;
            curr = sum;
            i++;
        }
        return curr;
    }
}
```

- 时间复杂度：*O*(n) 递归
- 空间复杂度：O(n) 递归
- 思路：动态规划，从下向上



9.21