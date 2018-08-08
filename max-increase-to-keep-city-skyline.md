max-increase-to-keep-city-skyline
===

1.问题描述
---

In a 2 dimensional array grid, each value grid[i][j] represents the height of a building located there. We are allowed to increase the height of any number of buildings, by any amount (the amounts can be different for different buildings). Height 0 is considered to be a building as well. 
At the end, the "skyline" when viewed from all four directions of the grid, i.e. top, bottom, left, and right, must be the same as the skyline of the original grid. A city's skyline is the outer contour of the rectangles formed by all the buildings when viewed from a distance. See the following example.
What is the maximum total sum that the height of the buildings can be increased?<br>

```
Example:
Input: grid = [[3,0,8,4],[2,4,5,7],[9,2,6,3],[0,3,1,0]]
Output: 35
Explanation: 
The grid is:
[ [3, 0, 8, 4], 
  [2, 4, 5, 7],
  [9, 2, 6, 3],
  [0, 3, 1, 0] ]

The skyline viewed from top or bottom is: [9, 4, 8, 7]
The skyline viewed from left or right is: [8, 7, 9, 3]

The grid after increasing the height of buildings without affecting skylines is:

gridNew = [ [8, 4, 8, 7],
            [7, 4, 7, 7],
            [9, 4, 8, 7],
            [3, 3, 3, 3] ]
```

Notes:<br> 
1 < grid.length = grid[0].length <= 50.<br>
All heights grid[i][j] are in the range [0, 100].<br>
All buildings in grid[i][j] occupy the entire grid cell: that is, they are a 1 x 1 x grid[i][j] rectangular prism.<br>

2.思路
---

这道题目是用一个二维数组中的元素来代表城市中建筑的高度，现在要把建筑的高度增加但是不改变城市的边界线，求总共可以增加的总的高度。可以用两个整数分别代表增高前和增高后建筑的总高度，
两者之差便是所求结果。每个位置都要取该行该列对应的最大值中较小的那一个。可以用两个循环求出每行每列对应的高的最大值，再用两个循环可得到每个位置对应的最大的高度，加起来之和便是
增高后建筑的总高度，最后返回结果即可。

3.代码
---

```c
class Solution {
public:
    int maxIncreaseKeepingSkyline(vector<vector<int>>& grid) {
        vector <int> col(grid.size(), 0);
        vector <int> row(grid[0].size(), 0);
        int sum1=0;
        for (int i=0; i<grid.size(); i++) {
            for (int j=0; j<grid[0].size(); j++) {
                sum1+=grid[i][j];
                col[i]=col[i]>grid[i][j]?col[i]:grid[i][j];
                row[j]=row[j]>grid[i][j]?row[j]:grid[i][j];
            }
        }
        int sum2=0;
        for (int i=0; i<grid.size(); i++) {
            for (int j=0; j<grid[0].size(); j++) {
                sum2+=col[i]<row[j]?col[i]:row[j];
            }
        }
        return sum2-sum1;
    }
};
```
