Rotate Image
===

1.问题描述
---

You are given an n x n 2D matrix representing an image.<br>
Rotate the image by 90 degrees (clockwise).<br>
Note:<br>
You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. <br>
DO NOT allocate another 2D matrix and do the rotation.<br>
Example 1:
```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

Example 2:

```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

2.思路
---

分析题意，得出规律，编写代码即可。（但是要多申请空间）

3.代码
---

```c
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int m=matrix.size(), n=matrix[0].size();
        vector <vector<int>> tmp(matrix);
        for (int i=0; i<m; i++) {
            for (int j=0; j<n; j++) {
                matrix[i][j]=tmp[m-1-j][i];
            }
        }
    }
};
```
