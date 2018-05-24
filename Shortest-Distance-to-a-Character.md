Shortest Distance to a Character
=======

1.问题描述
----

Given a string S and a character C, return an array of integers representing the shortest distance from the character C in the string.<br>
Example 1:<br>
Input: S = "loveleetcode", C = 'e'<br>
Output: [3, 2, 1, 0, 1, 0, 0, 1, 2, 2, 1, 0]<br>
给定一个字符数组和一个字符，返回一个数组，数组中的元素分别代表字符数组当前的元素距离给定的字母的最小距离。

2.思路
----

要得到其到给定字符的最小距离，可以先把给定字符的位置找到，再依次求出距离，取其中最小的，但是这样太费时间。可以用两次遍历来实现。我们不难发现，第一个给定的目标
字符出现之前，它前面的最小距离即为到第一个字母的距离，同理可知最后一个目标字符出现之后元的元素到它的最小距离。可以用pos来标记目标字符的位置，因为要取的是最小的距离
，所以可以先把pos置为-m，其中m是字符数组的长度，先正向遍历，再反向遍历，就可以把位于中间的元素到目标字符的字符的最小距离得出来。

3.代码
---

```c
class Solution {
public:
    vector<int> shortestToChar(string S, char C) {
        int m=S.size();
        vector <int> ans(m,m);
        int pos=-m;
        for (int i=0; i<S.size(); i++) {
            if (S[i]==C) pos=i;
            ans[i]=min(ans[i], abs(i-pos));
        }
        for (int j=m-1; j>=0; j--) {
            if (S[j]==C) pos=j;
            ans[j]=min(ans[j], abs(j-pos));
        }
        return ans;
    }
};
```
