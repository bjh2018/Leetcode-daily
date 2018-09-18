Valid Parenthesis String
====

1.问题描述
---

Given a string containing only three types of characters: '(', ')' and '*', write a function to check whether this string is valid. We define the validity of a string by these rules: <br>
Any left parenthesis '(' must have a corresponding right parenthesis ')'.<br>
Any right parenthesis ')' must have a corresponding left parenthesis '('.<br>
Left parenthesis '(' must go before the corresponding right parenthesis ')'.<br>
'*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string.<br>
An empty string is also valid.<br>

Example 1:<br>

```
Input: "()"
Output: True
```

Example 2:

```
Input: "(*)"
Output: True
```

Example 3:

```
Input: "(*))"
Output: True
```

2.思路
---

一看到这道题目，想到可以通过记录三个符号的个数，通过判断个数的大小关系来确定是否满足条件。但是这种做法忽略了右括号在左面，左括号在右边的情况，所以不能解决
这道题目。但是也可以用计数来解决。首先从正方向开始循环，当右括号的个数币比左括号于“*”的个数之和大时，说明不满足条件，因为右括号只能与它前面的左括号匹配。
但这一次的循环只是满足了每个右括号都有左括号和它配对，但是不能满足每个左括号都有右括号与之匹配，所以要再逆向进行一次循环即可。

3.代码
---

```c
class Solution {
public:
    bool checkValidString(string s) {
        int m=0, n=0, v=0;
        if (s.size()==1&&s[0]!='*') return false;
        for (int i=0; i<s.size(); i++) {
            if (s[i]=='(') {
                m++;
            }
            else if (s[i]==')') n++;
            else v++;
            if (n>m&&n>m+v) {
                return false;
            }
        }
        m=0; n=0; v=0;
        for (int i=s.size()-1; i>=0; i--) {
             if (s[i]=='(') {
                m++;
            }
            else if (s[i]==')') n++;
            else v++;
            if (m>n&&m>n+v) {
                return false;
            }
        }
        return true;
    }
};
```

[其他解法](https://www.cnblogs.com/grandyang/p/7617017.html)
