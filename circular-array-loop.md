circular-array-loop
===

1.问题描述
---

You are given an array of positive and negative integers. If a number n at an index is positive, then move forward n steps. Conversely, if it's negative (-n), move backward n steps. Assume the first element of the array is forward next to the last element, and the last element is backward next to the first element. Determine if there is a loop in this array. A loop starts and ends at a particular index with more than 1 element along the loop. The loop must be "forward" or "backward'.
Example 1: Given the array [2, -1, 1, 2, 2], there is a loop, from index 0 -> 2 -> 3 -> 0.
Example 2: Given the array [-1, 2], there is no loop.
Note: The given array is guaranteed to contain no element "0".
Can you do it in O(n) time complexity and O(1) space complexity?<br>

2.思路
---

有这道题目可知索引是向前还是向后取决于数组中元素的整数，可以用一个变量m来确定索引是向前还是向后，又因为数组中不含0，所以可以用乘法来确定索引是不是始终向一个方向走，如果与上一个方向相同的话，
就改变m的值，看下一个对应的索引是否与当前的方向相同，如果不同就返回false，否则，则在循环结束之后返回true即可。还要注意数组的长度一定比1大，而且第一个元素不可能是向后的。

3.代码
---

```c
class Solution {
public:
    bool circularArrayLoop(vector<int>& nums) {
        if (nums.size()<=1) return false;
        int m=nums[0];
        if (m<0) return false;
        for (int i=m; i<nums.size(); i+=m) {
            if (nums[i-m]*nums[i]>0) {
                m=nums[i];
            }
            else 
                return false;
        }
        return true;
    }
};
```
