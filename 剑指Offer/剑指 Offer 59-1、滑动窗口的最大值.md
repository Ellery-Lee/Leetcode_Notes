# [剑指offer59-1、滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

- 题目要求：给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

## 方法一：暴力解 27.60%

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums == null || nums.length == 0){
            return new int[0];
        }
        int left = 0;
        int right = 0;
        int[] ans = new int[nums.length - k + 1];
        int i = 0;
        while(right < nums.length){
            //达到滑动窗口大小再开始找最大值
            if(right - left + 1 == k){
                ans[i++] = findMax(nums, left, right);
                left++;
            }
            right++;
        }
        return ans;
    }
    public int findMax(int[] nums, int left, int right){
        int ans = Integer.MIN_VALUE;
        for(int i = left; i <= right; i++){
            ans = Math.max(nums[i], ans);
        }
        return ans;
    }
}
```

- 时间复杂度：O(Nk),k为滑动窗口大小
- 空间复杂度：O(1)



## 方法二：单调队列 82.98%

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums == null || nums.length == 0){
            return new int[0];
        }
        Deque<Integer> deque = new ArrayDeque<>();
        int[] ans = new int[nums.length - k + 1];
        //未形成窗口
        for(int i = 0; i < k; i++){
            while(!deque.isEmpty() && deque.peekLast() < nums[i]){
                deque.pollLast();
            }
            deque.offerLast(nums[i]);
        }
        ans[0] = deque.peekFirst();
        //形成窗口
        for(int i = k; i < nums.length; i++){
            //窗口左边界是最大值，要从队列中删去
            if(deque.peekFirst() == nums[i-k]){
                deque.pollFirst();
            }
            while(!deque.isEmpty() && deque.peekLast() < nums[i]){
                deque.pollLast();
            }
            deque.offerLast(nums[i]);
            ans[i-k + 1] = deque.peekFirst();
        }
        return ans;
    }
}
```

- 时间复杂度：O(N)
- 空间复杂度：O(1)