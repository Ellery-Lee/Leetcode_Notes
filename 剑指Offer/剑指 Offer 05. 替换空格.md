#### 剑指 Offer 05. 替换空格

- 题目要求：请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。



## 方法一：StringBuilder 100%

```java
class Solution {
    public String replaceSpace(String s) {
        if(s == null || s.length() == 0){
            return "";
        }
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < s.length(); i++){
            if(' ' == s.charAt(i)){
                sb.append("%20");
            }else{
                sb.append(s.charAt(i));
            }
        }
        return sb.toString();
    }
}
```

- 时间复杂度：*O*(n）遍历一遍
- 空间复杂度：O(n) StringBuilder
- 思路：遍历字符串，遇到空格就append(“%20”)



## 方法二：字符数组 100%

```java
class Solution {
    public String replaceSpace(String s) {
        if(s == null || s.length() == 0){
            return "";
        }
        char[] temp = new char[3 * s.length()];
        int pointer = 0;
        for(int i = 0; i < s.length(); i++){
            if(s.charAt(i) == ' '){
                temp[pointer++] = '%';
                temp[pointer++] = '2';
                temp[pointer++] = '0';
            }else{
                temp[pointer++] = s.charAt(i);
            }
        }
        return new String(temp, 0, pointer);
    }
}
```



## 方法三：API 100%

```java
class Solution {
    public String replaceSpace(String s) {
        if(s == null || s.length() == 0){
            return "";
        }
        return s.replace(" ", "%20");
    }
}
```





9.20