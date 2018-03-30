First Missing Positive
===

1.问题描述
---

Given an unsorted integer array, find the first missing positive integer. <br>
For example,<br>
Given [1,2,0] return 3,<br>
and [3,4,-1,1] return 2. <br>
Your algorithm should run in O(n) time and uses constant space.<br>
给出一个未分类的整型数组，找出缺失的第一个正整数，正整数是从1开始的。

2.思路
---

数组是未分类的，所以数组中的数既有正数也有负数，故可知证书的范围在1到数组的长度之间，我们只需要把在范围内的数都该成满足nums[i]=i+1的形式，然后再通过一次遍历找出不满足条件的
整数返回即可。

3.代码I
---

```c
if (numsSize==0) return 1;
    for (int i=0; i<numsSize; i++) {
        if (nums[i]>=1&&nums[i]<=numsSize&&nums[nums[i]-1]!=nums[i]) {
            int temp=nums[nums[i]-1];
            nums[nums[i]-1]=nums[i];
            nums[i]=temp;
            i--;//nums[i]的值发生了改变，所以i要减1，再重新判断是否满足条件
        }
    }
    int i;
    for (i=0; i<numsSize; i++) {
        if (nums[i]!=i+1) {
            break;
        }
    }
    return i+1;
    }
```

4.代码II
---

```c
int firstMissingPositive(int* nums, int numsSize) {
    int i = 0;
    int p = numsSize;

    while (i < p) {
        int n = nums[i];
        if (n == i+1)
            ++i;                 // Found it! Look for the next one.
        else if (n < 1 || n > p || n == nums[n-1])
            nums[i] = nums[--p]; // Useless. Get new candidate from the end.
        else {
            nums[i] = nums[n-1]; // Within range; put it in the right place.
            nums[n-1] = n;
        }
    }

    return p + 1;

}
```

这个代码是把不满足条件的都调到后面去，最后数组的排列中缺少的第一个正数就是p+1，其中比较特殊的是当前的元素比该等于的数要大，也要把它调到后面去。
