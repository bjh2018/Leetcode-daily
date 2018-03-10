Unique Paths
===

1.问题描述
---

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).<br>
The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).<br>
How many possible unique paths are there?<br> 
Note: m and n will be at most 100.<br>
机器人在m x n的方格的左上角，求它到方格的右下角的方法的种数。

2.思路
---

根据题意可以知道，机器人要向下走m-1步，向右走n-1步，根据数学的排列组合方式可知，与顺序无关，结果为(m-1+n-1)!/((m-1)! * (n-1)!),即为(m-1+1)*(m-1+2) * ... * (m-1+n-1)/1 * 2 * 3 * ... * (n-1),
再编写程序即可。<br>

3.代码I
---

```c
int uniquePaths(int m, int n) {
    int small=m>n?n-1:m-1;
    int large=m>n?m-1:n-1;
    if (small==0||large==0) {
        return 1;
    }
    long long a=1,b=1;//因为要算阶乘，很有可能结果超出整数范围
    for (int i=1; i<=small; i++) {
        a=a*(large+i);
        b=b*i;
    }
    return a/b;
}
```

4.代码II
---

```c
int uniquePaths(int m, int n) {
    int grid[m][n];
    int i, j;
    for (i = 1; i < m; i++) {
        grid[i][0] = 1;
    }
    for (j = 0; j < n; j++) {
        grid[0][j] = 1;
    }
    for (i = 1; i < m; i++) {
        for (j = 1; j < n; j++) {
            grid[i][j] = grid[i-1][j] + grid[i][j-1];
        }
    }
    return grid[m-1][n-1];
}
```

其实这道题和爬楼梯很像，都可以用递推来实现，如果是一个2x2的田字格的话，步骤数就等于它到达它上方的步骤数加上到达它左边的步骤数，也就是说如果我们把最后一个格看作田字格的右下角的话，那么它的步骤也等于那
两项相加，根据题意可知在边缘处的格到达离它最近的下方所走的步数为1，所以把第一行和第一列的元素都置成一，最后再加起来即可。
