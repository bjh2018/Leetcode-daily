construct-the-rectangle
===

1.问题描述
---

For a web developer, it is very important to know how to design a web page's size. So, given a specific rectangular web page’s area, your job by now is to design a rectangular web page, whose length L and width W satisfy the following requirements:<br>

```
1. The area of the rectangular web page you designed must equal to the given target area.

2. The width W should not be larger than the length L, which means L >= W.

3. The difference between length L and width W should be as small as possible.
```

You need to output the length L and the width W of the web page you designed in sequence. <br>

Example:<br>

```
Input: 4
Output: [2, 2]
Explanation: The target area is 4, and all the possible ways to construct it are [1,4], [2,2], [4,1]. 
But according to requirement 2, [1,4] is illegal; according to requirement 3,  [4,1] is not optimal compared to [2,2]. So the length L is 2, and the width W is 2.
```

给定一个整数来代表区域的面积，找到其可能对应的长和宽，并且使得它们相差最小，且宽要小于等于长，返回包含长和宽的数值的数组即可。

2.思路
---

由题意可知长和宽相等时，它们相差最小，也就是说对给定的数开根号的话，如果可以被直接完全开根号的话，直接返回这个结果就行，如果开不尽，也会得到一个整数，
然后对这个整数进行循环，直到得到一个整数可以被面积整除或者当这个整数变成比1小的数就结束循环，然后再讨论这两种情况即可。

3.代码
---

```c
class Solution {
public:
    vector<int> constructRectangle(int area) {
        vector <int> ans(2,0);
        int m=sqrt(area);
        while (area%m!=0&&m>=1) {
            m--;
        }
        if (m<1) {
            ans[0]=area; ans[1]=1;
        }
        else
            ans[0]=(area/m); ans[1]=m;
        return ans;
    }
};
```
