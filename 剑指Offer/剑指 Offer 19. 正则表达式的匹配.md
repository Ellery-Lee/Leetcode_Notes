#### [剑指 Offer 19. 正则表达式的匹配](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)

请实现一个函数用来匹配包含'. '和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不匹配。

## 方法一：动态规划 77.55%

```java
class Solution {
    public boolean isMatch(String s, String p) {
        if(s == null || p == null){
            return false;
        }
        int m = s.length() + 1;
        int n = p.length() + 1;
        //dp,dp状态，前i个s字符是否可以用j个p字符匹配
        boolean[][] dp = new boolean[m][n];
        //表示空字符串可以匹配
        dp[0][0] = true;
        //p不为空时匹配空字符串，必须p的偶数字符处才可以匹配
        for(int j = 2; j < n; j+=2){
            dp[0][j] = dp[0][j-2] && p.charAt(j-1) == '*'; 
        }
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                //p当前为'*'时分三种情况
                if(p.charAt(j-1) == '*'){
                    //匹配0个前一字符
                    if(dp[i][j-2]){
                        dp[i][j] = true;
                    //匹配n个前一字符
                    }else if(dp[i-1][j] && s.charAt(i-1) == p.charAt(j-2)){
                        dp[i][j] = true;
                    //匹配n个'.'字符
                    }else if(dp[i-1][j] && p.charAt(j-2) == '.'){
                        dp[i][j] = true;
                    }
                //p不为'*'时分两种情况
                }else{
                    //s和p当前字符相同
                    if(dp[i-1][j-1] && s.charAt(i-1) == p.charAt(j-1)){
                        dp[i][j] = true;
                    //p当前字符为'.'
                    }else if(dp[i-1][j-1] && p.charAt(j-1) == '.'){
                        dp[i][j] = true;
                    }
                }
            }
        }
        return dp[m-1][n-1];
    }
}
```

- 时间复杂度：O(mn)
- 空间复杂度：O(mn)