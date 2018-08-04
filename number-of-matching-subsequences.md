number-of-matching-subsequences
===

1.问题描述
---

Given string S and a dictionary of words words, find the number of words[i] that is a subsequence of S.<br>

```
Example :
Input: 
S = "abcde"
words = ["a", "bb", "acd", "ace"]
Output: 3
Explanation: There are three words in words that are a subsequence of S: "a", "acd", "ace".
```

Note:<br>
All words in words and S will only consists of lowercase letters.<br>
The length of S will be in the range of [1, 50000].<br>
The length of words will be in the range of [1, 5000].<br>
The length of words[i] will be in the range of [1, 50].<br>

2.思路
---

首先想到的时延续上一道题目的思路来做，只是要把S遍历的次数很多，所以超时了。借鉴别人的代码得到，可以用一个二维数组来记录不同的字母在S字符串中对应的
位置，由提示可知，给定的字符串和字符串数组中字母均为小写字母，所以可以确定二维数组的行数最多为26行，列数无法确定。遍历S字符串一次就可以得到dp数组。然后从
words字符串数组的第一行开始遍历，用二分法查找判断字符串中的字符是否在容器内出现过。

3.代码I（超时）
---

```c
class Solution {
public:
    int numMatchingSubseq(string S, vector<string>& words) {
        int res=0;
        for (int i=0; i<words.size(); i++) {
            int m=0;
            for (int j=0; j<S.size(); j++) {
                if (words[i][m]==S[j]) {
                    m++;
                }
                if (m==words[i].size()) {
                    res++; break;}
            }
        }
        return res;
    }
};
```

4.代码II（超时）
---

```c
class Solution {
public:
    int numMatchingSubseq(string S, vector<string>& words) {
        int res=0;
        for (int i=0; i<S.size(); i++) {
            for (int j=0; j<words.size(); j++) {
                if (words[j][0]==S[i]) {
                    words[j].erase(0,1);
                if (words[j].size()==0) {
                    res++;
                }
            }
            }
        }
        return res;
    }
};
```

这个代码是遍历words数组，如果words数组的第一个元素与当前S字符串中的元素相同，就把数组的第一个元素删除，如果其对应的某一行长度为0，则说明该行对应的字符串
是符合条件的，在结果上加1即可。但这种方法依旧超时。

C++中string erase函数的使用（三种）
---

（1）erase(pos,n); 删除从pos开始的n个字符，比如erase(0,1)就是删除第一个字符<br>
（2）erase(position);删除position处的一个字符(position是个string类型的迭代器)<br>
（3）erase(first,last);删除从first到last之间的字符（first和last都是迭代器）<br>

5.代码III
---

```c
class Solution {
public:
    int numMatchingSubseq(string S, vector<string>& words) {
        vector <vector<int>> dp(26);
        int res=0;
        for (int i=0; i<S.size(); i++) {
            dp[S[i]-'a'].push_back(i);
        }
        for (int j=0; j<words.size(); j++) {
            int index=-1;
            bool m=true;
            for (auto c:words[j]) {
                auto x=upper_bound(dp[c-'a'].begin(), dp[c-'a'].end(), index);
                if (x==dp[c-'a'].end()) {
                    index=-1; m=false;
                }
                else {
                    index=*x;
                }
            }
            if (m) res++;
        }
        return res;
    }
};
```

auto是c++11中的新特性，定义为自动推断变量的类型。<br>
upper_bound()是二分查找函数，返回第一个比x大的值。<br>
lower_bound()返回的是一个不小于x的距离x最短值
