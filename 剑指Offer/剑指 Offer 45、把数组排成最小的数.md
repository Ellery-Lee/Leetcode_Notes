# [剑指 Offer 45、把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

- 题目要求：输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。



## 方法一：快速排序 97.31%

```java
class Solution {
    public String minNumber(int[] nums) {
        String[] strs = new String[nums.length];
        for(int i = 0; i < nums.length; i++){
            strs[i] = String.valueOf(nums[i]);
        }
        quickSort(strs, 0, strs.length - 1);
        StringBuilder ans = new StringBuilder();
        for(String s : strs){
            ans = ans.append(s);
        }
        return ans.toString();
    }
    public void quickSort(String[] strs, int left, int right){
        if(left >= right){
            return;
        }
        int l = left;
        int r = right;
        String pivotValue = strs[left];
        while(l < r){
            //pivotValue在前小于在后，右指针左移
            while(l < r && (pivotValue + strs[r]).compareTo(strs[r] + pivotValue) <= 0){
                r--;
            }
            //pivotValue在后小于在前，左指针右移
            while(l < r && (strs[l] + pivotValue).compareTo(pivotValue + strs[l]) <= 0){
                l++;
            }
            //交换不符合要求的l，r两索引或者l==r
            swap(strs, l, r);
        }
        //把pivot放在分界点
        swap(strs, left, l);
        //递归
        quickSort(strs, left, l-1);
        quickSort(strs, l+1, right);
    }

    public void swap(String[] strs, int i, int j){
        String temp = strs[i];
        strs[i] = strs[j];
        strs[j] = temp;
    }
}
```

- 时间复杂度：*O*（nlog(n)）快排
- 空间复杂度：O（n）字符串列表所占空间



## 方法二：lamda表达式 52.30%

```java
class Solution {
    public String minNumber(int[] nums) {
        String[] strs = new String[nums.length];
        for(int i = 0; i < nums.length; i++){
            strs[i] = String.valueOf(nums[i]);
        }
        //lamda表达式,这里是comparator的compare方法，里面用到了String的compareTo方法
        Arrays.sort(strs, (x, y) -> (x+y).compareTo(y+x));
        StringBuilder ans = new StringBuilder();
        for(String s : strs){
            ans = ans.append(s);
        }
        return ans.toString();
    }
}
```

