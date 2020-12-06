#### [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

- 题目要求：输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。



## 方法一：stack 43.17%

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
    public int[] reversePrint(ListNode head) {
        if(head == null){
            return new int[0];
        }
        Deque<Integer> stack = new ArrayDeque<>();
        while(head != null){
            stack.push(head.val);
            head = head.next;
        }
        int[] ans = new int[stack.size()];
        int i = 0;
        while(!stack.isEmpty()){
            ans[i++] = stack.pop();
        }
        return ans;
    }
}
```

- 时间复杂度：*O*(n）两次遍历
- 空间复杂度：O(n) 栈
- 思路：后进先出，使用栈结构



## 方法二：递归 43.17%

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
    List<Integer> temp;
    public int[] reversePrint(ListNode head) {
        if(head == null){
            return new int[0];
        }
        temp = new ArrayList<>();
        helper(head);
        int[] ans = new int[temp.size()];
        for(int i = 0; i < temp.size(); i++){
            ans[i] = temp.get(i);
        }
        return ans;
    }
    public void helper(ListNode head){
        if(head == null){
            return;
        }
        helper(head.next);
        temp.add(head.val);
        return;
    }
}
```

- 时间复杂度：*O*(n）两次遍历
- 空间复杂度：O(n)  递归栈
- 思路：后进先出，使用栈结构



9.21