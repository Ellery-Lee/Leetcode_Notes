# [剑指offer57、和为s的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

- 题目要求：输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

## 方法一：滑动窗口 19.25%

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        int left = 1;
        int right = 0;
        int sum = 0;
        List<int[]> list = new ArrayList<>();
        while(left <= target / 2){
            if(sum < target){
                right++;
                sum += right;
            }else if(sum > target){
                sum -= left;
                left++;
            }else{
                int[] temp = new int[right - left + 1];
                for(int i = left; i <= right; i++){
                    temp[i-left] = i;
                }
                list.add(temp);
                sum -= left;
                left++;
            }
        }
        return list.toArray(new int[list.size()][]);
    }
}
```

- 时间复杂度：O(N)
- 空间复杂度：O(1)
