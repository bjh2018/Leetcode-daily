Maximum Product of Word Lengths
===

1.问题描述
---

Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.<br>
Example 1:

```
Input: ["abcw","baz","foo","bar","xtfn","abcdef"]
Output: 16 
Explanation: The two words can be "abcw", "xtfn".
```

Example 2:

```
Input: ["a","ab","abc","d","cd","bcd","abcd"]
Output: 4 
Explanation: The two words can be "ab", "cd".
```

Example 3:

```
Input: ["a","aa","aaa","aaaa"]
Output: 0 
Explanation: No such pair of words.
```

2.思路
---

要求两个字符串不含公共的元素，而且字符串中只含小写字母，共有26个字母，可以用32为的整型数进行与运算判断他们是否含有公共元素，32位中有23位来代表是否含有该元素，如果
有的话，该位上的数字就位1，如果没有就是0，所以首先初始化时，就把mask数组中的元素全都置为0，再用与运算来判断两个字符串是否含有公共元素，最后返回最大的乘积
即可。

3.代码
---

```c
class Solution {
public:
    int maxProduct(vector<string>& words) {
        vector <int> mask(words.size(),0);
        int res=0;
        for (int i=0; i<words.size(); i++) {
            for (int j=0; j<words[i].size(); j++) {
                mask[i] |= (1 << (words[i][j]-'a'));
            }
        }
        for (int i=0; i<words.size(); i++) {
            for (int k=i+1; k<words.size(); k++) {
                if ((mask[i] & mask[k])==0) {
                    int m=words[i].size();
                    int n=words[k].size();
                    res=max(res, m*n);
                }
            }
        }
        return res;
    }
};
```

