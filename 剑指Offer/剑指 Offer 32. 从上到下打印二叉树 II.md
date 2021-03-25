#### [剑指 Offer 32. 从上到下打印二叉树 II](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。



## 方法一：层序遍历 100%

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
    public List<List<Integer>> levelOrder(TreeNode root) {
        if(root == null){
            return new ArrayList<>();
        }
        Deque<TreeNode> queue =new ArrayDeque<>();
        queue.offer(root);
        List<List<Integer>> res = new ArrayList<>();
        while(!queue.isEmpty()){
            int size = queue.size();
            List<Integer> list = new ArrayList<>();
            for(int i = 0; i < size; i++){
                TreeNode temp = queue.poll();
                list.add(temp.val);
                if(temp.left != null){
                    queue.offer(temp.left);
                }
                if(temp.right != null){
                    queue.offer(temp.right);
                }
            }
            res.add(list);
        }
        return res;
    }
}
```

时间复杂度：O(N) ： *N* 为二叉树的节点数量，即 BFS 需循环 *N* 次，占用 O*(*N*) 

空间复杂度 O(N) ：最差情况下，即当树为满二叉树时，最多有 N*/2 个树节点 **同时** 在 `deque` 中，使用 O*(*N*) 大小的额外空间。