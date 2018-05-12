H-Index
===

1.问题描述
---

Given an array of citations (each citation is a non-negative integer) of a researcher, write a function to compute the researcher's h-index.<br>
According to the definition of h-index on Wikipedia: "A scientist has index h if h of his/her N papers have at least h citations each, and the other N − h papers have no more than h citations each."<br>
Example:<br>
Input: citations = [3,0,6,1,5]<br>
Output: 3 <br>
Explanation: [3,0,6,1,5] means the researcher has 5 papers in total and each of them had<br> 
             received 3, 0, 6, 1, 5 citations respectively. <br>
             Since the researcher has 3 papers with at least 3 citations each and the remaining<br> 
             two with no more than 3 citations each, his h-index is 3.<br>
Note: If there are several possible values for h, the maximum one is taken as the h-index.<br>
如果N篇论文中的引用次数至少为h次，其它的论文被引用的次数都小于h，那么h为该科学家的指数。当科学家存在多个指数的时候，把最大的当作他的指数。

2.思路
---

也就是说要使得当前数组中的元素大于h，其他都要小于h，把数组中的元素按照从小到大的顺序排列，从0开始遍历，找出最大的h，使得已经遍历到的数都比它，而后面的元素都比它小，也就是说循环进行下去的条件是没有超过数组的长度，
还有一个就是当前元素的下标要小于它对应的元素的值，最后返回最后一个满足条件的下标即可。

3.代码
---

```c
class Solution {
public:
    int hIndex(vector<int>& citations) {
        sort(citations.begin(),citations.end(),greater <int> ());
        int i=0;
        for (; i<citations.size()&&i<citations[i]; i++) {}
        return i;
    }
};
```
