#### [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/submissions/)

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

## 方法一：回溯法 100%

```java
class Solution {
    int m, n, k;
    boolean[][] visited;
    public int movingCount(int m, int n, int k) {
        this.m = m;
        this.n = n;
        this.k = k;
        //维护访问节点数组
        this.visited = new boolean[m][n];
        return dfs(0, 0, 0, 0);
    }
    //深度搜索(回溯)
    //si表示行的数位和
    //sj表示列的数位和
    public int dfs(int i, int j, int si, int sj){
        if(i >= m || j >= n || (si + sj) > k || visited[i][j] == true){
            return 0;
        }
        visited[i][j] = true;
        return 1 + dfs(i+1, j, (i+1) % 10 == 0 ? si - 8 : si + 1, sj) + dfs(i, j+1, si, (j+1) % 10 == 0 ? sj - 8 : sj + 1);
    }
}
```

- 时间复杂度(MN)
- 空间复杂度(MN)



## 方法二：BFS 13.37%

```java
class Solution {
    public int movingCount(int m, int n, int k) {
        boolean[][] visited = new boolean[m][n];
        Deque<int[]> queue = new ArrayDeque<>();
        queue.offer(new int[]{0, 0, 0, 0});
        int res = 0;
        while(queue.size() > 0){
            int[] x = queue.poll();
            int i = x[0];
            int j = x[1];
            int si = x[2];
            int sj = x[3];
            if(i >= m || j >= n || (si + sj) > k || visited[i][j] == true){
                continue;
            }
            visited[i][j] = true;
            res++;
            queue.offer(new int[]{i+1, j, (i+1) % 10 == 0 ? si - 8 : si + 1, sj});
            queue.offer(new int[]{i, j+1, si, (j+1) % 10 == 0 ? sj - 8 : sj + 1});
        }
        return res;
    }
}
```

- 时间复杂度(MN)
- 空间复杂度(MN)

