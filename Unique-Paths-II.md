Unique Paths II
===

1.问题描述
---

Follow up for "Unique Paths":<br>
Now consider if some obstacles are added to the grids. How many unique paths would there be?<br>
An obstacle and empty space is marked as 1 and 0 respectively in the grid.<br>
For example,<br>
There is one obstacle in the middle of a 3x3 grid as illustrated below.<br>
[<br>
  [0,0,0],<br>
  [0,1,0],<br>
  [0,0,0]<br>
]<br>
The total number of unique paths is 2.<br>
这个题目是在Unique Paths的基础上又增加的一道题目，它比第一个题目增加了障碍，也就是说解决这个问题的关键就是对障碍的处理。

2.思路
---

依然才用Unique Paths的基本思路，还是把先把第一行和第一列都赋好值，如果遇到障碍，则说明后面的路走不通了，所以要把后的元素都赋值为0，代表无路可走。
在再一次遍历求总的种数的时候，如遇到障碍，就立刻把该值赋为0，代表遇到障碍，此路不同，最后返回最后一个数即可。

3.代码
---

```c
int uniquePathsWithObstacles(int** obstacleGrid, int obstacleGridRowSize, int obstacleGridColSize) {
    int m=obstacleGridRowSize,n=obstacleGridColSize;
    int dp[m][n];
    for (int i=0; i<m; i++) {
        for (int j=0; j<n; j++) {
            dp[i][j]=0;
        }
    }
    int i, j;
    for(int i = 0; i < m; i ++) {
            if(obstacleGrid[i][0] == 1) {
                dp[i][0] = 0;
                break;
            } else {
                dp[i][0] = 1;
            }
        }
        
        for(int j = 0; j < n; j ++) {
            if(obstacleGrid[0][j] == 1) {
                dp[0][j] = 0;
                break;
            } else {
                dp[0][j] = 1;
            }
        }
        
        for(int i = 1; i < m; i ++) {
            for(int j = 1; j < n; j ++) {
                if(obstacleGrid[i][j] == 1) {
                    dp[i][j] = 0;
                } else {
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
                }
            }
        }
        return dp[m - 1][n - 1];
    }
```
    
    
4.总结
 ---
    
（1）一开始并没有把刚刚生成的数组的值都赋为0，导致出现错误，这可能是由于二维数组如果只单纯声明的话，不会有默认值。而解决这个题目时默认了二维数组中的每一个数
 都是0，所以出现了错误。<br>
（2）还有就是掌握这种求录得走法的方法，是先在一个方格中，再扩展到n*n方格的右下角中，以及遇到障碍时的解决办法，实际上，这也是递归的一种变式。
