132 Pattern
===

1.问题描述
---

Given a sequence of n integers a1, a2, ..., an, a 132 pattern is a subsequence ai, aj, ak such that i < j < k and ai < ak < aj. Design an algorithm that takes a list of n numbers as input and checks whether there is a 132 pattern in the list.<br>
Note: n will be less than 15,000.,<br>
Example 1:<br>
Input: [1, 2, 3, 4]<br>
<br>
Output: False<br>
<br>
Explanation: There is no 132 pattern in the sequence.<br>
<br>
Example 2:<br>
Input: [3, 1, 4, 2]<br>
<br>
Output: True
<br>
Explanation: There is a 132 pattern in the sequence: [1, 4, 2].<br>
<br>
Example 3:<br>
Input: [-1, 3, 2, 0]<br>
<br>
Output: True<br>
<br>
Explanation: There are three 132 patterns in the sequence: [-1, 3, 2], [-1, 3, 0] and [-1, 2, 0].<br>
给定一个n个整数a1，a2，...，an的序列，一个132模式是一个子序列ai，aj，ak，使得i <j <k且ai <ak <aj。 设计一个算法，将n个数字列表作为输入，并检查列表中是否有132个模式。<br>
注意：n将小于15,000。<br>

2.思路
---

首先从第一个数开始遍历，并且在遍历的过程中，不断地去较小的值，让它当作ai,遍历的数当作aj，另一个循环从第二个数开始遍历，当作ak，看是否满足条件即可。<br>

3.代码I
---

```c
bool find132pattern(int* nums, int numsSize) {
    if (numsSize<=2) return false;
    int temp=0;
    int min=2147483647;
    for (int i=0; i<numsSize; i++) {
        min=(min<nums[i])?min:nums[i];
        for (int j=i+1; j<numsSize; j++) {
            if (nums[j]<nums[i]&&min<nums[j]) {
                return 1;
            }
        }
    }
    return 0;
}
```

4.代码II
---

```c
bool find132pattern(int* nums, int numsSize) {
    if (numsSize < 3)
        return false;
    static int stack[15000];
    int top = 0;
    int last = INT_MIN;
    while (numsSize--) {
        if (nums[numsSize] < last)
            return true;
        while (top&&stack[top-1]<nums[numsSize]) {
            last = stack[--top];
        }
        stack[top++]=nums[numsSize];
    }
    return false;
}
```

last代表aj,num[numsSize]代表ai,stack[top]代表ak，可以得知在lat赋值的同时就已经保证了它的值要比它后面所有元素的值都大，所以就要用stack来储存气候的值，只要找到它前面的值比它也小，就说明存在这样132的形式。
