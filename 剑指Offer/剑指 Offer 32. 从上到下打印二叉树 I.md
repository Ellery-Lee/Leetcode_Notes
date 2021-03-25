#### [剑指 Offer 32. 从上到下打印二叉树 I](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。



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
    public int[] levelOrder(TreeNode root) {
        if(root == null){
            return new int[0];
        }
        Deque<TreeNode> queue =new ArrayDeque<>();
        queue.offer(root);
        ArrayList<Integer> res = new ArrayList<>();
        while(!queue.isEmpty()){
            int size = queue.size();
            for(int i = 0; i < size; i++){
                TreeNode temp = queue.poll();
                res.add(temp.val);
                if(temp.left != null){
                    queue.offer(temp.left);
                }
                if(temp.right != null){
                    queue.offer(temp.right);
                }
            }
        }
        int[] ans = new int[res.size()];
        for(int i = 0 ; i < res.size(); i++){
            ans[i] = res.get(i);
        }
        return ans;
    }
}
```

时间复杂度：O(N) ： *N* 为二叉树的节点数量，即 BFS 需循环 *N* 次，占用 O*(*N*) 

空间复杂度 O(N) ：最差情况下，即当树为满二叉树时，最多有 N*/2 个树节点 **同时** 在 `deque` 中，使用 O*(*N*) 大小的额外空间。