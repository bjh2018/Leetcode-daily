Find Pivot Index
===

1.问题描述
---

Given an array of integers nums, write a method that returns the "pivot" index of this array.br> 
We define the pivot index as the index where the sum of the numbers to the left of the index is equal to the sum of the numbers to the right of the index. <br>
If no such index exists, we should return -1. If there are multiple pivot indexes, you should return the left-most pivot index. <br>
Example 1:<br>
Input: <br>
nums = [1, 7, 3, 6, 5, 6]<br>
Output: 3<br>
Explanation: <br>
The sum of the numbers to the left of index 3 (nums[3] = 6) is equal to the sum of numbers to the right of index 3.<br>
Also, 3 is the first index where this occurs.<br>
<br>
Example 2:<br>
Input: <br>
nums = [1, 2, 3]<br>
Output: -1<br>
Explanation: <br>
There is no index that satisfies the conditions in the problem statement.<br>
给定一个数组，看是否存在一个元素，它左面的元素和它右边的元素的和相同，如果存在，就返回它的下标，如果存在多个这样的数，就返回最左边的使之成立的数的下标。如果不存在，就返回-1.

2.思路
---

因为当存在多个这样的数时，要返回的是最左边的数，所以就把第一个数右面的数都加起来，然后把左边的数先置为0，再通过减右边，加左边的来判断左右相加之和是否为0.

3.代码
---

```c
int pivotIndex(int* nums, int numsSize) {
    int ans=0;
    int rsum=0,lsum=0;
    for (int i=1; i<numsSize; i++)
        rsum+=nums[i];
    while (ans<numsSize) {
        if (rsum==lsum) return ans;
        rsum-=nums[ans+1];
        lsum+=nums[ans];
        ans++;
    }
    return -1;
}
```

