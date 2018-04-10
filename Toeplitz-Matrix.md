Toeplitz Matrix
===

1.问题描述
---

A matrix is Toeplitz if every diagonal from top-left to bottom-right has the same element.<br>
Now given an M x N matrix, return True if and only if the matrix is Toeplitz.<br>
 <br>
Example 1:<br>
Input: matrix = [[1,2,3,4],[5,1,2,3],[9,5,1,2]]<br>
Output: True<br>
Explanation:<br>
1234<br>
5123<br>
9512<br>
<br>
In the above grid, the diagonals are "[9]", "[5, 5]", "[1, 1, 1]", "[2, 2, 2]", "[3, 3]", "[4]", and in each diagonal all elements are the same, so the answer is True.<br>
Example 2:<br>
Input: matrix = [[1,2],[2,2]]<br>
Output: False<br>
Explanation:<br>
The diagonal "[1, 2]" has different elements.<br>
给定一个二维数组，如果对角线上的元素相同，就返回true，否则，则返回false。

2.思路
---

如果从正面想的话，就要保证每个对角线都要满足元素相等，所以直接比较该元素和与其相邻的在同一对角线上的数即可，如果不相等，直接返回false即可。

3.代码
---

```c
bool isToeplitzMatrix(int** matrix, int matrixRowSize, int *matrixColSizes) {
    for (int i = 0; i < matrixRowSize - 1; ++i)
    {
    	for (int j = 0; j < *matrixColSizes - 1; ++j)
    	{
    		if (matrix[i][j] != matrix[i + 1][j + 1])
    		{
    			return false;
    		}
    	}
    }
    return true;
}
```
