Contains Duplicate III
===

1.问题描述
---

Given an array of integers, find out whether there are two distinct indices i and j in the array such that the absolute difference between nums[i] and nums[j] is at most t and the absolute difference between i and j is at most k. <br>
给一个数组，看是否有满足题中条件的两个数，如果有，就返回true，如果没有，就返回false。

2。思路
---

就是简单地遍历数组看是否满足条件即可，要注意的是两个数之间的距离一定是非负数，所以要用三目运算符来使两数之间的距离的距离为一非负数。

3.代码
---

```c
bool containsNearbyAlmostDuplicate(int* nums, int numsSize, int k, int t) {
    for (int i=0; i<numsSize; i++) {
        for (int j=i+1; j<numsSize; j++) {
            long int dis=(nums[i]>nums[j])?(nums[i]-nums[j]):(nums[j]-nums[i]);
            if (dis>=0&&dis<=t&&j-i<=k) {
                return true;
            }
        }
    }
    return false;
}
```

4.代码II
---

```c
int cmpptr(const void* a,const void* b){
	long num1=(*(*(int**)a));
	long num2=(*(*(int**)b));
	long ret=num1-num2;
	if (ret>0) {
		return 1;
	}
	else {
		return -1;
	}
}

bool containsNearbyAlmostDuplicate(int* nums, int numsSize, int k, int t) {
    int** ptr=(int**)calloc(numsSize, sizeof(int*));
	for (int i=0;i<numsSize;i++) {
		ptr[i]=&nums[i];
	}
	qsort(ptr, numsSize, sizeof(int*), cmpptr);
	if (k==0) {
		return false;
	}
	for (int i=0;i<numsSize;i++) {
		for (int j=i+1;j<numsSize;j++) {
			long num1=(*(ptr[i]));
			long num2=(*(ptr[j]));
			long num3=num1+t;
			if (num2>num1+t) {
				break;
			}
			long add1=ptr[i];
			long add2=ptr[j];
			if (labs((add1-add2)/4)<=k) {
				return true;
			}
		}
	}
	return false;
}
```

