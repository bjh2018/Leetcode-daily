bulls-and-cows
===

1.问题描述
---

You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.
Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. 
Please note that both secret number and friend's guess may contain duplicate digits.<br>
Example 1:

```
Input: secret = "1807", guess = "7810"

Output: "1A3B"

Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.
```

Example 2:

```
Input: secret = "1123", guess = "0111"

Output: "1A1B"

Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.
```

2.思路
---

这道题目是让我们找出给定的两个字符串中相同位置相等的数的个数以及猜对了数字但是位置不相同的数字的个数，也就是说两个字符串中存在某种对应关系，又因为字符串中都是数字，所以可以用一个整型的数组来记录
secret字符串中各个元素的个数，再运用一个循环找出公牛的数量，当两个字符串对应的字母不同并且此时guess字符串对应的哈希表存在的话，就把母牛的数量加1，然后要把此时guess对应的字母在哈希表中的数量减少1.
最后应用to_string把整型的数换成字符型，然后再加上A(B)即可。

3.代码
---

```c
class Solution {
public:
    string getHint(string secret, string guess) {
        int m[256]={0}, bull=0, cow=0;
        int l=secret.size();
        for (int i=0; i<l; i++) {
            if (secret[i]==guess[i]) bull++;
            else {
                ++m[secret[i]];
            }
        }
        for (int i=0; i<l; i++) {
            if (secret[i]!=guess[i] && m[guess[i]]) {
                cow++;
                --m[guess[i]];
            }
        }
        return to_string(bull)+"A"+to_string(cow)+"B";
    }
};
```
