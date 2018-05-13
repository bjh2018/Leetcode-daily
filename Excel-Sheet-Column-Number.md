Excel Sheet Column Number
===

1.问题描述
---

Given a column title as appear in an Excel sheet, return its corresponding column number.<br>
For example:<br>
    A -> 1<br>
    B -> 2<br>
    C -> 3<br>
    ...<br>
    Z -> 26<br>
    AA -> 27<br>
    AB -> 28 <br>
    ...<br>
Example 1:<br>
Input: "A"<br>
Output: 1<br>
Example 2:<br>
Input: "AB"<br>
Output: 28<br>
Example 3:<br>
Input: "ZY"<br>
Output: 701<br>
给定一个Excel表格中显示的列标题，返回其相应的列号。<br>

2.思路
---

根据分析可以得到给定字符串所得的数字，可以得知它们之间的数量级是要乘以26，因为总共有26个字母，而且A代表的是1，所以字母要减去‘A’之后再加上1.如此循环即可。

3.代码
---

```c
int titleToNumber(char* s) {
    int ans=0;
    for (int i=0; i<strlen(s); i++) {
        ans=ans*26+s[i]-'A'+1;
    }
    return ans;
}
```
