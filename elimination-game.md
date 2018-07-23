elimination-game
===

1.问题描述
---

There is a list of sorted integers from 1 to n. Starting from left to right, remove the first number and every other number afterward until you reach the end of the list.
Repeat the previous step again, but this time from right to left, remove the right most number and every other number from the remaining numbers.
We keep repeating the steps again, alternating left to right and right to left, until a single number remains.
Find the last number that remains starting with a list of length n.<br>
Example: <br>

```
Input:
n = 9,
1 2 3 4 5 6 7 8 9
2 4 6 8
2 6
6

Output:
6
```

2.思路
---

第一次从左向右删除时，奇数都被删除了，只剩下了偶数，如果让n除以2，就可以得到一个从1到n/2的数列，下一次再从右向左删除时，返回的数就时该函数对应n/2的值在1-n/2数组中的镜像，
所谓镜像，就是例如在1，2，3，4中，1的镜像是4，2的镜像是3，不断进行递归就可以得到正确的结果。（可以通过不断地取一半的数来进行递归）

3.代码
---

```c
class Solution {
public:
    int lastRemaining(int n) {
        return n == 1 ? 1 : 2 * (1 + n / 2 - lastRemaining(n / 2));  
    }
};
```

