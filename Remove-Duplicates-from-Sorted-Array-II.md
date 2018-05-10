Remove Duplicates from Sorted Array II
===

1.问题描述
---

Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.<br>
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.<br>
Example 1:<br>
Given nums = [1,1,1,2,2,3],<br>
<br>
Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.<br>
<br>
It doesn't matter what you leave beyond the returned length.<br>
Example 2:<br>
Given nums = [0,0,1,1,1,1,2,3,3],<br>
<br>
Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.<br>
<br>
It doesn't matter what values are set beyond the returned length.<br>
Clarification:<br>
Confused why the returned value is an integer but your answer is an array?<br>
Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.<br>
Internally you can think of this:<br>
// nums is passed in by reference. (i.e., without making a copy)<br>
int len = removeDuplicates(nums);<br>
<br>
// any modification to nums in your function would be known by the caller.<br>
// using the length returned by your function, it prints the first len elements.<br>
for (int i = 0; i < len; i++) {<br>
    print(nums[i]);<br>
}<br>
给定一个有序数组nums，就地删除重复项，使得重复项至多出现两次并返回新的长度。不要为其他数组分配额外空间，必须通过在O（1）额外内存中就地修改输入数组来实现此目的<br>

2.思路
---

可以用一个index来记录新生成的数组的元素，如果当前元素不等于它前一个元素，就把它加到新的数组中，或者i=1，或者当前的元素不等于新数组的前两个元素，就再把它加上。

3.代码
---

```c
int removeDuplicates(int* nums, int numsSize) {
    if (numsSize==0) return 0;
    int i=1,index=1;
    for (i=1; i<numsSize; i++) {
        if (nums[i]!=nums[i-1]||i==1||nums[i]!=nums[index-2]) {
            nums[index++]=nums[i];
        }
    }
    return index;
}
```
