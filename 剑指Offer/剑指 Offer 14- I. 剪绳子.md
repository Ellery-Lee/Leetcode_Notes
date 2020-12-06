#### [剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。



## 方法一：动态规划 40.31%

```java
class Solution {
    public static int cuttingRope(int n) {
        if(n < 2){
            return 0;
        }
        if(n == 2){
            return 1;
        }
        if(n == 3){
            return 2;
        }
        int[] dp = new int[n+1];    //dp数组代表当前下标长度的绳子分成若干段后各段长度乘积的最大值
        dp[1] = 1;
        dp[2] = 2; //当n大于3时，dp[1] = 1, dp[2] = 2, dp[3] = 3
        dp[3] = 3;
        for(int i = 3; i <= n; i++){
            for(int j = 1; j <= i/2; j++){
                dp[i] = Math.max(dp[i], dp[i-j] * dp[j]);
            }
        }
        return dp[n];
    }
}
```

思路：动态规划，从下而上地进行递归。特别注意当n < 3时返回值和n > 3时的返回值不一样。



## 方法二：贪心算法 100%

```java
class Solution {
    public static int cuttingRope(int n) {
        if(n < 2){
            return 0;
        }
        if(n == 2){
            return 1;
        }
        if(n == 3){
            return 2;
        }
        int a = n / 3;
        int b = n % 3;
        if(b == 0){
            return (int)Math.pow(3, a);
        }
        if(b == 1){
            return (int)Math.pow(3, a-1)*(2*2);
        }
        return (int)Math.pow(3, a) * 2; //b == 2
    }
}
```

时间复杂度：O(1)，只有求模和求余、次方运算

空间复杂度：O(1)，没有用到额外空间

思路：尽可能将绳子以长度 3 等分为多段时，乘积最大。

![Snipaste_2020-10-22_21-04-01](D:\JavaHub\学习相关\课堂截图\Snipaste_2020-10-22_21-04-01.png)