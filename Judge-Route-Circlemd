Judge Route Circle
===

1.问题描述
---

Initially, there is a Robot at position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to the original place. <br>
The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are R (Right), L (Left), U (Up) and D (down). The output should be true or false representing whether the robot makes a circle.<br> 
Example 1:<br>
Input: "UD"<br>
Output: true<br>
<br>
Example 2:<br>
Input: "LL"<br>
Output: false<br>
最初，位置（0,0）处有一个机器人。 给出它的一系列动作，判断这个机器人是否有一个圆圈，这意味着它移回到原来的位置。移动顺序由一个字符串表示。 而每一个动作都是由一个人物来表现的。 有效的机器人移动R（右），L（左），U（上）和D（下）。 输出应该是真或假，表示机器人是否做出圆圈。<br>

2.思路
---

把左右和上下分为两类，用坐标的方法来记结果。如果向左x就减一，向右x就加一。如果向下y就加一，向上y就加一。如果最后x和y都是0，则说明最后机器人回到了原点。

3.代码
---

```c
bool judgeCircle(char* moves) {
    int len=strlen(moves);
    int x=0, y=0;
    for (int i=0;i<len; i++) {
        if (moves[i]=='L') x--;
        else if (moves[i]=='R') x++;
        else if (moves[i]=='U') y++;
        else if (moves[i]=='D') y--;
    }
    return (x==0&&y==0);
}
```

