Contains Duplicate
===

1.问题描述
----

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct. <br>
如果数组中有数出现了至少两次，就返回true，如果没有重复出现的数字，就返回false。

2.思路
---

把数组遍历两次，如果找到重复的数字，就直接返回即可，如果没有，就返回false，这种暴力的解决方法思路很简单，但是耗时太长。

3.代码I
---

```c
bool containsDuplicate(int* nums, int numsSize) {
    for (int i=0; i<numsSize; i++) {
        for (int j=i+1; j<numsSize; j++) {
            if (nums[i]==nums[j]) {
                return 1;
            }
        }
    }
    return 0;
}
```

4.代码II
---

```c
int comp(const void* a, const void* b)
{
    if(*(int* )a == *(int* )b)
    {
        return 0;
    }
    else
    {
        return (*(int* )a > *(int* )b)? 1 : -1;
    }
}

bool containsDuplicate(int* nums, int numsSize) {
    int i = 0;
    int zeroCount = 0;
    int xorResult = 0;
    
    qsort(nums, numsSize, sizeof(int), comp);
    for(; i < numsSize - 1; i++)
    {
        if(nums[i+1] - nums[i]  == 0)
        {
            return true;
        }

    }
    
    return false;
}
```

这个代码运用了qsort函数，直接比较当前元素和其后的元素即可，如果相等，就可以直接返回true。
