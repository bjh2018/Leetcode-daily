minimum-moves-to-equal-array-elements
===

1.问题描述
===

Given a non-empty integer array of size n, find the minimum number of moves required to make all array elements equal, where a move is incrementing n - 1 elements by 1.

```
Example: 
Input:
[1,2,3]

Output:
3

Explanation:
Only three moves are needed (remember each move increments two elements):

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```

2.思路
---

题意是让剩余的n-1个元素进行一次操作就加1，翻过来就是最大的值每次减1，直到数组中的元素完全相同，所以最后元素肯定会都减小成数组中最小的那一个数，只要得知
数组中最小的元素和数组中元素之和，然后做差即可得到结果。

3.代码
---

```c
class Solution {
public:
    int minMoves(vector<int>& nums) {
        int min=nums[0];
        int sum=nums[0];
        for (int i=1; i<nums.size(); i++) {
            if (nums[i]<min) {
                min=nums[i];
            }
            sum+=nums[i];
        }
        return sum-min*nums.size();
    }
};
```
