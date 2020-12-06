# 剑指offer56-2、[数组中数字出现的次数]

- 题目要求：在一个数组 `nums` 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

## 方法：异或法

```java
class Solution {
    public int[] singleNumbers(int[] nums) {
        int temp = 0;
        int[] ans = new int[2];
        for(int i = 0; i < nums.length; i++){
            temp ^= nums[i];
        }
        int lowBit = temp & (-temp);  //负数是正数反码+1，想与得到最低为1
        for(int i : nums){
            if((i & lowBit) == 0){
                ans[0] ^= i;
            }else{
                ans[1] ^= i;
            }
        }
        return ans;
    }
}
```

