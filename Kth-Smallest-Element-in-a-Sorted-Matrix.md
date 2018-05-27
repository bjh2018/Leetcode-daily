Kth Smallest Element in a Sorted Matrix
====

1.问题描述
----

Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.<br>
Note that it is the kth smallest element in the sorted order, not the kth distinct element. <br>
Example: <br>
matrix = [<br>
   [ 1,  5,  9],<br>
   [10, 11, 13],<br>
   [12, 13, 15]<br>
],<br>
k = 8,<br>
<br>
return 13.<br>
Note: <br>
You may assume k is always valid, 1 ≤ k ≤ n^2.
给定一个二维数组，其中每行每列都按升序排列，返回数组中第K最小的数。

2.思路
---

可以用vector动态数组储存给定的二维数组中的数，然后用sort函数排序，返回数组中第K个数即为所求。

3.代码
---

```c
class Solution {
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        int m=matrix.size();
        vector <int> temp;
        for (int i=0; i<m; i++) {
            for (int j=0; j<m; j++) {
                temp.push_back(matrix[i][j]);
            }
        }
        sort(temp.begin(),temp.end());
        return temp[k-1];
     }
};
```

4.代码II
----

```c
class Solution {
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
    multiset <int> set;
        int m=matrix.size();
        for (int i=0; i<m; i++)
            for (int j=0; j<m; j++)
                set.insert(matrix[i][j]);
        multiset <int>::iterator s=set.begin();
        while (--k) s++;
        return *s;
    }
};
```

这个代码是用的multiset容器，它允许有重复的数字，而且它自身就存在比较函数，所以不用再重新排序，它不能通过下标直接访问元素，所以要通过指针来返回相应的值。
