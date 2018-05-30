Swap Nodes in Pairs
====

1.问题描述
----

Given a linked list, swap every two adjacent nodes and return its head.<br>
Example:<br>
Given 1->2->3->4, you should return the list as 2->1->4->3.<br>
给定一个链表，交换每两个相邻节点并返回其头部。

2.思路
----

以给定的链表1->2->3->4为例，在该链表的头部添加一个表头p，链表会变成0->1->2->3->4，进行第一次交换之后链表变为0->2->1->3->4，其中可以发现，0的后边变成
了2，2的后边变成了1，1的后面变成了3，所以要运用链表来实现这种改变，其中，p->next指向的是1，p->next->next指向的是2，我们令临时的指针等于2所在的位置，
剩余操作在代码中体现。

3.代码
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
    ListNode* swapPairs(ListNode* head) {
        ListNode *p, *s;
        p=new ListNode(0);
        p->next=head;
        head=p;
        while (p->next!=NULL&&p->next->next!=NULL) {
            s=p->next->next;
            p->next->next=s->next;//1的后面变成3
            s->next=p->next;//2的后面变成1
            p->next=s;//0的后面变成2
            p=s->next;
        }
        return head->next;
    }
};
```
