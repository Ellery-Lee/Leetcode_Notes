#### [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

## 方法一：递归分治 100%

```java
class Solution {
    public boolean verifyPostorder(int[] postorder) {
        //分治
        return isBST(postorder, 0, postorder.length - 1);
    }

    //判断[i,j]区间数组是不是二叉搜索树
    public boolean isBST(int[] postorder, int i, int j){
        //左右边界无法构成区间返回true
        if(i >= j){
            return true;
        }
        //从左区间开始遍历，当前结点小于根节点向右移动
        int p = i;
        while(postorder[p] < postorder[j]){
            p++;
        }
        //记录第一个大于根结点的结点的数组索引
        int m = p;
        //从第一个大于根结点的结点开始，当前结点大于根节点向右移动
        while(postorder[p] > postorder[j]){
            p++;
        }
        //需要满足当前结点索引等于右区间结点索引(代表符合二叉搜索树)并且左子树和右子树都为二叉搜索树
        return p == j && isBST(postorder, i, m - 1) && isBST(postorder, m, j-1); 
    }
}
```

- 时间复杂度：*O*(n^2^）每个结点都要遍历,O(N)最坏情况链表每轮遍历所有结点

- 空间复杂度：O(n) 最坏情况，递归深度N