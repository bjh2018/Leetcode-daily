score-after-flipping-matrix
===

1.问题描述
---

We have a two dimensional matrix A where each value is 0 or 1.
A move consists of choosing any row or column, and toggling each value in that row or column: changing all 0s to 1s, and all 1s to 0s.
After making any number of moves, every row of this matrix is interpreted as a binary number, and the score of the matrix is the sum of these numbers.
Return the highest possible score.<br>
Example 1:

```
Input: [[0,0,1,1],[1,0,1,0],[1,1,0,0]]
Output: 39
Explanation:
Toggled to [[1,1,1,1],[1,0,0,1],[1,1,1,1]].
0b1111 + 0b1001 + 0b1111 = 15 + 9 + 15 = 39
```

2.思路
---

翻转任意一行或任意一列，经过任意次数的翻转之后使得每行对应的数加起来和最大，说明首先要把第一列都换成1，使得最高位是1而不是0，然后极了每一列中0的个数，使得每一列中1的个数达到
最大，可以用一个数组来记录每一列对应的0的个数，如果0的个数比总列数的一般要多，说明要翻转这一列，使得该列中1的个数达到最大，最后把每行对应的数加起来就可以得到结果。

3.代码
---

```c
class Solution {
public:
    int matrixScore(vector<vector<int>>& A) {
        int m=A.size(), n=A[0].size();
        vector <int> t(n+1,0);
        for (int i=0; i<m; i++) {
            if (A[i][0]==0) {
                for (int j=0; j<n; j++) {
                    A[i][j]=1-A[i][j];
                    if (A[i][j]==0) ++t[j];
                }
            }
            else {
                for (int j=1; j<n; j++) {
                    if (A[i][j]==0) ++t[j];
                }
            }
        }
        for (int j=1; j<n; j++) {
            if (t[j]*2>m) {
                for (int i=0; i<m; i++) {
                    A[i][j]=1-A[i][j];
                }
            }
        }
        int sum=0,temp=0;
        for (int i=0; i<m; i++) {
            for (int j=0; j<n; j++) {
                temp=temp*2+A[i][j];
            }
            sum+=temp;
            temp=0;
        }
        return sum;
    }
};
```
