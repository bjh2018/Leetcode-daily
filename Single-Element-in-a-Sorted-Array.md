Single Element in a Sorted Array
===

1.问题描述
---

Given a sorted array consisting of only integers where every element appears twice except for one element which appears once. Find this single element that appears only once.<br> 
Example 1:<br>
Input: [1,1,2,3,3,4,4,8,8]<br>
Output: 2<br>
<br>
Example 2:<br>
Input: [3,3,7,7,10,11,11]<br>
Output: 10<br>
给定一个按顺序排好的数组，除一个数外，其他数都出现两次，找出这个只出现一次的数，并返回。

2.思路
---

（1）首先想到的就是用异或来实现，因为别的数都出现了两次，相同的数异或结果为0，0和任何数异或的结果都是它本身。<br>
（2）但是这道题是按顺序排列的，所以可以让前一个数与其后一个数比较，要注意的是下标是以2为单位上涨的。

3.代码I
---

```c
int singleNonDuplicate(int* nums, int numsSize) {
    int ans=0;
    for (int i=0; i<numsSize; i=i+2) {
        if (nums[i]!=nums[i-1]) {
            ans=nums[i];
        }
    }
    return ans;
}
```

4.代码II
---

```c
int singleNonDuplicate(int* nums, int numsSize) {
    int ans=0;
    for (int i=0; i<numsSize; i=i+1) {
        ans=ans^nums[i];
    }
    return ans;
}
```
