# [剑指offer61、扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

- 题目要求：从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。


## 方法一：哈希表 91.71%

```java
class Solution {
    public boolean isStraight(int[] nums) {
        Set<Integer> set = new HashSet<>();
        int max = Integer.MIN_VALUE;
        int min = Integer.MAX_VALUE;
        for(int i = 0; i < nums.length; i++){
            if(nums[i] == 0){
                continue;
            }
            if(set.contains(nums[i])){
                return false;
            }else{
                set.add(nums[i]);
            }
            max = Math.max(max, nums[i]);
            min = Math.min(min, nums[i]);
        }
        return max - min < 5;
    }
}
```

- 时间复杂度：O(1)
- 空间复杂度：O(1) 
- **关键：max - min < 5**

