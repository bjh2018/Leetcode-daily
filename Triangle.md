triangle
===

1.问题描述
---

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.
For example, given the following triangle

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

2.思路
---

因为要求路径的最小值，而且最后一行的元素最多，所以可以用一个数组来储存最后一行的数字，然后再运用两个循环使得储存的数字对应的和不断的更新为最小的数，要注意的一点
是元素只能与与其相邻的元素求和，所以只要比较两种情况即可，又因为第一行只有一个元素，而路径中必须包含每一行，所以最后只要返回sum[0]即为所求。

3.代码
---

```c
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int len=triangle.size();
        if (len==0) return 0;
        if (len==1) return triangle[0][0];
        vector <int> sum=triangle[len-1];
        for (int i=len-2; i>=0; i--) {
            for (int j=0; j<triangle[i].size(); j++) {
                sum[j]=min(sum[j]+triangle[i][j],sum[j+1]+triangle[i][j]);
            }
        }
        return sum[0];
    }
};
```

    
