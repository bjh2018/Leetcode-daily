Rotate Array
===

1.问题描述
---

Rotate an array of n elements to the right by k steps.<br>
For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].<br>
以k个步骤向右旋转n个元素的数组。例如，当n = 7和k = 3时，数组[1,2,3,4,5,6,7]被旋转到[5,6,7,1,2,3,4]<br>

2.思路
---

根据题目的描述可以想到用一个数组来储存原数组中的元素，然后再分析它们元素变化的规律即可。可以发现改变后的数组的前k个元素的下标是numsSize-k+i，后面元素的
下标为i-k，详见下面代码。还要注意的是k的至很可能比数组的长度要大，所以要进行去余数的操作，避免循环。

3.代码
---

```c
void rotate(int* nums, int numsSize, int k) {
    k=k%numsSize;
    int *stack=(int *)malloc(sizeof(int)*numsSize);
    for (int i=0; i<numsSize; i++) {
        stack[i]=nums[i];
    }
        for (int i=0; i<k;i++) {
        nums[i]=stack[numsSize-k+i];
    }
    for (int i=k; i<numsSize; i++) {
        nums[i]=stack[i-k];
    }
}
```

4.其他代码
---

```c
void reverse( int *nums,int begin,int end ){
    int tmp = 0;
    while( begin < end ){
        tmp = nums[begin];
        nums[begin++] = nums[end];
        nums[end--] = tmp;
    }
}
void three_reverse( int *nums,int numsSize,int n ){
    reverse(nums,0,n-1);
    reverse(nums,n,numsSize-1);
    reverse(nums,0,numsSize-1);
}
void rotate(int* nums, int numsSize, int k) {
    k %= numsSize;
    three_reverse(nums,numsSize,numsSize-k);
}
```
