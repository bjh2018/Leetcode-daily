Sum of Left Leaves
===

1.问题描述
---

Find the sum of all left leaves in a given binary tree.<br>
Example:<br>
There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.<br>
查找给定二叉树中所有左叶的总和并返回。

2.思路
---

如果当前指针的左叶存在，并且它没有子叶，就把它的值加到结果上，如果有子叶，就用递归把它的右边和左边的子叶再进行计算，如此循环即可。

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
    int sumOfLeftLeaves(TreeNode* root) {
        if (!root) return 0;
        int sum=0;
        if (root->left!=NULL&&!root->left->left&&!root->left->right)
            sum+=root->left->val;
        return sum+sumOfLeftLeaves(root->left)+sumOfLeftLeaves(root->right);
    }
};
```
