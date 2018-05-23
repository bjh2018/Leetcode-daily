Two Sum IV - Input is a BST
====

1.问题描述
----

Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.<br>
Example 1:<br>
Input:

```
    5
   / \
  3   6
 / \   \
2   4   7
```

Target = 9<br>
Output: True<br>

Example 2:<br>
Input: <br>

```
    5
   / \
  3   6
 / \   \
2   4   7
```

Target = 28<br>

Output: False<br>
给定一个二进制搜索树和一个目标编号，如果BST中存在两个元素，则它们的和等于给定目标，则返回true。

2.思路
---

因为要找出满足条件的两个数，所以可以用一个set的容器来解决。把k减去各个分支所对应的数都储存在set容器中，如果找到一个数与容器中的数相等，那么就存在这样的两个数，使得它们之和
等于k。

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
bool process(TreeNode* root, int k, set<int>& m) {
    if (root==NULL) return false;
    if (m.find(root->val)!=m.end()) return true;
    else {
        m.insert(k-root->val);
        return process(root->left, k, m)||process(root->right, k, m);
    }
}
class Solution {
public:
    bool findTarget(TreeNode* root, int k) {
        set <int> m;
        return process(root, k, m);
    }
};
```

4.总结
---

掌握这种求两个不同分支对应的数之和为给定的值的方法，如果当前元素不符合条件就把他对应的相加为k的数添加到数组中，在以后的遍历中看是否有元素等于它即可，还要注意对各种容器的
灵活运用。
