Subarray Sum Equals K
===

1.问题描述
---

Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.<br>
Example 1:<br>
Input:nums = [1,1,1], k = 2<br>
Output: 2<br>
<br>
Note:<br>
The length of the array is in range [1, 20,000].<br>
The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].<br>
给定一个数组，判断是否有连续的子数组，它的元素之和是否等于k。

2.思路
---

用一个数组来记录各个元素相加之和，然后把它们做减法就可以得到不同长度不同元素的子数组的和，然后和给定的数k比较即可。

3.代码I
---

```c
int subarraySum(int* nums, int numsSize, int k) {
    int *temp=(int*)malloc(sizeof(int)*numsSize+1);
    memset(temp,0,sizeof(int));
    temp[0]=0;
    for (int i=1; i<numsSize+1; i++)
        temp[i]=temp[i-1]+nums[i-1];
    int ans=0;
    for (int i=0; i<numsSize+1; i++) {
        for (int j=i+1; j<numsSize+1; j++) {
            if (temp[j]-temp[i]==k){
                ++ans;
            }
        }
    }
    return ans;
}
```

4.代码II
---

```c
int subarraySum(int* nums, int numsSize, int k) {
    int cnt = 0;
    for(int j=0; j<numsSize; j++)
    {
        int tmpSum = 0;
        for(int i=j; i<numsSize; i++)
        {
            tmpSum += nums[i];
            if(tmpSum < k)
            {
                continue;
            }
            else if(tmpSum == k)
            {
                cnt++;
            }
            /*else
            {
                tmpSum= nums[i];
            }*/
        }
    }
    return cnt;
}
```

在遍历的过程中把和算出来并与k比较即可。
