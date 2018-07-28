next-greater-element-i
===

1.问题描述
---

You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2. 
The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. If it does not exist, output -1 for this number. <br>
Example 1:

```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
Output: [-1,3,-1]
Explanation:
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
```

Example 2:

```
Input: nums1 = [2,4], nums2 = [1,2,3,4].
Output: [3,-1]
Explanation:
    For number 2 in the first array, the next greater number for it in the second array is 3.
    For number 4 in the first array, there is no next greater number for it in the second array, so output -1.
```

2.思路
---

用三个循环来实现，前两个循环要找到给定数组在原数组中的位置，再从当前位置出发，看当前的元素右边是否存在比它大的数，如果存在就把结果数组中的数变成这个较大的数，如果不存在，就保证原数组中的元素位-1即可。

3.代码
---

```c
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& findNums, vector<int>& nums) {
        int m=findNums.size(), n=nums.size();
        vector <int> a(m,-1);
        for (int i=0; i<m; i++) {
            for (int j=0; j<n-1; j++) {
                if (findNums[i]==nums[j]) {
                    for (int p=j+1; p<n; p++) {
                        if (nums[p]>nums[j]) {
                            a[i]=nums[p]; break;}
                    }
                }
            }
        }
        return a;
    }
};
```

4.其他代码
---

```c
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& findNums, vector<int>& nums) {
        
        vector<int> ret; 
        int len1 = findNums.size(), len2 = nums.size();
        
        for(int i=0; i<len1; i++)
        {
        	int n = findNums[i];
        	vector<int>::iterator itr = find(nums.begin(), nums.end(), n);
        	if(itr == nums.end())ret.push_back(-1);
			else
			{
				while(*itr<=n && itr!=nums.end())
        		{
					itr++;
				}
				if(itr == nums.end())ret.push_back(-1);
				else ret.push_back(*itr);
			}
        }
        
        return ret;
    }

};
```

用find函数找到当前元素在对应数组中的位置，然后对位置进行讨论，并运用指针，可以节省时间。
