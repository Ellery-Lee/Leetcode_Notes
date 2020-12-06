# NC88、寻找第K大[答案参考](https://blog.csdn.net/roamer_nuptgczx/article/details/52106972)

- 题目要求：给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

```
[1,3,5,2,2],5,3
返回：2
```



## 方法一：快排

```java
import java.util.*;

public class Finder {
    public int findKth(int[] a, int n, int K) {
        QuickSort(a, 0, n-1);
        return a[n-K];
    }
    public void QuickSort(int[] nums, int left, int right){
        //为了递归需要left和right指针
        //如果left和right指向同一个位置返回，递归结束条件
        if(right - left < 1){
            return;
        }
        //执行三数中值分割法，找到pivot
        int pivot = findPivot(nums, left, right);
//        int pivot = left + (right - left) / 2;
        //把pivot放在数组最右边
        swap(nums, pivot, right);
        //左右两指针向中间遍历，r = right-1是因为最右边是pivot元素
        int l = left;
        int r = right - 1;
        //当l=r时跳出，说明到达分割点
        while(l < r){
            while(l < r && nums[l] <= nums[right]){
                l++;
            }
            while(l < r && nums[r] >= nums[right]){
                r--;
            }
            if(l < r){
                //交换左右两指针
                swap(nums, l, r);
            }else{
                //l==r，跳出，进行递归
                break;
            }
        }
        //把最右边的pivot换到分割点，以r分割
        swap(nums, right, r);
        //遍历
        QuickSort(nums, left, r-1);
        QuickSort(nums, r+1, right);
    }
    
    public void swap(int[] nums, int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    public int findPivot(int[] nums, int left, int right){
        int mid = left + (right - left) / 2;
        if(nums[left] > nums[mid]){
            swap(nums, left, mid);
        }
        if(nums[left] > nums[right]){
            swap(nums, left, right);
        }
        if(nums[mid] > nums[right]){
            swap(nums, mid, right);
        }
        return mid;
    }
}
```

