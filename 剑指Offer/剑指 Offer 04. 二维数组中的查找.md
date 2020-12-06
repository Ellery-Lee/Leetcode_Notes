#### 剑指 Offer 04. 二维数组中的查找

- 题目要求：在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。



## 方法一：二叉搜索树 100%

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0){
            return false;
        }
        int i = 0;
        int j = matrix[0].length - 1;
        while(i <= matrix.length - 1 && j >= 0){
            if(matrix[i][j] == target){
                return true;
            }else if(matrix[i][j] > target){
                j--;
            }else if(matrix[i][j] < target){
                i++;
            }
        }
        return false;
    }
}
```

- 时间复杂度：*O*(n）最坏情况遍历一遍
- 空间复杂度：O(1) 没有额外空间
- 思路：如果从矩阵左上角和右下角走会不好判断，但如果从右上角和左下角走相当于搜索二叉树，比如从右上角走，当前值跟target比较，如果大，就往左走，当前列砍掉，如果小，就往下走，当前行砍掉。相当于搜索树的左右两个结点。



9.19