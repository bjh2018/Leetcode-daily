Distribute Candies
===

1.问题描述
---

Given an integer array with even length, where different numbers in this array represent different kinds of candies. Each number means one candy of the corresponding kind. You need to distribute these candies equally in number to brother and sister. Return the maximum number of kinds of candies the sister could gain. <br>
Example 1:<br>
Input: candies = [1,1,2,2,3,3]<br>
Output: 3<br>
Explanation:
There are three different kinds of candies (1, 2 and 3), and two candies for each kind.<br>
Optimal distribution: The sister has candies [1,2,3] and the brother has candies [1,2,3], too.<br> 
The sister has three different kinds of candies. <br>
<br>
Example 2:<br>
Input: candies = [1,1,2,3]<br>
Output: 2<br>
Explanation: For example, the sister has candies [2,3] and the brother has candies [1,1].<br> 
The sister has two different kinds of candies, the brother has only one kind of candies. <br>
Note: <br>
The length of the given array is in range [2, 10,000], and will be even.<br>
The number in given array is in range [-100,000, 100,000].<br>
根据题目描述和例子，可以知道，此题是让求每个人分得的糖果的种类的最大值，可以看成是分成两个人，一定要平均分配，也就是最多能分得的糖果的种类
为数组长度的一半，关键是判断数组中有效的数字的个数，也就是看把数组缩到没有重复数字的情况，看他的数组的长度与原数组长度的一半的关系。

2.思路
---

应用qsoort函数对给定的数组进行排序，然后再判断当前元素与其上一个元素是否相等，用一个整型的变量来记录有效长度，再比较即可。

3.代码
---

```c
int cmp(const void *a, const void *b) {
    return *(int*)a-*(int*)b;
}
int distributeCandies(int* candies, int candiesSize) {
    int sum=1;
    qsort(candies,candiesSize,sizeof(int),cmp);
    for (int i=1; i<candiesSize; i++) {
        if (candies[i]!=candies[i-1]) {
            sum++;
        }
    }
    return sum>=(candiesSize/2)?(candiesSize/2):sum;
}
```

4.其他代码
---

```c
int distributeCandies(int* candies, int candiesSize) {
    
    char hash[200001] = {0};
    int half_candiesSize = candiesSize >> 1;
    int kind_count = 0;
    
    for (int i = 0; i < candiesSize; i++){
        if (hash[candies[i]+100000] == 0){
            kind_count++;
            hash[candies[i]+100000] = 1;
            if (kind_count >= half_candiesSize){
                return half_candiesSize;
            }
        }
    }
    
    return kind_count;
    
}
```
从note中可以看出，数组中元素的个数最多为100000个，所以把一个数组的长度设为200001，并且如果一个数出现过一次，那么它在对应数组中的值就会变为1，这样再遍历
到和它相等的数时，就不会再算到有效长度中，就能得出有效长度。

关于hash
----
[hash实例讲解](https://blog.csdn.net/xiaofei0859/article/details/73647775)
