Best Time to Buy and Sell Stock with Cooldown
===

1.问题描述
----

Say you have an array for which the ith element is the price of a given stock on day i.<br>
Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:<br>
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).<br>
After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)<br>
Example:<br>
Input: [1,2,3,0,2]<br>
Output: 3 <br>
Explanation: transactions = [buy, sell, cooldown, buy, sell]<br>
假设你有一个数组，其中第i个元素是第i天给定股票的价格。
设计一个算法来找到最大的利润。 您可以根据需要完成尽可能多的交易（即多次购买并出售股票的一个份额），并具有以下限制：
您不可以同时进行多笔交易（即您必须在再次购买之前出售股票）。
出售股票后，您无法在第二天买入股票。 （即冷却1天）<br>

2.思路
---

因为有冷冻期，所以在第i天有三种状态，用三个一维数组来代表第i天的状态。<br>
rest[i]代表在第i天之前的最后一个操作是冷冻.<br>
buy[i]代表在第i天之前的最后一个操作是买入股票。<br>
sell[i]代表在第i天之前的最后一个操作是卖出股票。<br>
可以得到如下的递推表达式：<br>

```
buy[i]=max(rest[i-1]-prices,buy[i-1]);
sell[i]=max(buy[i-1]+prices,sell[i-1];
rest[i]=(buy[i-1],sell[i-1],rest[i-1]);
```

但是如何保证[buy, rest, buy]的情况不会出现，这是由于buy[i] <= rest[i]， 即rest[i] = max(sell[i-1], rest[i-1])，这保证了[buy, rest, buy]不会出现。
又因为在冷冻的期间不进行任何操作，所以rest[i]=sell[i-1];所以上述表达式可以精简为两个递推式，然后可以用变量pre_buy,pre_sell来记录前一个就可以省略
申请动态数组。

3.代码
---

```c
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int buy=INT_MIN, pre_buy=0, pre_sell=0, sell=0;
        int m=prices.size();
        if (m<2) return 0;
        for (int i=0; i<m; i++) {
            pre_buy=buy;
            buy=max(pre_sell-prices[i], pre_buy);
            pre_sell=sell;
            sell=max(pre_sell, pre_buy+prices[i]);
        }
        return sell;
    }
};
```
