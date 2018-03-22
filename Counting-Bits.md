Counting Bits
===

1.问题描述
---

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.<br> 
Example:<br>
For num = 5 you should return [0,1,1,2,1,2].<br>
给一个数num，返会一个数组，数组中的元素代表从0到num的数的二进制中1的个数.

2.思路
---

不难发现后面的数的二进制中1的个数与前面的数有关，只需要把下标为i/2的元素的一的个数加上，再加上当前的数对2的余数即为档期那的书二进制中1的个数。

3.代码
---

```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* countBits(int num, int* returnSize) {
    int *ans=(int *)malloc(sizeof(int)*(num+1));
    ans[0]=0;
    for (int i=0; i<num+1; i++) {
        ans[i]=i%2+ans[i/2];
    }
    *returnSize=num+1;
    return ans;
}
```

4.代码II
---

```c
int* countBits(int num, int* returnSize) {
    *returnSize = num+1;
    int i;
    int count;
    int* nums = (int *)malloc(sizeof(int)*(*returnSize));
    for(i=0;i<*returnSize;i++)
    {
        count = 0;
        if(i==0)
            nums[i] = 0;
        int tag = i;
        while(tag!=0)
        {
            if(((tag>>1)<<1)!=tag)//代表此位为1
                count++;
            tag>>=1;
        }
        nums[i] = count;
    }
    return nums;
}
```
利用移位运算，如果tag先向右移一位第一位会自动补成零，而原先的最后一位就会消失，在想左移一位的话，则会使第一位变成原来的第一位，而最后一位会变成0，如果tag的值没变，则表明最后一位是0，如果变了则说明最后
一位是1，就把count进行加一的操作，然后再把tag享有移一位，判断改变后的tag最后一位是不是0，直到最后tag变成0.
