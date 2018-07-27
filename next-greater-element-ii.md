next-greater-element-ii
===

1.问题描述
---

Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.<br> 
Example 1:

```
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number; 
The second 1's next greater number needs to search circularly, which is also 2.
```

2.思路
---

这道题目是要找到给定的数组中每个元素按照一定的顺序看是否有比它大的数，如果存在，就在结果数组中添加这个数，如果不村在，就在结果数组中加上-1.所以就是要判断是否存在这样的数，还有就是要
构成循环时如何返回正确的对应的数，可以增加j的下限，然后用减法得到正确的数组中的索引，再用temp判断是否存在这样的数即可。

3.代码
---

```c
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int l=nums.size(), temp=0;
        vector<int> ans(l,0);
        for (int i=0; i<l; i++) {
            temp=nums[i];
            for (int j=i+1; j<l+i; j++) {
                if (j<l&&temp<nums[j]) {
                    temp=nums[j]; break;
                }
                else if (j>=l&&temp<nums[j-l]){
                    temp=nums[j-l]; break;
                }
            }
            if (temp!=nums[i]) ans[i]=temp;
            else ans[i]=-1;
        }
        return ans;
    }
};
```
