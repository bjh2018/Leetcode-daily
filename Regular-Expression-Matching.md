Regular Expression Matching
===

1问题描述
---

Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.<br>
'.' Matches any single character.<br>
'*' Matches zero or more of the preceding element.<br>
The matching should cover the entire input string (not partial).<br>
Note:<br>
s could be empty and contains only lowercase letters a-z.<br>
p could be empty and contains only lowercase letters a-z, and characters like . or *.<br>
Example 1:<br>
Input:<br>
s = "aa"<br>
p = "a"<br>
Output: false<br>
Explanation: "a" does not match the entire string "aa".<br>
Example 2:<br>
Input:<br>
s = "aa"<br>
p = "a*"<br>
Output: true<br>
Explanation: '*' means zero or more of the precedeng element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".<br>
Example 3:<br>
Input:<br>
s = "ab"<br>
p = ".*"<br>
Output: true<br>
Explanation: ".*" means "zero or more (*) of any character (.)".<br>
Example 4:<br>
Input:<br>
s = "aab"<br>
p = "c*a*b"<br>
Output: true<br>
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore it matches "aab".<br>
Example 5:<br>
Input:<br>
s = "mississippi"<br>
p = "mis*is*p*."<br>
Output: false<br>
给定一个输入字符串和一个模式（p），实现正则表达式匹配，支持'.'和'*' . "."匹配任何单个字符。 '*'匹配零个或多个前面的元素。匹配应覆盖整个输入字符串（不是部分）。

2.思路
---

根据题意可以得知，"*" 号可以匹配两个或多个前面的元素，而 "." 可以匹配任何单个字符或者不匹配任何字符。根据递归的思想可以得知，如果它的第二个元素时"*"号的话，可以直接返回
isMatch(s+2,p),因为可以重复0次，但是如果第一个元素为".",且s中元素的个数不为0，或者两字符串的第一个元素的相同，就返回isMatch(s+1,p)，因为.可以重复0个元素,
而 "*" 可以重复它前面的元素。当当前元素为.或者元素相等的时候，就要返回isMatch(s+1,p+1),因为如果元素相等的话，就要让两个元素都向前移一位。

3.代码
---

```c
bool isMatch(char* s, char* p) {
    if (p[0]=='\0') return s[0]=='\0';
    if (p[1]=='*') return isMatch(s,p+2)||(((p[0]=='.'&&s[0]!='\0')||p[0]==s[0])&& isMatch(s+1, p));
    return ((p[0]=='.'&&s[0]!='\0')||(p[0]==s[0]))&& isMatch(s+1, p+1);
}
```
