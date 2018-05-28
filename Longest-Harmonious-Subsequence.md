Longest Harmonious Subsequence
====

1.问题描述
----

We define a harmonious array is an array where the difference between its maximum value and its minimum value is exactly 1.<br>
Now, given an integer array, you need to find the length of its longest harmonious subsequence among all its possible subsequences.<br>
Example 1:<br>
Input: [1,3,2,2,5,2,3,7]<br>
Output: 5<br>
Explanation: The longest harmonious subsequence is [3,2,2,2,3].<br>
<br>
Note: The length of the input array will not exceed 20,000.<br>
定义一个和谐数组，它的最大值和最小值之间差1，求给定的数组的子数组中和谐数组的最大的长度。

2.思路
---

由和谐数组的定义可知，和谐数组中只包含两种不同的数，也就是说我们只要在给定的数组中找出相差为1的两个数的最大的长度即可。分析可得，数组中的每个数应该都对应
一个自己的长度，有两个因素，所以可以用map容器来解决。其中map中的第二个因素就是该数在数组中的个数。再用一次循环遍历，找出比当前元素大1的元素，再把它们的
总长度与结果比较取其中较大的，最后返回即可。

3.代码
---

```c
class Solution {
public:
    int findLHS(vector<int>& nums) {
       map <int, int> m;
       for (int i=0; i<nums.size(); i++) {
           m[nums[i]]++;
       }
        int ans=0;
       for (int i=0; i<nums.size(); i++) {
           if (m[nums[i]-1]>0) {
               ans=max(ans, m[nums[i]]+m[nums[i]-1]);
           }
       }
        return ans;
      }
};
```

4.用sort解决
-----

```c
class Solution {
public:
    int findLHS(vector<int>& nums) {
      sort(nums.begin(),nums.end());
        int start=0,newstart=0;
        int ans=0;
        for (int i=1; i<nums.size(); i++) {
            if (nums[i]-nums[start]>1) {
                start=newstart;
            }
            if (nums[i]!=nums[i-1]) {
                newstart=i;
            }
            if (nums[i]==nums[start]+1){
                ans=max(ans, i-start+1);
            }
        }
        return ans;
    }
};
````

先用sort函数对给定的数组排序，要找的其实就是相邻相差为1的元素的总个数，可以通过下标作差得到长度，但是比较的元素要改变，所以当出现与此时的元素不同的元素
时，就用newstart来记下它的位置，又因为要看与前一个元素的差是否为1，所以用start来标记被比较的值，当当前元素与要比较的元素的差大于1，就改变start，
最后，取最大的长度即可。
