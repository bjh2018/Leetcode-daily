Jump Game
===

1.问题描述
----

Given an array of non-negative integers, you are initially positioned at the first index of the array.<br>
Each element in the array represents your maximum jump length at that position.<br>
Determine if you are able to reach the last index.<br>
Example 1:<br>
Input: [2,3,1,1,4]<br>
Output: true<br>
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.<br>
Example 2:<br>
Input: [3,2,1,0,4]<br>
Output: false<br>
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.<br>
给定一个数组，代表你每次能向前移动的最大距离，判断是否能到达最后的位置。

2.思路
---

用一个数max_来代表走到当前这一步所能到达的最大的位置，判断是否能到达最后的位置，如果它所能到达的最大的位置都到不了现在的i，那么肯定就不能到达
终点，当能到达的最大的位置比数组长度-1还大或者等于时，说明已经可以到达终点，返回true即可。

3.代码
----

```c
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int m=nums.size(),max_=0;
        for (int i=0; i<m; i++) {
            if (max_>=m-1) return true;
            else if (max_<i) return false;
            max_=max(max_,i+nums[i]);
        }
        return max_>=m-1;
    }
};
```
