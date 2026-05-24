# Leetcode 21.合并两个有序链表
>Problem: [21.合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/description/?envType=problem-list-v2&envId=linked-list)

## 个人思路
作为我在leetcode上练手的第一题，我是知道大致思路的：*先大小依次遍历所给的两个链表，然后再填入一个大链表中。* 有点像数组的做法。但是问题在于，**我对于遍历链表以及将其连入另一个链表的操作很陌生。** 我不知道什么时候**添加指针**，应该添加几个指针，所以这道基础题我觉得对于我这个初学者来说还是很有价值的。


## Code
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* l=(ListNode*)malloc(sizeof(ListNode));
        l->next=nullptr;//创立头节点
        ListNode* p=l;//维护一个指针就行

        //遍历两个链表
        while(l1!=nullptr&&l2!=nullptr){
            if(l1->val<l2->val){
                p->next=l1;
                l1=l1->next;
            }
            else{
                p->next=l2;
                l2=l2->next;
            }
            p=p->next;
            }

        //链接未处理完的链表
         if(l2==nullptr){
                p->next=l1;
            }
        else{
                p->next=l2;
        }

        ListNode* result=l->next;
        free(l);
        return result;
    }
};
```

## 思考补充
受ds老师启发，突然发现本题好像不需要另外建立一张空表，直接选最小节点当头节点就好了。
```cpp
    // 确定新链表的头节点
        ListNode* head = nullptr;
        if (l1->val <= l2->val) {
            head = l1;
            l1 = l1->next;
        } else {
            head = l2;
            l2 = l2->next;
        }
```
后续方法就和上面一样了，链表的操作逻辑和数组还是有很大的不同的。

