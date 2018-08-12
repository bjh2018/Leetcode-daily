Median of Two Sorted Arrays
===

1.问题描述
---

There are two sorted arrays nums1 and nums2 of size m and n respectively.
Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).
You may assume nums1 and nums2 cannot be both empty.<br>
 
Example 1:

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

Example 2:

```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

2.思路
---

用一个数组吧nums1和nums2中的元素组合到同一个数组中，然后用sort函数使数组中的元素按从小到大的顺组排列，分析新的数组的长度，若为奇数，就取中间的数，
若是偶数，就取中间的两个数的平均值。

3.代码
---

```c
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m=nums1.size(), n=nums2.size();
        vector <int> stack(m+n, 0);
        int count=0;
        for (int i=0; i<m; i++) {
            stack[count++]=nums1[i];
        }
        for (int j=0; j<n; j++) {
            stack[count++]=nums2[j];
        }
        sort(stack.begin(), stack.end());
        if ((m+n)%2==0) {
            return (stack[(m+n-1)/2]+stack[(m+n+1)/2])/2.0;
        }
        else {
            return (double)stack[(m+n-1)/2];
        }
    }
};
```
