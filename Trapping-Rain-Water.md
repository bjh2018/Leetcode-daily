Trapping Rain Water
===

1.问题描述
---

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.<br>
![image](https://github.com/bjh2018/Leetcode-daily/blob/master/rainwatertrap.png)

Example:

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

给定n个非负整数表示每个条的宽度为1的高程图，计算下雨后能够捕获多少水。

2.思路
---

把两个边缘的整数当作容器的边缘，取较小的整数代表容器的高，算出此时对应的所盛的水的体积。然后在两个整数之间的距离大于1的条件下，向前推进，去除不能盛水的部分，最后得到所能盛的水
的体积。总体的思路就是先看做一个整体，然后再对其各部分进行讨论，得出结果。用level记录当前的情况对应的水平面的高度，lower记作下一个水平面的高度，如果lower比lever小，说明岁的体
积多算了level-lower，在结果上减去即可，当lower>level时，说明多算了level，而且水平面要升高，少算了一部分，最后再加上即可。

3.代码
---

```c
class Solution {
public:
    int trap(vector<int>& height) {
        int L=height.size();
        if (L<=2) return 0;
        int j=L-1, i=0, level=min(height[i], height[j]);
        int res=level*(j-i-1);
        while (j-i>1) {
            int lower=height[height[i]<=height[j]? ++i:--j];
            if (level>lower) {
                res-=lower;
            }
            else {
                res-=level;
                res+=min(height[i]-level, height[j]-level)*(j-i-1);
                level=min(height[i],height[j]);
            }
        }
        return res;
    }
};
```
