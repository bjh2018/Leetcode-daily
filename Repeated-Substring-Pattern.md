Repeated Substring Pattern
===

1.问题描述
----

Given a non-empty string check if it can be constructed by taking a substring of it and appending multiple copies of the substring together. You may assume the given string consists of lowercase English letters only and its length will not exceed 10000.<br> 
Example 1:<br>
Input: "abab"<br>
<br>
Output: True<br>
<br>
Explanation: It's the substring "ab" twice.<br>
<br>
Example 2:<br>
Input: "aba"<br>
<br>
Output: False<br>
<br>
Example 3:<br>
Input: "abcabcabcabc"<br>
<br>
Output: True<br>
<br>
Explanation: It's the substring "abc" four times. (And the substring "abcabc" twice.)<br>

2.思路
----

因为重复环节的长度时未知的，所以要从长度为1的部分开始循环，然后用俩个变量来比较对应位置的元素是否相等，为了让它一直和最前面几个最小单元比较，就把i一直对长度m比较
，如果j的大小与数组的长度减1相等，说明找到了循环的部分，返回true，其他情况返回false。

3.代码
---

```c
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        int n=s.length();
        for (int m=1; m<n; m++) {
            if (n%m==0) {
                for (int i=0, j=0; j<n&&s[i]==s[j]; ++i, ++j, i=i%m) {
                    if (j==n-1) return true;
                }
            }
        }
        return false;
    }
};
```
