Reverse Bits
===

1.问题描述
---

Reverse bits of a given 32 bits unsigned integer.<br>
Example:<br>
Input: 43261596<br>
Output: 964176192<br>
Explanation: 43261596 represented in binary as 00000010100101000001111010011100,<br> 
             return 964176192 represented in binary as 00111001011110000010100101000000.<br>
把一个整数的二进制表示反转，然后在输出反转后的二进制所代表的整数。

2.思路
---

这道题和反转整数的那道题很像，只不过这道题是二进制，那道题是十进制而已。还是在求出当前二进制的时候，就把它加到结果上，然后再让结果一直乘以2即可。

3.代码
---

```c
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        int ans=0;
    for (int i=0; i<32; i++) {
        ans=ans*2+n%2;
        n=n/2;
    }
    return ans;
    }
};
```

4.其他代码
---

```c
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        uint32_t res = 0;
        for (int i = 0; i < 32; i++) {
            res <<= 1;
            res += n & 1;
            n >>= 1;
        }
        return res;
    }
};
```

这个代码是用位运算来解决的。原数不断右移取出最低位，赋给新数的最低位后新数再不断左移。
