Fair Candy Swap
===

1.问题描述
---

Alice and Bob have candy bars of different sizes: A[i] is the size of the i-th bar of candy that Alice has, and B[j] is the size of the j-th bar of candy that Bob has.
Since they are friends, they would like to exchange one candy bar each so that after the exchange, they both have the same total amount of candy.  (The total amount of candy a person has is the sum of the sizes of candy bars they have.)
Return an integer array ans where ans[0] is the size of the candy bar that Alice must exchange, and ans[1] is the size of the candy bar that Bob must exchange.
If there are multiple answers, you may return any one of them.  It is guaranteed an answer exists.<br>
 
Example 1:

```
Input: A = [1,1], B = [2,2]
Output: [1,2]
```

Example 2:

```
Input: A = [1,2], B = [2,3]
Output: [1,2]
```

Example 3:

```
Input: A = [2], B = [1,3]
Output: [2,3]
```

Example 4:

```
Input: A = [1,2,5], B = [2,4]
Output: [5,4]
```

2.思路
---

题目中的两个数组中的元素分别代表两个人所拥有的糖果棒的数量，通过交换其中的两个元素是两者拥有的数量一致。首先想到的是先把两者的总糖果数计算出来，然后通过
两个循环把交换的所有情况都判断一下，如果有满足条件的情况，跳出循环，返回即可。

3.代码
---

```c
class Solution {
public:
    vector<int> fairCandySwap(vector<int>& A, vector<int>& B) {
        int sum1=0, sum2=0;
        vector<int>ans(2,-1);
        for (int i=0; i<A.size(); i++) 
            sum1+=A[i];
        for (int j=0; j<B.size(); j++)
            sum2+=B[j];
        for (int i=0; i<A.size(); i++) {
            for (int j=0; j<B.size(); j++) {
                if (sum1-A[i]+B[j]==sum2-B[j]+A[i]) {
                    ans[0]=A[i]; ans[1]=B[j]; break;
                }
            }
            if (ans[0]>=1) break;
        }
        return ans;
    }
};
```
