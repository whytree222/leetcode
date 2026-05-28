# Leetcode 83. 删除排序链表中的重复元素
>Problem: [83. 删除排序链表中的重复元素](https://leetcode.cn/problems/remove-duplicates-from-sorted-list/description/?envType=problem-list-v2&envId=linked-list)

## 个人思路
其实本题在思维上还是很简单的，所给的链表是有序的，直接在所给链表上进行操作即可。本人此题主要问题还是在于对于链表操作的**基本功不扎实**。

我来说说我的问题：
1.没有考虑到空表情况，缺乏这种思维 *（没考虑的话本题无法正常运行）*

2.在进行删除操作时，逻辑有误。
```cpp
if(p->val==p->next->val){
                p->next=p->next->next;
                p=p->next;
            }
```
多出的 `p=p-next;`很明显是错误的，如链表开头为1 1 1

3.返回应当返回head而不是p

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
    ListNode* deleteDuplicates(ListNode* head) {
        if(head==nullptr) return head;//空表
        
        ListNode* p=head;
        while(p->next){
            if(p->val==p->next->val){
                p->next=p->next->next;
            }
            else{
                p=p->next;
            }
        }
    return head;}
};
```
