Coin Change
====

1.问题描述
---

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.<br> 
Example 1:<br>
coins = [1, 2, 5], amount = 11<br>
return 3 (11 = 5 + 5 + 1) <br>
Example 2:<br>
coins = [2], amount = 3<br>
return -1. <br>
Note:<br>
You may assume that you have an infinite number of each kind of coin.<br>
给定一个数组，数组中元素的值代表硬币的面值，给定一个整数，代表兑换硬币的总钱数，并返回要达到给定的钱数所需要的硬币数量的最小值。

2.思路
---

可以申请一个数组来储存各种和的最小的硬币数，并且把他们先置为-1，第一个元素的值为0，从和为1开始遍历，如果当前元素的值比和i的值小，或者等于i，并且他们差值
对应的种数不为-1使，就要对temp[i]的值进行改变，如果temp[i]>0，说明它已经被改变过，要从它对应的种数和当前他们差值加一种选最小的，如果它的置为-1，直接把当前的
种数赋值给它即可。

3.代码
---

```c
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector <int> temp(amount+1,-1);
        temp[0]=0;
        for (int i=1; i<=amount; i++) {
            for (int j=0; j<coins.size(); j++) {
                if (i-coins[j]>=0 && temp[i-coins[j]]!=-1) {
                    temp[i]=temp[i]>0?min(temp[i], temp[i-coins[j]]+1):temp[i-coins[j]]+1;
                }
            }
        }
        return temp[amount];
    }
};
```

4.总结
----

利用另一个数组来记录不同的的和所对应的种数，并且对每一个和都从硬币面值从一开始就遍历，在此过程中不断地取较小的值，就可以使最后结果最小。
