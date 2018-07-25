max-consecutive-one
===

1.问题描述
---

Given a binary array, find the maximum number of consecutive 1s in this array.<br>
Example 1:

```
Input: [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s.
    The maximum number of consecutive 1s is 3.
```

Note: <br>
The input array will only contain 0 and 1.<br>
The length of input array is a positive integer and will not exceed 10,000<br>

2.思路
---

由题意可得，数组中只含0和1，所以可以用相加的方式来记录连续的1的个数，当当前的元素不为1时，就把现在的和与前一个较大的和进行比较，然后再把sum置为0，
再进行下一次循环，知道循环结束，最后再进行一次比较，因为有可能数组中只含有1，而ans与sum没有进行过比较。

3.代码
---

```c
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int sum=0, len=nums.size(), ans=INT_MIN;
        if (len==0) return 0;
        for (int i=0; i<len; i++) {
            if (nums[i]==1) {
                sum=sum+1;
            }
            else {
                ans=ans>sum?ans:sum;
                sum=0;
            }
        }
        return ans>sum?ans:sum;
    }
};
```

4.其他代码
---

```c
class Solution {
public:
    int findMaxConsecutiveOnes(vector<int>& nums) {
        int sum=0, len=nums.size(), ans=0;
        for (int i=0; i<len; i++) {
            sum*=nums[i];
            sum+=nums[i];
            ans=ans>sum?ans:sum;
        }
        return ans;
    }
};
```

因为数组中只含0和1，所以可以用乘和加的方式，当sum遇到0时就会变成0，遇到1时就会叠加，然后再比较sum的值，最后返回最大的和即为连续的1的最大的个数。
