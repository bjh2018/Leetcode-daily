Image Smoother
===

1.问题描述
---

Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a cell has less than 8 surrounding cells, then use as many as you can.<br>
Example 1:

```
Input:
[[1,1,1],
 [1,0,1],
 [1,1,1]]
Output:
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]
Explanation:
For the point (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0
For the point (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0
For the point (1,1): floor(8/9) = floor(0.88888889) = 0
```

2.思路
---

这道题目其实是让我们把当前元素与其周围的元素相加，然后求他们的平均值，并且平均值是向下取的。所以问题的关键就是把不同位置的元素周围的元素的和即数量都记录下来，
然后再取平均值即可，可以用sum来记录和，用count来记录个数。对于在(i,j)位置的元素，要分为三大类来看其周围元素的情况，一种是上一行，本行，以及下一行，然后再讨论
列的情况即可，又因为整数与整数相除所得的结果本身就是向下取的，所以直接再把结果添加到结果对应的二维数组中即可。

3.代码
---

```c
class Solution {
public:
    vector<vector<int>> imageSmoother(vector<vector<int>>& M) {
        int m=M.size(), n=M[0].size();
        if (m==0) return M;
        vector<vector<int>>ans(m,vector<int>(n,0));
        for (int i=0; i<m; i++) {
            for (int j=0; j<n; j++) {
                int sum=M[i][j], count=1;
                if (i+1<m) {
                    sum+=M[i+1][j]; count++;
                    if (j+1<n) {
                        sum+=M[i+1][j+1]; count++;
                    }
                    if (j-1>=0) {
                        sum+=M[i+1][j-1]; count++;
                    }
                }
                if (i-1>=0) {
                    sum+=M[i-1][j]; count++;
                    if (j+1<n) {
                        sum+=M[i-1][j+1]; count++;
                    }
                    if (j-1>=0) {
                        sum+=M[i-1][j-1]; count++;
                    }
                }
                if (j-1>=0) {
                    sum+=M[i][j-1]; count++;
                }
                if (j+1<n) {
                    sum+=M[i][j+1]; count++;
                }
                ans[i][j]=sum/count;
            }
        }
        return ans;
    }
};
```
