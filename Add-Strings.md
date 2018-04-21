Add Strings
======

1.问题描述
---

Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.<br>
Note: <br>
The length of both num1 and num2 is < 5100.<br>
Both num1 and num2 contains only digits 0-9.<br>
Both num1 and num2 does not contain any leading zero.<br>
You must not use any built-in BigInteger library or convert the inputs to integer directly.<br>
给定两个以字符串表示的非负数整数num1和num2，返回num1和num2的总和。<br>
注意：<br>
num1和num2的长度都是<5100。<br>
num1和num2都只包含数字0-9。<br>
num1和num2都不包含任何前导零。<br>

2.思路
---

先把两个字符串的长度用函数求出来，然后再倒序相加，也就是从最后一位个位开始相加，注意用temp来确定是否进位，然后再最后判断一下要返回的是什么，根据是否进位
来判断返回的字符串，在相加的过程中要注意字母与整数之间的转换，还要注意在一开始设置返回的字符串时，就要把它的长度多设置两位，并把最后一位设为'\0'，以免出现
乱码。

3.代码
---

```c
char* addStrings(char* num1, char* num2) {
    int len1=strlen(num1), len2=strlen(num2);
    int len=len1>len2?len1:len2;
    char *res=(char *)malloc(sizeof(char)*(len+2));
    res[len+1]='\0';
    --len1;--len2;
    int temp=0;
    while (len1>=0||len2>=0) {
        if (len1>=0&&len2>=0){
        temp+=num1[len1]-'0'+num2[len2]-'0';
        }
        else if(len1>=0&&len2<0) {
            temp+=num1[len1]-'0';
        }
        else {
            temp+=num2[len2]-'0';
        }
        res[len--]=temp%10+'0';
        temp=temp/10;
        len1--;len2--;
    }
    if (temp) {
        res[0]=temp+'0';
        return res;
    }
    return res+1;
}
```

4.其他代码
----

```c
#define max(a,b) ((a)>(b)? (a):(b))
char* addStrings(char* num1, char* num2) {
    int len1=strlen(num1),len2=strlen(num2);
    int i,j,k=1+max(len1,len2);
    char carry=0;
    char *sum=(char *)malloc(sizeof(char)*(1+k));
    sum[k--]='\0';
    for(i=len1-1,j=len2-1;i>=0||j>=0;i--,j--,k--){
        char a= i>=0 ? num1[i] : '0';
        char b= j>=0 ? num2[j] : '0';
        sum[k]=(a+b+carry-2*'0')%10+'0';
        carry=(a+b+carry-2*'0')/10;
    }
    if(carry==1){
        sum[k]='1';
        return sum;
    }
    else
        return sum+1;         
}
```

基本思路相同，在细节上注意即可。
