Set Matrix Zeroes
===

1.问题描述
---

Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in-place.<br>
Example 1:<br>
Input: <br>
[<br>
  [1,1,1],<br>
  [1,0,1],<br>
  [1,1,1]<br>
]<br>
Output:<br> 
[<br>
  [1,0,1],<br>
  [0,0,0],<br>
  [1,0,1]<br>
]<br>
Example 2:<br>
Input: <br>
[<br>
  [0,1,2,0],<br>
  [3,4,5,2],<br>
  [1,3,1,5]<br>
]<br>
Output:<br> 
[<br>
  [0,0,0,0],<br>
  [0,4,5,0],<br>
  [0,3,1,0]<br>
]<br>
Follow up:<br>
A straight forward solution using O(mn) space is probably a bad idea.<br>
A simple improvement uses O(m + n) space, but still not the best solution.<br>
Could you devise a constant space solution?<br>
给定一个m×n的矩阵，如果一个元素为0，则将其整个行和列设置为0.

2.思路
---

用两个数组来记录0所在行和列，说先把数组中的元素都置为0，在遍历一次二维数组，把符合条件的改成0，最后再遍历一次数组，把0所在的列和行的元素都置为0.

3.代码
---

```c
void setZeroes(int** matrix, int matrixRowSize, int matrixColSize) {
    int r=matrixRowSize, c=matrixColSize;
    int m[r];for (int k=0; k<r; k++) m[k]=0;
    int n[c];for (int q=0; q<c; q++) n[q]=0;
    for (int i=0; i<r; i++) {
        for (int j=0; j<c; j++){
            if (matrix[i][j]==0){ 
                m[i]=1;n[j]=1;}
        }
    }
    for (int i=0; i<r; i++)
        for (int j=0; j<c; j++)
            if (m[i]==1||n[j]==1)
                matrix[i][j]=0;
    return 0;
}
```

    
