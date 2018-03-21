Rotate String
===

1.问题描述
---

We are given two strings, A and B.<br>
A shift on A consists of taking string A and moving the leftmost character to the rightmost position. For example, if A = 'abcde', then it will be 'bcdea' after one shift on A. Return True if and only if A can become B after some number of shifts on A.<br>
Example 1:<br>
Input: A = 'abcde', B = 'cdeab'<br>
Output: true<br>
<br>
Example 2:<br>
Input: A = 'abcde', B = 'abced'<br>
Output: false<br>
Note:<br>
A and B will have length at most 100.<br>
我们有两个字符串，A和B.A上的移位包括将字符串A移动并将最左边的字符移动到最右边的位置。 例如，如果A ='abcde'，那么在A上进行一次移位之后，它将是'bcdea'。返回True当且仅当A可以在A上进行一些移位后变成B。<br>

2.思路
---

用一个字符串来储存二倍的字符串A，然后用strstr函数来判断B是不是A的子字符串即可。

3.代码
---

```c
bool rotateString(char* A, char* B) {
    if(NULL == A || NULL == B)
        return false;
    int lena = strlen(A);
    int lenb = strlen(B);
    /*length not equal*/
    if(lena != lenb)
        return false;
    char *pos = NULL;
    char *AA = (char *)malloc((2 * lena +1) *sizeof(char));
    snprintf(AA,2*lena + 1,"%s%s",A,A);
    /*whether B is substr of AA*/
    pos = strstr(AA,B);
    if(pos)
        return true;
    return false;
}
```

4.总结
---

strstr函数：<br>
strstr(str1,str2) 函数用于判断字符串str2是否是str1的子串。如果是，则该函数返回str2在str1中首次出现的地址；否则，返回NULL<br>
snprintf函数<br>
函数原型为int snprintf(char *str, size_t size, const char *format, ...)。<br>
功能：<br>
将可变个参数(...)按照format格式化成字符串，然后将其复制到str中<br>
(1) 如果格式化后的字符串长度 < size，则将此字符串全部复制到str中，并给其后添加一个字符串结束符('\0')；<br>
(2) 如果格式化后的字符串长度 >= size，则只将其中的(size-1)个字符复制到str中，并给其后添加一个字符串结束符('\0')，返回值为欲写入的字符串长度。<br>
头文件#include<stdio.h><br>
函数返回值：<br>
若成功则返回欲写入的字符串长度，若出错则返回负值。<br>
与snprintf的返回值不同，sprintf的返回值是成功写入的字符串长度，此处需要谨慎处理！<br>
