Excel Sheet Column Title
===

1.问题描述
---

Given a positive integer, return its corresponding column title as appear in an Excel sheet.<br>
For example:<br>
    1 -> A<br>
    2 -> B<br>
    3 -> C<br>
    ...<br>
    26 -> Z<br>
    27 -> AA<br>
    28 -> AB <br>
    ...<br>
Example 1:<br>
Input: 1<br>
Output: "A"<br>
Example 2:<br>
Input: 28<br>
Output: "AB"<br>
Example 3:<br>
Input: 701<br>
Output: "ZY"<br>
给定一个整数，返回相应的字符串。

2.思路
---

给定字母返回数字的时候是要乘以26，然后再返回的过程，按常理来说是要对26取余，因为要返回相应的A B C...，所以要先减去1，然后再取余，再让n除以26。按照这种顺序
得出来的字符串与正确结果正好相反，所以要再申请一个数组，把结果反过来。

3.代码
---

```c
char* convertToTitle(int n) {
    char s[100]={0};
    int i=0;
    while (n){
        n=n-1;
        s[i++]=n%26+'A';
        n=n/26;
    }
    char *p=(char *)malloc (sizeof(char)*(i+1));
    int j=0;
    while (i--){
        p[j++]=s[i];
    }
    return p;
}
```

4.总结
---

一开始是先取余再减一，发现当n是26的时候会出现两个字母，所以应该先减再取余。
