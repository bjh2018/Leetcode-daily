Sort Characters By Frequency
===

1.问题描述
---

Given a string, sort it in decreasing order based on the frequency of characters.<br>
Example 1: 

```
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

Example 2: 

```
Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.
```

Example 3: 

```
Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```

2.思路
---

由ASCII可知，字符串中的元素的ASCII的值是从0到255，可以用vector申请空间，元素的类型为pair<int,int>，前一个int代表该元素对应的个数，后一个int来储存
该元素，用sort函数可以把元素按照其对应的个数排列，所以要重新写一个比较函数，排列完之后再遍历，改变字符串s中的元素，返回s即可。

3.代码I
---

```c
class Solution {
public:
    string frequencySort(string s) {
        class m{
            public:
            bool operator() (const pair<int,int> &a, const pair<int, int> & b) {
                return a.first>b.first;
            }
        };
        vector <pair<int,char>> n(256);
        for (int i=0; i<256; i++) {
            n[i]={0,i};
        }
        for (auto c:s) {
            n[c].first++;
        }
        sort(n.begin(), n.end(), m());
        for (int i=0,j=0; i<256; i++) {
            if (n[i].first==0) 
                break;
            while (n[i].first>0) {
                s[j++]=n[i].second;
                n[i].first--;
            }
        }
        return s;
    }
};
```

4.其他代码
---

```c
class Solution {
public:
    string frequencySort(string s) { 
        map <char,int> p;
        for (auto c:s) {
            p[c]++;
        }
        sort (s.begin(), s.end(), [&](const char &a, const char &b){
            return (p[a]>p[b]||p[a]==p[b]&&a<b);
        });
              return s;
    }
};
```
[链接](https://www.cnblogs.com/grandyang/p/6231504.html)
