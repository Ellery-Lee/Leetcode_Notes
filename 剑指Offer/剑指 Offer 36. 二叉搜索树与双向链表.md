# 剑指 Offer 36. 二叉搜索树与双向链表

- 题目要求：输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。



## 方法一：中序遍历DFS 100%

```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val,Node _left,Node _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
    Node lastNode = null;
    public Node treeToDoublyList(Node root) {
        if(root == null){
            return null;
        }
        inorder(root);
        Node headNode = lastNode;
        while(headNode != null && headNode.left != null){
            headNode = headNode.left;
        }
        headNode.left = lastNode;
        lastNode.right = headNode;
        return headNode;
    }
    public void inorder(Node root){
        if(root == null){
            return;
        }
        inorder(root.left);

        if(lastNode != null){
            lastNode.right = root;
        }
        root.left = lastNode;
        lastNode = root;

        inorder(root.right);
    }
}
```

- 时间复杂度：*O*(n）每个结点都要遍历

- 空间复杂度：O(n) 最坏情况

