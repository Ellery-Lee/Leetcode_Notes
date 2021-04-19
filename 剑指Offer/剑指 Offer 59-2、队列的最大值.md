# [剑指offer59-2、队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/submissions/)

- 题目要求：请定义一个队列并实现函数 max_value 得到队列里的最大值，要求函数max_value、push_back 和 pop_front 的均摊时间复杂度都是O(1)。

  若队列为空，pop_front 和 max_value 需要返回 -1


## 方法一：单调队列 28.93%

```java
class MaxQueue {
    //队列
    Queue<Integer> queue;
    //单调不增队列，维护最大值
    Deque<Integer> deque;
    public MaxQueue() {
        queue = new LinkedList<>();
        deque = new ArrayDeque<>();
    }
    
    public int max_value() {
        if(deque.isEmpty()){
            return -1;
        }
        return deque.peekFirst();
    }
    
    public void push_back(int value) {
        queue.offer(value);
        while(!deque.isEmpty() && value > deque.peekLast()){
            deque.pollLast();
        }
        deque.offerLast(value);
    }
    
    public int pop_front() {
        if(queue.isEmpty()){
            return -1;
        }else if(deque.peekFirst().equals(queue.peek())){
            deque.pollFirst();
        }
        return queue.poll();
    }
}

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue obj = new MaxQueue();
 * int param_1 = obj.max_value();
 * obj.push_back(value);
 * int param_3 = obj.pop_front();
 */
```

- 时间复杂度：O(1)
- 空间复杂度：O(N) 单调队列
- **注意：Integer比较这里使用”==“不通过，使用”equals“全部通过。**使用”==“会把相同值的两个对象判断为”false“(除-128~127)， Integer重写了equals方法，所以使用”==“比较地址，”equals“比较值。

