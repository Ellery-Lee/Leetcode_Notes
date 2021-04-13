# [剑指 Offer 40、最小的K个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

- 题目要求：输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。


## 方法一：快排 53.22%

```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        quickSort(arr, 0, arr.length - 1);
        return Arrays.copyOf(arr, k);
    }

    public void quickSort(int[] arr, int low, int high){
        //终止条件
        if(low >= high){
            return;
        }
        //左指针
        int left = low;
        //右指针
        int right = high;
        //pivot参考值，这里选取第一个元素
        int pivotValue = arr[low];
        while(left < right){
            //右指针左移,这里必须先判断右指针，这样能保证跳出的时候左指针是指向小于等于pivot的值(因为pivot取的时最左边的，如果时最右边就先判断左指针)
            while(left < right && arr[right] >= pivotValue){
                right--;
            }
            //左指针右移
            while(left < right && arr[left] <= pivotValue){
                left++;
            }
            //此时两指针指向元素都不满足规则(arr[left] > pivotValue && arr[right] < pivotValue)或者left==right，交换两指针
            swap(arr, left, right);
        }
        //把pivotValue值放入分界点
        swap(arr, low, left);
        quickSort(arr, low, left - 1);
        quickSort(arr, left + 1, high);
    }

    public void swap(int[] arr, int i, int j){
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```

- 时间复杂度：*O*（nlog(n)）快排
- 空间复杂度：O（n）递归栈最差情况
- **思路**：快排数组，返回前k个数
