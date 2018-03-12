Teemo Attacking
===

1.问题描述
---

In LOL world, there is a hero called Teemo and his attacking can make his enemy Ashe be in poisoned condition. Now, given the Teemo's attacking ascending time series towards Ashe and the poisoning time duration per Teemo's attacking, you need to output the total time that Ashe is in poisoned condition. <br>
You may assume that Teemo attacks at the very beginning of a specific time point, and makes Ashe be in poisoned condition immediately.<br>
Example 1:<br>
Input: [1,4], 2<br>
Output: 4<br>
Explanation: At time point 1, Teemo starts attacking Ashe and makes Ashe be poisoned immediately.<br> 
This poisoned status will last 2 seconds until the end of time point 2. <br>
And at time point 4, Teemo attacks Ashe again, and causes Ashe to be in poisoned status for another 2 seconds. <br>
So you finally need to output 4.<br>
<br>
Example 2:<br>
Input: [1,2], 2<br>
Output: 3<br>
Explanation: At time point 1, Teemo starts attacking Ashe and makes Ashe be poisoned.<br> 
This poisoned status will last 2 seconds until the end of time point 2. <br>
However, at the beginning of time point 2, Teemo attacks Ashe again who is already in poisoned status.<br> 
Since the poisoned status won't add up together, though the second poisoning attack will still work at time point 2, it will stop at the end of time point 3. <br>
So you finally need to output 3.<br>
数组中的元素代表Teemo进攻Ashe的时间点，后面的数字代表中毒持续的时间，求中毒的总时间。

2.思路
---

根据题意可知只有当数组中后面的元素减去他前面的元素的差大于等于duration，总时间才会加上duration，如果差小于duration，就要在结果上直接加上差即可，还有要注意当数组的长度为0时，中毒的时间一定为0.

3.代码I
---

```c
int findPoisonedDuration(int* timeSeries, int timeSeriesSize, int duration) {
    if (!timeSeriesSize) return 0;
    int num=duration;
    for (int i=1; i<timeSeriesSize; i++) {
        if (timeSeries[i]-timeSeries[i-1]>=duration) {
            num=num+duration;
        }
        else {
            num=num+timeSeries[i]-timeSeries[i-1];
        }
    }
    return num;
}
```

4.代码II
---

```c
#define Min(x,y) ((x) <= (y) ? (x) : (y)) 

int findPoisonedDuration(int* timeSeries, int timeSeriesSize, int duration) {
    if (timeSeriesSize ==0 || timeSeries == NULL){
        return 0;
    }
    int val =0;
    for(int i=1;i<timeSeriesSize;i++){
         val += Min( *(timeSeries+i) - *(timeSeries+(i-1)) , duration );
    }
    
    val+=duration;
    
    return val;
}
```

直接定义了Min再用循环取差和duration中较小的那一个，并在结果上累加，最后返回结果即可。
