# 剑指 Offer 39、数组中出现次数超过一半的数字

- 题目要求：数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

- ```
  输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
  输出: 2
  ```

## 方法一：排序 78.56%

```java
class Solution {
    public int majorityElement(int[] nums) {
        if(nums == null && nums.length == 0){
            return -1;
        }
        Arrays.sort(nums);
        return nums[nums.length / 2];
    }
}
```

- 时间复杂度：*O*（nlog(n)）归并排序
- 空间复杂度：O（1）没有用到额外空间
- **思路**：因为个数超过一半，所以数组中间的数字一定是要找的数字。

## 方法二：分治算法

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        if(lists == null && lists.length == 0){
            return null;
        }
        
        ListNode dummy = new ListNode();
        ListNode temp = dummy;

        PriorityQueue<ListNode> pq = new PriorityQueue<>(new Comparator<ListNode>(){
            //@override
            public int compare(ListNode l1, ListNode l2){
                return l1.val - l2.val;
            }

        });

        for(int i = 0; i < lists.length; i++){
            if(lists[i] == null){
                continue;
            }else{
                pq.offer(lists[i]);
            }
        }

        while(!pq.isEmpty()){
            ListNode nextnode = pq.poll();
            temp.next = nextnode;
            temp = temp.next;
            if(nextnode.next != null){
                pq.offer(nextnode.next);
            }
        }
        return dummy.next;
    }
}
```

- 时间复杂度：*O*（nk*log(k)）每个元素访问需要log（k）因为优先队列是用堆实现的，也就是二叉树。总共有nk个元素，k是链表个数
- 空间复杂度：O（k）优先队列空间
- **思路**：优先队列法，把每个链表的当前最小节点放入队列中排序，每次从队列取出最小节点安放在结果链表尾部，知道队列中没有节点，返回链表。



- timeline

1. ~~2020.7.8-~~
2. 2020.7.9
3. 2020.7.10
4. 2020.7.15
5. 2020.7.22
6. 2020.8.6