# [剑指 Offer 42、连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

- 题目要求：输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

  要求时间复杂度为O(n)。


## 方法一：动态规划 17%

```java
class Solution {
    public int maxSubArray(int[] nums) {
        //动态规划定义：
        //dp[i]表示以nums[i]结尾的最大连续子数组和
        int[] dp = new int[nums.length];
        //初始化dp[]
        dp[0] = nums[0];
        //维护返回值
        int ans = dp[0];
        for(int i = 1; i < nums.length; i++){
            int temp = dp[i-1] + nums[i];
            //如果前一个最大连续子数组和对当前nums[i]的连续数组贡献为负，则舍弃
            //当前最大连续子数组和就是nums[i]
            if(temp < nums[i]){
                dp[i] = nums[i];
            }else{//如果dp[i-1]对nums[i]贡献不为负，则加上dp[i-1]
                dp[i] = temp;
            }
            ans = Math.max(ans, dp[i]);
        }
        return ans; 
    }
}
```

- 时间复杂度：*O*（n）动态规划
- 空间复杂度：O（n）维护dp数组



## 方法二：动态规划(优化) 97%

```java
class Solution {
    public int maxSubArray(int[] nums) {
        //由于只用到了dp[i-1]，所以这里只维护一个pre就可以优化空间复杂度
        int res = nums[0];
        int pre = 0;
        for(int i = 0 ; i < nums.length; i++){
            if(pre > 0){
                pre = nums[i] + pre;
            }else{
                pre = nums[i];
            }
            res = Math.max(res, pre);
        }
        return res;
    }
}
```

- 时间复杂度：*O*（n）动态规划
- 空间复杂度：O（1）