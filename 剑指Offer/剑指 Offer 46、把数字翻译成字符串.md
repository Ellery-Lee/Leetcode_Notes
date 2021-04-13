# [剑指 Offer 46、把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/submissions/)

- 题目要求：给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。



## 方法一：动态规划 100%

```java
class Solution {
    public int translateNum(int num) {
        String s = String.valueOf(num);
        //初始化dp[0]=1,dp[1]=1
        int a = 1;
        int b = 1;
        for(int i = 2; i <= s.length(); i++){
            String temp = s.substring(i-2, i);
            int tempNum = (temp.compareTo("10") >= 0 && temp.compareTo("25") <= 0) ? a + b : b;
            a = b;
            b = tempNum;
        }
        return b;
    }
}
```
