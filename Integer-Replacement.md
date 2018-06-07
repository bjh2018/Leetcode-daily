Integer Replacement
====

1.问题描述
---

Given a positive integer n and you can do operations as follow: <br>
<br>
If n is even, replace n with n/2.<br>
If n is odd, you can replace n with either n + 1 or n - 1.<br>
<br>
What is the minimum number of replacements needed for n to become 1?<br>
Example 1: <br>
Input:<br>
8<br>
<br>
Output:<br>
3<br>
<br>
Explanation:<br>
8 -> 4 -> 2 -> 1<br>
<br>
Example 2:<br> 
Input:<br>
7<br>
<br>
Output:<br>
4<br>
<br>
Explanation:<br>
7 -> 8 -> 4 -> 2 -> 1<br>
or<br>
7 -> 6 -> 3 -> 2 -> 1<br>
给定一个正整数n，你可以做如下操作：
如果n是偶数，则用n / 2替换n。
如果n是奇数，则可以用n + 1或n - 1替换n。
求n变为1所需的最小替换次数。

2.思路
---

分析题目不难发现要运用递归来做这道题，因为取n-1和n+1是两种情况，会出现很多分支，递归解决比较好。当n=1时，返回0，结束循环。如果n位偶数，就返回它的一半，然后
在结果上加上1.如果n为奇数，则说明n-1和n+1均为偶数，可以在结果上加2，再取n-1和n+1的一般所对应的步数中较小的那一个。

3.代码
---

```c
class Solution {
public:
    int integerReplacement(int n) {
        if (n==1) return 0;
        if(n%2==0) return 1+integerReplacement(n/2);
        else {
            long long m=n;
            return 2+min(integerReplacement((m-1)/2), integerReplacement((m+1)/2));
        }
    }
};
```

4.总结
---

要格外注意的一点就是n+1很有可能超出整数范围，所以要用long long型的数来代替n来进行变换。
