# [剑指offer68-1、二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/submissions/)

- 题目要求：给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。


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
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null){
            return null;
        }
        if(root.val < p.val && root.val < q.val){
            return lowestCommonAncestor(root.right, p, q);
        }else if(root.val > p.val && root.val > q.val){
            return lowestCommonAncestor(root.left, p, q);
        }
        return root;
    }
}
```

- 时间复杂度：O(N)
- 空间复杂度：O(N) 
