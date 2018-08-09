fizz-buzz
===

1.问题描述
---

Write a program that outputs the string representation of numbers from 1 to n.<br>
But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.<br>
Example:

```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```

2.思路
---

根据题目中的要求吧所有的情况列出来即可，注意最后吧整形的数转换正字符串类型的元素要用函数to_string。

3.代码
---

```c
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector <string> ret;
        for (int i=1; i<=n; i++) {
            if (i%15==0) ret.push_back("FizzBuzz");
            else if (i%3==0) ret.push_back("Fizz");
            else if (i%5==0) ret.push_back("Buzz");
            else ret.push_back(to_string(i));
        }
        return ret;
    }
};
···
