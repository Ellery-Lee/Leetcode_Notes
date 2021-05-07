#### [剑指 Offer 17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/submissions/)

输入数字 `n`，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

## 方法一：暴力解 99.99%

```java
class Solution {
    public int[] printNumbers(int n) {
        int size = (int)Math.pow(10, n) - 1;
        int[] ans = new int[size];
        for(int i = 0; i < size; i++){
            ans[i] = i+1;
        }
        return ans;
    }
}
```

- 时间复杂度：O(10^n^)
- 空间复杂度：O(1)