# 28、实现strStr()

- 题目要求：实现 strStr() 函数。给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

- **说明**：当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。

- ```
  输入: haystack = "hello", needle = "ll"
  输出: 2
  
  输入: haystack = "aaaaa", needle = "bba"
  输出: -1
  ```

## 方法一：子串逐一比较法  33.12%

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.equals("")){
            return 0;
        }

        for(int i = 0; i < haystack.length(); i++){
            if(haystack.charAt(i) == needle.charAt(0) && (haystack.length() - i >= needle.length())){
                if(helper(haystack.substring(i, i + needle.length()), needle)){
                    return i;
                }
            }
        }
        return -1;
    }

    public boolean helper(String par, String son){
        for(int i = 0; i < par.length(); i++){
            if(par.charAt(i) != son.charAt(i)){
                return false;
            }
        }
        return true;
    }
}
```

- 时间复杂度：*O*（(n-m)m)最坏情况每个字符都要进行判断。n为haystack大小，m为needle大小
- 空间复杂度：O(1）没有用到额外空间
- **思路**：对haystack每个字符进行遍历，如果首字母和needle首字母相同，则调用判断函数进行判断。



## 方法二：子串逐一比较法（改进）：滑动窗口法 75.32%

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.equals("")){
            return 0;
        }
        int h = haystack.length();
        int n = needle.length();
        for(int start = 0; start < h - n + 1; start++){
            if(haystack.substring(start, start + n).equals(needle)){
                return start;
            }
        }
        return -1;
    }

}
```

- 时间复杂度：*O*（(n-m)m)最坏情况每个字符都要进行判断。n为haystack大小，m为needle大小
- 空间复杂度：O(1）没有用到额外空间
- **思路**：相比方法一，这个思路更明确，并且直接使用了string内置方法判断两字符串是否相等，还对循环条件做了优化。



## 方法三：双指针法 48.79%

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.equals("")){
            return 0;
        }
        int h = haystack.length();
        int n = needle.length();
        int pointer = 0;
        int count = 0;
        int curleng = 0;
        while(pointer < h - n + 1){
            if(haystack.charAt(pointer) == needle.charAt(0)){
                while(count < n && haystack.charAt(pointer) == needle.charAt(count)){
                    count++;
                    pointer++;
                    curleng++;
                }
                if(count == n){
                    return pointer - n;
                }else{
                    pointer = pointer - curleng + 1;
                    count = 0;
                    curleng = 0;
                }
            }else{
                pointer++;
            }
        }
        return -1;
    }

}
```

- 时间复杂度：*O*（(n-m)m)最坏情况每个字符都要进行判断。n为haystack大小，m为needle大小

- 空间复杂度：O(1）没有用到额外空间

- **思路**：只需要子串第一个字符跟needle第一个字符比较就可，跟方法一相似。

  移动 pn 指针，直到 pn 所指向位置的字符与 needle 字符串第一个字符相等。

  通过 pn，pL，curr_len 计算匹配长度。

  如果完全匹配（即 curr_len == L），返回匹配子串的起始坐标（即 pn - L）。

  如果不完全匹配，回溯。使 pn = pn - curr_len + 1， pL = 0， curr_len = 0。




- timeline

1. ~~2020.6.28-~~
2. 2020.6.29
3. 2020.6.31
4. 2020.7.5
5. 2020.7.12
6. 2020.7.27