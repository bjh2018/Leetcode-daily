Search a 2D Matrix
===

1.问题描述
----

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:<br>
Integers in each row are sorted from left to right.<br>
The first integer of each row is greater than the last integer of the previous row.<br>
Example 1:<br>
Input:<br>
matrix = [<br>
  [1,   3,  5,  7],<br>
  [10, 11, 16, 20],<br>
  [23, 30, 34, 50]<br>
]<br>
target = 3<br>
Output: true<br>
Example 2:<br>
Input:<br>
matrix = [<br>
  [1,   3,  5,  7],<br>
  [10, 11, 16, 20],<br>
  [23, 30, 34, 50]<br>
]<br>
target = 13<br>
Output: false<br>
给定一个二维数组，其中每一行的元素都是按升序排列的，并且该行的第一个元素比上一行的最后一个元素要大，看给定的数组中是否存在一个元素使它的值与target相等。

2.思路
---

由题意可知，该数组中的元素按升序排列的，要注意的是二维数组的行数和列数均不为0才有意义，故有两种方法解决（1）先判断给定的元素与数组的第一个元素和最后一个元素
之间的大小关系，然后再在二维数组中遍历，看是否存在元素的值等于target。（2）运用二分法，先找到数组中间的元素行属于列数之和mid=(start+end)/2，它所对应的
元素的行数为mid/n，n为每行中元素的个数，列数为mid%n，然后判断它与target的大小关系，决定是向前走一位，还是向后退一位，直到最后start<=end不成立结束循环。

3.代码
----

```c
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m=matrix.size(),temp=0;
        if (m==0) return false;
        int n=matrix[0].size();
        if (n==0) return false;
        if (target<matrix[0][0]||target>matrix[m-1][n-1]) return false;
        for (int i=0; i<m; i++) {
            for (int j=0; j<n; j++) {
                if (target-matrix[i][j]==0) {
                    temp=1; break;
                }
            }
        }
        return temp==1?true:false;
        }
};
```

```c
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if (matrix.empty()) return false;
        int m=matrix.size(),n=matrix[0].size();
        int start=0,end=m*n-1;
        while (start<=end) {
            int mid=(start+end)/2, i=mid/n,j=mid%n;
            if (matrix[i][j]==target) return true;
            else if (matrix[i][j]>target) end=mid-1;
            else start=mid+1;
        }
        return false;
    }
};
```
