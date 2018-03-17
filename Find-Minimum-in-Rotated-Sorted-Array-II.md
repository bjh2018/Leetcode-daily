Find Minimum in Rotated Sorted Array II
====

1.问题描述
---

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.<br>
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).<br>
Find the minimum element.<br>
The array may contain duplicates.<br>
假设某升序的数组在某个关键的点处旋转，数组中可能含有重复的数字，找出数组中最小的数。

2.思路
---

用暴力的方法，直接先把第一个当做是最小的数，再遍历数组，让它和后面的元素比较，取其中较小的数，最终返回即可。

3.代码I
---

```c
int findMin(int* nums, int numsSize) {
    int ans=nums[0];
    for (int i=1; i<numsSize; i++) {
        if (ans>nums[i]) {
            ans=nums[i];
        }
    }
    return ans;
}
```

4.代码II
---

```c
int findMin(int* nums, int numsSize) {
    int start=0;
    int end=numsSize-1;
    
    while (start<end) {
        int mid=(start+end)/2;
        
        //注意这里找的是最小值
        //nums[mid]大于nums[end]，说明最小值在最右边
        //反之，最小值在最左边
        if (nums[mid]>nums[end]) {
            start=mid+1;
        }
        else if (nums[mid]<nums[end]) {
            end=mid;
        }
        
        //当mid==end时候,end--
        else {
            end--;
        }
    }
    
    return nums[end];
    //这里返回nums[start]或者nums[end]都是可以的
}    
```
