Symmetric Tree
===

1.问题描述
---

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).<br>
For example, this binary tree [1,2,2,3,4,4,3] is symmetric: <br>

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following [1,2,2,null,3,null,3] is not:

```
    1
   / \
  2   2
   \   \
   3    3
```

2.思路
---

因为要给定的字符串是否对自己是否是镜像的，所以要用两个该类型的指针a、b，并且每个节点（除基部以外）都有两个方向，一个指向左边，另一个指向右边，如果满足镜像的话，
说明a->left=b->right,并且b->left=a->right,只有这两个条件满足时，才能说明满足镜像。还要注意的是很有可能其中一个变为空，而另一个不为空，所以要讨论这种情况。
当两个指针都指向为空时，则说明满足镜像，返回true即可。

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
    bool judge(TreeNode* a, TreeNode* b) {
        if (!a&&!b) {
            return true;
        }
        else if ((!a&&b)||(a&&!b)) return false;
        else if (a->val!=b->val) return false;
        return (judge(a->left, b->right)&&judge(a->right, b->left));
    }
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        else return judge(root->left, root->right);
    }
};
```
