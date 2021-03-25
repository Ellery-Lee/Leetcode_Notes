#### [剑指 Offer 32. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/solution/mian-shi-ti-32-iii-cong-shang-dao-xia-da-yin-er--3/)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。



## 方法一：层序遍历+双端队列 99.7%

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
        //双端队列
        Queue<TreeNode> queue = new LinkedList<>();
        //结果集
        List<List<Integer>> res = new ArrayList<>();
        if(root != null){
            queue.add(root); 
        } 
        while(!queue.isEmpty()){
            //单层结果集
            LinkedList<Integer> temp = new LinkedList<>();
            //队列长度需要存入变量，否则在for循环会不断更新
            int length = queue.size();
            for(int i = 0; i < length; i++){
                TreeNode node = queue.poll();
                //偶数层顺序放入
                if(res.size() % 2 == 0){
                    temp.addLast(node.val);
                }else{//奇数层逆序放入
                    temp.addFirst(node.val);
                }
                //当前节点子节点放入队列
                if(node.left != null){
                    queue.add(node.left);
                }
                if(node.right != null){
                    queue.add(node.right);
                }
            }
            //结果集添加当前层结果集
            res.add(temp);
        }
        return res;
    }
}
```

时间复杂度：O(N) ： *N* 为二叉树的节点数量，即 BFS 需循环 *N* 次，占用 O*(*N*) ；双端队列的队首和队尾的添加和删除操作的时间复杂度均为 O*(1) 。

空间复杂度 O(N) ：最差情况下，即当树为满二叉树时，最多有 N*/2 个树节点 **同时** 在 `deque` 中，使用 O*(*N*) 大小的额外空间。