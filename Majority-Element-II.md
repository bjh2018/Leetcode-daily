Majority Element II
===

1.问题描述
---

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.<br>
Note: The algorithm should run in linear time and in O(1) space.<br>
Example 1:

```
Input: [3,2,3]
Output: [3]
```

Example 2:

```
Input: [1,1,1,3,3,2,2,2]
Output: [1,2]
```

2.思路
---

因为要找到出现次数大于n/3的元素，首先想到的是先对数组排序，然后在索引上加上n/3,如果这两个数相同，则说明该元素满足条件，否则，就从当前索引开始，
找出第一个不与当前元素相同的元素的索引，然后再进行相同的操作。对于数组长度小于3的数组，要分情况讨论，因为它所加的n/3结果为0，是没有意义的。

3.代码
---

```c
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int n=nums.size();
        vector <int> ans;
        if (n<=2) {
            if (n==2&&nums[0]==nums[1]) {
                nums.pop_back();
            }
            return nums;
        }
        sort(nums.begin(), nums.end());
        int i=0;
        int temp=n/3;
        while (i+temp<nums.size()) {
            if (nums[i+temp]==nums[i]){
                ans.push_back(nums[i]); 
                i+=temp;
            }
            int index=i; i++;
            while (nums[i]==nums[index]) {
                    i++;
            }
        }
        return ans;
    }
};
```

4.其他代码
---

```c
class Solution {
public:
  vector<int> majorityElement(vector<int>& nums) {
    vector<int> res;
    auto x = 0, cx = 0;
    auto y = 1, cy = 0;
    for(auto i: nums) {
      if(i == x) {
        cx ++;
      } else if (i == y) {
        cy ++;
      } else if(cx == 0) {
        cx = 1;
        x = i;
      } else if (cy == 0) {
        cy = 1;
        y = i;
      } else {
        cy -- ;
        cx -- ;
      }
    }
   
    cx = cy = 0;
    for(auto i: nums) {
      cx += i==x?1:0;
      cy += i==y?1:0;
    }
    if(cx > nums.size() / 3) res.push_back(x);
    if(cy > nums.size() / 3) res.push_back(y);

    return res;
  }
};
```

可以用 [摩尔投票法](https://blog.csdn.net/tinyjian/article/details/79110473) 解决。因为由题意可知，数组中出现次数多于n/3的元素最多有两个
所以给x和y赋上不同的值，然后再循环，最后会得到两个数字，但是题中并没有说这样的数一定存在，所以要再用一个循环来验证得到的数是否满足条件。
[详情解答](https://www.cnblogs.com/grandyang/p/4606822.html)
