Maximum Average Subarray I
====

1.问题描述
-----


Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.<br> 
Example 1:<br>
Input: [1,12,-5,-6,50,3], k = 4<br>
Output: 12.75<br>
Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75<br>
给定一个由n个整数组成的数组，找到具有最大平均值的给定长度k的连续子数组。 你需要输出最大的平均值。

2.思路
----

因为是先要找出相应的个数，所以先循环找出第一个符合长度的连续的子数组，求出它的平均值后再与设定的值比较，由于是连续的子数组，所以只要从下标为0开始从在sum上减去下标对应的值，再循环遍历，
最后返回结果即可。

3.代码
---

```c
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
        double max=-10000.0;
        double sum=0.0;
        int last=0;
        for (int i=0; i<nums.size(); i++) {
            sum+=nums[i];
            if (i<k-1)
                continue;
            double ans=sum/k;
            max=max>ans?max:ans;
            sum-=nums[last++];
        }
        return max;
    }
};
```
