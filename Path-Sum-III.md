Path Sum III
===

1.问题描述
---

You are given a binary tree in which each node contains an integer value.<br>
Find the number of paths that sum to a given value.<br>
The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).<br>
The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000. <br>

Example: 
---

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

2.思路
---

这道题目跟path sum拿到题目很像，但是那道题目是要求从根到底部看是否能够使枝叶的和等于给定的值，而这个只是找出给定的数中，所以要求很多种情况，
可以再写一个函数来确定每一个不同的开头所符合条件的情况的总种数。另一个函数是来确定不同的开头的种类。

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
int help(struct TreeNode* root, int m) {
    int ans=0;
    if (root==NULL) return ans;
    if (root->val==m) ans++;
    return ans+help(root->left, m-root->val)+help(root->right, m-root->val);
}
int pathSum(struct TreeNode* root, int sum) {
    if (root==NULL) return 0;
    else return help(root,sum)+pathSum(root->left, sum)+pathSum(root->right, sum);
}
```

4.总结
---

要注意不同的题目的不同的情况。
