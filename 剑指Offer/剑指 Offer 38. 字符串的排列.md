# [剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

- 输入一个字符串，打印出该字符串中字符的所有排列。你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

## 方法一：回溯 42.52%

```java
class Solution {
    //结果集
    List<String> res = new ArrayList<>();
    //单个序列
    char[] seq;
    public String[] permutation(String s) {
        if(s == null || s.length() == 0){
            return new String[0];
        }
        seq = s.toCharArray();
        backtracking(0);
        return res.toArray(new String[res.size()]);
    }
    
    //回溯法
    public void backtracking(int index){
        //如果固定位置到达序列末端，将此序列加入结果集，返回
        if(index == seq.length - 1){
            res.add(String.valueOf(seq));
            return;
        }
        //去重哈希表
        Set<Character> set = new HashSet<>();
        for(int i = index; i < seq.length; i++){
            if(set.contains(seq[i])){
                continue;
            }
            //将seq[i]加入去重集
            set.add(seq[i]);
            //固定seq[i]元素
            swap(i, index);
            //继续递归推进
            backtracking(index+1);
            //取消固定seq[i]元素
            swap(i, index);
        }
    }

    public void swap(int i, int j){
        char temp = seq[i];
        seq[i] = seq[j];
        seq[j] = temp;
    }
}
```

- 时间复杂度：*O*(N!N）排列次数N*(N-1)*(N-2)*(N-3)...字符串拼接O(N)

- 空间复杂度：O(n^2^) 递归深度N，辅助去重setN，总共O(N^2^)

