# Leetcode 2.两数相加
>Probelm[ 2.两数相加 ](https://leetcode.cn/problems/add-two-numbers/?envType=problem-list-v2&envId=linked-list)

## 个人思路
我一开始是想遍历两个链表，将他们放进两个数组中，然后再对两个数组求和，即算出原来的数，然后再将他们相加，将求出的和从个位开始放进数组c当中，再将数组c每一位数放进链表的一个新链表的节点中。

先说说我这个思路以及我操作上存在的**问题**：

**1.如果将数组中的数相加的话是一定会溢出的，所以必须使用==逐位相加法==**

**2.我对于何时需要维护一个尾指针存在疑问**
<span style="color: red;">答：如果在操作后还需要用到链表则需要维护尾指针（如需要返回这个链表），如果不需要则随意。</span>

**3.不知道如何去创立一个新链表（不是节点，是链表）**
```cpp
ListNode* l3=new ListNode(c[0]);
        for(int i=0;c[i]!=-1;i++){
            l3->val=c[i];
            l3=l3->next;
        }
```
~~我干的~~
<span style="color: red;">答：见我写的代码</span>

不管怎样，至少我现在知道这道题最主要的思路是——**“模拟”**，也就是当成==竖式加法==来做。

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* l=new ListNode();//建立一个头节点
        ListNode* p=l;//维护一个尾指针
        int carry=0;

        //开始模拟
        while(l1&&l2){
            int n=(l1->val+l2->val+carry)%10;
            carry=(l1->val+l2->val+carry)/10;
            p->next=new ListNode(n);//注意此处是如何链接结点的
            p=p->next;l1=l1->next;l2=l2->next;
        }

        //处理剩余部分
        while(l1){
            int n=(l1->val+carry)%10;
            carry=(l1->val+carry)/10;
            p->next=new ListNode(n);
            p=p->next;
            l1=l1->next;
        }
        while(l2){
            int n=(l2->val+carry)%10;
            carry=(l2->val+carry)/10;
            p->next=new ListNode(n);
            p=p->next;
            l2=l2->next;
        }
        //如果最后还有进位
        if(carry!=0){
            p->next=new ListNode(carry);
            p=p->next;
        }
    return l->next;}
};
```
这是在我阅读了部分题解后我能写出的最好的code，至于复杂度嘛......暂时无需在意，看看我以后能不能优化一下。

![本题代码的执行用时分布和消耗内存分布](../images/test.png)