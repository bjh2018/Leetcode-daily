Reverse Words in a String III
===

1.问题描述
---

Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.<br>
Example 1:<br>
Input: "Let's take LeetCode contest"<br>
Output: "s'teL ekat edoCteeL tsetnoc"<br>
<br>
Note: In the string, each word is separated by single space and there will not be any extra space in the string. <br>
给定一个字符串，你需要颠倒每个单词中的字符顺序，同时仍然保留空格和初始单词顺序。

2.思路
---

这道题目时颠倒指定的位置，所以打算写一个函数来实现颠倒确定区间的元素。可以用一个字符型的变量来当作媒介，实现第一个和最后一个元素的交换。最关键的就是最后的一组的颠倒，就在
循环结束之后，再颠倒即可。这样也解决了字符串中没有空格的情况。

3.代码
---

```c
void reverse (int start, int end, char *s) {
    char temp;
    while (start<end) {
        temp=s[start];
        s[start]=s[end];
        s[end]=temp;
        start++;
        end--;
    }
}
char* reverseWords(char* s) {
    int start=0,temp=0,i=0;
    for (i=0; s[i]; i++) {
        if (s[i]==' ') {
            reverse(start, i-1,s);
            start=i+1;
        }
    }
    reverse(start, i-1,s);
    return s;
}
```
