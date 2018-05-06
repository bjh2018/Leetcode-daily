3Sum Closest
===

1.问题描述
---

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.<br>
Example:<br>
Given array nums = [-1, 2, 1, -4], and target = 1.<br>
<br>
The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).<br>
给定一组数，取其中任意三个数的和，使它到给定的target的距离最小，并返回这三个数的和。

2.思路
---

其实和3sum的基本思路是一样的，定住一个元素，让它后面的元素任意取两个，使得和到target的距离最小。关键就是判定让前一个坐标＋和让后一个坐标-的情况。可以用sum来记录这三个数的和，让difference来记录与target之间的距离，difference可以为负数，让r来代表三个数的
的和，并每经过一个循环都把它改变。根据difference的正负来确定坐标的前移和后退。如果它的值为负数的话，说明当前三个数的和比target小，因为数组中的数已经按从大到小的顺序排列，所以就让s++，这样才能使差减小地最小，如果difference时正数，就让e--，这样就可以使
和减少的最少。

3.代码
---

```c
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(),nums.end());
        int i=0,difference,min=INT_MAX,r,sum;
        while (i<nums.size()) {
            int s=i+1, e=nums.size()-1;
            while (s<e) {
                sum=nums[i]+nums[s]+nums[e];
                difference=sum-target;
                if (abs(difference)<min){
                    r=sum;min=abs(difference);
                }
                if (difference==0) return r;
                else if (difference<0) s++;
                else if (difference>0) e--;
            }
            i++;
        }
        return r;
    }
};
```
