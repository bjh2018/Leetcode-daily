Transpose Matrix
===

1.问题描述
---

Given a matrix A, return the transpose of A.<br>
The transpose of a matrix is the matrix flipped over it's main diagonal, switching the row and column indices of the matrix.<br>
 
Example 1:

```
Input: [[1,2,3],[4,5,6],[7,8,9]]
Output: [[1,4,7],[2,5,8],[3,6,9]]
```

Example 2:

```
Input: [[1,2,3],[4,5,6]]
Output: [[1,4],[2,5],[3,6]]
```

2.思路
---

这道题目是给定一个m * n的矩阵，返回一个n * m的矩阵，并且返回的矩阵各个位置的元素是原矩阵行列的坐标对换得到的元素，所以问题的关键就是申请一个n*m二维数组，然后
通过两个循环对数组中的元素进行赋值即可。

3.代码
---

```c
class Solution {
public:
    vector<vector<int>> transpose(vector<vector<int>>& A) {
        int m=A[0].size(), n=A.size();
        vector <vector<int>> ans(m, vector<int>(n,0));
        for (int i=0; i<m; i++) {
            for (int j=0; j<n; j++) {
                ans[i][j]=A[j][i];
            }
        }
        return ans;
    }
};
```
