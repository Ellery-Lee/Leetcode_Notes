# [剑指 Offer 53-2. 0~n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

- 题目要求：一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。




## 方法一：二分查找 100%

```java
class Solution {
    public int missingNumber(int[] nums) {
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] == mid){
                left = mid + 1;
            }else{
                right = mid - 1;
            }
        }
        return left;
    }
}
```

- 时间复杂度：O（logn)
- 空间复杂度：O（1）

- **注意：遇到有序数组中搜索问题，首先想到二分法解决。**

## 方法二：遍历 100%

```java
class Solution {
    public int missingNumber(int[] nums) {
        for(int i = 0; i < nums.length; i++){
            if(nums[i] != i){
                return i;
            }
        }
        return nums.length;
    }
}
```

- 时间复杂度：O（n)
- 空间复杂度：O（1）

