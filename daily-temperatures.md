daily-temperatures
===

1.问题描述
---

Given a list of daily temperatures, produce a list that, for each day in the input, tells you how many days you would have to wait until a warmer temperature. If there is no future day for which this is possible, put 0 instead. 
For example, given the list temperatures = [73, 74, 75, 71, 69, 72, 76, 73], your output should be [1, 1, 4, 2, 1, 1, 0, 0]. 
Note: The length of temperatures will be in the range [1, 30000]. Each temperature will be an integer in the range [30, 100]. 

2.思路
---

用两个循环来暴力解决。用count来记录相差的位数，当出现第一个比当前位置的元素大的元素时，就跳出第二个循环，并把相差的位数添加到结果数组中，最后返回数组即可。

3.代码
---

```c
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        vector <int> ret;
        int temp=0, count=0;
        for (int i=0; i<temperatures.size(); i++) {
            for(int j=i+1; j<temperatures.size(); j++) {
                count++;
                if (temperatures[j]>temperatures[i]) {
                    temp=1; break;
                }
            }
            if (temp==0) ret.push_back(0);
            else ret.push_back(count);
            count=0; temp=0;
        }
        return ret;
    }
};
```
