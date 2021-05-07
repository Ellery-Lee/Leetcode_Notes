#### [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/submissions/)

输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。

## 方法一：回溯 100%

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    List<List<Integer>> ans = new ArrayList<>();
    public List<List<Integer>> pathSum(TreeNode root, int target) {
        //临时路径
        LinkedList<Integer> temp = new LinkedList<>();
        backTracking(root, target, temp);
        return ans;
    }
    public void backTracking(TreeNode root, int target, LinkedList<Integer> temp){
        //回溯出口
        if(root == null){
            return;
        }
        //加入当前路径
        temp.addLast(root.val);
        //满足路径条件
        if(root.val == target && root.left == null && root.right == null){
            List<Integer> list = new LinkedList<>(temp);
            ans.add(list);
        }
        backTracking(root.left, target - root.val, temp);
        backTracking(root.right, target - root.val, temp);
        //回溯，删除上一路径节点
        temp.removeLast();
    }
}
```

- 时间复杂度：*O*(n）遍历每个节点
- 空间复杂度：O(log(n)最长从根节点到叶节点的一条路径 