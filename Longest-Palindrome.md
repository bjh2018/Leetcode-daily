 Longest Palindrome
 ===
 
 1.问题描述
 ---
 
 Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.<br>
This is case sensitive, for example "Aa" is not considered a palindrome here.<br>
Note:<br>
Assume the length of given string will not exceed 1,010.<br> 
Example: <br>
Input:<br>
"abccccdd"<br>
<br>
Output:<br>
7<br>
<br>
Explanation:<br>
One longest palindrome that can be built is "dccaccd", whose length is 7.<br>
给定一个字符数组，求它里面的元素能构成的回文字符串的最大的长度。

2.思路
---

分析这道题目可以看出，如果其中的一个字符出现的次数是偶数，那么它肯定可以加到回文中，如果出现的次数是奇数的话，那么只有一个字母能加到上面。也就是这道题的关键
就是去找到各个字母出现的次数。根据题意，字符数组中的元素都是小写字母，一个字母对应一个ASCII值，z的值为123，所以可以定义一个长度为125的整型数组，把里面的元素
都初始化为0，然后再判断是不是偶数，如果是偶数的话，就在结果上加上2，最终判断结果与数组长度的关系，如果想等，说明所有的元素都被用上了，如果不相等，则说明肯定有字母出现的
次数为奇数，所以再在结果的基础上加上1即可。

3.代码
---

```c
int longestPalindrome(char* s) {
    int temp[125]={0};
    int i=0,ans=0;
    int len=strlen(s);
    while (i<len) {
        ++temp[s[i]];
        if (temp[s[i]]%2==0)
            ans=ans+2;
        i++;
    }
    if (ans==len) return ans;
    else return ans+1;
}
```
