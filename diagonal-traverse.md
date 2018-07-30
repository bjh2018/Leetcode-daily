diagonal-traverse
===

1.问题描述
---

Given a matrix of M x N elements (M rows, N columns), return all elements of the matrix in diagonal order as shown in the below image.<br> 
Example:

```
Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output:  [1,2,4,7,5,3,6,8,9]
Explanation:
```

![image](https://github.com/bjh2018/Leetcode-daily/blob/master/diagonal_traverse.png)

2.思路
---

由题意可得，在对角线遍历中，其两个下标之和为一个定值，并且值时从0开始怎加到一定的值，又因为遍历的顺序时不同的，可以用temp来判定方向。并且两种情况是
行递减或者列递减，但是要满足下标大于等于0，并且小于二位数组的行数和列数，不然就会发生错误，最后返回数组即可,还要注意的一点是开始的列数应该是sum加1.因为
他首先要进行一步减的操作，加1才不会缺少情况。

3.代码
---

```c
class Solution {
public:
    vector<int> findDiagonalOrder(vector<vector<int>>& matrix) {
        int temp=0, sum=0,count=0;
        vector<int> ret;
        if (matrix.empty()) return ret;
        int m=matrix.size(), n=matrix[0].size();
        while (sum<=m+n-2) {
            if (temp==0) {
                int i=sum+1;
                while (i--) {
                    if (i>=0&&sum-i>=0&&i<m&&sum-i<n) {
                    ret.push_back(matrix[i][sum-i]);}
                }
                temp=1;
            }
            else if (temp==1) {
                int j=sum+1;
                while (j--) {
                    if (sum-j>=0&&j>=0&&j<n&&sum-j<m){
                    ret.push_back(matrix[sum-j][j]);}
                }
                temp=0;
            }
            sum++;
        }
        return ret;
    }
};
```

4.其他代码
---

```c
class Solution {
public:
    vector<int> findDiagonalOrder(vector<vector<int>>& matrix) {
        if (matrix.empty() || matrix[0].empty()) return {};
        int row=matrix.size();
        int col=matrix[0].size();
        vector<int> res(row*col);
        int r=0,c=0;
        for(int i=0;i<row*col;i++)
        {
            res[i]=matrix[r][c];
            if((r+c)%2==0) 
            {
                if(c==col-1) r++;
                else if(r==0) c++;
                else
                {
                    r--;
                    c++;
                }
            }
            else
            {
                
                if(r==row-1) c++;
                else if(c==0) r++;
                else
                {
                    c--;
                    r++;
                }
            }
        } 
        return res;
    }
};
```

这个代码也是利用了下标之和有一定的关系来写的，用r和c分别代表行标和列标，如果之和为偶数的话，就行递减，列递加，如果为奇数，就行递加，列递减。还有要讨论
两种特殊情况，最后返回数组即可。注意当输入的数组为空时，什么都不返回。
