Find All Duplicates in an Array
===

1.问题描述
---

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.<br>
Find all the elements that appear twice in this array.<br>
Could you do it without extra space and in O(n) runtime?<br>
<br>
Example:<br>
Input:<br>
[4,3,2,7,8,2,3,1]<br>
<br>
Output:<br>
[2,3]<br>
找出给定数组中重复出现的元素并返回。

2.思路
---

根据题意可得数组中的元素和下标的范围相同，可以通过正负标记法来解决，就想到要把元素减去一得到的下标对应的元素全都变成负数，这样再遇到重复出现得下标时就可以把
它有转成了整数，但是这样是不正确的，因为还有一些数没有出现，就想到在第一次遍历的时侯，如果num[i]<0，而它此时又要加负号，则说明它重复出现了，就可以得出答案，

3.代码
---

```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* findDuplicates(int* nums, int numsSize, int* returnSize) {
    int sum=0;
    int *ans=(int *)malloc(sizeof(int)*numsSize);
    for (int i=0; i<numsSize; i++) {
        int index=abs(nums[i])-1;
        if (nums[index]<0) {
            ans[sum]=abs(index)+1;
            sum++;
        }
        nums[index]=-nums[index];
    }
    *returnSize=sum;
    return ans;
}
```

4.总结
---

要注意在写index的时候不要忘了在nums[i]前面加上取绝对值的函数，因为当遍历到重复的数字时，num[i]已经是一个负数,而元素的下标不可能是负数，还有就是要注意正负标记法的灵活运用。
