jewels-and-stones
===

1.问题描述
---

You're given strings J representing the types of stones that are jewels, and S representing the stones you have.  Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.
The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A".
<br>Example 1:

```
Input: J = "aA", S = "aAAbbbb"
Output: 3
```

Example 2:

```
Input: J = "z", S = "ZZ"
Output: 0
```

Note:<br>
S and J will consist of letters and have length at most 50.<br>
The characters in J are distinct.<br>

2.思路
---

题目中的意思是比较字符串S中与字符串J中元素相同的个数，又因为字符串中的元素均为字母，所以可以利用这个特性来记录J中元素的种类激起是否存在，查看ascii码表
可知要申请的整型数组的长度为58，然后对J遍历得到J中元素的存在情况，再对S遍历即可得出S中与J中元素相同的个数。

3.代码I
---

```c
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        vector <int> stack(58,0);
        for (int i=0; i<J.size(); i++) {
            stack[J[i]-'A']=1;
        }
        int count=0;
        for (auto c:S){
            if (stack[c-'A']==1) {
                count++;}
        }
        return count;
    }
};
```

4.代码II
---

```c
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        int answer=0;
         for(int j=0;j<J.size();j++)
        for(int i=0;i<S.size();i++)
        {
           if(S[i]==J[j])answer++;
        }
       
        return answer;
    }
};
```

直接一个一个与J字符串中的元素对比亦可得到结果。
