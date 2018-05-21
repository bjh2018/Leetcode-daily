Remove Linked List Elements
===

1.问题描述
---

Remove all elements from a linked list of integers that have value val.<br>
Example:<br>

```
Input:  1->2->6->3->4->5->6, val = 6
Output: 1->2->3->4->5
```

删除链表中与给定的val的值相同的节点，并返回改变后的链表。

2.思路
---

改变链表中指定的元素，其中删除最后的元素和开始的元素是比较特殊的。可以先删除头指针中的符合题目中删除条件的节点，找到新的链表的头指针，然后再从该指针出发
去判断它后面的元素是否应该删除，其中第一个元素肯定是不用删除的，所以从它后面的一位开始找，直到找到val的值与给定的值不同，就让p指向它，所以要保证p和p的下一位
都不为空，这样才能找出循环截至的条件。

3.代码
---

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* removeElements(struct ListNode* head, int val) {
    while (head!=NULL&&head->val==val) {
        head=head->next;
    }
    struct ListNode* p=head;
    while (p!=NULL&&p->next!=NULL) {
        if (p->next->val==val)
            p->next=p->next->next;
        else 
            p=p->next;
    }
    return head;
}
```
