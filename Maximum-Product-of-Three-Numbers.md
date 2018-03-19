 Maximum Product of Three Numbers
 ===
 
 1.问题描述
 ---
 
 Given an integer array, find three numbers whose product is maximum and output the maximum product.<br>
Example 1:<br>
Input: [1,2,3]<br>
Output: 6<br>
<br>
Example 2:<br>
Input: [1,2,3,4]<br>
Output: 24<br>
给定一个数组，找出其中的三个元素，使它们的乘积最大，并返回这个最大值。

2.思路
---

因为已经确定了相乘的数的个数，所以只需要找乘积的最大值即可，如果把数组按照从小到大的顺序排列的话，就可以得到两种情况，如果数组中全是正数，那么最大值就是最后三个
数的乘积，如果数组中有负数的话，负数的个数为1时，最大值还是最后三个数的乘积，但如果负数的个数大于1的话，最大的数很有可能是前两个数和最后一个数的乘积，所以要讨论
两种情况，就可以得到结果。

3.代码
---

```c
int comp(const void *a, const void *b) {
    return *(int *)a-*(int*)b;
}
int maximumProduct(int* nums, int numsSize) {
    qsort(nums,numsSize,sizeof(int),comp);
    int max1=nums[0]*nums[1]*nums[numsSize-1];
    int max2=nums[numsSize-1]*nums[numsSize-2]*nums[numsSize-3];
    return max1>max2?max1:max2;
}
```
