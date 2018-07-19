Spiral Matrix
===

1.问题描述
---

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.<br>
Example 1:

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
```

Example 2:

```
nput:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

2.思路
---

这道题目就是按照回字的循环输出给定二维数组相对应的一维数组，因为时循环的，所以可以把二维数组的边界分为4种情况，又因为要写二维数组去掉最外面的一层，其对应的
开始的位置以及最大的行数和列数都发生了变化，所以要用4个变量m,n,p,q来记录起始的位置以及所能到达的最大的位置。例如，在写开始的一行时，行数是不变的，而列数是
变化的，所以要利用列数的循环把它们都添加到一维数组中，结束循环之后，下一个要写的是列数不变，对应的行数递增，所以一开始要先判断一下是否存在下一行，如果不存在，
就返回当前的一位数组，如果存在，再利用循环改变行数来把元素添加到一维数组中。剩下的两种情况，行数不变，列数递减；列数不变，行数递减，以此类推即可。注意，
当给定的二维数组中不含元素时，直接返回不含元素的一维数组即可。

3.代码
---

```c
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector <int> ans;
        if (matrix.size()==0) return ans;
        int m=0, n=matrix.size()-1, p=0,q=matrix[0].size()-1;
        while (m<=n&&p<=q) {
            for (int i=m; i<=q; i++) {
                ans.push_back(matrix[m][i]);
            }
            m++;
            if (m>n) {
                return ans;
            }
            for (int i=m; i<=n; i++) {
                ans.push_back(matrix[i][q]);
            }
            q--;
            if (q<p) return ans;
            for (int i=q; i>=p; i--) {
                ans.push_back(matrix[n][i]);
            }
            n--;
            if (n<m) return ans;
            for (int i=n; i>=m;i--) {
                ans.push_back(matrix[i][p]);
            }
            p++;
            if (p>q) return ans;
        }
        return ans;
    }
};
```
