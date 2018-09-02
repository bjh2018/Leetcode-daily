Subarray Product Less Than K
===

1.问题描述
---

Your are given an array of positive integers nums.<br>
Count and print the number of (contiguous) subarrays where the product of all the elements in the subarray is less than k.<br>
Example 1:

```
Input: nums = [10, 5, 2, 6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6].
```

Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.

2.思路
---

这道题目是要找到满足乘积小于k的所有连续子数组的总个数，可以用two poionts + sliding window 来解决，我们定义0为起点，<br>
开始10 ans=1;<br>
10 5 ans=1+2=3（5可以，5和10也可以）<br>
10 5 2不符合条件，就改变起点，并在结果上除以10，再进行相同的操作即可。<br>
可知每找到符合条件的一个j，都会在结果上增加j+1-i，根据这个规律就可得到正确的结果。

3.代码
---

```c
class Solution {
public:
    int numSubarrayProductLessThanK(vector<int>& nums, int k) {
        int m=1;
        int ans=0;
        for (int i=0, j=0; j<nums.size(); j++) {
            m*=nums[j];
            while (i<=j&& m>=k) {
                m/=nums[i++];
            }
            ans+=j-i+1;
        }
        return ans;
    }
};
```
