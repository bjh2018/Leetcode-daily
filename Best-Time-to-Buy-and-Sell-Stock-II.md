 Best Time to Buy and Sell Stock II
 ===
 
 1.问题描述
 ---
 
 Say you have an array for which the ith element is the price of a given stock on day i.<br>
Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).<br>
给你顶一个数组，第i个元素代表第i天的股票价格，只有在售出现在的股票的条件下才能再重新购入股票，不限制交易的次数。

2.思路
---

可以先用一个数组来模拟这个过程，只需当当前的元素小与其后的元素的时候，相加即可。<br>
要注意的是一支股票再同一天可以买入也可以被立刻售出。比如说对于数组[3 4 7 3 2 9],可以把它相邻元素进行交易的结果携程如下数组[1 3 -4 -1 7],我们只需要把其中为正的数相加起来即可。

3.代码
---

```c
int maxProfit(int* prices, int pricesSize) {
    int ans=0;
    for (int i=0; i<pricesSize-1; i++) {
        if (prices[i+1]>prices[i]) {
            ans=ans+prices[i+1]-prices[i];
        }
    }
    return ans;
}
```

4.总结
---

起初联系它前面的一道题，当算把改变第一个数，然后把其后比他大的数与其作差，再从当前元素开始，找出比它大的数再相加，但是这种做法至少要用三个循环。而连续比较相邻两个元素数为大小的差并比较其实本质上和这种思路一样，只不过它把交易的次数最大化，把每个元素都利用了起来，比如说对数组[a b c]，若a<b<c的话，结果为b-a+c-b=c-a，
如果b<a<c,那么结果就是c-b，一定大于c-a，所以只需按上面代码的思路就可以得到正确的结果。
