Count of Smaller Numbers After Self
====

1.问题描述
---

You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].<br>
Example:<br>
Given nums = [5, 2, 6, 1]<br>
<br>
To the right of 5 there are 2 smaller elements (2 and 1).<br>
To the right of 2 there is only 1 smaller element (1).<br>
To the right of 6 there is 1 smaller element (1).<br>
To the right of 1 there is 0 smaller element.<br>
Return the array [2, 1, 1, 0]. <br>
给一个数组，找出数组中各个元素的右边比它小的元素的个数，并返回个数组成的数组。

2.思路
---

运用两个循环一次遍历数组即可。

3.代码I
---

```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* countSmaller(int* nums, int numsSize, int* returnSize) {
    int* ans=(int *)malloc(sizeof(int)*numsSize);
    //memset(ans,0,numsSize);
    for (int i=0; i<numsSize-1; i++) {
        ans[i]=0;
        for (int j=i+1; j<numsSize; j++) {
            if (nums[i]>nums[j]) {
                ans[i]=ans[i]+1;
            }
        }
    }
    *returnSize=numsSize;
    ans[numsSize-1]=0;
    return ans;
}
```
