#### [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

- 题目要求：把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  




## 方法一：二分查找 44.86%

```java
class Solution {
    public int minArray(int[] numbers) {
        if(numbers == null || numbers.length == 0){
            return 0;
        }
        int lk = 0;
        int rk = numbers.length - 1;
        while(lk < rk){
            int mid = lk + (rk - lk) / 2;
            if(numbers[mid] < numbers[rk]){
                rk = mid;
            }else if(numbers[mid] > numbers[rk]){
                lk = mid + 1;
            }else{
                rk -= 1;
            }
        }
        return numbers[lk];
    }
}
```

- 时间复杂度：*O*(log(n)) 递归
- 空间复杂度：O(1) 没有用到额外空间
- 思路：想的比较复杂，主要还是边界条件的判断，每次判断要跟rk进行比较。
  - 第一种情况是numbers[mid] < numbers[rk]，代表mid在右边的排序数组中，最小值的范围在[lk, mid]闭区间中。
  - 第二种情况是numbers[mid] > numbers[rk]，代表mid在左边的排序数组中，最小值范围在[mid+1, rk]当中。
  - 第三种情况是numbers[mid] == numbers[rk]，mid可能在左排序数组也可能在右排序数组，这个时候不能贸然缩小区间，这时候的处理是把rk-1，对区间做细微改动即可。因为不论mid在哪边，rk有mid代替，取不到rk也可以。
  - 最终返回lk

## 方法二：顺序查找 44.82%

```java
class Solution {
    public int minArray(int[] numbers) {
        if(numbers == null || numbers.length == 0){
            return 0;
        }
        int ans = numbers[0];
        for(int i = 1; i < numbers.length; i++){
            if(ans > numbers[i]){
                ans = numbers[i];
                return ans;
            }
        }
        return ans;
    }
}
```

- 时间复杂度：*O*(n) 顺序查找
- 空间复杂度：O(1) 没有用到额外空间
- 思路：顺序查找进行判断



9.21