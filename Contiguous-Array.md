Contiguous Array
====

1.问题描述
---

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1. <br>
Example 1:<br>
Input: [0,1]<br>
Output: 2<br>
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.<br>
<br>
Example 2:<br>
Input: [0,1,0]<br>
Output: 2<br>
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.<br>

2.思路
---

因为是要找到0和1的数目相等的良序的子数组的最大的长度，单纯地计算1和0的个数时间太长，因为数组中只有0和1，所以可以把为0的数改成是为-1，这样和就不会总是
增加，那么只需要找到和相等的数作差就可以找到和为0的子数组的长度，而子数组的长度可已通过下标的加减来实现，所以可以通过map容器来储存当前的和和其对应的下标，
再通过find函数找到与它相等的和的下标，作差即可得到又一个长度，再反复比较就可以得到最大的长度。

3。代码
---

```c
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        map<int,int> m;
        map<int,int>::iterator k;
        m[0]=-1;
        int sum=0,max_length=0;
        for (int i=0; i<nums.size(); i++) {
            sum+=(nums[i]==0)?-1:1;
            k=m.find(sum);
            if (k!=m.end()) {
                max_length=max(max_length, i-k->second);
            }
            else m[sum]=i;
        }
        return max_length;
    }
};
```
