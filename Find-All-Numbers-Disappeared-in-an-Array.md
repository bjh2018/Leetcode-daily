Find All Numbers Disappeared in an Array
===

1.问题描述
---

Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.<br>
Find all the elements of [1, n] inclusive that do not appear in this array.<br>
Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.<br>
Example: <br>
Input:<br>
[4,3,2,7,8,2,3,1]<br>
<br>
Output:<br>
[5,6]<br>
给定一个数组，数组中元素的大小a在一定的范围内，1<=a<=n，其中n为数组的长度，数组中的元素可能会出出现一次，也可能会出现两次，找出数组中缺失的元素。

2.思路
---

运用正负标记法就可以解决。可以看出数组中的元素和它的下标有一定的关系，把下标加一的话就是数组中应该有的所有的元素。所以可以把当前的元素减一，把以它为下标的元
素全部都设成负值，最后再遍历一边数组，把其中为正数的元素的下标加一就是要找的消失的元素。

3.代码
---

```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* findDisappearedNumbers(int* nums, int numsSize, int* returnSize) {
    for (int i=0; i<numsSize; i++) {
        int idx = abs(nums[i]) - 1;
        nums[idx] = (nums[idx] > 0) ? -nums[idx] : nums[idx];
    }
    int *ans=(int *)malloc(sizeof(int)*numsSize);
    int sum=0;
    for (int i=0; i<numsSize; i++) {
        if (nums[i]>0) {
            ans[sum]=i+1;
            sum++;
        }
    }
    *returnSize=sum;
    return ans;
}
```

4.代码II
---

```c
int* findDisappearedNumbers(int* nums, int numsSize, int* returnSize) {
 int* histogram = (int*) malloc(sizeof(int) * (numsSize + 1)); 
    memset(histogram, 0, sizeof(int) * numsSize);

    for (int index = 0; index < numsSize; index++) {
        histogram[nums[index]]++;
    }

    histogram[0] = 1;
    for (int index = 1; index <= numsSize; index++) {
        if (histogram[index] == 0) {
            histogram[histogram[0]] = index;
            histogram[0]++;
        }
    }
    *returnSize = histogram[0] - 1;
    return &histogram[1];
}
```

这个代码也是利用了元素和下标之间的关系，用histogram[0]来记录所找元素的个数，把元素存在histogram[1]之后的元素中。

