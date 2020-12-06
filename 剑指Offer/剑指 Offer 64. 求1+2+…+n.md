#### [剑指 Offer 64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/)

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。



## 方法一：递归(逻辑短路) 100%

```java
class Solution {
    public int sumNums(int n) {
        boolean temp = n > 1 && (n += sumNums(n-1)) > 0;
        return n;
    }
}
```

思路：使用逻辑运算符的短路效应代替递归需要的if判断出口

![Snipaste_2020-10-24_11-58-17](D:\JavaHub\学习相关\课堂截图\Snipaste_2020-10-24_11-58-17.png)

时间复杂度：O(n)，n次递归

空间复杂度：O(n)，递归空间

