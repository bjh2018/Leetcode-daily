Valid Triangle Number
===

1.问题描述
---

Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.<br> 
Example 1:<br>
Input: [2,2,3,4]<br>
Output: 3<br>
Explanation:<br><br>
Valid combinations are:<br> 
2,3,4 (using the first 2)<br>
2,3,4 (using the second 2)<br>
2,2,3<br>
给定一个全为非负整数的数组，从其中取三个数，判断是不是能构成三角形，返回能构成的三角形的数目。

2.思路
----

暴力解决，遍历三次，即可得出正确的次数。

3.代码I
---

```c
int triangleNumber(int* nums, int numsSize) {
    int ans=0;
    for (int i=0; i<numsSize-2; i++) {
        for (int j=i+1; j<numsSize-1; j++) {
            for (int m=j+1; m<numsSize; m++) {
                if (nums[i]+nums[j]>nums[m]&&nums[i]+nums[m]>nums[j]&&nums[j]+nums[m]>nums[i]) {
                    ans++;
                }
            }
        }
    }
    return ans;
}
```

4.代码II
---

```c
int comp(const void*a, const void*b) {
    return *(int *)a-*(int *)b;
}
int triangleNumber(int* nums, int numsSize) {
    int ans=0;
    qsort(nums,numsSize,sizeof(int),comp);
    for (int i = numsSize - 1; i >= 2; i--) {  
            int start=0, end=i-1;
        while (start<end) {
            if (nums[start]+nums[end]>nums[i]) {
                ans+=end-start;
                end--;
            }
            else {
                start++;
            }
        }
    }
        return ans;
}
```

其实一开始也看到这个题目的时候，就想到了3sum，打算先把数组按照从小到大的顺序排列好，然后定住一个元素，然后让它后面的任意两个元素相加，判断它们
三个数是否能组成三角形，但是发现好像不太科学。而这个思路是在给数组排好序的基础上，倒序遍历，让前面的数变化，如果它们的和比当前的数要大，则说明
存在确定的一组数满足条件，在结果上叠加即可。
