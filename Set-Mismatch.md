Set Mismatch
====

1.问题描述
---

The set S originally contains numbers from 1 to n. But unfortunately, due to the data error, one of the numbers in the set got duplicated to another number in the set, which results in repetition of one number and loss of another number. <br>
Given an array nums representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array. <br>
Example 1:<br>
Input: nums = [1,2,2,4]<br>
Output: [2,3]<br>
<br>
Note:<br>
The given array size will in the range [2, 10000].<br>
The given array's numbers won't have any order.<br>
集合S最初包含从1到n的数字。 但不幸的是，由于数据错误，集合中的其中一个数字被复制到集合中的另一个数字，导致重复一个数字并丢失另一个数字。
给定一个数组nums，表示错误发生后该组的数据状态。 你的任务是首先发现号码出现两次，然后找到丢失的号码。 以数组的形式返回它们。<br>

2.思路
---

因为数字的大小时从1到n，与下标有关，所以想到要利用另一个数组来记录各个元素在给定的数组中出现的次数，然后再让整数从1开始遍历，按照他们对应的次数来确定重复的数字和缺少的数字。还要注意的是因为要找的两个数字再返回的数组中的顺序是一定的，
所以在遍历的时候，先让两个变量储存它们，再一起加到要返回的数组中。

3.代码
---

```c
class Solution {
public:
    vector<int> findErrorNums(vector<int>& nums) {
        int n=nums.size();
        vector <int> temp(n+1,0);
        for (int i=0; i<n; i++) {
            temp[nums[i]]++;
        }
        vector <int> ans;
        int p,q;
        for (int i=1; i<n+1; i++) {
            if (temp[i]==2) p=i;
            else if (temp[i]==0) q=i;
        }
        ans.push_back(p);
        ans.push_back(q);
        return ans;
    }
};
```
