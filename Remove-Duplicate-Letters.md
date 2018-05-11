Remove Duplicate Letters
===

1.问题描述
---

Given a string which contains only lowercase letters, remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.<br> 
Example:<br>
Given "bcabc"<br>
Return "abc" <br>
Given "cbacdcbc"<br>
Return "acdb" <br>
给定一个只包含小写字母的字符串，删除重复的字母，以便每个字母只出现一次。 在所有可能的结果中，你必须确保你的结果在字典顺序中是最小的。

2.思路
---

其实解决这道题的难点在于如何使所得到的字符串在字典顺序中是最小。用两个数组来解决，一个使int型，一个是bool型。int型的数组是来记录给定的字符串
中各个元素的个数，bool型的数组则是为让已经被判断过的字母不再进行又一次判断，节省时间，如果当前元素比result的最后一个元素小，并且此时该元素的个数不为0，
就把result的最后一个元素删掉，并把它调成再进行判断的状态。然后在循环结束之后，把该元素加到result后即可。注意result的第一个元素是"0"，所以要用substr函数
才能返回正确的结果。

3.代码
---

```c
class Solution {
public:
    string removeDuplicateLetters(string s) {
        vector<int> sum(256,0);
        vector<bool> judge(256,false);
        for (int i=0; i<s.size(); i++)
            sum[s[i]]++;
        string result="0";
        for (int i=0; i<s.size(); i++){
            sum[s[i]]--;
            if (judge[s[i]]) continue;
            while (s[i]<result.back()&&sum[result.back()]){
                judge[result.back()]=false;
                result.pop_back();
            }
            result+=s[i];
            judge[s[i]]=true;
        }
        return result.substr(1);
    }
};
```

4.总结
---

1.关于substr函数<br>
substr有2种用法：<br>
假设：string s = "0123456789";<br>
<br>
string sub1 = s.substr(5); //只有一个数字5表示从下标为5开始一直到结尾：sub1 = "56789"<br>
string sub2 = s.substr(5, 3); //从下标为5开始截取长度为3位：sub2 = "567"<br>
2.注意符合循环的条件，要是结果在字典中的顺序最小，就要在当前的元素的个数不为0的情况下，判断是不是当前元素是不是比结果此时的最后一个元素
小，如果小，就把它删除，并把其状态改成可以在进入循环的状态，就要用一个布尔型的数组，所以要用两个vector容器才可以实现。
