plus-one
====

1.问题描述
---

Given a non-empty array of digits representing a non-negative integer, plus one to the integer.
The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.
You may assume the integer does not contain any leading zero, except the number 0 itself.<br>
Example 1:

```
Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

Example 2:

```
Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```

2.思路
---

在最后一位加上1，其实就是要考虑是否需要进位的情况，如果该位对应的数是9，说明需要进位，要把当前的位数对应的数字换成0，而且因为只是加上1，所以进位只能进一次，
如果当前的元素不是9，则说明不需要进位，直接加上1，然后返回数组即可。如果进行完循环之后数组的第一位是0，则说明要在数组的前面添上1来实现进位，最后返回数组即可。

3.代码
---

```c
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int n=digits.size();
        for (int i=n-1; i>=0; i--) {
            if (digits[i]==9) digits[i]=0;
            else {
                digits[i]+=1;
                return digits;
            }
        }
        if (digits.front()==0) digits.insert(digits.begin(),1);
        return digits;
    }
};
```

4.其他代码
---

```c
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        digits.back()++;
        int carry = 0;
        for (int i = digits.size()-1; i >= 0; i--) {
            digits[i] += carry;
            carry = digits[i] / 10;
            digits[i] %= 10;
        }
        if (carry > 0) {
            digits.insert(digits.begin(), carry);
        }
        return digits;
    }
};
```

这个代码是通过判断carry的大小来确定是否需要进位。
