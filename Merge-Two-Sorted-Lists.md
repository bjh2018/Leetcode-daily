Merge Two Sorted Lists
===

1.问题描述
---

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.<br>
Example: <br>
Input: 1->2->4, 1->3->4<br>
Output: 1->1->2->3->4->4<br>
给定两个已经排好序的链表，把它们也按照从小到大的顺序合并在一起，返回合并后的链表。

2.思路
---

（1）利用递归来解决，首先判断l1中的元素与l2中元素的大小关系,然后让符合条件的指针向后挪一位，让它等于剩下的元素合并后的链表，最后返回正确的链表即可。<br>
（2）重新定义一个链表，首先判断l1和l2中第一个元素的大小关系，确定头指针，然后把头指针赋给另一个指针，然后再进行相应的操作即可，最后返回头指针。

3.代码I
---

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2) {
    if (l1==NULL) return l2;
    if (l2==NULL) return l1;
    if (l1->val<=l2->val) {
        l1->next=mergeTwoLists(l1->next,l2);
        return l1;
    }
    else {
        l2->next=mergeTwoLists(l2->next,l1);
        return l2;
    }
}
```

4.代码II
---

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (l1==NULL) return l2;
        if (l2==NULL) return l1;
        ListNode *head=NULL;
        if (l1->val<=l2->val) {
            head=l1;
            l1=l1->next;
        }
        else {
            head=l2;
            l2=l2->next;
        }
        ListNode* p=head;
        while (l1&&l2) {
            if (l1->val<l2->val) {
                p->next=l1;
                l1=l1->next;
            }
            else {
                p->next=l2; l2=l2->next;
            }
            p=p->next;
        }
        if (l1) p->next=l1;
        else p->next=l2;
        return head;
    }
};
```
