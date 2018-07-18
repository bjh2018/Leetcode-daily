count-and-say
====

1.问题描述
---

The count-and-say sequence is the sequence of integers with the first five terms as following:

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

1 is read off as "one 1" or 11.<br>
11 is read off as "two 1s" or 21.<br>
21 is read off as "one 2, then one 1" or 1211.<br>
Given an integer n, generate the nth term of the count-and-say sequence.<br> 
Note: Each term of the sequence of integers will be represented as a string.<br> 
Example 1: <br>

```
Input: 1
Output: "1"
```

Example 2: 

```
Input: 4
Output: "1211"
```

2.思路
---

这道题目的关键是读懂题目，第一个是1，后一个字符串是对前一个字符串其中元素以及其个数的描述，n=2时，返回的字符串就是11，代表1个1，系啊一个字符串就是21，代表
两个1，按照这个规律就可以写出给定的n对应的字符串。因为每个字符串都是在前一个字符串的基础上写出来的，所以要先写出该字符串的前一个字符串。可以先用一个循环
来不断的写出1，2，····，n-1对应的字符串，然后再写出第n个数对应的字符串，可以利用string型的临时变量来记录字符串。

3.代码
---

```c
class Solution {
public:
    string countAndSay(int n) {
        string s= "1";
        for (int i=1; i<n; i++) {
            string temp= "";
            int count=1;
            for (int j=1; j<s.size(); j++) {
                if (s[j]==s[j-1]) count++;
                else {
                    temp=temp+(char)(count+'0')+s[j-1];
                    count=1;
                }
            }
            s=temp+(char)(count+'0')+s[s.size()-1];
        }
        return s;
    }
};
```
