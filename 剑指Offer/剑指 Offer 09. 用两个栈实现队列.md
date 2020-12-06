#### [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

- 题目要求：用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 



## 方法一：两个栈 84.12%

```java
class CQueue {
    Deque<Integer> stack1;
    Deque<Integer> stack2;
    public CQueue() {
        stack1 = new ArrayDeque<>();
        stack2 = new ArrayDeque<>();
    }
    
    public void appendTail(int value) {
        stack2.push(value);
    }
    
    public int deleteHead() {
        if(stack1.isEmpty()){
            while(!stack2.isEmpty()){
                stack1.push(stack2.pop());
            }
        }
        return stack1.isEmpty() ? -1 : stack1.pop();
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```

- 时间复杂度：*O*(n) 移动
- 空间复杂度：O(n) 栈
- 思路：左右两个栈，右边的栈入，左边的栈出，如果左边的栈为空，把右边的栈数字依次弹出压入左边栈可以实现。



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