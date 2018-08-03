is-subsequence
===

1.问题描述
---

Given a string s and a string t, check if s is subsequence of t. <br>
You may assume that there is only lower case English letters in both s and t. t is potentially a very long (length ~= 500,000) string, and s is a short string (<=100). <br>
A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ace" is a subsequence of "abcde" while "aec" is not).<br> 
Example 1:<br>
s = "abc", t = "ahbgdc"<br> 
Return true. <br>
Example 2:<br>
s = "axc", t = "ahbgdc"<br> 
Return false. <br>

2.思路
---

因为子字符串中字母的顺序与原字符串中字母的顺序相同，所以可以从原字符串的第一个元素开始来遍历，如果有元素与子字符串中的元素相同，就把加1判断下一个元素。如果最后下标与子字符串的长度相等，
则说明原字符串中有这样的子字符串，返回true即可。如果没有，就返回false。注意当子字符串的长度为0时，返回true即可。

3.代码
---

```c
class Solution {
public:
    bool isSubsequence(string s, string t) {
        int m=0;
        if (s.size()==0) return true;
        for (int i=0; i<t.size(); i++) {
            if (s[m]==t[i]) {
                m++;
            }
            if (m==s.size()) return true;
        }
        return false;
    }
};
```
