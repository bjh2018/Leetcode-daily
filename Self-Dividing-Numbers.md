Self Dividing Numbers
===

1.问题描述
---

A self-dividing number is a number that is divisible by every digit it contains. <br>
For example, 128 is a self-dividing number because 128 % 1 == 0, 128 % 2 == 0, and 128 % 8 == 0. <br>
Also, a self-dividing number is not allowed to contain the digit zero. <br>
Given a lower and upper number bound, output a list of every possible self dividing number, including the bounds if possible.<br> 
Example 1:<br>
Input: <br>
left = 1, right = 22<br>
Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 12, 15, 22]<br>
自分数是一个数字，它可以被其中包含的每个数字整除,给定两个数来代表数的范围，找出在这个范围内所有的自分数。

2.思路
---

因为要把每个数都判断一下，所以可以通过写一个函数来实现，要注意先判断各位得数是不是0，然后再判断是否可以整除。

3.代码
---

```c
bool judge(int n) {
    int num=n,temp=0;
    while (n>0) {
        int a=n%10;
        if (a==0) {
            temp=1;
            break;
        }
        else if (a!=0&&num%a!=0) {
            temp=1;
            break;
        }
        else if (a!=0&&num%a==0) {
            n=n/10;
        }
    }
    return temp==0;
}
int* selfDividingNumbers(int left, int right, int* returnSize) {
    int *ans=(int *)malloc(sizeof(int)*(right-left+1));
    int size=0;
    for (int i=left; i<=right; i++) {
        if (judge(i)) {
            ans[size++]=i;
        }
    }
    *returnSize=size;
    return ans;
}
```

4.总结
---

注意要分三种情况，因为如果只单纯地写两种情况的话，会出现除以0得情况，会造成运行时错误。
