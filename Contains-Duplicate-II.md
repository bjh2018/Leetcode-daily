Contains Duplicate II
====

1.问题描述
---

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k. <br>
给定一个数组，如果它们相等并且它们的下标之差小于给定的数，就返回正确，如果不存在这样的两个元素就返回错误。

2.思路
---

对数组直接进行遍历，然后看是否存在所要找的数即可。


3.代码I
---

```c
bool containsNearbyDuplicate(int* nums, int numsSize, int k) {
    for (int i=0; i<numsSize; i++) {
        for (int j=i+1; j<numsSize; j++) {
            if (nums[i]==nums[j]&&j-i<=k) return 1;
        }
    }
    return 0;
}
```

4.代码II
---

```c
bool containsNearbyDuplicate(int* nums, int numsSize, int k) {
    
    int min = INT_MAX, max = INT_MIN;
    for (int i = 0; i < numsSize; i++)
    {
        min = min < nums[i] ? min : nums[i];
        max = max > nums[i] ? max : nums[i];
    }
    
    int *hash = (int *)malloc(sizeof(int) * (max - min + 1));
    memset(hash, -1, (max - min + 1) * sizeof(int));
    for (int i = 0; i < numsSize; i++)
    {
        if (hash[nums[i] - min] == -1)
        {
            hash[nums[i] - min] = i;
        }
        else if (i - hash[nums[i] - min] <= k)
        {
            printf("i = %d  hash[nums[i] - min] = %d \n", i, hash[nums[i] - min]);
            return true;
        }
        else
        {
            hash[nums[i] - min] = i;
        }
    }
    
    
    return false;
}
```

找出数组中最大的数和最小的数，建立一个数组，数组的长度为最大值与最小值的差再加1，并把该数组的值都初始化为1，并用该数组来记录给定数组的每个元素的下标，如果出现当前元素的下标已经不为-1的情况，则说明前面肯定出现了一个与当前元素相等的数，
再比较它们的小标是否满足条件即可。

4.总结
---

因为要找重复的数字是否满足给定的条件，如果单纯遍历的话，就会好事很长，但是如果利用重复数组相等的条件，再加上一个辅助的数组就可以节省很多时间。
