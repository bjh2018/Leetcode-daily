Non-decreasing Array
===

1.问题描述
---

Given an array with n integers, your task is to check if it could become non-decreasing by modifying at most 1 element. <br>
We define an array is non-decreasing if array[i] <= array[i + 1] holds for every i (1 <= i < n). <br>
Example 1:

```
Input: [4,2,3]
Output: True
Explanation: You could modify the first 4 to 1 to get a non-decreasing array.
```

Example 2:

```
Input: [4,2,1]
Output: False
Explanation: You can't get a non-decreasing array by modify at most one element.
```

2.思路
---

由题意可知，是判断给定的数组中的元素构成的数列在至多改变一个元素的条件下是否满足是非递减数列，即满足array[i] <= array[i + 1]，如果存在两个元素不满足该条件
件，那么一定返回false。若只有一个元素不满足该条件，就要分情况讨论，改变原数组中元素的值，再继续进行遍历，返回结果即可。数组中的元素应该满足
nums[i-1]<=nums[i]<=nunms[i+1]，则可推出nums[i-1]<=nums[i+1]，说明nums[i]=nums[i+1]即可满足题设。如果nums[i-1]>nums[i+1],又因为一定满足nums[i-1]<=nums[i],
所以只需满足nums[i+1]=nums[i]即可。

3.代码
---

```c
class Solution {
public:
    bool checkPossibility(vector<int>& nums) {
        bool m=false;
        for (int i=0; i<nums.size()-1; i++) {
            if (nums[i]>nums[i+1]) {
                if (m) return false;
                if (i-1<0||nums[i-1]<=nums[i+1]){
                    nums[i]=nums[i+1];
                }
                else {
                    nums[i+1]=nums[i];
                }
                m=true;
            }
        }
        return true;
    }
};
```
