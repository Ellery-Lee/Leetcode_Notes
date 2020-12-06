#### [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

- 题目要求：输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。



## 方法一：递归 48.45%

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
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder == null || inorder == null){
            return null;
        }
        return hepler(preorder, inorder, 0, preorder.length - 1, 0, inorder.length - 1);
    }
    public TreeNode hepler(int[] preorder, int[] inorder, int preStart, int preEnd, int inStart, int inEnd){
        if(preStart > preEnd || inStart > inEnd){
            return null;
        }
        int temp = preorder[preStart];
        TreeNode node = new TreeNode(temp);
        int leftLength = 0;
        int midIndex = 0;
        for(int i = inStart; i <= inEnd; i++){
            if(inorder[i] == temp){
                leftLength = i - inStart;
                midIndex = i;
            }
        }
        node.left = hepler(preorder, inorder, preStart + 1, preStart + leftLength, inStart, midIndex - 1);
        node.right = hepler(preorder, inorder, preStart + leftLength + 1, preEnd, midIndex + 1, inEnd);
        return node;
    }
}
```

- 时间复杂度：*O*(n^2) 每个根节点都要O(n)查找
- 空间复杂度：O(n) 递归栈
- 思路：先序遍历和中序遍历的特点，先序遍历确定根节点，中序遍历分割左右子树



## 方法二：Map优化递归

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
    Map<Integer, Integer> map = new HashMap<>();
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if(preorder == null || inorder == null){
            return null;
        }
        for(int i = 0; i < inorder.length; i++){
            map.put(inorder[i], i);
        }
        return hepler(preorder, inorder, 0, preorder.length - 1, 0, inorder.length - 1);
    }
    public TreeNode hepler(int[] preorder, int[] inorder, int preStart, int preEnd, int inStart, int inEnd){
        if(preStart > preEnd || inStart > inEnd){
            return null;
        }
        int temp = preorder[preStart];
        TreeNode node = new TreeNode(temp);
        int midIndex = map.get(temp);
        int leftLength = midIndex - inStart;
        node.left = hepler(preorder, inorder, preStart + 1, preStart + leftLength, inStart, midIndex - 1);
        node.right = hepler(preorder, inorder, preStart + leftLength + 1, preEnd, midIndex + 1, inEnd);
        return node;
    }
}
```

- 时间复杂度：*O*(n) 遍历，优化后没有寻找的复杂度
- 空间复杂度：O(n) 递归栈
- 思路：先序遍历和中序遍历的特点，先序遍历确定根节点，中序遍历分割左右子树



9.21