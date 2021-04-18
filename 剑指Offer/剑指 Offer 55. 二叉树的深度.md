# [剑指 Offer 55.  二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/submissions/)

- 题目要求：输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。




## 方法一：后序遍历 100%

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
    public int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}
```

- 时间复杂度：O（n)遍历
- 空间复杂度：O（n）递归栈

