Add Digits
 ===
 
 1.问题描述
 ---
 
 Given a non-negative integer num, repeatedly add all its digits until the result has only one digit. <br>
For example: <br>
Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it. <br>
给一个非负数，把它的各位上的数相加，如果和小于10，就返回，如果大于等于10，就再进行相同的操作，直到结果为小于10的数，也就是只有一位。

2.思路
---

因为有相同的步骤所以就写了个函数，在不断地调用函数就可以解决这个问题。

3.代码I
---

```c
int sum(int num) {
    int res=0;
    while (num>0) {
        res=res+num%10;
        num=num/10;
    }
    return res;
}
int addDigits(int num) {
    int ans=sum(num);
    while (ans%10!=ans) {
        ans=sum(ans);
    }
    return ans;
}
```
