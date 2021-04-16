# [剑指 Offer 53-1. 在排序数组中查找数字](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/submissions/)

- 题目要求：统计一个数字在排序数组中出现的次数。




## 方法一：二分查找 100%

```java
class Solution {
    public int search(int[] nums, int target) {
        return helper(nums, target) - helper(nums, target - 1);
    }
    public int helper(int[] nums, int target){
        //二分查找
        if(nums == null || nums.length == 0){
            return 0;
        }
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] <= target){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        // 返回targer区间最右边的索引
        return right;
    }
}
```

- 时间复杂度：O（logn)
- 空间复杂度：O（1）
