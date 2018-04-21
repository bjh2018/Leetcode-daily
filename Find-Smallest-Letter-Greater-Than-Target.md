Find Smallest Letter Greater Than Target
===

1.问题描述
---

Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.<br> 
Letters also wrap around. For example, if the target is target = 'z' and letters = ['a', 'b'], the answer is 'a'. <br>
Examples:<br>
Input:<br>
letters = ["c", "f", "j"]<br>
target = "a"<br>
Output: "c"<br>
<br>
Input:<br>
letters = ["c", "f", "j"]<br>
target = "c"<br>
Output: "f"<br>
<br>
Input:<br>
letters = ["c", "f", "j"]<br>
target = "d"<br>
Output: "f"<br>
<br>
Input:<br>
letters = ["c", "f", "j"]<br>
target = "g"<br>
Output: "j"<br>
<br>
Input:<br>
letters = ["c", "f", "j"]<br>
target = "j"<br>
Output: "c"<br>
<br>
Input:<br>
letters = ["c", "f", "j"]<br>
target = "k"<br>
Output: "c"<br>
<br>
Note:<br>
letters has a length in range [2, 10000].<br>
letters consists of lowercase letters, and contains at least 2 unique letters.<br>
target is a lowercase letter.<br>
给定一个只包含小写字母的已排序字符列表，并给出一个目标字母目标，找到列表中比给定目标大的最小元素。<br>

2.思路
---

根据后面的例子可以知道，在不存在比target大的字母的时候，我们返回第一个即可，因为给定的字符数组是按照一定的顺序排列的。

3.代码
---

```c
char nextGreatestLetter(char* letters, int lettersSize, char target) {
    for (int i=0; i<lettersSize; i++) {
        if (letters[i]>target) {
            return letters[i];
        }
    }
    return letters[0];
}
```

4.其他代码
---

```c
char nextGreatestLetter(char* letters, int lettersSize, char target) {
    int low = 0;
    int high = lettersSize - 1;
    int mid;
    while (low <= high) {
        mid = (low + high) / 2;
        if (letters[mid] > target) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    if (letters[mid] > target) {
        return letters[mid];
    }
    return letters[(mid+1) % lettersSize];
}
```

用二分法和递归也可以解决。
