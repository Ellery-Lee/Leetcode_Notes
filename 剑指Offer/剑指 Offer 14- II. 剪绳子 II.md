#### [剑指 Offer 14- II. 剪绳子 II](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m - 1] 。请问 k[0]*k[1]*...*k[m - 1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。



## 方法一：循环求余 40.31%

```java
class Solution {
    public int cuttingRope(int n) {
        if(n < 1){
            return 0;
        }
        if(n == 1){
            return 1;
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
            return (int)helper(3, a, 1000000007);
        }else if(b == 1){
            return (int)((helper(3, a-1, 1000000007) * 4) % 1000000007);
        }
        return (int)((helper(3, a, 1000000007) * 2) % 1000000007);
    }
    public long helper(int x, int a, int const_num){
        long ans = 1;
        for(int i = 0; i < a; i++){
            ans = (ans*3) % const_num;
        }
        return ans;
    }
}
```

思路：这一题已经不能用动态规划了，取余之后max函数就不能用来比大小了。注意helper函数中使用long型变量存储中间值，有可能会越界

![Snipaste_2020-10-24_17-05-08](D:\JavaHub\学习相关\课堂截图\Snipaste_2020-10-24_17-05-08.png)