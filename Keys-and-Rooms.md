Keys and Rooms
===

1.问题描述
---

There are N rooms and you start in room 0.  Each room has a distinct number in 0, 1, 2, ..., N-1, and each room may have some keys to access the next room. <br>
Formally, each room i has a list of keys rooms[i], and each key rooms[i][j] is an integer in [0, 1, ..., N-1] where N = rooms.length.  A key rooms[i][j] = v opens the room with number v.<br>
Initially, all the rooms start locked (except for room 0). <br>
You can walk back and forth between rooms freely.<br>
Return true if and only if you can enter every room.<br>

Example 1:

```
Input: [[1],[2],[3],[]]
Output: true
Explanation:  
We start in room 0, and pick up key 1.
We then go to room 1, and pick up key 2.
We then go to room 2, and pick up key 3.
We then go to room 3.  Since we were able to go to every room, we return true.
```

Example 2:

```
Input: [[1,3],[3,0,1],[2],[0]]
Output: false
Explanation: We can't enter the room with number 2.
```

2.思路
---

这道题目是给定一个二维数组，代表各个房间所拥有的钥匙，判断能否走遍所有的房间。我们从房间0出发，会从房间0中得到一些钥匙，然后才可以进入要是
钥匙所对应的房间，也就是说这种找房间的步骤是有一定顺序的，要用顺序容器来记录这种顺序，还要用一个可除去重复元素的容器来记录已经到达的房间。
可以用stack容器来存储已经获得的钥匙，每遍历一个房间，就pop出来一个元素，直到stack中不含元素。用set容器来记录已经到达的房间号，如果set的长度与
二维数组的长度相同，说明已经去过了所有的房间。

3.代码
---

```c
class Solution {
public:
    bool canVisitAllRooms(vector<vector<int>>& rooms) {
        stack<int>DFS;
        DFS.push(0);
        set<int>visited;
        visited.insert(0);
        while (!DFS.empty()) {
            int i=DFS.top();
            DFS.pop();
            for (auto j:rooms[i]) {
                if (visited.count(j)==0) {//如果没有去过房间j，就把它添加到stack和set容器中
                    visited.insert(j);
                    DFS.push(j);
                }
                if (visited.size()==rooms.size()) return true;
            }
        }
        return visited.size()==rooms.size();
    }
};
```

[DFS与BFS算法](https://www.cnblogs.com/whywhy/p/4888632.html)
