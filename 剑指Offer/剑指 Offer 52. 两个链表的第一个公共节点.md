# 剑指 Offer 52. 两个链表的第一个公共节点

- 题目要求：输入两个链表，找出它们的第一个公共节点。




## 方法一：指针遍历 100%

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null){
            return null;
        }
        ListNode pA = headA;
        ListNode pB = headB;
        while(pA != pB){
            pA = pA.next;
            pB = pB.next;
            //这个if很重要
            if(pA != pB){
                if(pA == null){
                    pA = headB;
                }else if(pB == null){
                    pB = headA;
                }
            }
        }
        return pA;
    }
}
```

- 时间复杂度：O（n)
- 空间复杂度：O（1）
- **思路**：两次遍历一定能出结果，A+B长度相同，都走了这么多路，注意if很重要，如果没有相交节点，就需要跳出，不然会出现空指针异常。



- timeline

1. ~~2020.7.31-~~
2. 2020.8.1
3. 2020.8.2
4. 2020.8.7
5. 2020.8.14
6. 2020.8.29