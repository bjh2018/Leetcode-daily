Valid Palindrome
===

1.问题描述
---

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.<br> 
For example,<br>
"A man, a plan, a canal: Panama" is a palindrome.<br>
"race a car" is not a palindrome. <br>
Note:<br>
Have you consider that the string might be empty? This is a good question to ask during an interview.<br>
For the purpose of this problem, we define empty string as valid palindrome. <br>
忽略字母的大小写和标点符号，按正反两个方向看，字母的顺序不变。

2.思路
---

由题意可得字符串会成中心对称，就要在首尾分别遍历，看前面的元素和后面的元素是否相等，如果不相等就要停止循环，返回false，而解决这个问题的关键就是判断
字符串中的元素是不是在字母表中，还有就是要忽略字母的大小写。


3.代码I
---

```c
bool isPalindrome(char* s) {
    int len = strlen(s);
    if(!len) //字符串长度为0
        return true;
    char *p1 = s, *p2 = s + len - 1;
    while(p1 < p2){
        if(!isalnum(*p1)) {//判断该字符是不是在字母表中
            p1++;
            continue;}
        if(!isalnum(*p2)){
            p2--;
            continue;}
        if(tolower(*p1++) != tolower(*p2--)) 
            return false;
    }
    return true;
}
```

4.代码II
---

```c
bool isPalindrome(char* s) {
if(s==NULL)
        return true;
    if(!strcmp(s,"OP"))
        return false;
    int i=0,j=strlen(s)-1,flag=0;
    while(i<j){
        if(s[i]<'0'||(s[i]>'9'&&s[i]<'A')||(s[i]>'Z'&&s[i]<'a')||s[i]>'z'){//如果不是英文字母
            i++;
            continue;
        }
        if(s[j]<'0'||(s[j]>'9'&&s[j]<'A')||(s[j]>'Z'&&s[j]<'a')||s[j]>'z'){
            j--;
            continue;
        }
        if(s[i]>='a'&&s[i]<='z') s[i]=s[i]-32;//如果是小写字母，就把它转化成大写字母
        if(s[j]>='a'&&s[j]<='z') s[j]=s[j]-32;
        if(s[i]==s[j]){
            i++;
            j--;
            continue;
        }
        if(s[i]!=s[j]){
            flag=1;
            break;
        }
        
    }
    if(flag)
        return false;
    else return true;
}
```

4.总结
---

（1）isalnum函数：<br>
            原型：extern int isalnum(int c);<br>
            用法：
                 #include <ctype.h>/* 包含 <ctype.h> */<br>
                 功能：判断字符变量c是否为字母或数字<br>
                 说明：当c为数字0-9或字母a-z及A-Z时，返回非零值，否则返回零。<br>
  （2）tolower:
              功能是把字母字符转换成小写，非字母字符不做出处理.<br>
              头文件：在VC6.0可以是ctype.h或者stdlib.h，常用ctype.h<br>
              目前在头文件iostream中也可以使用，C++ 5.11已证明。<br>
              用 法: int tolower(int c);<br>
              说明：和函数int _tolower( int c );功能一样，但是_tolower在VC6.0中头文件要用ctype.h<br>
