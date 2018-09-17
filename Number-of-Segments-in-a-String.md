Number of Segments in a String
====

1.问题描述
---

Count the number of segments in a string, where a segment is defined to be a contiguous sequence of non-space characters.
Please note that the string does not contain any non-printable characters.
Example:
Input: "Hello, my name is John"
Output: 5

2.思路
---

根据题目中对段的描述可以得知，空格是解决问题的关键，空格的位置以及个数不同，得到的段的个数也就不同。首先用一个循环找到第一个不是空格的位置，从这个位置开始，
每碰到不连续的空格，就加1，如果空格出现在末尾，就要减去一段，才是对应字符串的所拥有连续序列的个数。

3.代码
---

```c
class Solution {
public:
    int countSegments(string s) {
        int m=0;
        int sum=0;
        for (; m<s.size(); m++) {
            if (s[m]!=' ') {
                break;
            }
        }
        if(m==s.size()) return 0;
        else sum=1;
            for (; m<s.size(); m++) {
                if (s[m]==' '&&s[m-1]!=' ')
                    sum++;
            }
        if (s[s.size()-1]==' ') sum--;
            return sum;
    }
};
```
