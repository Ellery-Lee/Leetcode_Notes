# [剑指 Offer 54.  二叉搜索树的第K大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/submissions/)

- 题目要求：给定一棵二叉搜索树，请找出其中第k大的节点。




## 方法一：中序遍历(倒序) 100%

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
    int index = -1;
    int res = -1;
    public int kthLargest(TreeNode root, int k) {
        this.index = k;
        inOrder(root);
        return res;
    }
    public void inOrder(TreeNode root){
        if(root == null){
            return;
        }
        inOrder(root.right);
        if(index == 0){
            return;
        }
        if(--index == 0){
            res = root.val;
        }
        inOrder(root.left);
    }
}
```

- 时间复杂度：O（n)遍历
- 空间复杂度：O（n）递归栈

