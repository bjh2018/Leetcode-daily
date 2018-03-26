Best Time to Buy and Sell Stock
===

1.问题描述
---

Say you have an array for which the ith element is the price of a given stock on day i.<br>
If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.<br>
Example 1:<br>
Input: [7, 1, 5, 3, 6, 4]<br>
Output: 5<br>
<br>
max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)<br>
<br>
Example 2:<br>
Input: [7, 6, 4, 3, 1]<br>
Output: 0<br>
<br>
In this case, no transaction is done, i.e. max profit = 0.<br>
给定的数组中第i个元素代表第i天股票的价格，你只能进行一次交易，买入一只股票，并在某一天把它出售，求你可以获得的最大的利益。<br>

2.思路
---

根据题意不难看出你买股票要再你出售股票的前面，并且你可以选则不出售股票，所以利润的最小值为0，而不是某一个变化的值，知道这两点之后，可以用对数组的两次遍历来找出你可以获得的最大的利润，
但是我发现和前面的一道题很相似，课以通过把数组的值付给一个指针数组，然后对其用qsort函数排序，直接比较即可，因为在对指针排序的时候，它的地址也会跟着改变，只要比较地址的大小就可以判断
是不是在它前面，但是这种思路又好像是画蛇添足，把它做麻烦了。

3.代码I
---

```c
int cmp(const void *a, const void *b) {
    int num1=*(*(int**)a);
    int num2=*(*(int**)b);
    return num1-num2;
}
int maxProfit(int* prices, int pricesSize) {
    int **p=(int **)malloc(sizeof(int*)*pricesSize);
    for (int i=0; i<pricesSize; i++) {
        p[i]=&prices[i];
    }
    qsort(p,pricesSize,sizeof(int*),cmp);
    int max=0;
    for (int i=0; i<pricesSize; i++) {
        for (int j=i+1; j<pricesSize; j++) {
            if (p[i]<p[j]) {
                int n=*p[j]-*p[i];
                max=max<n?n:max;
            }
        }
    }
    return max;
}
```

4.代码II
---

```c
int maxProfit(int* prices, int pricesSize) {
   int i,j,min,maxpro;maxpro=0;min=prices[0];
    for(i=1;i<pricesSize;i++)
    {if(prices[i]<min) min=prices[i];
if((prices[i]-min)>maxpro) maxpro=prices[i]-min;
}
return maxpro;
}
```

这个思路是把前面的元素不断地取小的数，然后用当前的数减去前面最小的值，把结果与0比较，取其中较大的。（其实以前也见过这种解法）
