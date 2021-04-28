# [剑指offer65、不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/submissions/)

- 题目要求：写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。




## 方法一：位运算 100%

```java
class Solution {
    public int add(int a, int b) {
        //负数和正数在计算机中都以补码存储，统一计算
        while(b != 0){//进位为0时跳出
            int c = (a&b) << 1;//c=进位
            a ^= b;//a=非进位和
            b = c;//b=进位
        }
        return a;
    }
}
```

- 时间复杂度：O(1)
- 空间复杂度：O(1) 
