# 剑指offer56-1、[数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

- 题目要求：一个整型数组 `nums` 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

## 方法：位运算

```java
class Solution {
    public int singleNumber(int[] nums) {
        int[] bitSum = new int[32];
        for(int i = 0; i < nums.length; i++){
            int bitMask = 1;
            for(int j = 31; j >= 0; j--){
                if((bitMask & nums[i]) != 0){
                    bitSum[j]++;
                }
                bitMask = bitMask << 1;
            }
        }
        int ans = 0;
        for(int i = 0; i < bitSum.length; i++){
            ans = ans << 1;
            ans += bitSum[i] % 3;
        }
        return ans;
    }
}
```

**思路：**如果一个数字出现三次，那么它的二进制表示的每一位(0或1)也出现三次，如果把所有出现三次的数字的二进制表示的每一位都分别加起来，那么每一位的和都能被3整除。把每一位都和三整除，余数就是出现一次的数字对应的二进制位。