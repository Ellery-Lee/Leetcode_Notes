# [剑指 Offer 50、第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/submissions/)

- 题目要求：在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。



## 方法一：哈希表 62.22%

```java
class Solution {
    public char firstUniqChar(String s) {
        if(s == null || s.length() == 0){
            return ' ';
        }
        //哈希表
        Map<Character, Boolean> map = new HashMap<>();
        char[] chars = s.toCharArray();
        for(int i = 0; i < chars.length; i++){
            map.put(chars[i], !map.containsKey(chars[i]));
        }
        for(int i = 0; i < chars.length; i++){
            if(map.get(chars[i]) == true){
                return chars[i];
            }
        }
        return ' ';
    }
}
```



- 时间复杂度：O(N) 哈希表
- 空间复杂度：O(N) 两次遍历
