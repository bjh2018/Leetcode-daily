Sum of Two Integers
===

1.问题描述
----

Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.<br>
Example:<br>
Given a = 1 and b = 2, return 3.<br>
给定两个整数，返回他们的和。要求不使用加减运算符。

2.思路
---

不能使用加减运算符，所以要用位运算。可以通过异或运算得到相加的和，用移位运算来进位。当数字用二进制表示时，如果两个位置都为1时就要进位，如果都为0的话，就不进位。
所以可以先用异或得到相加的和，再通过把其中的一个数向左移一位，在进行异或运算，这样就可以让结果的最后一位进位，一直进行这种操作，直到被进行移位操作的数变为0，就结束，返回结果即可。

3.代码
---

```c
class Solution {
public:
    int getSum(int a, int b) {
        int temp;
        while (b) {
            temp=a&b;
            a^=b;
            b=temp<<1;
        }
        return a;
    }
};
```

4.总结
---

举个例子: 11+5, 其二进制形式为11: 1011, 5: 0101<br>
1. 那么两个位置都为1的地方就需要进位, 所以进位值就为0001. 原位置两个数相加的结果为那个位置值的异或即1110, 即两个位置值如果不一样就为1, 一样的话要么两个位置原来值都为0结果也为0, 要么进位, 那么结果依然是0.<br> 
2. 接下来就要把进位位和下一位相加, 所以进位值左移一位,即0001变为0010, 重复上面操作可得新的进位值为0010, 原位置异或(即相加)结果为1100.<br>
3. 继续重复上面操作直到进位为0, 可得到最终结果10000, 即16<br>