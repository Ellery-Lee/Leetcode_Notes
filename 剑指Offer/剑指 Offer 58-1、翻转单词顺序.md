# [剑指offer58、翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/submissions/)

- 题目要求：输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

## 方法一：字符串分割 92.40%

```java
class Solution {
    public String reverseWords(String s) {
        if(s == null || s.length() == 0){
            return s;
        }
        String[] strs = s.trim().split(" ");
        StringBuilder sb = new StringBuilder();
        for(int i = strs.length - 1; i >= 0; i--){
            if("".equals(strs[i])){
                continue;
            }
            sb.append(strs[i]).append(" ");
        }
        return sb.toString().trim();
    }
}
```

- 时间复杂度：O(N)
- 空间复杂度：O(N)
