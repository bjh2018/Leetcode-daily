Largest Number At Least Twice of Others
===

1.问题描述
---

In a given integer array nums, there is always exactly one largest element.<br>
Find whether the largest element in the array is at least twice as much as every other number in the array.<br>
If it is, return the index of the largest element, otherwise return -1.<br>
Example 1:<br>
Input: nums = [3, 6, 1, 0]<br>
Output: 1<br>
Explanation: 6 is the largest integer, and for every other number in the array x,<br>
6 is more than twice as big as x.  The index of value 6 is 1, so we return 1.<br>
 <br>
Example 2:<br>
Input: nums = [1, 2, 3, 4]<br>
Output: -1<br>
Explanation: 4 isn't at least as big as twice the value of 3, so we return -1.<br>
Note:<br>
nums will have a length in the range [1, 50].<br>
Every nums[i] will be an integer in the range [0, 99].<br>
在给定的整数数组nums中，总是有一个最大的元素。
查找数组中的最大元素是否至少是数组中每个其他数字的两倍。
如果是，则返回最大元素的索引，否则返回-1。

2.思路
---

其实这道题目就是在看第1大的数是否比第2大的数的2倍大，也就是说要把数组按从小到大的顺序排列之后，比较它最后两位的大小关系即可，如果满足题述要求，就要返回
最大的值在原数组中的索引，所以要先用一个数组来记录不同值的索引，最后返回相应的值即可。

3.代码
---

```c
class Solution {
public:
    int dominantIndex(vector<int>& nums) {
        vector <int> m(100,0);
        int n=nums.size();
        for (int i=0; i<n; i++) {
            m[nums[i]]=i;
        }
        sort(nums.begin(),nums.end());
        if (nums[n-1]>=2*nums[n-2]) return m[nums[n-1]];
        else return -1;
    }
};
```

4.代码II
---

```c
class Solution {
public:
    int dominantIndex(vector<int>& nums) {
        if(!nums.size()) return -1;
        int n = nums.size();
        if(n==1) return 0;
        int max1 = nums[0],max2 = -1,index1 = 0;
        for(int i=1;i<n;++i) {
        	if(nums[i]>=max1) {
        		index1 = i;
                max2 = max1;
        		max1 = nums[i];
        	}
            else if(nums[i]>max2)
                max2 = nums[i];
        }
        if(max1>= (max2<<1))
        	return index1;
        else return -1;
    }
};
```

这个代码直接找到要比较的两个值，然后在进行比较即可。注意在对最大值呵第二大的值的寻找的过程中，每更新一次最大值，第二大的值也要改变。
