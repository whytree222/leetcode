# Leetcode 2.两数相加
>Probelm[ 2.两数相加 ](https://leetcode.cn/problems/add-two-numbers/?envType=problem-list-v2&envId=linked-list)

## 个人思路
我一开始是想遍历两个链表，将他们放进两个数组中，然后再对两个数组求和，即算出原来的数，然后再将他们相加，将求出的和从个位开始放进数组c当中，再将数组c每一位数放进链表的一个新链表的节点中。

先说说我这个思路以及我操作上存在的**问题**：

**1.如果将数组中的数相加的话是一定会溢出的，所以必须使用==逐位相加法==**

**2.我对于何时需要维护一个尾指针存在疑问**

**3.不知道如何去创立一个新链表（不是节点，是链表）**
```cpp
ListNode* l3=new ListNode(c[0]);
        for(int i=0;c[i]!=-1;i++){
            l3->val=c[i];
            l3=l3->next;
        }
```
~~我干的~~

