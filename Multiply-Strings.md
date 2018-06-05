Multiply Strings
====

1.问题描述
---

Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2, also represented as a string.<br>
Example 1:<br>
Input: num1 = "2", num2 = "3"<br>
Output: "6"<br>
Example 2:<br>
Input: num1 = "123", num2 = "456"<br>
Output: "56088"<br>
Note:<br>
The length of both num1 and num2 is < 110.<br>
Both num1 and num2 contain only digits 0-9.<br>
Both num1 and num2 do not contain any leading zero, except the number 0 itself.<br>
You must not use any built-in BigInteger library or convert the inputs to integer directly.<br>
给定两个非负数整数num1和num2表示为字符串，返回num1和num2的乘积，也表示为一个字符串。

2.思路
---

给定的两个整数，这两个整数的形式是字符型，这样就不用考虑数字的类型是long型还是int型了，而整数的乘法可以分步实现，具体参照[链接](http://www.cnblogs.com/TenosDoIt/p/3735309.html)
，然后按照乘法的规律算出结果后保存在一维整型数组中即可。第二步是进位，因为在计算的时候就把各位的乘积放到了数组的开始，所以从开头开始进位即可。第三步是找到首位不为0的位置，然后再
push到结果字符串中即可。

3.代码
---

```c
class Solution {
public:
    string multiply(string num1, string num2) {
        string res;
        int m=num1.size(),n=num2.size();
        int k=m+n-2, temp=0;
        vector <int> v(m+n,0);
        for (int i=0; i<m; i++) {
            for (int j=0; j<n; j++) {
                v[k-i-j]+=(num1[i]-'0')*(num2[j]-'0');
            }
        }
        for (int i=0; i<m+n; i++) {
            v[i]+=temp;
            temp=v[i]/10;
            v[i]%=10;
        }
        int i=m+n-1;
        while (v[i]==0) i--;
        if (i<0) return "0";
        while (i>=0) 
            res.push_back(v[i--]+'0');
        return res;
    }
};
```

