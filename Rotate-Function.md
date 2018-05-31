Rotate Function
===

1.问题描述
----

Given an array of integers A and let n to be its length. <br>
Assume Bk to be an array obtained by rotating the array A k positions clock-wise, we define a "rotation function" F on A as follow: <br>
F(k) = 0 * Bk[0] + 1 * Bk[1] + ... + (n-1) * Bk[n-1].<br>
Calculate the maximum value of F(0), F(1), ..., F(n-1). <br>
Note:<br>
n is guaranteed to be less than 105.<br>

Example: 
----

```
A = [4, 3, 2, 6]

F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26

So the maximum value of F(0), F(1), F(2), F(3) is F(3) = 26.
```

给定一个整数A的数组，n为它的长度。
假设Bk是通过顺时针旋转阵列A k位置获得的数组，我们在A上定义“旋转函数”F如下：
F（k）= 0 * Bk [0] + 1 * Bk [1] + ... +（n-1）* Bk [n-1]。
计算F（0），F（1），...，F（n-1）的最大值。

2.思路
---

因为要得到当前元素后面的元素乘以相应的因数再相加，所以要用两个循环来实现，又因为是按顺时针的顺序进行的，所以在大多数情况下有元素的下标超过数组的长度所对应的
的最大小标，所以在进行加法的时候，要判断该元素的下标是否合理，若不合理，就在该下标上减去数组的长度即可。还有要注意因数的大小改变，要把因数定义在第二个循环
之前，这样才能实现它本身的相加，如果在第二个循环内定义的话，n就只可能为一个数。

3.代码
---

```c
class Solution {
public:
    int maxRotateFunction(vector<int>& A) {
        int m=A.size();
        if (m==0) return 0;
        int ans=INT_MIN;
        for (int i=0; i<m; i++) {
            int temp=0;
            int n=1;
            for (int j=i+1; j<m+i; j++) {
                if (j>=m) {
                    temp=temp+n*A[j-m];
                }
                else temp=temp+n*A[j];
                n++;
            }
            ans=ans>temp?ans:temp;
        }
        return ans;
    }
};
```

4.代码II
---

```c
class Solution {
public:
    int maxRotateFunction(vector<int>& A) {
        int s1=0,s2=0,c=0;
        int n=A.size();
        for (int i=0; i<n; i++) {
            s1+=A[i];
            s2+=c*A[i];
            c++;
        }
        int res=s2;
        for (int i=1; i<n; i++) {
            s2+=s1;
            s2-=(n*A[n-i]);
            if (s2>res) res=s2;
        }
        return res;
    }
};
```

为了找规律，可以先把数字抽象为A,B,C,D。则有：<br>
F(0)=0*A+1*B+2*C+3*D,<br>
F(1)=3*A+0*B+1*C+2*C,<br>
F(2)=0*C+1*D+2*A+3*B,<br>
F(3)=0*B+1*C+2*D+3*A,<br>
可得到<br>
F(1)=F(0)+sum-4D<br>
F(2)=F(1)+sum-4C<br>
F(3)=F(2)+sum-4B<br>
故有 F(i)=F(i-1)+sum-n*A[n-i]，就可以按照这个规律写出如上代码。
