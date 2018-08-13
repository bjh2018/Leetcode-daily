# Pascal's Triangle

1.问题描述
---

Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

![image](https://github.com/bjh2018/Leetcode-daily/blob/master/PascalTriangleAnimated2.gif)

In Pascal's triangle, each number is the sum of the two numbers directly above it.<br>
Example:

```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

2.思路
---

由题意可知，在这样的三角形的中间元素的值存在这样的规律：m[i][j]=m[i-1][j-1]+m[i-1][j];又因为二维数组的列数是根据行数变化的，所以要先申请二维数组
的空间，再用函数push_back()把每行每列的数都设为1，最后按规律改变中间元素的值即可。

3.代码
---

```c
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> m;
        int count=1;
        for (int i=0; i<numRows; i++) {
            m.push_back(vector<int>(count,1));
            for (int j=1; j<count-1; j++) {
                m[i][j]=m[i-1][j-1]+m[i-1][j];
            }
            count++;
        }
        return m;
    }
};
```
