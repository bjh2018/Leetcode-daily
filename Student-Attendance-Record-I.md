Student Attendance Record I
===

1.问题描述
---

You are given a string representing an attendance record for a student. The record only contains the following three characters:<br> 
<br>
'A' : Absent.<br> 
'L' : Late.<br>
'P' : Present. <br>
<br>
A student could be rewarded if his attendance record doesn't contain more than one 'A' (absent) or more than two continuous 'L' (late).<br> 
You need to return whether the student could be rewarded according to his attendance record.<br>
Example 1:<br>
Input: "PPALLP"<br>
Output: True<br>
<br>
Example 2:<br>
Input: "PPALLL"<br>
Output: False<br>
用A，L，P分别代表缺勤、迟到和出勤三种情况，只有当缺勤的次数不超过一次，或者迟到的次数不超过2次，才能有评优的资格，给定一个字符串来代表这三种情况
，判断是否能评优的资格。

2.思路
---

用一个整型的数来代表缺勤的次数，然后用另一个数来判断是否又连续的三次迟到的情况，最后把两种情况综合一下返回即可。

3.代码
---

```c
bool checkRecord(char* s) {
    int a=0,b=0;
    for (int i=0; s[i]!='\0'; i++) {
        if (s[i]=='A') a++;
        if (s[i]=='L'&&s[i+1]=='L'&&s[i+2]=='L'&&s[i+2]!='\0') b=1;
    }
    if (a<=1&&b==0) return true;
    else return false;
}
```
