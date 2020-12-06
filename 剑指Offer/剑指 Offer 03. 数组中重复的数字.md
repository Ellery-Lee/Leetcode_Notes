# 剑指 Offer 03. 数组中重复的数字

- 题目要求：找出数组中重复的数字。在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。



## 方法一：哈希表 10.05%

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for(int i : nums){
            if(!set.contains(i)){
                set.add(i);
            }else{
                return i;
            }
        }
        return -1;
    }
}
```

- 时间复杂度：*O*(n）for循环遍历

- 空间复杂度：O(n) 哈希表



## 方法二：排序 60.12%

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        Arrays.sort(nums);
        int ans = Integer.MIN_VALUE;
        for(int i : nums){
            if(i == ans){
                return i;
            }else{
                ans = i;
            }
        }
        return -1;
    }
}
```

- 时间复杂度：*O*(nlog(n)）排序

- 空间复杂度：O(1） 



## 方法三：原地排序 100%

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        if(nums == null || nums.length == 0){
            return -1;
        }
        for(int i = 0; i < nums.length; i++){
            while(i != nums[i]){
                if(nums[i] == nums[nums[i]]){
                    return nums[i];
                }else{
                    int temp = nums[i];
                    nums[i] = nums[temp];
                    nums[temp] = temp;
                }
            }
        }
        return -1;
    }
}
```

- 时间复杂度：*O*(n）虽然双循环，但最坏2n

- 空间复杂度：O(1）原地排序 