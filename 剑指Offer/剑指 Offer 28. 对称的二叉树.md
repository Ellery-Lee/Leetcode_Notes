#### [剑指 Offer 28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

## 方法一：递归 100%

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if(root == null){
            return true;
        }
        return helper(root, root);
    }
    public boolean helper(TreeNode left, TreeNode right){
        //如果左右两子结点都是null，为true
        if(left == null && right == null){
            return true;
        }
        //如果左右两子结点有一个不是null，为false
        if(left == null || right == null){
            return false;
        }
        //要求左右两子结点值相等，left.left=right.right && left.right=right.left
        return left.val == right.val && helper(left.left, right.right) && helper(left.right, right.left);
    }
}
```

- 时间复杂度：*O*(n）最多调用N/2次递归

- 空间复杂度：O(n) 最坏情况，链表