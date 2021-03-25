#### [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/solution/jian-zhi-offer-35-fu-za-lian-biao-de-fu-zhi-ha-xi-/)

请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

## 方法一：哈希表 100%

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null){
            return null;
        }
        Map<Node, Node> dic = new HashMap<>();
        Node cur = head;
        //复制各结点，建立“原节点 -> 新节点” 的 Map 映射
        while(cur != null){
            dic.put(cur, new Node(cur.val));
            cur = cur.next;
        }
        cur = head;
        //构建新链表的 next 和 random 指向
        while(cur != null){
            Node temp = dic.get(cur);
            temp.next = dic.get(cur.next);
            temp.random = dic.get(cur.random);
            cur = cur.next;
        }
        //返回新链表的头结点
        return dic.get(head);
    }
}
```

- 时间复杂度：*O*(n）遍历两遍全部结点

- 空间复杂度：O(n) 建立所有结点的映射



## 方法二：拼接+拆分 100%

```java
/*
// Definition for a Node.
class Node {
    int val;
    Node next;
    Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
*/
class Solution {
    public Node copyRandomList(Node head) {
        if(head == null){
            return null;
        }
        //复制各节点，并构建拼接链表
        Node cur = head;
        while(cur != null){
            Node temp = new Node(cur.val);
            temp.next = cur.next;
            cur.next = temp;
            cur = temp.next;
        }
        //构建各新节点的 random 指向
        cur = head;
        while(cur != null){
            if(cur.random != null){
                cur.next.random = cur.random.next;
            }
            cur = cur.next.next;
        }
        //拆分两链表
        cur = head.next;
        Node pre = head;
        Node res = head.next;
        while(cur.next != null){
            pre.next = pre.next.next;
            cur.next = cur.next.next;
            pre = pre.next;
            cur = cur.next;
        }
        pre.next = null;//单独处理原链表尾节点
        return res;//返回新链表头节点
    }
}
```

- 时间复杂度：*O*(n）遍历三遍全部结点

- 空间复杂度：O(1) 无额外空间