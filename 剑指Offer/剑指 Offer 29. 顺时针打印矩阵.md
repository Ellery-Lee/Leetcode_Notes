#### [剑指 Offer 29. 顺时针打印矩阵](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

## 方法一：模拟+定边界 100%

```java
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if(matrix == null){
            return null;
        }
        if(matrix.length == 0){
            return new int[0];
        }
        //上下左右边界
        int l = 0;
        int r = matrix[0].length - 1;
        int t = 0;
        int b = matrix.length - 1;
        //结果集index
        int index = 0;
        int[] res = new int[(r+1) * (b+1)];
        while(true){
            //从左到右
            for(int i = l; i <= r; i++){
                res[index++] = matrix[t][i];
            }
            if(++t > b){
                break;
            }
            //从上到下
            for(int i = t; i <= b; i++){
                res[index++] = matrix[i][r];
            }
            if(--r < l){
                break;
            }
            //从右到左
            for(int i = r; i >= l; i--){
                res[index++] = matrix[b][i];
            }
            if(--b < t){
                break;
            }
            //从下到上
            for(int i = b; i >= t; i--){
                res[index++] = matrix[i][l];
            }
            if(++l > r){
                break;
            }
        }
        return res;
    }
}
```

- 时间复杂度：*O*(MN）M,N分别为矩阵行数和列数

- 空间复杂度：O(1) 无额外空间