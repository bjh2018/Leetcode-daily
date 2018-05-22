Reverse Linked List
===

1.问题描述
---

Reverse a singly linked list.<br>
Example:<br>

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```

把给定的链表颠倒，然后返回即可。

2.思路
---

```
原始链表      1——2——3——4                                    
             head     nextNode
第一次转换后  head ：  2——3——4
             newhead：1
第二次转换后  head ：  3——4
             newhead：2——1
第三次转换后  head：   4
             newhead：3——2——1
第四次转换后  head：   NULL
             newhead：4——3——2——1
```

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
struct ListNode* reverseList(struct ListNode* head) {
    if (head==NULL) return head;
    struct ListNode* start=head;
    struct ListNode* temp=NULL;
    while (head->next) {
        temp=head->next->next;
        head->next->next=start;
        start=head->next;
        head->next=temp;
    }
    return start;
}
```
