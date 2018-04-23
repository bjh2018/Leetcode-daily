Merge Sorted Array
====

1.问题描述
---

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.<br>
Note:<br>
The number of elements initialized in nums1 and nums2 are m and n respectively.<br>
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.<br>
Example:<br>
Input:<br>
nums1 = [1,2,3,0,0,0], m = 3<br>
nums2 = [2,5,6],       n = 3<br>
<br>
Output: [1,2,2,3,5,6]<br>
把给定的两个数组中的元素都合并到num1中，num1的长度足够大，并且保证合并后的数组是按从大到小的顺序排列的。

2.思路
---

先把num2中的元素都添加到num1的末尾，然后用qsort函数排列即可。

3.代码I
---

```c
int cmp(const void * a, const void *b) {
    return *(int*)a-*(int*)b;
}
void merge(int* nums1, int m, int* nums2, int n) {
    int j=0;
    for (int i=m; i<=m+n-1; i++) {
        nums1[i]=nums2[j++];
    }
    qsort(nums1,m+n,sizeof(int),cmp);
}
```

4.代码II
---

```c
void merge(int* nums1, int m, int* nums2, int n) {
    int i = m - 1, j = n - 1, tar = m + n - 1;
        while (j >= 0) {
            nums1[tar--] = i >= 0 && nums1[i] > nums2[j] ? nums1[i--] : nums2[j--];
        }
}
```

因为这两个数组已经排好序了，所以可以倒序找出较大的数，把它赋给新的数组的最后一位，然后再一直向下进行即可。
