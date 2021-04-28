# [剑指offer66、构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/submissions/)

- 题目要求：给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B[i] 的值是数组 A 中除了下标 i 以外的元素的积, 即 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。




## 方法一：表格分割 81.91%

```java
class Solution {
    public int[] constructArr(int[] a) {
        if(a == null || a.length == 0){
            return new int[0];
        }
        int[] dp = new int[a.length];
        dp[0] = 1;
        //右三角临时变量
        int temp = 1;
        for(int i = 1; i < a.length; i++){
            dp[i] = dp[i-1] * a[i-1];
        }
        for(int i = a.length - 2; i >= 0; i--){
            temp *= a[i+1];
            dp[i] *= temp;
        }
        return dp;
    }
}
```

- 时间复杂度：O(N)
- 空间复杂度：O(1) 
