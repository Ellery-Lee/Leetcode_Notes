#### [剑指 Offer 19. 正则表达式的匹配](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)

请实现一个函数用来匹配包含'. '和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不匹配。

## 方法一：动态规划 77.55%

```java
class Solution {
    public boolean isMatch(String s, String p) {
        int m = s.length() + 1;
        int n = p.length() + 1;
        //dp状态，s的前m个字符和p的前n个字符能否匹配
        boolean[][] dp = new boolean[m][n];
        //代表两个空字符串能够匹配
        dp[0][0] = true;
        //s为空字符串，p为偶数为时可以保持空字符串
        for(int j =2 ; j < n; j+=2){
            dp[0][j] = dp[0][j-2] && p.charAt(j-1) == '*';
        }
        //dp
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                if(p.charAt(j-1) == '*'){
                    if(dp[i][j-2]){
                        dp[i][j] = true;
                    }else if(dp[i-1][j] && s.charAt(i-1) == p.charAt(j-2)){
                        dp[i][j] = true;
                    }else if(dp[i-1][j] && p.charAt(j-2) == '.'){
                        dp[i][j] = true;
                    }
                }else{
                    if(dp[i-1][j-1] && s.charAt(i-1) == p.charAt(j-1)){
                        dp[i][j] = true;
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