Rotated Digits
===

1.问题描述
---

X is a good number if after rotating each digit individually by 180 degrees, we get a valid number that is different from X.  Each digit must be rotated - we cannot choose to leave it alone.<br>
A number is valid if each digit remains a digit after rotation. 0, 1, and 8 rotate to themselves; 2 and 5 rotate to each other; 6 and 9 rotate to each other, and the rest of the numbers do not rotate to any other number and become invalid.<br>
Now given a positive number N, how many numbers X from 1 to N are good?<br>
Example:<br>
Input: 10<br>
Output: 4<br>
Explanation: <br>
There are four good numbers in the range [1, 10] : 2, 5, 6, 9.<br>
Note that 1 and 10 are not good numbers, since they remain unchanged after rotating.<br>
Note:<br>
N  will be in range [1, 10000].<br>
如果在将每个数字单独旋转180度后，X是一个很好的数字，我们得到一个与X不同的有效数字。每个数字都必须旋转 - 我们不能选择让它独立。
如果每个数字在旋转后保留一位数字，则该数字有效。 0,1和8自转; 2和5相互旋转; 6和9相互旋转，其余的数字不会旋转到任何其他数字并且变得无效。<br>
现在给出一个正数N，输出从1到N满足条件的数的个数。<br>

2.思路
---

我们要判断旋转180度后该数的情况就要把该数的各个位的数都判断一遍。而每个位的数都是0-9的一个数，其中如果出现3 4 7就一定不符合条件，因为它们旋转180度后的数字没有意义，如果是2 5 6 9就有可能是真的，要继续看下一位。一开始要把判断的布尔型的数设为false，因为1 0 8旋转180度
后还是它本身，不符合旋转后数字改变的条件。

3.代码
---

```c
bool judge (int n) {
    bool ans=false;
    while (n>0) {
        int num=n%10;
        if (num==3||num==7||num==4) 
            return false;
        if (num==2||num==5||num==6||num==9) 
            ans=true;
        n=n/10;
    }
    return ans;
}
int rotatedDigits(int n) {
    int count=0;
    for (int i=1; i<=n; i++){
        if(judge(i)) count++;
    }
    return count;
}
```
