# [剑指 Offer 49、丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)

- 题目要求：我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。



## 方法一：动态规划 99.07%

```java
class Solution {
    public int nthUglyNumber(int n) {
        //三指针法
        int a = 0, b = 0, c = 0;
        //初始化dp数组
        int[] dp = new int[n];
        dp[0] = 1;
        for(int i = 1; i < n; i++){
            int num1 = dp[a] * 2;
            int num2 = dp[b] * 3;
            int num3 = dp[c] * 5;
            dp[i] = Math.min(Math.min(num1, num2), num3);
            if(dp[i] == num1){
                a++;
            }
            if(dp[i] == num2){
                b++;
            }
            if(dp[i] == num3){
                c++;
            }
        }
        return dp[n-1];

    }
}
```



- 时间复杂度：O(N) 遍历dp数组
- 空间复杂度：O(N) dp数组
- 递推公式xn+1=min(xa×2,xb×3,xc×5)
