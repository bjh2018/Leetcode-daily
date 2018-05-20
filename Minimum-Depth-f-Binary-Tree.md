Minimum Depth of Binary Tree
===

1.问题描述
---

Given a binary tree, find its minimum depth.<br>
The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.<br>
Note: A leaf is a node with no children.<br>
Example:<br>
Given binary tree [3,9,20,null,null,15,7],<br>

```
    3
   / \
  9  20
    /  \
   15   7
```

return its minimum depth = 2.
返回给定二叉树的最小的长度。

2.思路
---

和那道求二叉树的最长的长度相同，也是要运用递归的方法。但是有一种特殊情况，就是一个根可能只有一个分支会延伸下去，如果是左边是空的话，就返回右边的分支
再加1，这样就不会在左边的分支上再做改变了，如果右边的分支是空的，也这样处理即可。

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
    int minDepth(TreeNode* root) {
        if (!root) return 0;
        int m=minDepth(root->left);
        int n=minDepth(root->right);
        if (root->left==NULL) 
            return n+1;
        else if(root->right==NULL)
            return m+1;
        else {
        if (m<n) return m+1;
        else return n+1;
        }
    }
};
```
