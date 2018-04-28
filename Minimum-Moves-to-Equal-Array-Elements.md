Minimum Moves to Equal Array Elements
===

1.问题描述
---

Given a non-empty integer array of size n, find the minimum number of moves required to make all array elements equal, where a move is incrementing n - 1 elements by 1.<br>
Example: <br>
Input:<br>
[1,2,3]<br>
<br>
Output:<br>
3<br>
<br>
Explanation:<br>
Only three moves are needed (remember each move increments two elements):<br>
<br>
[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]<br>
给定一个大小为n的非空整数数组，找到使所有数组元素相等所需的最小移动次数，其中移动将n-1个元素递增1。

2.思路
---

其实这是一个数学问题，我们用sum来表示未移动之前的数组中元素的总和，用n来代表数组的元素的大小，用min来代表数组中元素的最小值，用x来代表移动后的数的值，那么会有<br>
sum + m * (n-1) = n * x<br>
其中<br>
x=min+m<br>
则可推出<br>
m=sum-min*n<br>
所以首先把最小值遍历出来，然后再在结果上一直加num[i]-min，那么最终得到的结果就是所求的值。

3.代码I（C）
---

```c
int minMoves(int* nums, int numsSize) {
    int min=nums[0];
    int sum=0;
    for (int i=1; i<numsSize; i++) {
        min=min>nums[i]?nums[i]:min;
    }
    for (int i=0; i<numsSize; i++) {
        sum+=nums[i]-min;
    }
    return sum;
}
```

4.代码II（C++）
---

```c
class Solution {
public:
    int minMoves(vector<int>& nums) {
        int min=nums[0];
        int sum=0;
        for (int i=0; i<nums.size(); i++)
            min=min<nums[i]?min:nums[i];
        for (int i=0; i<nums.size(); i++)
            sum+=nums[i]-min;
        return sum;
    }
};
```

```c
class Solution {
public:
    int minMoves(vector<int>& nums) {
        int sum, min;
        sum = nums[0];
        min = nums[0];
        for(int i = 1; i < nums.size(); i++){
            sum += nums[i];
            if(min > nums[i])   min = nums[i];
        }
        return sum - nums.size() * min;
    }
};
```

思路大致相同，只不过是先把sum算了出来，在最后再直接返回结果的算式。
