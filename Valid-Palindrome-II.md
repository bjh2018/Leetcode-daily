Valid Palindrome II
===

1.问题描述
---

Given a non-empty string s, you may delete at most one character. Judge whether you can make it a palindrome. <br>
Example 1:<br>
Input: "aba"<br>
Output: True<br>
<br>
Example 2:<br>
Input: "abca"<br>
Output: True<br>
Explanation: You could delete the character 'c'.<br>
给一个非空的字符串，你最多可已删除其中一个字母，判断你做过改变之后的字符串是不是有效的回文。

2.思路
---

遇到判断回文的问题，一般都是要从两头来看是否相等，当遇到不相等的情况时，就要删除一个字母，这就涉及到两种情况，所以要用两个循环来完成。基本省的四路就是只要
遇到不相等的情况，就按一个方向进行删除，然后最后看使它成为回文要删除的字母的个数是否满足条件。

3.代码
---

```c
bool validPalindrome(char* s) {
    int len=strlen(s);
    int i=0, j=len-1, ans1=0;
    while (i<j) {
        if (s[i]==s[j]) {
            i++;
            j--;
        }
        else {
            ans1++;
            j--;
        }
    }
    i=0;
    j=len-1;
    int ans2=0;
    while (i<j) {
        if (s[i]==s[j]) {
            i++;
            j--;
        }
        else {
            ans2++;
            i++;
        }
    }
    return ans1<=1||ans2<=1;
}
```

4.总结
---

起初的时候也是这种思路，只不过判断了一下当前j的元素是否与下一个i对应的元素相等，或者当前i的元素是否与下一个j的元素相等来判断是要删除那一个元素，
但这种方法存在缺陷，比如对于字符串ebcbbececabbacecbbcbe而言，就同时满足以上两种情况，无法做出判断，所以还是要用两个循环，能更简洁地解决这个问题。
