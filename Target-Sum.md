Target Sum
===

1.问题描述
---

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.<br> 
Find out how many ways to assign symbols to make sum of integers equal to target S. <br>
Example 1:<br>
Input: nums is [1, 1, 1, 1, 1], S is 3.<br> 
Output: 5<br>
Explanation: <br>
<br>
-1+1+1+1+1 = 3<br>
+1-1+1+1+1 = 3<br>
+1+1-1+1+1 = 3<br>
+1+1+1-1+1 = 3<br>
+1+1+1+1-1 = 3<br>
<br>
There are 5 ways to assign symbols to make the sum of nums be target 3.<br>
<br>
Note:<br>
The length of the given array is positive and will not exceed 20.<br> 
The sum of elements in the given array will not exceed 1000.<br>
Your output answer is guaranteed to be fitted in a 32-bit integer.<br>
给定一个数组，数组中元素在加减时前面的符号有两种情况，+和-，找出有多少种方法满足所有元素之和等于S。

2.思路
---

其实可以看出，每个元素都有两种情况，我们可以通过在S上加减当前的元素使S的值变化，而且种数应该等于在S上加当前元素和减当前元素两种情况的种数之和。同时要注意改变数组的起始位置和数组的长度。当数组的长度为0时，如果S
的值为0，就返回1，否则返回0.

3.代码
---

```c
int findTargetSumWays(int* nums, int numsSize, int S) {
       // return numsSize?findTargetSumWays(nums+1, numsSize-1, S+*nums)+findTargetSumWays(nums+1, numsSize-1, S-*nums):!S;
    if (numsSize==0&&S==0) return 1;
    else if (numsSize==0&&S!=0) return 0;
    else {
        return findTargetSumWays(nums+1, numsSize-1, S+*nums)+findTargetSumWays(nums+1, numsSize-1, S-*nums);
    }
}
```

其中被注释掉的部分为改良版，是关于逻辑运算！的应用，其中!0的值为1，其他整数前加!的值均为0.
