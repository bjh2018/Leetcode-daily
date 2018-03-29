Reverse String II
===

1.问题描述
---

Given a string and an integer k, you need to reverse the first k characters for every 2k characters counting from the start of the string. If there are less than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and left the other as original. <br>
<br>
Example:<br>
Input: s = "abcdefg", k = 2<br>
Output: "bacdfeg"<br>
<br>
Restrictions:<br> 
The string consists of lower English letters only.<br>
Length of the given string and k will in the range [1, 10000]<br>
给定一个字符串和一个整数k，则需要对从字符串开头算起的每2k个字符的前k个字符进行反转。如果剩下的数小于k，就把他们都反转，如果大于k而小于2k，就把前k个字符反转，如果大于2k，也是要把前k个字符反转。

2.思路
---

根据题目中的描述可知，当下标以2*k来相加的话，反转前k个数只需满足剩余的字符数比k大即可，剩下的情况就是全都需要反转的情况，在循环的过程中不难看出要实现对字符串中一部分的反转，所以可以通过写函数来实现，在不断的调用函数来满足对相应长度的字符串的改变。

3.代码
---

```c
void reverse(int begin, int end, char *s) {
    char tmp;
    while(begin<end) {
        tmp=s[end];
        s[end--]=s[begin];
        s[begin++]=tmp;
    }
}
char* reverseStr(char* s, int k) {
    int len=strlen(s);
    for (int i=0; i<len; i+=2*k) {
        if (len-i>=k) {
            reverse(i, i+k-1,s);
        }
        else{
            reverse(i, len-1, s);
        }
    }
    return s;
}
```

4.总结
---

（1）在实现对相应长度的反转的过程中要注意，指示单穿的交换第一个和最后一个是不可能实现反转的，因为在对其中一个赋值的同时，它就发生了变化，不再与之前相同，所以要用一个char型的中间变量来实现互换。<br>
（2）还有就是要注意i是以2*k为单位进行相加的，k个元素也是包括当前元素的，所以在判断剩下的元素的个数时是与len作比较。<br>
（3）最后要注意把多种情况中相痛的融合到一起，可以减少运行时间。
