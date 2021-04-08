# 剑指 Offer 37. 序列化二叉树

- 题目要求：请实现两个函数，分别用来序列化和反序列化二叉树。



## 方法一：BFS 58%

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
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        if(root == null){
            return "[]";
        }
        StringBuilder sb = new StringBuilder("[");
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        //层序遍历，null值也放入
        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            if(node != null){
                sb.append(node.val + ",");
                queue.offer(node.left);
                queue.offer(node.right);
            }else{
                sb.append("null,");
            }
        }
        //除去最后一个","加上"]",返回
        return sb.deleteCharAt(sb.length() - 1).append("]").toString();
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if("[]".equals(data)){
            return null;
        }
        //去除[]并分割字符串
        String[] vals = data.substring(1,data.length() - 1).split(",");
        //构建根结点
        TreeNode root = new TreeNode(Integer.parseInt(vals[0]));
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        //因为根结点使用了vals[0]，所以数组遍历从1开始
        int index = 1;
        while(!queue.isEmpty()){
            TreeNode node = queue.poll();
            //如果不是null就创建结点并放入队列
            if(!"null".equals(vals[index])){
                node.left = new TreeNode(Integer.parseInt(vals[index]));
                queue.offer(node.left);
            }
            //数组向后遍历
            index++;
            //如果不是null就创建结点并放入队列
            if(!"null".equals(vals[index])){
                node.right = new TreeNode(Integer.parseInt(vals[index]));
                queue.offer(node.right);
            }
            //数组向后遍历
            index++;
        }
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

- 时间复杂度：*O*(n）每个结点都要遍历
- 空间复杂度：O(n) 最坏情况N/2个结点
- 思路：
  - 序列化：层序遍历，把每个结点都放入队列（包括null），输出字符串
  - 反序列化：借助字符串数组遍历，构建结点的左右子节点

