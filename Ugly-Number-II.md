Ugly Number II
===

1.问题描述
---

Write a program to find the n-th ugly number.<br> 
Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers. <br>
Note that 1 is typically treated as an ugly number, and n does not exceed 1690.<br>
找出从1开始的第n个丑数，其中丑数是被2 3 5这三个数中的数整除后为1的数。

2.思路
---

首先，写了一个函数来判断是不是符合条件，然后再从1开始遍历，找到第n个符合条件的数，但这种方法耗时很长，最终超时了。其实从1开始找丑数也可以让他们成以2 3 5这三个数其中的一个，也就是建立一个数组，
找出其中最小的数，把它添加到数组中，要注意只有当当前的数被添加到数组中之后，才对它进行乘以2或3或5.然后再重复这个步骤。

3.代码（超时）
---

```c
bool judge(int m) {
    while (m!=0&&m!=1) {
        if (m%2==0) m/=2;
        if (m%3==0) m/=3;
        if (m%5==0) m/=5;
    }
    return m==1;
}
int nthUglyNumber(int n) {
    int count=0,i;
    for ( i=1; ; i++) {
        if (judge(i)) count++;
        if (count==n) break;
    }
    return i;
}
```

4.代码（Accepted）

```c
int nthUglyNumber(int n) {
    int *ans=(int *)malloc(sizeof(int)*n);
    ans[0]=1;
    int x=0, y=0, z=0;
    int a=2, b=3, c=5;
    for (int i=1; i<n; i++) {
        int temp=a>b?b:a;
        int min=temp<c?temp:c;
        ans[i]=min;
        if(min==a){
        a=2*ans[++x];
        }
        if(min==b){
        b=3*ans[++y];
        }
        if(min==c){
        c=5*ans[++z];}
    }
    return ans[n-1];
}
```

5.总结
---

（1）在利用第二种方法的时候要注意，乘以2 3 5属于三种情况，所以要用三个if来计数。
（2）其实在超时之后很容易想到乘以这三个数，来找到第n个丑数，但是却不知道该怎么留下原始的东西，所以不如就把三种情况都罗列出来，在合适的情况下分别进行
自己的乘法，再取最小值赋值给数组即可。<br>
[参考思路](https://blog.csdn.net/guang09080908/article/details/47780619)
