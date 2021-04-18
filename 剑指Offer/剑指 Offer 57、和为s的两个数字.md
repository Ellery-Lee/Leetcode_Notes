# [剑指offer57、和为s的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

- 题目要求：输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

## 方法一：哈希表 5.2%

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < nums.length; i++){
            map.put(nums[i], i);
        }
        for(int i = 0; i < nums.length; i++){
            int temp = target - nums[i];
            if(map.containsKey(temp) && map.get(temp) != i){
                return new int[]{nums[i], nums[map.get(temp)]};
            }
        }
        return null;
    }
}
```

- 时间复杂度：O(N)
- 空间复杂度：O(N)

## 方法二：双指针 95.03%

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while(left < right){
            int temp = nums[left] + nums[right];
            if(temp > target){
                right--;
            }else if(temp < target){
                left++;
            }else{
                return new int[]{nums[left], nums[right]};
            }
        }
        return null;
    }
}
```

- 时间复杂度：O(N)
- 空间复杂度：O(1)