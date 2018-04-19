Valid Square
===

1.问题描述
---

Given the coordinates of four points in 2D space, return whether the four points could construct a square.<br>
The coordinate (x,y) of a point is represented by an integer array with two integers.<br>
Example:<br>
Input: p1 = [0,0], p2 = [1,1], p3 = [1,0], p4 = [0,1]<br>
Output: True<br>
<br>
Note:<br> 
All the input integers are in the range [-10000, 10000].<br>
A valid square has four equal sides with positive length and four equal angles (90-degree angles).<br>
Input points have no order.<br>
给定四个坐标，判断他们能不能构成一个正方形，要注意的是坐标的顺序是随机的。

2.思路
---

正方形是四条边都相等，四个角都为直角的四边形，首先想到的是要根据这个条件先判断四条边是否相等，但是由于坐标给出的顺序是不按照一定的规律的，所以这种方法
并不不能判断是否能组成一个正方形。但是正方形可以分割成四个等腰直角三角形，并且任意的三个坐标都可以组成一个等腰直角三角形，等腰直角三角形的条件为最大的一条边
长度的平方等于较小的那两条边的平方的和，因为不确定哪条边是最大的，所以要分三种情况来讨论。

3.代码
---

```c
bool triangle(int *p1, int *p2, int *p3) {
    int a=(*p1-*p2)*(*p1-*p2)+(*(p1+1)-*(p2+1))*(*(p1+1)-*(p2+1));
    int b=(*p1-*p3)*(*p1-*p3)+(*(p1+1)-*(p3+1))*(*(p1+1)-*(p3+1));
    int c=(*p3-*p2)*(*p3-*p2)+(*(p3+1)-*(p2+1))*(*(p3+1)-*(p2+1));
    return ((a>b&&a>c&&b==c&&a==b+c)||(b>a&&b>c&&a==c&&b==a+c)||(c>a&&c>b&&a==b&&c==a+b));
}
bool validSquare(int* p1, int p1Size, int* p2, int p2Size, int* p3, int p3Size, int* p4, int p4Size) {
    return (triangle(p1,p2,p3)&&triangle(p1,p2,p4)&&triangle(p1,p4,p3)&&triangle(p4,p2,p3));
}
```
