Maximum Depth of Binary Tree
===

1.问题描述
---

Given a binary tree, find its maximum depth.<br>
The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.<br>
Note: A leaf is a node with no children.<br>
Example:<be>
Given binary tree [3,9,20,null,null,15,7],<br>

```
3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.<br>
给定一个二叉树，求它最大的深度。

2.思路
---

基本上是采用递归的思想，要想使深度最大，就要在根部的左右俩侧中取较大的深度，然后返回较大的加1即可。

3.代码
---

```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (!root) return 0;
        int left=maxDepth(root->left);
        int right=maxDepth(root->right);
        if(left>right)
            return left+1;
        else
            return right+1;
    }
};
```

4.总结
---

一开始也是用递归，但是很不幸的超时了，因为要取其中较大的一个的时候用三目运算，并没有把这两个数分别用字母代表，导致运行时间多了一倍，递归用了四次，
超时在所难免，所以以后在比较的时候，可以先把他们赋值给变量，再比较变量即可。
