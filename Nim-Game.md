Nim Game
===

1.问题描述
---

You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.
Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.<br>
Example:

```
Input: 4
Output: false 
Explanation: If there are 4 stones in the heap, then you will never win the game;
             No matter 1, 2, or 3 stones you remove, the last stone will always be 
             removed by your friend.
```

2.思路
---

这道题目关键是要找到规律，分析问题可得:<br>
n=1,2,3时，一定会赢，true<br>
n=4时，怎样都不会赢，false<br>
n=5,6,7,有机会赢（5-1=4， 6-2=4，7-3=4），true<br>
n=8时，一定不会赢，false<br>
n=9,10,11时，有机会赢（9-1=8，10-2=8，11-3=8）<br>
......<br>
可知，当n是4的倍数时，先捡石头的人肯定不会赢，其余情况下先捡石头的人有可能会赢。根据这一规律即可判断是否先出的人会赢。

3.代码
---

```c
class Solution {
public:
    bool canWinNim(int n) {
        if (n%4==0) return false;
        else return true;
    }
};
```

[详解](https://www.cnblogs.com/grandyang/p/4873248.html)
