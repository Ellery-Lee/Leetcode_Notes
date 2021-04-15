# [剑指 Offer 48、最长不含重复字符的子字符串](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/submissions/)

- 题目要求：请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。



## 方法一：滑动窗口 31.31%

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s == null || s.length() == 0){
            return 0;
        }
        HashSet<Character> set = new HashSet<>();
        int ans = 0;
        //双指针法
        int left = 0;
        int right = 0;
        while(right < s.length()){
            Character c = s.charAt(right);
            //判断右侧指针是否重复，不重复加入set右移，维护最大值
            //重复则删除左指针元素左移，直到不重复
            if(!set.contains(c)){
                set.add(c);
                ans = Math.max(right - left + 1, ans);
                right++;
            }else{
                set.remove(s.charAt(left));
                left++;
            }
        }
        return ans;
    }
}
```

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if(s == null || s.length() == 0){
            return 0;
        }
        HashSet<Character> set = new HashSet<>();
        int ans = 0;
        //滑动窗口
        for(int l = 0, r = 0; r < s.length(); r++){
            Character c = s.charAt(r);
            //如果右指针元素重复，删除左指针元素并右移直到不重复
            while(set.contains(c)){
                set.remove(s.charAt(l++));
            }
            //不重复则加入set并维护最大长度
            set.add(c);
            ans = Math.max(ans, r - l + 1);
        }
        
        return ans;
    }
}
```



- 时间复杂度：O(N) 遍历字符串
- 空间复杂度：O(N) HashSet

## 方法二：动态规划

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> dic = new HashMap<>();
        int res = 0;
        int temp = 0;
        for(int i = 0; i < s.length(); i++){
            int j = dic.getOrDefault(s.charAt(i), -1);
            dic.put(s.charAt(i), i);
            //当前路径大小
            temp = temp < i - j ? temp + 1 : i - j;
            res = Math.max(res, temp);
        }
        return res;
    }
}
```

- 时间复杂度：O(N) 遍历字符串
- 空间复杂度：O(1) 最多128(ASCII码大小)