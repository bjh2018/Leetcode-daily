Bulb Switcher
===

1.问题描述
---

There are n bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the ith round, you toggle every i bulb. For the nth round, you only toggle the last bulb. Find how many bulbs are on after n rounds.<br> 
Example:<br>
Given n = 3.<br> 
<br>
At first, the three bulbs are [off, off, off].<br>
After first round, the three bulbs are [on, on, on].<br>
After second round, the three bulbs are [on, off, on].<br>
After third round, the three bulbs are [on, off, off]. <br>
<br>
So you should return 1, because there is only one bulb is on.<br>
最初有n个灯泡关闭。你首先打开所有的灯泡。然后，你关闭每一个第二个灯泡。在第三轮中，您每隔一个灯泡切换一次（如果它关闭则打开，如果打开则关闭）。对于第一轮，你切换每一个灯泡。对于第n轮，您只能切换最后一个灯泡。查找n轮后有多少个灯泡是开着的。<br>
例：<br>
给定n = 3。<br>
<br>
起初，三个灯泡[关闭，关闭，关闭]。<br>
第一轮后，三个灯泡[开，开，开]。<br>
第二轮后，三个灯泡[开，关，开]。<br>
第三轮后，三个灯泡[开，关，关]。<br>

2.思路
---

根据题意可知，如果灯被切换的次数为偶数的话，就是关着的，如果是奇数，那么灯就是开着的，只要灯的编号是一个数的倍数，那么它就会进行一次切换，比如<br>
2  1 * 2 2 * 1<br>
3  1 * 3 3 * 1<br>
4  1 * 4 2 * 2 4 * 1<br>
可以看出只有当该数是一个平方的数的时候执行的次数才是个奇数，也就是说这道题是要找满足是平方数的数的个数。

3.代码
---

```c
int bulbSwitch(int n) {
   int i=0,count=0;
   for (i=1; i*i<=n; i++) {
       ++count;
   }
    return count;
}
```
