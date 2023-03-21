# 0207 Intersection of Two Linked Lists
Given two (singly) linked lists, determine if the two lists intersect. Return the inter­ secting node. Note that the intersection is defined based on reference, not value. That is, if the kth node of the first linked list is the exact same node (by reference) as the jth node of the second linked list, then they are intersecting.

## 思路

两链表相交->两节点指针相等（该节点next指针指向内存地址相等）

假定A是较长链表，curA、curB分别指向A、B链表的头节点

因为相交，所以交点往后节点数相等，所以先时curA移动(lenA-lenB)个节点，往后AB长度相同

接着判断curA与curB是否相同，如果不同，则同时往后移动一个节点

## AC代码
```c++
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
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* curA=headA,*curB=headB;

        int lenA=0,lenB=0;
        while(curA!=nullptr){
            lenA++;
            curA=curA->next;
        }
        while(curB!=nullptr){
            lenB++;
            curB=curB->next;
        }

        curA=headA;
        curB=headB;
        if(lenA<lenB){       //使A链表长于B链表
            swap(curA,curB);
            swap(lenA,lenB);
        }

        int gap=lenA-lenB;
        while(gap--){
            curA=curA->next;
        }

        while(curA!=nullptr&&curA!=curB){
            curA=curA->next;
            curB=curB->next;
        }
        if(curA) return curA;
        return nullptr;
    }
};
```
