Can Place Flowers
===

1.问题描述
---

Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.<br>
Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.<br>
Example 1:<br>
Input: flowerbed = [1,0,0,0,1], n = 1<br>
Output: True<br>
<br>
Example 2:
Input: flowerbed = [1,0,0,0,1], n = 2<br>
Output: False<br>
<br>
Note:<br>
The input array won't violate no-adjacent-flowers rule.<br>
The input array size is in the range of [1, 20000].<br>
n is a non-negative integer which won't exceed the input array size.<br>
给定一个数组，数组中的元素如果等于1，则代表已经种上了花，如果是0，则代表还没种东西，可以在上面种花，要注意的是花不能相邻种植，只能隔一块空地再种植，并且给定的数组中1和0的位置不违反这个规则。

2.思路
---

要想知道该位置能不能种花，就要知道它前面的元素和后面的元素是否都为0，只有当三个元素连着都为0时才能种花，如果能种花就把该元素改为1，防止再次遍历到该元素时出错，还有就是要注意第一个元素和最后一个元素，它们只需判断其后或者其前的元素即可，所以要把这两种情况
单独讨论。<br>


3.代码
---

```c
bool canPlaceFlowers(int* flowerbed, int flowerbedSize, int n) {
    int num=0;
    for (int i=0; i<flowerbedSize; i++) {
        if (i==0&&flowerbed[i+1]==0&&flowerbed[i]==0) {
                num++;
                flowerbed[i]=1;
        }
        else if (i==flowerbedSize-1&&flowerbed[i-1]==0&&flowerbed[i]==0) {
            num++;
            flowerbed[i]=1;
        }
        else if (flowerbed[i]==0&&flowerbed[i+1]==0&&flowerbed[i-1]==0) {
            num++;
            flowerbed[i]=1;
        } 
    }
    return n<=num;
}
```

4.总结
---

要解决这个问题就要知道能种花的条件，并且把已经中号的花标记好也是很重要的。一开始认为1和0的排列（如果要是种的花的数目最大的花）只有1010...和0101...两种，但是后来才发现给定的已经拍好的数组中的元素不一定是这样排列的，可能是1001...，所以不能用异或来解决。
