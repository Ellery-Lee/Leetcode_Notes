# [剑指 Offer 47、礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/submissions/)

- 题目要求：在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？



## 方法一：动态规划二维 83.26%

```java
class Solution {
    public int maxValue(int[][] grid) {
        if(grid == null || grid.length == 0){
            return 0;
        }
        //状态：以当前元素为终点的最大价值
        int[][] dp = new int[grid.length][grid[0].length];
        //初始化dp
        dp[0][0] = grid[0][0];
        //初始化dp第一列
        for(int i = 1; i < grid.length; i++){
            dp[i][0] = dp[i-1][0] + grid[i][0];
        }
        //初始化dp第一行
        for(int i = 1; i < grid[0].length; i++){
            dp[0][i] = dp[0][i-1] + grid[0][i];
        }
        //从左往右，从上往下遍历更新dp
        for(int i = 1; i < grid.length; i++){
            for(int j = 1; j < grid[0].length; j++){
                dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]) + grid[i][j];
            }
        }
        return dp[grid.length - 1][grid[0].length - 1];
    }
}
```



## 方法二：动态规划一维 98.39%

```java
class Solution {
    public int maxValue(int[][] grid) {
        if(grid == null || grid.length == 0){
            return 0;
        }
        //状态：以当前元素为终点的最大价值
        int[] dp = new int[grid[0].length];
        //初始化dp
        dp[0] = grid[0][0];
        //初始化dp第一行
        for(int i = 1; i < grid[0].length; i++){
            dp[i] = dp[i-1] + grid[0][i];
        }
        //从左往右，从上往下遍历更新dp
        //因为只用到上一行和当前元素左边，所以以为数组dp就够用
        for(int i = 1; i < grid.length; i++){
            for(int j = 0; j < grid[0].length; j++){
                if(j == 0){
                    dp[j] = dp[j] + grid[i][j];
                }else{
                    //dp[j]代表该元素上一行正上方
                    dp[j] = Math.max(dp[j-1], dp[j]) + grid[i][j];
                }
            }
        }
        return dp[grid[0].length-1];
    }
}
```

