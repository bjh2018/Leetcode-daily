Binary Tree Tilt
===

1.问题描述
---

Given a binary tree, return the tilt of the whole tree.<br>
The tilt of a tree node is defined as the absolute difference between the sum of all left subtree node values and the sum of all right subtree node values. Null node has tilt 0.<br>
The tilt of the whole tree is defined as the sum of all nodes' tilt.<br>
Example:<br>
Input: <br>
Note:<br> 
The sum of node values in any subtree won't exceed the range of 32-bit integer. <br>
All the tilt values won't exceed the range of 32-bit integer.<br>
给定一棵二叉树，返回整棵树的倾斜度。树节点的倾斜被定义为所有左子树节点值的总和与所有右子树节点值的总和之间的绝对差值。 空节点具有倾斜0。整个树的倾斜度被定义为所有节点倾斜的总和。<br>

2.思路
---

根据题意可以看出，我们要求出该节点的左边和右边所有的节点值之和，所以用递归比较容易实现，即用一个函数来代表该节点的值，然后再在该函数中应用递归，返回当前的值加上它左边和右边的值，最终返回的就是改节点的值。

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
int sum(struct TreeNode * a) {
    if (a==NULL) return 0;
    else return a->val+sum(a->left)+sum(a->right);
}
int findTilt(struct TreeNode* root) {   
    if(root == NULL) return 0;
    else return abs(sum(root->left)-sum(root->right))+findTilt(root->left)+findTilt(root->right);
}
```

4.代码II
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
int getsum(struct TreeNode* root,int* sum)
{
    if(root==NULL)
        return 0;
    int left=getsum(root->left,sum);
    int right=getsum(root->right,sum);
    *sum=*sum+(left>right?left-right:right-left);
    return left+right+root->val;
}
int findTilt(struct TreeNode* root) {
    int sum=0,s;
    s=getsum(root,&sum);
    return sum;
}
```

这个代码的大致思想与第一个代码相同，亮点在于把sum的值改变地很有意思，直接对其取地址，通过改变指针指向的值来改变sun的值，十分巧妙。
