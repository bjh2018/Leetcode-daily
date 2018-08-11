Maximum Length of Repeated Subarray
===

1.问题描述
---

Given two integer arrays A and B, return the maximum length of an subarray that appears in both arrays.<br>
Example 1:

```
Input:
A: [1,2,3,2,1]
B: [3,2,1,4,7]
Output: 3
Explanation: 
The repeated subarray with maximum length is [3, 2, 1].
```

Note:<br>
1 <= len(A), len(B) <= 1000<br>
0 <= A[i], B[i] < 100<br>

2.思路
---

给定两个整数数组去求他们公共的连续的子序列的最大的长度，这种极值问题一般要用dp来解决。用一个二维数组dp，其中dp[i][j]代表数组A的前i个元素和数组B的前j个元素
最长子数组的长度，如果dp[i][j]!=0，那么A[i]一定与B[j]相等，题目中给定的例子可以得到dp数组

```
  1 2 3 2 1
3 0 0 1 1 1
2 0 1 0 2 0
1 1 0 0 0 3
4 0 0 0 0 0 
7 0 0 0 0 0
```

由图可得，dp值不为0的地方，都是当A[i] == B[j]的地方，而且还要加上左上方的dp值，即dp[i-1][j-1]，所以当前的dp[i][j]就等于dp[i-1][j-1] + 1，而一旦A[i] != B[j]时，直接赋值为0，
不用多想，因为子数组是要连续的，一旦不匹配了，就不能再增加长度了。我们每次算出一个dp值，都要用来更新结果res，这样就能得到最长相同子数组的长度了。

3.代码
---

```c
class Solution {
public:
    int findLength(vector<int>& A, vector<int>& B) {
        int res=0;
        vector<vector<int>> dp(A.size(), vector<int>(B.size(), 0));
        for (int i=0; i<B.size(); i++) {
            if (B[i]==A[0]) {
                dp[0][i]=1;
            }
            else dp[0][i]=0;
        }
        for (int i=0; i<A.size(); i++) {
            if (A[i]==B[0]) {
                dp[i][0]=1;
            }
            else dp[i][0]=0;
        }
        for (int i=1; i<A.size(); i++) {
            for (int j=1; j<B.size(); j++) {
                if (A[i]==B[j]) {
                    dp[i][j]=dp[i-1][j-1]+1;
                    res=max(res, dp[i][j]);
                }
                else {
                    dp[i][j]=0;
                }
            }
        }
        return res;
    }
};
```

4.简化代码
---

```c
class Solution {
public:
    int findLength(vector<int>& A, vector<int>& B) {
        int res = 0;
        vector<vector<int>> dp(A.size() + 1, vector<int>(B.size() + 1, 0));
        for (int i = 1; i < dp.size(); ++i) {
            for (int j = 1; j < dp[i].size(); ++j) {
                dp[i][j] = (A[i - 1] == B[j - 1]) ? dp[i - 1][j - 1] + 1 : 0;
                res = max(res, dp[i][j]);
            }
        }
        return res;
    }
};
```
