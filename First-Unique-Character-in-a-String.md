First Unique Character in a String
===

1.问题描述
---

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1. <br>
Examples: <br>
s = "leetcode"<br>
return 0.<br>
<br>
s = "loveleetcode",<br>
return 2.<br>
<br>
Note: You may assume the string contain only lowercase letters.<br>
给定一个字符串，找出第一个不重复的字符，要注意字符串中只含小写字母。

2.思路
---

该字符串中只含小写字母，说明我们可以借用一个数组来代表该字母出现的次数，数组的长度是26，数组的下标等于当前元素的ASCII值减去a的ASCII值，就可以一一对应地
代表字符串中的元素，如果值为1的话，说明该元素是第一次出现，要比较它与其后地元素是否相等，如果没有出现相等的情况，就直接返回当前元素的下标即可。

3.代码I
---

```c
int firstUniqChar(char* s) {
   char *m,*n;
   int num[26]={0};
    memset(num,26,0);
    for (m=s;*m;m++) {
        num[*m-'a']++;
        if (num[*m-'a']>1) continue;
        for (n=m+1;*n;n++) {
            if (*n==*m) break;
        }
        if (*n==NULL&&num[*m-'a']==1) return m-s;
    }
    return -1;
}
```

4.代码II
---

```c
int firstUniqChar(char* s) {
    int hash[26] = {0};
    for(int i=0; s[i]!='\0'; i++) {
        hash[s[i]-'a']++;
    }
    for(int i=0; s[i]!='\0'; i++) {
        if(hash[s[i]-'a'] == 1) {
            return i;
        }
    }
    return -1;
}
```

代码I与代码II的本质思想相同，只不过代码II运用两个循环，更加简单明了。

4.总结
---

因为只含26个小写字母，所以字母出现的次数可以单独地记录下来，并且构成数组，这也是解决这个题的巧妙之处。
