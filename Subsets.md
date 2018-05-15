Subsets
===

1.问题描述
---

Given a set of distinct integers, nums, return all possible subsets (the power set).<br>
Note: The solution set must not contain duplicate subsets.<br>
Example:<br>
Input: nums = [1,2,3]<br>
Output:<br>
[<br>
  [3],<br>
  [1],<br>
  [2],<br>
  [1,2,3],<br>
  [1,3],<br>
  [2,3],<br>
  [1,2],<br>
  []<br>
]<br>
给定一组不同的整数nums，返回所有可能的子集。

2.思路
---

要求找到给定的数组所有的可能的子集，不难发现当前层的集合 = 上一层的集合 + 上一层的集合加入当前层处理的元素得到的所有集合，
因此可以从第二层开始（第一层是空集合）迭代地求最后一层的所有集合。要注意空集也是子集的一种，所以把空集作为第一层来循环，
首先对二维数组先初始化，使它的第一个元素是空集，然后在此基础上递归迭代即可。

3.代码
---

```c
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector <vector<int> > ans(1, vector<int> ());
        //sort (nums.begin(),nums.end());
        for (int i=0; i<nums.size(); i++){
            int n=ans.size();
            for (int j=0; j<n; j++) {
                ans.push_back(ans[j]);
                ans.back().push_back(nums[i]);
            }
        }
        return ans;
    }
};
```
