Path Sum
===

1.问题描述
---

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.<br>
Note: A leaf is a node with no children.<br>
Example:<br>
Given the below binary tree and sum = 22,<br>

```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```

return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.<br>
给定一棵二叉树和一个和，确定树是否有根到叶的路径，以便沿路径加起来的所有值等于给定的总和。

2.思路
---

基本上是运用递归的思想，在sum上减去当前的跟对应的值，然后分两个路径，一个是指向根的左边，一个是指向右边，如果到达最后一个根，并且当前的值恰好等于sum的值，就返回正确，
其他情况就返回false，注意当root为空时，直接返回false即可。

3.代码
---

```c
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */
bool hasPathSum(struct TreeNode* root, int sum) {
    if(root==NULL) return false;
    else if (root->left==NULL&&root->right==NULL&&root->val==sum) return true;
    else if (hasPathSum(root->left, sum-root->val)|| hasPathSum(root->right,sum-root->val))
        return true;
    else return false;
}
```

4.总结
---

一开始也是想到要用减法，如果sum等于0，就返回正确，但其实当sum=0的时候很有可能没有到达根的最后一位，而且此时对应的root也是空的，不好判断。所以要从sum等于0的前一个步骤
来进行分析。如果此时root的左右均为空，而且root对应的值恰好等于此时sum的值，就返回true，否则就判断root的左右两只回路即可。
