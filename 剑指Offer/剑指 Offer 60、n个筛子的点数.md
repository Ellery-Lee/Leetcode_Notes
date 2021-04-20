# [剑指offer60、n个筛子的点数](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/)

- 题目要求：把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率。

  你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。
  


## 方法一：动态规划 100%

```java
class Solution {
    public double[] dicesProbability(int n) {
        //动态规划数组，这里优化过了空间复杂度，采用两个一维数组
        double[] dp = new double[6];
        //初始化dp数组
        Arrays.fill(dp, 1.0/6.0);
        for(int i = 2; i <= n; i++){
            //新一轮dp数组
            //[n, 6n]一共有6n - n + 1种点数
            double[] temp = new double[5 * i + 1];
            //正向递推
            //遍历f(n-1)中各点数和的概率，并将其加至f(n)中相关项
            for(int j = 0; j < dp.length; j++){
                for(int k = 0; k < 6; k++){
                    //dp[j]对temp[j+k]贡献本身的1/6概率
                    temp[j+k] += dp[j] / 6.0;
                }
            }
            dp = temp;
        }
        return dp;
    }
}
```

- 时间复杂度：O(n^2^)
- 空间复杂度：O(N) 

