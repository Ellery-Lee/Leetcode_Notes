# [剑指 Offer 44、数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

- 题目要求：数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

  请写一个函数，求任意第n位对应的数字。
  


## 方法一：数字规律 100%

```java
class Solution {
    public int findNthDigit(int n) {
        int digit = 1;//数字位数
        long start = 1;//digit位数的第一个数字
        long count = 9;//1、所有digit位数所占的位数
        while(n > count){
            n -= count;
            digit += 1;
            start *= 10;
            count = 9 * start * digit;
        }
        //2、确定n所在的数字num
        //此时的n时相对于start的位置
        long num = start + (n-1) / digit;//n-1是因为start从0开始
        //3、确定n时num的第几位
        return Long.toString(num).charAt((n-1) % digit) - '0';//n-1是因为String下标从0开始
    }
}
```

- 时间复杂度：*O*（log(n)）所求数位 n 对应数字 num 的位数 digit 最大为 O(logn) ；第一步最多循环 O(logn) 次；第三步中将 num 转化为字符串使用 O(logn) 时间；因此总体为 O(logn) 。
- 空间复杂度：O（log(n)）将数字 num转化为字符串 `str(num)` ，占用 *O*(log*n*) 的额外空间。
- log(n)是因为数字n的十进制位数为log10(n)
- 思路，见原文
