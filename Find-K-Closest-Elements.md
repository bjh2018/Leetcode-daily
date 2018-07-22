Find K Closest Elements
===

1.问题描述
---

Given a sorted array, two integers k and x, find the k closest elements to x in the array. The result should also be sorted in ascending order. If there is a tie, the smaller elements are always preferred. <br>
Example 1:

```
Input: [1,2,3,4,5], k=4, x=3
Output: [1,2,3,4]
```

Example 2:

```
Input: [1,2,3,4,5], k=4, x=-1
Output: [1,2,3,4]
```

2.思路
---

这道题目是给定一个已经排好顺序的数组，给定两个整数k和x，找出距离x最近的k个数，并且返回的数组中的元素也是要按照从小到大的顺序排列，其实也就是在原数组的开头和
结尾删除一定个数的元素，最后返回数组即可，因为肯定有开头或者结尾的数距离给定的数最远（由二分法可以解释），故根据这个思路写出代码即可。

3.代码
---

```c
class Solution {
public:
    vector<int> findClosestElements(vector<int>& arr, int k, int x) {
        vector <int> ans=arr;
        while (ans.size() > k) {
            int left=abs(ans[0]-x);
            int right=abs(ans.back()-x);
            if (left<=right) {
                ans.pop_back();
            }
            else
                ans.erase(ans.begin());
        }
        return ans;
    }
};
```
