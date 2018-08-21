Majority Element
====

1.问题描述
---

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.<br>
You may assume that the array is non-empty and the majority element always exist in the array.<br>
Example 1:

```
Input: [3,2,3]
Output: 3
```

Example 2:

```
Input: [2,2,1,1,1,2,2]
Output: 2
```

2.思路
----

由题中描述可知，给定的数组中一定存在一个数，它在数组中出现的次数超过n/2,其中n为数组的长度。于是想到用sort函数给数组排序，然后再从第一个元素开始遍历，
如果从当前位置出发向后再走n/2步，若该位置的元素与当前元素相同，说明该元素的个数大于n/2，否则，就让i再向前走一步，判断它的n/2步对应的元素是否与它相同，
最后返回出现次数最多的元素即可。

3.代码
---

```c
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n=nums.size();
        sort(nums.begin(), nums.end());
        /*int i=0, ans=0;
         int temp=n/2;
        while (i+temp<nums.size()) {
            if (nums[i+temp]==nums[i]){
                ans=nums[i]; break;
            }
            else i++;
        }
        return ans;*/
        return nums[n/2];
    }
};
```

其实对数组排完序之后，直接返回数组中间的数即可，因为题目描述中提到，一定存在次数超过n/2的元素，也就是说排序后的数组中间的元素一定出现的次数超过了n/2.

4.其他代码
---

```c
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int maj=nums[0];
        int count=1;
        for (int i=1; i<nums.size(); i++) {
            if (nums[i]==maj) {
                count++;
            }
            else {
                if (count==0) {
                    maj=nums[i]; count=1;
                }
                else {
                    count--;
                }
            }
        }
        return maj;
    }
};
```

Moore投票算法: 我们维护一个当前的候选众数和一个初始为0的计数器。遍历数组时，我们看当前的元素x:<br>
如果计数器是0, 我们将候选众数置为 x 并将计数器置为 1 <br>
如果计数器非0, 我们根据x与当前的候选众数是否相等对计数器+1或者-1<br> 
一趟之后, 当前的候选众数就是所求众数. 时间复杂度 = O(n). 
